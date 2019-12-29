---
title: ブランチオフィスに関する考慮事項
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.openlocfilehash: 5a07553e6662fd79230d566ba2049c5e8997f4d6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403581"
---
# <a name="branch-office-considerations"></a>ブランチ オフィスに関する考慮事項

> 適用対象:Windows Server 2019、Windows Server (半期チャネル)、 

この記事では、ブランチオフィスでのシールドされたバーチャルマシンの実行に関するベストプラクティスと、Hyper-v ホストで HGS への接続が制限されている期間がある可能性がある他のリモートシナリオについて説明します。

## <a name="fallback-configuration"></a>フォールバック構成

Windows Server バージョン1709以降では、プライマリ HGS が応答していないときに使用するために、Hyper-v ホスト上に追加のホストガーディアンサービス Url のセットを構成できます。
これにより、ローカルの HGS クラスターを実行できます。ローカルの HGS クラスターは、ローカルサーバーがダウンしている場合に、企業のデータセンターの HGS にフォールバックする機能で、プライマリサーバーとして使用されます。

フォールバックオプションを使用するには、2つの HGS サーバーをセットアップする必要があります。 Windows Server 2019 または Windows Server 2016 を実行し、同じクラスターまたは異なるクラスターの一部にすることができます。 クラスターが異なる場合は、運用方法を確立して、2つのサーバー間で構成証明ポリシーが同期されていることを確認する必要があります。 どちらも、シールドされた Vm を実行するように Hyper-v ホストを正しく承認し、シールドされた Vm を起動するために必要なキーマテリアルを持っている必要があります。 2つのクラスター間で共有暗号化証明書と署名証明書のペアを使用することも、別の証明書を使用して、シールドデータ内のガーディアン (暗号化/署名証明書のペア) の両方を承認するように HGS シールドされた VM を構成することもできます。拡張子.

次に、Hyper-v ホストを Windows Server バージョン1709または Windows Server 2019 にアップグレードし、次のコマンドを実行します。
```powershell
# Replace https://hgs.primary.com and https://hgs.backup.com with your own domain names and protocols
Set-HgsClientConfiguration -KeyProtectionServerUrl 'https://hgs.primary.com/KeyProtection' -AttestationServerUrl 'https://hgs.primary.com/Attestation' -FallbackKeyProtectionServerUrl 'https://hgs.backup.com/KeyProtection' -FallbackAttestationServerUrl 'https://hgs.backup.com/Attestation'
```

フォールバックサーバーの構成を解除するには、両方のフォールバックパラメーターを省略するだけです。
```powershell
Set-HgsClientConfiguration -KeyProtectionServerUrl 'https://hgs.primary.com/KeyProtection' -AttestationServerUrl 'https://hgs.primary.com/Attestation'
```

Hyper-v ホストがプライマリサーバーとフォールバックサーバーの両方で構成証明を渡すには、両方の HGS クラスターで構成証明情報が最新の状態であることを確認する必要があります。
さらに、仮想マシンの TPM の暗号化を解除するために使用する証明書は、両方の HGS クラスターで使用できる必要があります。
各 HGS を異なる証明書で構成し、両方の VM が信頼するように構成するか、両方の HGS クラスターに証明書の共有セットを追加することができます。

フォールバック Url を使用してブランチオフィスで HGS を構成する方法の詳細については、ブログ記事「 [Windows Server バージョン1709でのシールドされた vm のブランチオフィスサポートの向上](https://blogs.technet.microsoft.com/datacentersecurity/2017/11/15/improved-branch-office-support-for-shielded-vms-in-windows-server-version-1709/)」を参照してください。


## <a name="offline-mode"></a>オフラインモード

オフラインモードでは、HGS に到達できない場合に、シールドされた VM の電源をオンにすることができます。 Hyper-v ホストのセキュリティ構成が変更されていない場合に限ります。
オフラインモードは、Hyper-v ホストで特別なバージョンの VM TPM キー保護機能をキャッシュすることによって機能します。
キープロテクターは、(仮想化ベースのセキュリティ id キーを使用して) ホストの現在のセキュリティ構成に対して暗号化されます。
ホストが HGS と通信できず、そのセキュリティ構成が変更されていない場合は、キャッシュされたキー保護機能を使用して、シールドされた VM を起動できます。
新しいコード整合性ポリシーが適用されたり、セキュアブートが無効になったりするなど、システムのセキュリティ設定が変更された場合、キャッシュされたキープロテクターは無効になり、ホストは HGS で証明する必要があります。これにより、シールドされた Vm を再びオフラインにすることができます。

オフラインモードでは、ホストガーディアンサービスクラスターと Hyper-v ホストの両方について、Windows Server Insider Preview ビルド17609以降が必要です。
これは、既定で無効になっている HGS のポリシーによって制御されます。
オフラインモードのサポートを有効にするには、HGS ノードで次のコマンドを実行します。

```powershell
Set-HgsKeyProtectionConfiguration -AllowKeyMaterialCaching:$true
```

キャッシュ可能なキープロテクターは各シールドされた VM に対して一意であるため、HGS でこの設定を有効にした後で、再起動せずに、シールドされた Vm を起動してキャッシュ可能なキー保護機能を取得する必要があります。
シールドされた VM が古いバージョンの Windows Server を実行している Hyper-v ホストに移行する場合、または古いバージョンの HGS から新しいキー保護機能を取得する場合は、オフラインモードで起動することはできませんが、HGS へのアクセスが利用可能になったときにオンラインモードで実行を継続できます。でき.
