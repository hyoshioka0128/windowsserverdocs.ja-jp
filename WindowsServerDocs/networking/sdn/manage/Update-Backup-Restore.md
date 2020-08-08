---
title: SDN インフラストラクチャのアップグレード、バックアップ、復元
description: このトピックでは、SDN インフラストラクチャを更新、バックアップ、および復元する方法について説明します。
manager: grcusanz
ms.topic: article
ms.assetid: e9a8f2fd-48fe-4a90-9250-f6b32488b7a4
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/27/2018
ms.openlocfilehash: daca883456a32c707fc2c7b9bfd6193b0d917b58
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942582"
---
# <a name="upgrade-backup-and-restore-sdn-infrastructure"></a>SDN インフラストラクチャのアップグレード、バックアップ、復元

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、SDN インフラストラクチャを更新、バックアップ、および復元する方法について説明します。

## <a name="upgrade-the-sdn-infrastructure"></a>SDN インフラストラクチャをアップグレードする
SDN インフラストラクチャは、Windows Server 2016 から Windows Server 2019 にアップグレードできます。 アップグレードの順序付けについては、「SDN インフラストラクチャを更新する」セクションで説明したのと同じ手順を実行します。 アップグレードする前に、ネットワークコントローラーデータベースのバックアップを作成することをお勧めします。

ネットワークコントローラーのコンピューターの場合は、NetworkControllerNode コマンドレットを使用して、アップグレードの完了後にノードの状態を確認します。 他のノードをアップグレードする前に、ノードが "アップ" 状態に戻っていることを確認します。 すべてのネットワークコントローラーノードをアップグレードすると、ネットワークコントローラーは、1時間以内にネットワークコントローラークラスター内で実行されているマイクロサービスを更新します。 即時更新は、networkcontroller コマンドレットを使用してトリガーできます。

ソフトウェア定義ネットワーク (SDN) システムのすべてのオペレーティングシステムコンポーネントに同じ Windows 更新プログラムをインストールします。これには次のものが含まれます。

- SDN が有効になっている Hyper-v ホスト
- ネットワークコントローラー Vm
- ソフトウェア Load Balancer Mux Vm
- RAS ゲートウェイ Vm

>[!IMPORTANT]
>System Center Virtual Manager を使用する場合は、最新の更新プログラムのロールアップで更新する必要があります。

各コンポーネントを更新するときに、Windows 更新プログラムのインストールに標準の方法のいずれかを使用できます。 ただし、ワークロードのダウンタイムを最小限に抑え、ネットワークコントローラーデータベースの整合性を確保するには、次の手順を実行します。

1. 管理コンソールを更新します。<p>ネットワークコントローラーの Powershell モジュールを使用する各コンピューターに更新プログラムをインストールします。  NetworkController ロールが単独でインストールされているすべての場所を含めることができます。 ネットワークコントローラーの Vm 自体を除外する。これらの更新は、次の手順で行います。

2. 最初のネットワークコントローラー VM で、すべての更新プログラムをインストールし、を再起動します。

3. 次のネットワークコントローラー VM に進む前に、コマンドレットを使用して、 `get-networkcontrollernode` 更新して再起動したノードの状態を確認します。

4. 再起動サイクル中に、[ネットワークコントローラー] ノードが停止するのを待ってから、もう一度バックアップします。<p>VM を再起動した後、状態が "**_アップ_**" に戻るまで数分かかることがあります。 出力の例については、「」を参照してください。

5. 各 SLB Mux VM に更新プログラムを1つずつインストールして、ロードバランサーインフラストラクチャの継続的な可用性を確保します。

6. Hyper-v ホストと RAS ゲートウェイを更新します。これは、**スタンバイ**モードになっている ras ゲートウェイを含むホストから始まります。<p>RAS ゲートウェイ Vm は、テナント接続を失わずにライブで移行することはできません。 更新サイクル中に、テナント接続が新しい RAS ゲートウェイにフェールオーバーする回数を最小限に抑えるように注意する必要があります。 ホストと RAS ゲートウェイの更新を調整することにより、各テナントは1回フェールオーバーされます。

    a. ライブマイグレーションが可能な Vm のホストを退避させします。<p>RAS ゲートウェイ Vm はホスト上に残す必要があります。

    b. このホストの各ゲートウェイ VM に更新プログラムをインストールします。

    c. 更新でゲートウェイ VM を再起動する必要がある場合は、VM を再起動します。

    d. 更新されたばかりのゲートウェイ VM が含まれているホストに更新プログラムをインストールします。

    e. 更新プログラムによって必要になった場合は、ホストを再起動します。

    f. スタンバイゲートウェイを含む追加のホストごとに、この手順を繰り返します。<p>スタンバイゲートウェイが残っていない場合は、残りのすべてのホストに対して同じ手順を実行します。


### <a name="example-use-the-get-networkcontrollernode-cmdlet"></a>例: networkcontrollernode コマンドレットを使用する

この例では、 `get-networkcontrollernode` ネットワークコントローラー vm のいずれかで実行されるコマンドレットの出力を確認できます。

出力例に表示されるノードの状態は次のとおりです。

- NCNode1.contoso.com = Down
- NCNode2.contoso.com = 上
- NCNode3.contoso.com = 上

>[!IMPORTANT]
>追加のノードを一度に1つずつ更新する前に、ノードの状態が変更_**されるまで**_ 数分待つ必要があります。

すべてのネットワークコントローラーノードを更新すると、ネットワークコントローラーは1時間以内にネットワークコントローラークラスター内で実行されているマイクロサービスを更新します。

>[!TIP]
>コマンドレットを使用して即時更新をトリガーすることができ `update-networkcontroller` ます。


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

### <a name="example-use-the-update-networkcontroller-cmdlet"></a>例: networkcontroller コマンドレットを使用する
この例では、 `update-networkcontroller` ネットワークコントローラーを強制的に更新するコマンドレットの出力を確認できます。

>[!IMPORTANT]
>インストールする更新プログラムがこれ以上ない場合は、このコマンドレットを実行します。


```Powershell
PS C:\> update-networkcontroller
NetworkControllerClusterVersion NetworkControllerVersion
------------------------------- ------------------------
10.1.1                          10.1.15
```

## <a name="backup-the-sdn-infrastructure"></a>SDN インフラストラクチャをバックアップする

ネットワークコントローラーデータベースの定期的なバックアップによって、障害やデータの損失が発生した場合にビジネスの継続性が確保されます。  ネットワークコントローラー Vm をバックアップするだけでは十分ではありません。これは、複数のネットワークコントローラーノードでセッションが続行されることがないためです。

**要件:**
* 共有とファイルシステムへの読み取り/書き込みアクセス許可を持つ SMB 共有と資格情報。
* ネットワークコントローラーが GMSA を使用してインストールされている場合は、必要に応じて、グループの管理されたサービスアカウント (GMSA) を使用することもできます。

**作業**

1. 任意の VM バックアップ方法を使用するか、Hyper-v を使用して各ネットワークコントローラー VM のコピーをエクスポートします。<p>ネットワークコントローラー VM をバックアップすると、データベースの暗号化解除に必要な証明書が確実に存在するようになります。

2. System Center Virtual Machine Manager (SCVMM) を使用している場合は、SCVMM サービスを停止し、SQL Server 経由でバックアップします。<p>ここでの目的は、この期間中に SCVMM に更新が行われないようにすることです。これにより、ネットワークコントローラーのバックアップと SCVMM の間に不整合が生じる可能性があります。

   >[!IMPORTANT]
   >ネットワークコントローラーのバックアップが完了するまで、SCVMM サービスを再起動しないでください。

3. コマンドレットを使用してネットワークコントローラーデータベースをバックアップし `new-networkcontrollerbackup` ます。

4. コマンドレットを使用して、バックアップの完了と成功を確認し `get-networkcontrollerbackup` ます。

5. SCVMM を使用している場合は、SCVMM サービスを開始します。



### <a name="example-backing-up-the-network-controller-database"></a>例: ネットワークコントローラーデータベースをバックアップする

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

### <a name="example-checking-the-status-of-a-network-controller-backup-operation"></a>例: ネットワークコントローラーのバックアップ操作の状態を確認する

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

## <a name="restore-the-sdn-infrastructure-from-a-backup"></a>バックアップから SDN インフラストラクチャを復元する

バックアップから必要なすべてのコンポーネントを復元すると、SDN 環境が動作状態に戻ります。

>[!IMPORTANT]
>手順は、復元されるコンポーネントの数によって異なります。


1. 必要に応じて、Hyper-v ホストと必要な記憶域を再展開します。

2. 必要に応じて、ネットワークコントローラー Vm、RAS ゲートウェイ Vm、および Mux Vm をバックアップから復元します。

3. すべての Hyper-v ホスト上の NC ホストエージェントと SLB ホストエージェントを停止します。

    ```
    stop-service slbhostagent

    stop-service nchostagent
    ```

4. RAS ゲートウェイの Vm を停止します。

5. SLB Mux Vm を停止します。

6. コマンドレットを使用してネットワークコントローラーを復元し `new-networkcontrollerrestore` ます。

7. 復元が正常に完了したことを確認するには、restore **ProvisioningState**を確認してください。

8. SCVMM を使用している場合は、ネットワークコントローラーのバックアップと同時に作成されたバックアップを使用して SCVMM データベースを復元します。

9. バックアップからワークロード Vm を復元する場合は、ここで作成します。

10. Networkcontrollerconfigurationstate コマンドレットを使用してシステムの正常性を確認します。

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

### <a name="example-restoring-a-network-controller-database"></a>例: ネットワークコントローラーデータベースを復元する

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

### <a name="example-checking-the-status-of-a-network-controller-database-restore"></a>例: ネットワークコントローラーのデータベース復元の状態を確認する

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


表示される構成状態メッセージの詳細については、「 [Windows Server 2016 ソフトウェア定義ネットワークスタックのトラブルシューティング](https://docs.microsoft.com/windows-server/networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack)」を参照してください。