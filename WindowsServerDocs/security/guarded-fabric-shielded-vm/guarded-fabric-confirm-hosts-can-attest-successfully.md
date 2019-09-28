---
title: 保護されたホストが証明できることを確認する
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 7485796b-b840-4678-9b33-89e9710fbbc7
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 02/05/2019
ms.openlocfilehash: bc047bbc23f4edfbbd77fb3e2d7258241d1f19d0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386702"
---
# <a name="confirm-guarded-hosts-can-attest"></a>保護されたホストが証明できることを確認する 

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016


ファブリック管理者は、Hyper-v ホストを保護されたホストとして実行できることを確認する必要があります。 少なくとも1つの保護されたホストで、次の手順を実行します。

1.  Hyper-v の役割とホストガーディアンの Hyper-v サポート機能をまだインストールしていない場合は、次のコマンドを使用してインストールします。

        Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart

2.  Hgs サーバーで、Hyper-v ホストが HGS DNS 名を解決し、ポート 80 (または、HTTPS を設定している場合は 443) に接続できることを確認します。

2.  ホストのキーの保護と構成証明の Url を構成します。

    - **Windows PowerShell を使用**する場合:管理者特権の Windows PowerShell コンソールで次のコマンドを実行して、キーの保護と構成証明の Url を構成できます。 @No__t 0FQDN @ no__t-1 の場合は、HGS クラスターの完全修飾ドメイン名 (FQDN) を使用します (たとえば、hgs サーバーで**HgsServer**コマンドレットを実行して、url を取得するように hgs 管理者に依頼します)。

        `Set-HgsClientConfiguration -AttestationServerUrl 'http://<FQDN>/Attestation' -KeyProtectionServerUrl 'http://<FQDN>/KeyProtection'`

        フォールバック HGS サーバーを構成するには、このコマンドを繰り返し、キーの保護と構成証明サービスのフォールバック Url を指定します。 詳細については、「[フォールバック構成](guarded-fabric-manage-branch-office.md#fallback-configuration)」を参照してください。 

    - **VMM 経由**:System Center 2016-Virtual Machine Manager (VMM) を使用している場合は、VMM で構成証明とキー保護の Url を構成できます。 詳細については、「 **VMM で保護**されたホストのプロビジョニング」の「[グローバル HGS 設定を構成する](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-hosts#configure-global-hgs-settings)」を参照してください。
    
    >**メモ**
    > - Hgs 管理者が[hgs サーバーで HTTPS を有効](guarded-fabric-configure-hgs-https.md)にした場合は、`https://` で url を開始します。
    > - Hgs 管理者が HGS サーバーで HTTPS を有効にし、自己署名証明書を使用している場合は、すべてのホストの信頼されたルート証明機関ストアに証明書をインポートする必要があります。 これを行うには、各ホストで次のコマンドを実行します。<br>
        `Import-Certificate -FilePath "C:\temp\HttpsCertificate.cer" -CertStoreLocation Cert:\LocalMachine\Root`
    
3.  ホストで構成証明の試行を開始して、構成証明の状態を表示するには、次のコマンドを実行します。

        Get-HgsClientConfiguration

    コマンドの出力は、ホストが構成証明を受けたかどうかを示し、現在は保護されています。 @No__t-0 が**True**を返さない場合は、HGS 診断ツール[HgsTrace](https://technet.microsoft.com/library/mt718831.aspx)を実行して調査できます。 診断を実行するには、ホストの管理者特権の Windows PowerShell プロンプトで次のコマンドを入力します。

        Get-HgsTrace -RunDiagnostics -Detailed

    > [!IMPORTANT]
    > Windows Server 2019 または Windows 10 バージョン1809を使用していて、コード整合性ポリシーを使用している場合、`Get-HgsTrace` は**コード整合性ポリシーのアクティブ**な診断の失敗を返します。
    > 失敗した診断が唯一の場合は、この結果を無視しても問題ありません。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [シールドされた VMの展開](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)

## <a name="see-also"></a>関連項目

- [ホストガーディアンサービス (HGS) を展開する](guarded-fabric-deploying-hgs-overview.md)
- [シールドされた VMの展開](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)

