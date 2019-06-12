---
title: アップグレード、バックアップ、および復元の SDN インフラストラクチャ
description: このトピックでは、更新、バックアップ、および、SDN インフラストラクチャを復元する方法について説明します。
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: e9a8f2fd-48fe-4a90-9250-f6b32488b7a4
ms.author: grcusanz
author: shortpatti
ms.date: 08/27/2018
ms.openlocfilehash: 7916377f58261d0ccaa3fa24f135fccca3d5e79b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446332"
---
# <a name="upgrade-backup-and-restore-sdn-infrastructure"></a>アップグレード、バックアップ、および復元の SDN インフラストラクチャ

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、更新、バックアップ、および、SDN インフラストラクチャを復元する方法について説明します。 

## <a name="upgrade-the-sdn-infrastructure"></a>SDN インフラストラクチャをアップグレードします。
SDN インフラストラクチャは、Windows Server 2019 に Windows Server 2016 からアップグレードできます。 順序付けをアップグレードするには、「SDN インフラストラクチャの更新」セクションで説明したように、同じ一連手順に従います。 アップグレードする前に、ネットワーク コント ローラーのデータベースのバックアップを実行することをお勧めします。

ネットワーク コント ローラー マシンの場合に、Get NetworkControllerNode コマンドレットを使用して、アップグレードが完了した後に、ノードの状態を確認します。 ノードの他のノードをアップグレードする前に「稼働」状態に戻ったことを確認します。 すべてのネットワーク コント ローラーのノードをアップグレードすると、ネットワーク コント ローラーは 1 時間以内に、ネットワーク コント ローラーがクラスター内で実行されているマイクロ サービスを更新します。 Update networkcontroller コマンドレットを使用して直ちに更新をトリガーすることができます。 

すべてのオペレーティング システム コンポーネントが含まれるソフトウェア定義ネットワーク (SDN) システムの同じ Windows 更新プログラムをインストールします。

- SDN には、HYPER-V ホストが有効になっています。
- ネットワーク コント ローラー Vm
- ソフトウェア ロード バランサー Mux Vm
- RAS ゲートウェイ Vm 

>[!IMPORTANT]
>System Center Virtual Manager を使用する場合は、最新の更新プログラムのロールアップに更新する必要があります。

各コンポーネントを更新するときに、標準的なメソッドのいずれかの Windows 更新プログラムをインストールするために使用できます。 ただし、最小限のダウンタイムのワークロードとネットワーク コント ローラーのデータベースの整合性を確実には、次の手順に従います。

1. 管理コンソールを更新します。<p>ネットワーク コント ローラーの Powershell モジュールを使用するコンピューターの各更新プログラムをインストールします。  単独でインストールされている RSAT NetworkController ロールがあることを任意の場所などです。 ネットワーク コント ローラー Vm 自体を除く次の手順で更新します。

2. 最初のネットワーク コント ローラーの VM では、すべての更新プログラムをインストールし、再起動します。

3. 次のネットワーク コント ローラー VM を次に進む前に使用して、`get-networkcontrollernode`コマンドレットを更新して再起動するノードの状態を確認します。

4. 再起動サイクル中にネットワーク コント ローラーのノードがダウンしてもう一度を待ちます。<p>VM を再起動した後に戻るまでに数分がかかることができます、 **_を_** 状態。 出力の例は、次を参照してください。 

5. ロード バランサーのインフラストラクチャの継続的可用性を確保するに 1 つの各 SLB Mux VM に更新プログラムをインストールします。

6. HYPER-V ホストと以降では、RAS ゲートウェイが含まれているホストでは、RAS ゲートウェイを更新**スタンバイ**モード。<p>テナントの接続を失うことがなく、RAS ゲートウェイの Vm をライブ移行できません。 更新プログラムのサイクル中にする必要がある回数を最小限に抑える新しい RAS ゲートウェイへの接続のフェールオーバーのテナントします。 ホストと RAS ゲートウェイの更新プログラムを調整することで、各テナントは最大で失敗を 1 回、します。

    a. ライブ マイグレーションの対応する Vm のホストを退避します。<p>RAS ゲートウェイ Vm は、ホスト上に残る必要があります。

    b. このホスト上の各ゲートウェイ VM には、更新プログラムをインストールします。

    c. 更新プログラムには、ゲートウェイ VM の再起動が必要な場合は、VM を再起動します。  

    d. ゲートウェイが更新されました VM を含むホスト上の更新プログラムをインストールします。

    e. 更新プログラムで必要な場合は、ホストを再起動します。

    f. スタンバイ ゲートウェイを含む追加の各ホストに対して繰り返します。<p>スタンバイ ゲートウェイが残っていない場合は、残りのすべてのホストの同様の手順を以下します。


### <a name="example-use-the-get-networkcontrollernode-cmdlet"></a>以下に例を示します。Get networkcontrollernode コマンドレットを使用します。 

この例の出力が参照してください。、`get-networkcontrollernode`内、ネットワーク コント ローラー Vm のいずれかからコマンドレットを実行します。  

例の出力結果に表示されるノードの状態を示します。

- NCNode1.contoso.com = ダウン
- NCNode2.contoso.com を =
- NCNode3.contoso.com = Up

>[!IMPORTANT]
>ノードへの変更の状態まで数分を待機する必要があります _**を**_ 、一度に 1 つずつ追加ノードを更新する前にします。

すべてのネットワーク コント ローラーのノードを更新して、ネットワーク コント ローラーは 1 時間以内に、ネットワーク コント ローラーがクラスター内で実行されているマイクロ サービスを更新します。 

>[!TIP]
>使用して、即時更新をトリガーすることができます、`update-networkcontroller`コマンドレット。


```Powershell
PS C:\> get-networkcontrollernode
Name            : NCNode1.contoso.com
Server          : NCNode1.Contoso.com
FaultDomain     : fd:/NCNode1.Contoso.com
RestInterface   : Ethernet
NodeCertificate :
Status          : Down

Name            : NCNode2.Contoso.com
Server          : NCNode2.contoso.com
FaultDomain     : fd:/ NCNode2.Contoso.com
RestInterface   : Ethernet
NodeCertificate :
Status          : Up

Name            : NCNode3.Contoso.com
Server          : NCNode3.Contoso.com
FaultDomain     : fd:/ NCNode3.Contoso.com
RestInterface   : Ethernet
NodeCertificate :
Status          : Up
```

### <a name="example-use-the-update-networkcontroller-cmdlet"></a>以下に例を示します。Update networkcontroller コマンドレットを使用します。
この例の出力が参照してください。、`update-networkcontroller`コマンドレットを更新するネットワーク コント ローラーを使用します。 

>[!IMPORTANT]
>インストールにも更新がある場合は、このコマンドレットを実行します。


```Powershell
PS C:\> update-networkcontroller
NetworkControllerClusterVersion NetworkControllerVersion
------------------------------- ------------------------
10.1.1                          10.1.15
```

## <a name="backup-the-sdn-infrastructure"></a>SDN インフラストラクチャのバックアップ

ネットワーク コント ローラーのデータベースの定期的なバックアップにより、災害やデータ損失が発生した場合のビジネス継続性。  セッションが複数のネットワーク コント ローラーのノードは引き続き確実にできないために、ネットワーク コント ローラーの Vm をバックアップするための十分ではありません。

**要件:**
* SMB 共有と、共有とファイル システムへの読み取り/書き込みアクセス許可を持つ資格情報。
* 同様に GMSA を使用して、ネットワーク コント ローラーがインストールされた場合にも、グループ管理サービス アカウント (GMSA) を使用できます。

**手順:**

1. 任意の VM のバックアップ方法を使用して、または HYPER-V を使用して、各ネットワーク コント ローラー VM のコピーをエクスポートします。<p>ネットワーク コント ローラー VM のバックアップにより、データベースの復号化のために必要な証明書が存在します。  

2. System Center Virtual Machine Manager (SCVMM) を使用する場合は、SCVMM サービスを停止し、SQL Server を使用してバックアップを作成します。<p>ここでの目的では、更新プログラムを取得行われていないことを SCVMM にこの時点では、ネットワーク コント ローラーのバックアップおよび SCVMM の間に不整合が生じる可能性の中に確認します。  

   >[!IMPORTANT]
   >再始めないでください SCVMM サービス、ネットワーク コント ローラーのバックアップが完了するまでです。

3. ネットワーク コント ローラーのデータベースをバックアップ、`new-networkcontrollerbackup`コマンドレット。

4. 完了と成功した場合、バックアップの確認、`get-networkcontrollerbackup`コマンドレット。

5. SCVMM を使用する場合は、SCVMM サービスを開始します。



### <a name="example-backing-up-the-network-controller-database"></a>以下に例を示します。ネットワーク コント ローラーのデータベースをバックアップします。

```Powershell
$URI = "https://NC.contoso.com"
$Credential = Get-Credential

# Get or Create Credential object for File share user

$ShareUserResourceId = "BackupUser"

$ShareCredential = Get-NetworkControllerCredential -ConnectionURI $URI -Credential $Credential | Where {$_.ResourceId -eq $ShareUserResourceId }
If ($ShareCredential -eq $null) {
    $CredentialProperties = New-Object Microsoft.Windows.NetworkController.CredentialProperties
    $CredentialProperties.Type = "usernamePassword"
    $CredentialProperties.UserName = "contoso\alyoung"
    $CredentialProperties.Value = "<Password>"

    $ShareCredential = New-NetworkControllerCredential -ConnectionURI $URI -Credential $Credential -Properties $CredentialProperties -ResourceId $ShareUserResourceId -Force
}

# Create backup

$BackupTime = (get-date).ToString("s").Replace(":", "_")

$BackupProperties = New-Object Microsoft.Windows.NetworkController.NetworkControllerBackupProperties
$BackupProperties.BackupPath = "\\fileshare\backups\NetworkController\$BackupTime"
$BackupProperties.Credential = $ShareCredential

$Backup = New-NetworkControllerBackup -ConnectionURI $URI -Credential $Credential -Properties $BackupProperties -ResourceId $BackupTime -Force
```

### <a name="example-checking-the-status-of-a-network-controller-backup-operation"></a>以下に例を示します。ネットワーク コント ローラーのバックアップ操作の状態の確認

```Powershell
PS C:\ > Get-NetworkControllerBackup -ConnectionUri $URI -Credential $Credential -ResourceId $Backup.ResourceId
| ConvertTo-JSON -Depth 10
{
    "Tags":  null,
    "ResourceRef":  "/networkControllerBackup/2017-04-25T16_53_13",
    "InstanceId":  "c3ea75ae-2892-4e10-b26c-a2243b755dc8",
    "Etag":  "W/\"0dafea6c-39db-401b-bda5-d2885ded470e\"",
    "ResourceMetadata":  null,
    "ResourceId":  "2017-04-25T16_53_13",
    "Properties":  {
                    "BackupPath":  "\\\\fileshare\backups\NetworkController\\2017-04-25T16_53_13",
                    "ErrorMessage":  "",
                    "FailedResourcesList":  [

                                            ],
                    "SuccessfulResourcesList":  [
                                                    "/networking/v1/credentials/11ebfc10-438c-4a96-a1ee-8a048ce675be",
                                                    "/networking/v1/credentials/41229069-85d4-4352-be85-034d0c5f4658",
                                                    "/networking/v1/credentials/b2a82c93-2583-4a1f-91f8-232b801e11bb",
                                                    "/networking/v1/credentials/BackupUser",
                                                    "/networking/v1/credentials/fd5b1b96-b302-4395-b6cd-ed9703435dd1",
                                                    "/networking/v1/virtualNetworkManager/configuration",
                                                    "/networking/v1/virtualSwitchManager/configuration",
                                                    "/networking/v1/accessControlLists/f8b97a4c-4419-481d-b757-a58483512640",
                                                    "/networking/v1/logicalnetworks/24fa1af9-88d6-4cdc-aba0-66e38c1a7bb8",
                                                    "/networking/v1/logicalnetworks/48610528-f40b-4718-938e-99c2be76f1e0",
                                                    "/networking/v1/logicalnetworks/89035b49-1ee3-438a-8d7a-f93cbae40619",
                                                    "/networking/v1/logicalnetworks/a9c8eaa0-519c-4988-acd6-11723e9efae5",
                                                    "/networking/v1/logicalnetworks/d4ea002c-c926-4c57-a178-461d5768c31f",
                                                    "/networking/v1/macPools/11111111-1111-1111-1111-111111111111",
                                                    "/networking/v1/loadBalancerManager/config",
                                                    "/networking/v1/publicIPAddresses/2c502b2d-b39a-4be1-a85a-55ef6a3a9a1d",
                                                    "/networking/v1/GatewayPools/Default",
                                                    "/networking/v1/servers/4c4c4544-0058-5810-8056-b4c04f395931",
                                                    "/networking/v1/servers/4c4c4544-0058-5810-8057-b4c04f395931",
                                                    "/networking/v1/servers/4c4c4544-0058-5910-8056-b4c04f395931",
                                                    "/networking/v1/networkInterfaces/058430d3-af43-4328-a440-56540f41da50",
                                                    "/networking/v1/networkInterfaces/08756090-6d55-4dec-98d5-80c4c5a47db8",
                                                    "/networking/v1/networkInterfaces/2175d74a-aacd-44e2-80d3-03f39ea3bc5d",
                                                    "/networking/v1/networkInterfaces/2400c2c3-2291-4b0b-929c-9bb8da55851a",
                                                    "/networking/v1/networkInterfaces/4c695570-6faa-4e4d-a552-0b36ed3e0962",
                                                    "/networking/v1/networkInterfaces/7e317638-2914-42a8-a2dd-3a6d966028d6",
                                                    "/networking/v1/networkInterfaces/834e3937-f43b-4d3c-88be-d79b04e63bce",
                                                    "/networking/v1/networkInterfaces/9d668fe6-b1c6-48fc-b8b1-b3f98f47d508",
                                                    "/networking/v1/networkInterfaces/ac4650ac-c3ef-4366-96e7-d9488fb661ba",
                                                    "/networking/v1/networkInterfaces/b9f23e35-d79e-495f-a1c9-fa626b85ae13",
                                                    "/networking/v1/networkInterfaces/fdd929f1-f64f-4463-949a-77b67fe6d048",
                                                    "/networking/v1/virtualServers/15a891ee-7509-4e1d-878d-de0cb4fa35fd",
                                                    "/networking/v1/virtualServers/57416993-b410-44fd-9675-727cd4e98930",
                                                    "/networking/v1/virtualServers/5f8aebdc-ee5b-488f-ac44-dd6b57bd316a",
                                                    "/networking/v1/virtualServers/6c812217-5931-43dc-92a8-1da3238da893",
                                                    "/networking/v1/virtualServers/d78b7fa3-812d-4011-9997-aeb5ded2b431",
                                                    "/networking/v1/virtualServers/d90820a5-635b-4016-9d6f-bf3f1e18971d",
                                                    "/networking/v1/loadBalancerMuxes/5f8aebdc-ee5b-488f-ac44-dd6b57bd316a_suffix",
                                                    "/networking/v1/loadBalancerMuxes/d78b7fa3-812d-4011-9997-aeb5ded2b431_suffix",
                                                    "/networking/v1/loadBalancerMuxes/d90820a5-635b-4016-9d6f-bf3f1e18971d_suffix",
                                                    "/networking/v1/Gateways/15a891ee-7509-4e1d-878d-de0cb4fa35fd_suffix",
                                                    "/networking/v1/Gateways/57416993-b410-44fd-9675-727cd4e98930_suffix",
                                                    "/networking/v1/Gateways/6c812217-5931-43dc-92a8-1da3238da893_suffix",
                                                    "/networking/v1/virtualNetworks/b3dbafb9-2655-433d-b47d-a0e0bbac867a",
                                                    "/networking/v1/virtualNetworks/d705968e-2dc2-48f2-a263-76c7892fb143",
                                                    "/networking/v1/loadBalancers/24fa1af9-88d6-4cdc-aba0-66e38c1a7bb8_10.127.132.2",
                                                    "/networking/v1/loadBalancers/24fa1af9-88d6-4cdc-aba0-66e38c1a7bb8_10.127.132.3",
                                                    "/networking/v1/loadBalancers/24fa1af9-88d6-4cdc-aba0-66e38c1a7bb8_10.127.132.4"
                                                ],
                    "InProgressResourcesList":  [

                                                ],
                    "ProvisioningState":  "Succeeded",
                    "Credential":  {
                                        "Tags":  null,
                                        "ResourceRef":  "/credentials/BackupUser",
                                        "InstanceId":  "00000000-0000-0000-0000-000000000000",
                                        "Etag":  null,
                                        "ResourceMetadata":  null,
                                        "ResourceId":  null,
                                        "Properties":  null
                                    }
                }
}
```

## <a name="restore-the-sdn-infrastructure-from-a-backup"></a>SDN インフラストラクチャをバックアップから復元します。

必要なすべてのコンポーネントをバックアップから復元するときに、SDN 環境を動作状態に返します。  

>[!IMPORTANT]
>手順は、復元のコンポーネントの数によって異なります。


1. 必要に応じて、HYPER-V ホストと必要な記憶域を再デプロイします。

2. 必要に応じて、ネットワーク コント ローラー Vm、RAS ゲートウェイの Vm および Mux Vm をバックアップから復元します。 

3. 停止の NC ホスト エージェントとすべての HYPER-V ホストで SLB ホスト エージェント:

    ```
    stop-service slbhostagent

    stop-service nchostagent
    ```

4. RAS ゲートウェイの Vm を停止します。

5. SLB Mux Vm を停止します。

6. ネットワーク コント ローラーの復元、`new-networkcontrollerrestore`コマンドレット。

7. 復元の確認**ProvisioningState**復元が正常に完了したかを把握します。

8. SCVMM を使用する場合、ネットワーク コント ローラーのバックアップと同時に作成されたバックアップを使用して、SCVMM のデータベースを復元します。

9. ワークロード Vm をバックアップから復元する場合は、今すぐ行います。

10. デバッグ networkcontrollerconfigurationstate コマンドレットを使用してシステムの正常性を確認します。

```Powershell
$cred = Get-Credential
Debug-NetworkControllerConfigurationState -NetworkController "https://NC.contoso.com" -Credential $cred

Fetching ResourceType:     accessControlLists
Fetching ResourceType:     servers
Fetching ResourceType:     virtualNetworks
Fetching ResourceType:     networkInterfaces
Fetching ResourceType:     virtualGateways
Fetching ResourceType:     loadbalancerMuxes
Fetching ResourceType:     Gateways
```

### <a name="example-restoring-a-network-controller-database"></a>以下に例を示します。ネットワーク コント ローラーのデータベースを復元します。
 
```Powershell
$URI = "https://NC.contoso.com"
$Credential = Get-Credential

$ShareUserResourceId = "BackupUser"
$ShareCredential = Get-NetworkControllerCredential -ConnectionURI $URI -Credential $Credential | Where {$_.ResourceId -eq $ShareUserResourceId }

$RestoreProperties = New-Object Microsoft.Windows.NetworkController.NetworkControllerRestoreProperties
$RestoreProperties.RestorePath = "\\fileshare\backups\NetworkController\2017-04-25T16_53_13"
$RestoreProperties.Credential = $ShareCredential

$RestoreTime = (Get-Date).ToString("s").Replace(":", "_")
New-NetworkControllerRestore -ConnectionURI $URI -Credential $Credential -Properties $RestoreProperties -ResourceId $RestoreTime -Force
```

### <a name="example-checking-the-status-of-a-network-controller-database-restore"></a>以下に例を示します。ネットワーク コント ローラーのデータベースの復元の状態の確認

```PowerShell
PS C:\ > get-networkcontrollerrestore -connectionuri $uri -credential $cred -ResourceId $restoreTime | convertto-json -depth 10
{
    "Tags":  null,
    "ResourceRef":  "/networkControllerRestore/2017-04-26T15_04_44",
    "InstanceId":  "22edecc8-a613-48ce-a74f-0418789f04f6",
    "Etag":  "W/\"f14f6b84-80a7-4b73-93b5-59a9c4b5d98e\"",
    "ResourceMetadata":  null,
    "ResourceId":  "2017-04-26T15_04_44",
    "Properties":  {
                    "RestorePath":  "\\\\sa18fs\\sa18n22\\NetworkController\\2017-04-25T16_53_13",
                    "ErrorMessage":  null,
                    "FailedResourcesList":  null,
                    "SuccessfulResourcesList":  null,
                    "ProvisioningState":  "Succeeded",
                    "Credential":  null
                }
}
```


表示される状態メッセージの構成については、次を参照してください。 [、Windows Server 2016 ソフトウェア定義ネットワーク スタックのトラブルシューティングを行う](https://docs.microsoft.com/windows-server/networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack)します。