---
title: Branch Office に関する考慮事項
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.openlocfilehash: d93c37227af1eb62368fbcd4ec5d6a48374b45ff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877063"
---
# <a name="branch-office-considerations"></a>ブランチ オフィスに関する考慮事項

> 適用対象:Windows Server 2019、Windows Server (半期チャネル) 

この記事では、HYPER-V ホストが HGS に接続を制限して期間をいる可能性がブランチ オフィスでのシールドされた仮想マシンとその他のリモートのシナリオを実行するためのベスト プラクティスについて説明します。

## <a name="fallback-configuration"></a>フォールバックの構成

Windows Server バージョン 1709 以降では、構成できますホスト ガーディアン サービスの Url のセットを追加で使用するための HYPER-V ホストにプライマリ HGS が応答していない場合。
これにより、ローカル サーバーがダウンしている場合に、企業のデータ センターの HGS フォールバックすることができますパフォーマンス向上のため、プライマリ サーバーとして使用されるローカル HGS クラスターを実行することができます。

フォールバック オプションを使用するには、2 つの HGS サーバーを設定する必要があります。 同じまたは別のクラスターの一部にして Windows Server 2016 または Windows Server 2019 を実行ができます。 クラスターが異なる場合は、構成証明書ポリシーを確認する運用方法は 2 つのサーバー間で同期を確立するされます。 シールドされた Vm を実行し、シールドされた Vm の起動に必要なキー マテリアルを HYPER-V ホストを正しく承認するためにできるように、両方必要があります。 共有暗号化と署名証明書、2 つのクラスター間でのペアがあるか、または別の証明書を使用し、構成することもできます、HGS にシールドされた VM をシールド データにガーディアン (暗号化または署名証明書のペア) の両方を承認するにはファイルです。

Windows Server バージョン 1709 または Windows Server 2019 するために、HYPER-V ホストをアップグレードし、次のコマンドを実行します。
```powershell
# Replace https://hgs.primary.com and https://hgs.backup.com with your own domain names and protocols
Set-HgsClientConfiguration -KeyProtectionServerUrl 'https://hgs.primary.com/KeyProtection' -AttestationServerUrl 'https://hgs.primary.com/Attestation' -FallbackKeyProtectionServerUrl 'https://hgs.backup.com/KeyProtection' -FallbackAttestationServerUrl 'https://hgs.backup.com/Attestation'
```

フォールバック サーバーの構成を解除するには、両方のフォールバック パラメーターを省略します。
```powershell
Set-HgsClientConfiguration -KeyProtectionServerUrl 'https://hgs.primary.com/KeyProtection' -AttestationServerUrl 'https://hgs.primary.com/Attestation'
```

プライマリおよびフォールバックの両方のサーバーの構成証明を渡すために、HYPER-V ホストの順番は、構成証明情報が両方のクラスターを HGS で最新の状態であることを確認する必要があります。
さらに、仮想マシンの TPM の暗号化を解除するために使用する証明書は、両方の HGS クラスターで使用できる必要があります。
別の証明書を各 HGS の構成し、両方を信頼する VM を構成または HGS の両方のクラスターに共有証明書のセットを追加できます。

HGS フォールバック Url を使用してブランチ オフィス内の構成に関する追加情報は、ブログの投稿を参照してください。 [Windows Server バージョン 1709 でシールドされた Vm のブランチ オフィス サポートが向上](https://blogs.technet.microsoft.com/datacentersecurity/2017/11/15/improved-branch-office-support-for-shielded-vms-in-windows-server-version-1709/)します。


## <a name="offline-mode"></a>オフライン モード

オフライン モードでは、有効にする HGS に到達できないときに、HYPER-V ホストのセキュリティの構成が変更されていない限り、シールドされた VM を許可します。
オフライン モードでは、VM の TPM キーの保護機能、HYPER-V ホスト上の特別なバージョンをキャッシュすることによって機能します。
キー保護機能は、(仮想化ベースのセキュリティ id キーを使用して)、ホストの現在のセキュリティ構成に暗号化されます。
ホストは HGS と通信できるが、セキュリティの構成が変更されていない場合は、キャッシュされたキー保護機能を使用して、シールドされた VM を開始することがあります。
システムのセキュリティ設定を変更して、キャッシュされたキーの保護機能を無効にするなど、新しいコード整合性ポリシーが適用されているまたはセキュア ブートを無効になっているホストがシールドされた Vm を再起動できますオフライン前に、HGS を証明する必要があります。

オフライン モードでは、ホスト ガーディアン サービスのクラスターと HYPER-V ホストの両方の 17609 またはそれ以降の Windows Server Insider プレビュー ビルドが必要です。
これは、HGS は、既定で無効になっているポリシーによって制御されます。
オフライン モードのサポートを有効にするには、HGS ノードに、次のコマンドを実行します。

```powershell
Set-HgsKeyProtectionConfiguration -AllowKeyMaterialCaching:$true
```

キャッシュ可能なキー保護機能は、シールドされた VM ごとに一意であるため完全 (再起動がない) をシャット ダウンし、HGS でこの設定が有効にした後、キャッシュ可能なキー保護機能を取得する、シールドされた Vm を起動する必要があります。
自体オフライン モードで起動することはできませんが、HGS へのアクセスが使用できる場合は、オンライン モードで稼働を継続できること、シールドされた VM は、Windows Server の以前のバージョンを実行する HYPER-V ホストに移行または HGS の以前のバージョンから新しいキー プロテクターを取得、できます。
