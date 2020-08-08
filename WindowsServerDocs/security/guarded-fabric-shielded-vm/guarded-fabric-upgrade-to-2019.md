---
title: Windows Server 2019 への保護されたファブリックのアップグレード
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 11/21/2018
ms.openlocfilehash: 53b0610e32f8cd3c6b7e3d086690ef4b72612ed6
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996141"
---
# <a name="upgrade-a-guarded-fabric-to-windows-server-2019"></a>Windows Server 2019 への保護されたファブリックのアップグレード

> 適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

この記事では、既存の保護されたファブリックを Windows Server 2016、Windows Server バージョン1709、または Windows Server バージョン1803から Windows Server 2019 にアップグレードするために必要な手順について説明します。

## <a name="whats-new-in-windows-server-2019"></a>Windows Server 2019 の新機能

Windows Server 2019 で保護されたファブリックを実行すると、いくつかの新機能を利用できます。

**ホストキーの構成証明**は、tpm 構成証明で使用可能な tpm 2.0 デバイスが hyper-v ホストにない場合に、シールドされた vm を簡単に実行できるように設計された、最新の構成証明モードです。 ホストキーの構成証明では、キーペアを使用して HGS でホストを認証し、ホストが Active Directory ドメインに参加する必要がなくなるため、HGS と企業フォレスト間の AD 信頼を排除し、開いているファイアウォールポートの数を減らすことができます。 ホストキーの構成証明は、Windows Server 2019 で非推奨とされている構成証明 Active Directory 置き換わるものです。

**V2 構成証明バージョン**-今後、ホストキーの構成証明と新機能をサポートするために、HGS にバージョン管理を導入しました。 Windows Server 2019 に HGS を新規インストールすると、v2 構成証明が使用されます。つまり、Windows server 2019 ホストのホストキーの構成証明をサポートしても、Windows Server 2016 で v1 ホストをサポートすることができます。 2019への一括アップグレードは、v2 を手動で有効にするまでバージョン v1 に残ります。 ほとんどのコマンドレットでは、-HgsVersion パラメーターを使用して、レガシまたは最新の構成証明ポリシーを使用するかどうかを指定できます。

**Linux のシールドされた vm のサポート**-Windows Server 2019 を実行する hyper-v ホストでは、linux のシールドされた vm を実行できます。 Linux のシールドされた Vm は Windows Server バージョン1709以降、windows server 2019 をサポートするための最初の長期的なサービスチャネルリリースです。

**ブランチオフィスの改善**-オフラインシールドされた Vm と hyper-v ホスト上のフォールバック構成をサポートするブランチオフィスで、シールドされた vm を簡単に実行できるようになりました。

**TPM ホストバインド**-最も安全なワークロードに対して、シールドされた VM は、それが作成された最初のホスト上でのみ実行され、それ以外はホストの TPM を使用してそのホストにバインドできるようになりました。 これは、ホスト間で移行する必要がある一般的なデータセンターのワークロードではなく、特権アクセスワークステーションとブランチオフィスに最適です。

## <a name="compatibility-matrix"></a>互換性マトリックス

保護されたファブリックを Windows Server 2019 にアップグレードする前に、次の互換性マトリックスを確認して、構成がサポートされているかどうかを確認してください。

|  | WS2016 HGS | WS2019 HGS|
|---|---|---|
|**Hyper-v ホストの WS2016** | サポートされています | サポート<sup>1</sup>|
|**Hyper-v ホストの WS2019** | サポートされない<sup>2</sup> | サポートされています|

<sup>1</sup> windows server 2016 ホストは、v1 構成証明プロトコルを使用して、windows SERVER 2019 HGS サーバーに対してのみ証明できます。 V2 構成証明プロトコル (ホストキーの構成証明を含む) でのみ使用できる新機能は、Windows Server 2016 ホストではサポートされていません。

<sup>2</sup> Microsoft は、TPM 構成証明を使用して windows server 2019 ホストが windows SERVER 2016 HGS サーバーに対して正常に証明することを防ぐ問題を認識しています。 この制限は、Windows Server 2016 の今後の更新プログラムで解決される予定です。

## <a name="upgrade-hgs-to-windows-server-2019"></a>HGS を Windows Server 2019 にアップグレードする

Hyper-v ホストをアップグレードする前に、HGS クラスターを Windows Server 2019 にアップグレードすることをお勧めします。これにより、Windows Server 2016 または2019を実行しているすべてのホストが正常に証明を続行できるようになります。

HGS クラスターをアップグレードするには、アップグレード中に一度に1つのノードをクラスターから一時的に削除する必要があります。 これにより、Hyper-v ホストからの要求に応答するクラスターの容量が減り、応答時間が遅くなったり、テナントのサービスが停止したりする可能性があります。 HGS サーバーをアップグレードする前に、構成証明とキー解放要求を処理するのに十分な容量があることを確認します。

HGS クラスターをアップグレードするには、クラスターの各ノードで、一度に1ノードずつ、次の手順を実行します。

1.  `Clear-HgsServer`管理者特権の PowerShell プロンプトでを実行して、クラスターから HGS サーバーを削除します。 このコマンドレットは、HGS のレプリケートされたストア、HGS web サイト、およびノードをフェールオーバークラスターから削除します。
2.  HGS サーバーがドメインコントローラー (既定の構成) である場合は、を実行して、 `adprep /forestprep` `adprep /domainprep` OS のアップグレード用にドメインを準備するために、アップグレードする最初のノードでを実行する必要があります。 詳細については、 [Active Directory Domain Services アップグレード](../../identity/ad-ds/deploy/upgrade-domain-controllers.md#supported-in-place-upgrade-paths)に関するドキュメントを参照してください。
3.  Windows Server 2019 へ[のインプレースアップグレード](../../get-started-19/install-upgrade-migrate-19.md)を実行します。
4.  ノードをクラスターに再び参加させるには、 [HgsServer](guarded-fabric-configure-additional-hgs-nodes.md)を実行します。

すべてのノードが Windows Server 2019 にアップグレードされたら、必要に応じて、HGS のバージョンを v2 にアップグレードして、ホストキーの構成証明などの新機能をサポートすることができます。

```powershell
Set-HgsServerVersion  v2
```

## <a name="upgrade-hyper-v-hosts-to-windows-server-2019"></a>Hyper-v ホストを Windows Server 2019 にアップグレードする

Hyper-v ホストを Windows Server 2019 にアップグレードする前に、HGS クラスターが既に Windows Server 2019 にアップグレードされていること、およびすべての Vm を Hyper-v サーバーから移動したことを確認します。

1.  サーバーで Windows Defender アプリケーション制御コード整合性ポリシーを使用している場合 (常に TPM 構成証明を使用している場合)、サーバーのアップグレードを試行する前に、ポリシーが監査モードであるか無効になっていることを確認してください。 [WDAC ポリシーを無効にする方法について説明します。](/windows/security/threat-protection/windows-defender-application-control/disable-windows-defender-application-control-policies)
2.  [Windows server のアップグレードのコンテンツ](../../upgrade/upgrade-overview.md)に記載されているガイダンスに従って、ホストを windows server 2019 にアップグレードします。 Hyper-v ホストがフェールオーバークラスターの一部である場合は、[クラスターのオペレーティングシステムのローリングアップグレード](../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md)を使用することを検討してください。
3.  Windows Defender Application Control ポリシーを[テストして再度有効](/windows/security/threat-protection/windows-defender-application-control/audit-windows-defender-application-control-policies)にします (アップグレード前に有効にした場合)。
4.  を実行して `Get-HgsClientConfiguration` 、 **Ishostguarded = True**であるかどうかを確認します。これは、ホストが hgs サーバーで構成証明を正常に渡すことを意味します。
5.  TPM 構成証明を使用している場合は、構成証明を成功させるために、アップグレード後に[tpm ベースラインまたはコード整合性ポリシーを再キャプチャ](guarded-fabric-add-host-information-for-tpm-trusted-attestation.md)することが必要になる場合があります。
6.  ホストでシールドされた Vm の実行をもう一度開始します。

## <a name="switch-to-host-key-attestation"></a>ホストキーの構成証明に切り替えます

Active Directory ベースの構成証明を現在実行していて、ホストキーの構成証明にアップグレードする場合は、次の手順に従います。 Active Directory ベースの構成証明は、Windows Server 2019 では非推奨とされており、将来のリリースでは削除される可能性があることに注意してください。

1.  次のコマンドを実行して、HGS サーバーが v2 構成証明モードで動作していることを確認します。 既存の v1 ホストは、HGS サーバーが v2 にアップグレードされても、引き続き証明されます。

    ```powershell
    Set-HgsServerVersion v2
    ```

2.  各 Hyper-v ホストから[ホストキーを生成](guarded-fabric-create-host-key.md)し、HGS に登録します。 HGS は引き続き Active Directory モードで動作しているため、新しいホストキーがすぐに有効にならないという警告が表示されます。 これは意図的なものです。ホストキーをすべてのホストが正常に証明できるようになるまでは、ホストキーモードに変更しないでください。

3.  すべてのホストに対してホストキーが登録されたら、ホストキーの構成証明モードを使用するように HGS を構成できます。

    ```powershell
    Set-HgsServer -TrustHostKey
    ```

    ホストキーモードで問題が発生し、Active Directory ベースの構成証明に戻す必要がある場合は、HGS で次のコマンドを実行します。

    ```powershell
    Set-HgsServer -TrustActiveDirectory
    ```