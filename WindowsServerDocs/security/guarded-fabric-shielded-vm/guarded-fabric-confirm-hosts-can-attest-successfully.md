---
title: 保護されたホストを証明できることを確認します。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 7485796b-b840-4678-9b33-89e9710fbbc7
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 02/05/2019
ms.openlocfilehash: 6b67208176b426f52d3c5106f8de09ad334d3b01
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829533"
---
# <a name="confirm-guarded-hosts-can-attest"></a>保護されたホストを証明できることを確認します。 

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016


ファブリック管理者は、HYPER-V ホストが保護されたホストとして実行できることを確認する必要があります。 少なくとも 1 つの保護されたホストで次の手順を完了するには。

1.  したが既にインストールされていない場合、Hyper-v の役割と Host Guardian HYPER-V サポート機能は、次のコマンドを使用してインストールします。

        Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart

2.  HYPER-V ホストが HGS の DNS 名を解決することができ、HGS サーバーでポート 80 (または HTTPS を設定する場合は 443) に到達するネットワーク接続を持つようにします。

2.  ホストのキーの保護と構成証明 Url を構成します。

    - **Windows PowerShell を使って**:キーの保護と構成証明 Url を構成するには、管理者特権での Windows PowerShell コンソールで、次のコマンドを実行します。 &lt;FQDN&gt;、HGS クラスターの完全修飾ドメイン名 (FQDN) を使用して (hgs.bastion.local など、またはを実行する HGS 管理者に問い合わせて、 **Get HgsServer** HGS サーバーを取得するコマンドレット、Url)。

        `Set-HgsClientConfiguration -AttestationServerUrl 'http://<FQDN>/Attestation' -KeyProtectionServerUrl 'http://<FQDN>/KeyProtection'`

        フォールバック HGS サーバーを構成するには、このコマンドを実行し、キーの保護と構成証明サービスのフォールバック Url を指定します。 詳細については、次を参照してください。[フォールバック構成](guarded-fabric-manage-branch-office.md#fallback-configuration)します。 

    - **VMM を介して**:System Center 2016 - Virtual Machine Manager (VMM) を使用している場合は、VMM の構成証明とキー保護の Url を構成できます。 詳細については、次を参照してください。[グローバル HGS 設定を構成する](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-hosts#configure-global-hgs-settings)で**プロビジョニングには、VMM でのホストが保護されている**します。
    
    >**メモ**
    > - 場合 HGS 管理者[HGS サーバーで HTTPS を有効になって](guarded-fabric-configure-hgs-https.md)、開始を含む Url`https://`します。
    > - HGS 管理者は、HGS サーバーで HTTPS を有効にし、自己署名証明書を使用した場合は、すべてのホスト上の信頼されたルート証明機関ストアに証明書をインポートする必要があります。 これを行うには、各ホストで、次のコマンドを実行します。<br>
        `Import-Certificate -FilePath "C:\temp\HttpsCertificate.cer" -CertStoreLocation Cert:\LocalMachine\Root`
    
3.  ホスト上の構成証明試行を開始し、構成証明の状態を表示する、するには、次のコマンドを実行します。

        Get-HgsClientConfiguration

    コマンドの出力は、ホストが構成証明を渡すしは今後、保護するかどうかを示します。 場合`IsHostGuarded`返さない**True**、HGS 診断ツールを実行することができます[Get HgsTrace](https://technet.microsoft.com/library/mt718831.aspx)、調査します。 診断を実行するには、ホストで管理者特権での Windows PowerShell プロンプトで次のコマンドを入力します。

        Get-HgsTrace -RunDiagnostics -Detailed

    > [!IMPORTANT]
    > Windows Server 2019 または Windows 10、バージョンは 1809 を使用しているコードの整合性ポリシーを使用している場合`Get-HgsTrace`のエラーを返す可能性があります、**コード整合性ポリシー Active**診断します。
    > だけ失敗した診断がある場合に、この結果を無視してかまいません。

## <a name="next-step"></a>次の手順

>[!div class="nextstepaction"]
[シールドされた Vm をデプロイします。](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)

## <a name="see-also"></a>関連項目

- [ホスト ガーディアン サービス (HGS) のデプロイします。](guarded-fabric-deploying-hgs-overview.md)
- [シールドされた Vm をデプロイします。](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)

