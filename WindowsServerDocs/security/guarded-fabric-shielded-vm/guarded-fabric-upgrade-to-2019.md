---
title: Windows Server 2019 への保護されたファブリックのアップグレード
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 11/21/2018
ms.openlocfilehash: 274bdf027947ffb6fe807d4acd0a3b2174c20e28
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867453"
---
# <a name="upgrade-a-guarded-fabric-to-windows-server-2019"></a>Windows Server 2019 への保護されたファブリックのアップグレード

> 適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

この記事では、Windows Server 2016、Windows Server バージョン 1709 または Windows Server を Windows Server 2019 バージョン 1803 から既存の保護されたファブリックのアップグレードに必要な手順について説明します。

## <a name="whats-new-in-windows-server-2019"></a>Windows Server 2019 の新機能

Windows Server 2019 で保護されたファブリックを実行するといくつかの新機能の利用できます。

**ホスト キーの構成証明**は、最新の構成証明モードを HYPER-V ホストは、TPM 構成証明に使用できる TPM 2.0 デバイスを持っていない場合は、シールドされた Vm を実行するが容易に設計されています。 ホスト キーの構成証明では、キーのペアを使用して、ホストを HGS、要件、Active Directory ドメインに参加させるホストを削除する HGS と会社のフォレスト間の AD 信頼を排除し、開かれたファイアウォール ポートの数を減らすことを認証します。 ホスト キーの構成証明には、Active Directory 認証は、Windows Server 2019 は非推奨が置き換えられます。

**V2 の構成証明のバージョン**- 今後は、ホスト キーの構成証明と新機能をサポートするバージョン管理 HGS を導入しました。 Windows Server 2019 ホストのホスト キーの構成証明をサポートしても v1 ホスト、Windows Server 2016 でサポートを意味します。 v2 の構成証明を使用して、サーバーで Windows Server 2019 HGS の新規インストールが発生します。 V2 を手動で有効にするまで、2019年へのインプレース アップグレードはバージョン v1 で残ります。 ほとんどのコマンドレットは、レガシまたは最新の構成証明書ポリシーを使用するかどうかを指定することができます - HgsVersion パラメーターを指定するようになりました。

**シールドされた Vm の Linux のサポート**-Windows Server 2019 を実行している HYPER-V ホストできる実行 Linux のシールドされた Vm。 Linux のシールドされた Vm で Windows Server バージョン 1709 導入された、Windows Server 2019 がそれらをサポートする最初の時間の長い用語サービス チャネル リリース。

**Office の機能強化を分岐**-オフラインのシールドされた Vm とフォールバックの構成対応のブランチ オフィスで、HYPER-V ホストでシールドされた Vm を実行しやすくなっています。

**TPM ホスト バインディング**-ホストの TPM を使用してそのホストに VM をバインドする、最もセキュリティで保護するワークロード、シールドされた VM が作成され、他の最初のホストでのみ実行するのようになりましたことができます。 ホスト間で移行する必要がある一般的なデータ センターのワークロードではなく、privileged access workstation およびブランチ オフィスを使用します。

## <a name="compatibility-matrix"></a>互換性対応表

Windows Server 2019 に、保護されたファブリックをアップグレードする前に、構成がサポートされているかどうかに、次の互換性対応表を確認します。

|  | WS2016 HGS | WS2019 HGS|
|---|---|---|
|**WS2016 Hyper V ホスト** | サポートされている | サポートされている<sup>1</sup>|
|**WS2019 Hyper V ホスト** | サポートされていない<sup>2</sup> | サポートされている|

<sup>1</sup> v1 の構成証明プロトコルを使用して Windows Server 2019 HGS サーバーに対しては、Windows Server 2016 ホストは証明できるのみです。 ホスト キーの構成証明を含む、v2 の構成証明プロトコルでのみ利用できる新機能 Windows Server 2016 ホストはサポートされていません。

<sup>2</sup>マイクロソフトは、Windows Server 2016 の HGS サーバーに対して正常に証明から TPM 構成証明を使用して、Windows Server 2019 ホストの防止、問題を認識しています。 この制限は Windows Server 2016 の今後の更新で修正されます。

## <a name="upgrade-hgs-to-windows-server-2019"></a>Windows Server 2019 HGS にアップグレードします。

すべてのホスト Windows Server 2016 または 2019、実行されているかどうかを続けると正常にするために、HYPER-V ホストをアップグレードする前に、Windows Server 2019 に HGS クラスターをアップグレードすることをお勧めします。

HGS クラスターをアップグレードするには、アップグレード中に、一度にクラスターから 1 つのノードを一時的に削除することが必要ですが。 これは、HYPER-V ホストからの要求に応答するクラスターの容量を減らすし、テナントの低速な応答時間やサービスの停止になる可能性があります。 HGS サーバーをアップグレードする前に、構成証明とキーのリリースの要求を処理するための十分な容量があることを確認します。

HGS クラスターをアップグレードするには、時に 1 つのノード、クラスターの各ノードで、次の手順を実行します。

1.  HGS サーバーを実行して、クラスターから削除`Clear-HgsServer`管理者特権の PowerShell プロンプトでします。 このコマンドレットでは、レプリケートされた HGS ストア、HGS の web サイト、およびノードをフェールオーバー クラスターから削除されます。
2.  実行する必要があります、HGS サーバーがドメイン コント ローラー (既定の構成) の場合は、`adprep /forestprep`と`adprep /domainprep`OS アップグレード ドメインの準備にアップグレードされる最初のノードにします。 参照してください、 [Active Directory Domain Services のアップグレードに関するドキュメント](https://docs.microsoft.com/windows-server/identity/ad-ds/deploy/upgrade-domain-controllers#supported-in-place-upgrade-paths)詳細についてはします。
3.  実行、 [、インプレース アップグレード](../../get-started-19/install-upgrade-migrate-19.md)Windows Server 2019 にします。
4.  実行[Initialize HgsServer](guarded-fabric-configure-additional-hgs-nodes.md)ノードをクラスターに参加させる。

すべてのノードを Windows Server 2019 にアップグレードすると、v2 ホスト キーの構成証明などの新機能をサポートするために必要に応じて、HGS バージョンをアップグレードできます。

```powershell
Set-HgsServerVersion  v2
```

## <a name="upgrade-hyper-v-hosts-to-windows-server-2019"></a>Windows Server 2019 を HYPER-V ホストをアップグレードします。

Windows Server 2019 するために、HYPER-V ホストをアップグレードする前に、HGS クラスターが既に Windows Server 2019 にアップグレードして、HYPER-V サーバーからのすべての Vm を移動したことを確認します。

1.  (常に、ケース TPM 構成証明を使用する場合)、サーバーを Windows Defender アプリケーション制御コード整合性ポリシーを使用している場合は、ポリシーが監査モードでまたはサーバーをアップグレードする前に無効になっていることを確認します。 [WDAC ポリシーを無効にする方法について説明します](https://docs.microsoft.com/en-us/windows/security/threat-protection/windows-defender-application-control/disable-windows-defender-application-control-policies)
2.  ガイダンスに従って、 [Windows Server のアップグレード センター](http://aka.ms/upgradecenter)のホストを Windows Server 2019 をアップグレードします。 HYPER-V ホストがフェールオーバー クラスターの一部の場合は、使用を検討して、[クラスター オペレーティング システムのローリング アップグレード](../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md)します。
3.  [テストおよび再有効化する](https://docs.microsoft.com/en-us/windows/security/threat-protection/windows-defender-application-control/audit-windows-defender-application-control-policies)した 1 つのアップグレードの前に有効になっている場合、Windows Defender Application Control ポリシー。
4.  実行`Get-HgsClientConfiguration`場合にチェックする**IsHostGuarded = True**、つまりホストでは、HGS サーバーと構成証明に合格が。
5.  TPM 構成証明を使用している場合は、する必要があります[TPM ベースラインまたはコード整合性ポリシーを再キャプチャ](guarded-fabric-add-host-information-for-tpm-trusted-attestation.md)証明書を渡すにアップグレードした後。
6.  開始を実行しているシールドされた Vm のホストでもう一度!

## <a name="switch-to-host-key-attestation"></a>キーの構成証明のホストへの切り替え

Active Directory ベースの構成証明を現在実行されているし、ホスト キーの構成証明にアップグレードする場合は、次の手順に従います。 Active Directory ベースの構成証明が Windows Server 2019 は非推奨し、将来のリリースで削除される可能性がありますに注意してください。

1.  HGS サーバーが次のコマンドを実行して v2 構成証明モードで動作していることを確認します。 V1 の既存のホストは、HGS サーバーが v2 にアップグレードした場合にもを証明し続けます。

    ```powershell
    Set-HgsServerVersion v2
    ```

2.  [ホスト キーの生成](guarded-fabric-create-host-key.md)から各 Hyper-v ホストをホストし、HGS に登録します。 HGS は引き続き、Active Directory モードで動作、ため、新しいホスト キーがすぐに反映されないことの警告が表示されます。 これは、ホスト キーを正常に証明できるすべてのホストまでホスト キーのモードに変更したくないと、意図的です。

3.  ホスト キーは、すべてのホストに対して登録されているとは、ホスト キーの構成証明モードを使用するように HGS を構成できます。

    ```powershell
    Set-HgsServer -TrustHostKey
    ```

    ホスト キーのモードでの問題が発生する Active Directory ベースの構成証明に戻す必要がある場合は、HGS で、次のコマンドを実行します。

    ```powershell
    Set-HgsServer -TrustActiveDirectory
    ```