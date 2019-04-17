---
title: "更新プログラム、バックアップと復元のソフトウェアによるネットワーク制御インフラストラクチャ"
description: "このトピックは、Windows Server 2016 での更新、バックアップと復元の SDN インフラストラクチャについてソフトウェア定義ネットワーク ガイドの一部です。"
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: e9a8f2fd-48fe-4a90-9250-f6b32488b7a4
ms.author: grcusanz
author: grcusanz
ms.openlocfilehash: bb7194ec865db980962853b87d68a84a5446269e
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="update-backup-and-restore-software-defined-networking-infrastructure"></a>更新プログラム、バックアップと復元のソフトウェアによるネットワーク制御インフラストラクチャ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックには、次のセクションが含まれています。

- [SDN インフラストラクチャを更新](#bkmk_Updating)
- [バックアップ、SDN インフラストラクチャ](#bkmk_backup)
- [SDN インフラストラクチャをバックアップから復元します。](#bkmk_restore)

## <a name="bkmk_Updating"></a>SDN インフラストラクチャを更新

更新は、ソフトウェアによるネットワーク制御 (SDN) システムのオペレーティング システムのコンポーネントのすべての Windows 更新プログラムをインストールするプロセスです。  これにより、SDN が含まれます。Hyper-v ホスト、ネットワーク コントローラー Vm、ソフトウェア ロード バランサー マルチプレクサー Vm と RAS ゲートウェイ Vm を有効にします。  同じ更新プログラムがインストールされている一連の正確なこれらすべてのコンポーネントがあることが重要です。  System Center Virtual Machine Manager が使用されている場合もに更新することも、最新の更新プログラムのロールアップにもをお勧めします。

各コンポーネントの更新は、windows の更新プログラムをインストールするための標準的な方法を使用して、以下の手順が説明されてただし従う必要があるワークロードの場合、時間を最小限に抑えることを確認し、ネットワーク コントローラーのデータベースの整合性を確保します。

### <a name="step-1-update-the-management-consoles"></a>手順 1: 管理コンソールを更新します。
各ネットワーク コントローラーの Powershell モジュールを使用するコンピューター上の必要な更新プログラムをインストールします。  任意の場所を単独でインストールされている、RSAT NetworkController 役割であるこれが含まれます。  これは、手順 2 で更新するように、ネットワーク コントローラー Vm 自体含まれていません。

### <a name="step-2-update-the-network-controllers"></a>手順 2: ネットワーク コントローラーを更新します。
これは、最も重要な手順更新サイクルで各ネットワーク コントローラー VM 更新する必要があるあり、[次へ] を続行する前に、ネットワーク コントローラー クラスターで完全にバックアップがオンラインであるためです。

1 つのネットワーク コントローラー VM を起動し、すべての必要な更新プログラムをインストールします。  必要な場合は、VM を再起動します。

次に進む前にネットワーク コントローラーのバーチャル マシンが更新されたノードの状態を確認する get networkcontrollernode を使用し、再起動します。  ネットワーク コントローラー ノードの再起動サイクル中に、下へ移動し、戻るともう一度を待ちます。  VM が再起動された後はアップ状態に戻すには数分まだかかることができます。

#### <a name="example-using-get-networkcontrollernode-to-check-the-status-of-network-controller-nodes"></a>例: get networkcontrollernode を使用してネットワーク コントローラーのノードの状態を確認するには

この例では、ネットワーク コントローラー Vm のいずれかの内側から get networkcontrollernode を実行してからの出力を示します。  NCNode1.contoso.com がダウンしている他の 2 つのノードが正常な状態が表示されます。  必要がありますになるまで待機状態まで数分にそのノードの任意の他のノードの更新を続行する前にセットアップします。

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

ネットワーク コントローラーのすべてのノードは、アップ状態では後でのみに、その他のネットワーク コントローラーのノードごとにこの手順を繰り返しますできますか。  一度に 1 つの各ノードの更新プログラムを続行します。

すべてのネットワーク コントローラーのノードを更新すると、ネットワーク コントローラーは 1 時間以内にネットワーク コントローラー クラスター内で実行されている microservices を更新します。  更新 networkcontroller コマンドレットを使用して即時更新プログラムをトリガーすることができます。

#### <a name="example-using-update-networkcontroller-to-force-network-controller-to-update"></a>例: 更新プログラムをネットワーク コントローラーを強制的に更新 networkcontroller の使用

このコマンドは、更新プログラムをインストールするまでの残りができない場合、更新 networkcontroller の結果を示します。

```Powershell
PS C:\> update-networkcontroller
NetworkControllerClusterVersion NetworkControllerVersion
------------------------------- ------------------------
10.1.1                          10.1.15
```

### <a name="step-3-update-slb-muxes"></a>手順 3: 更新プログラムの SLB Muxes

ロード バランサーのインフラストラクチャの継続的可用性を確保する時に、いずれかの各 SLB Mux VM で更新プログラムをインストールします。

### <a name="step-4-update-hyper-v-hosts-and-ras-gateways"></a>手順 4: 更新プログラムの Hyper-V ホストと RAS ゲートウェイ

RAS ゲートウェイ Vm は、テナント接続を失うことがなく移行、ライブですることはできません、ために、接続にフェールオーバーする新しい RAS ゲートウェイ更新サイクル中にそのテナントの回数を最小限に抑えるために注意を払う必要があります。  RAS ゲートウェイ、ホストの更新を調整して各テナントはのみフェールオーバー最大で 1 回です。  

以降では、スタンバイ モードにする RAS ゲートウェイが含まれているホストは、ホストごとに次の手順に従います。

1.  ライブ マイグレーションの対応であるバーチャル マシンのホストを退避します。  RAS ゲートウェイ Vm は、ホスト上に残ります必要があります。
2.  このホスト上の各ゲートウェイ仮想マシンに更新プログラムをインストールします。
3.  更新プログラムがゲートウェイ VM を再起動する必要がある場合は、VM を再起動します。  
4.  ゲートウェイが同じ更新された VM を格納しているホストに更新プログラムをインストールします。
5.  更新プログラムで必要な場合は、ホストを再起動します。
6.  スタンバイのゲートウェイを含む各追加のホストを繰り返します。  スタンバイ ゲートウェイが残っていない場合は、残りのすべてのホストの同じ手順をに従ってください。

## <a name="bkmk_backup"></a>バックアップ、SDN インフラストラクチャ

ネットワーク コントローラーのデータベースの定期的なバックアップでは、災害やデータの損失が発生した場合、ビジネス継続性を確保に重要です。  ネットワーク コントローラー Vm のバックアップは不十分ですので、複数のネットワーク コントローラーのノードにクォーラムが保持されることは保証されません。
要件:
 * SMB 共有および、共有とファイル システムへの読み取り/書き込みアクセス許可を持つ資格情報。
 * また、GMSA を使用して、ネットワーク コントローラーがインストールされた場合必要に応じて、グループ管理サービス アカウント (GMSA) を使用できます。

バックアップを実行するこれらの手順に従います。

1. 任意の VM のバックアップ方法を使用してネットワーク コントローラー Vm をバックアップするか、Hyper-V を使用して、各ネットワーク コントローラー VM のコピーをエクスポートします。  これは、インフラストラクチャの Vm の復元を含む完全な再構築が実行した場合、データベースの暗号化を解除の必要な証明書が存在することを確認します。
2. System Center Virtual Machine Manager (SCVMM) を使用している場合は、SCVMM サービスを停止し、更新が行われていないことを SCVMM SCVMM とネットワーク コントローラーのバックアップの間に矛盾が生じる可能性がこの期間中にすることを確認する SQL Server を使用してバックアップを作成します。  再起動しない、SCVMM サービス、ネットワーク コントローラーのバックアップが完了するまでです。
3. ネットワーク コントローラーを新しい networkcontrollerbackup を使用してデータベースをバックアップします。

 #### <a name="example-backing-up-the-network-controller-database"></a>ネットワーク コントローラーのデータベースをバックアップする例。
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

4. 完了し、バックアップの成功を確認するには、get networkcontrollerbackup を使用します。

 #### <a name="example-checking-the-status-of-a-network-controller-backup-operation"></a>例: ネットワーク コントローラーのバックアップ操作のステータスの確認

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

5.  SCVMM を使用する場合は、SCVMM サービスを開始するようになりました。

## <a name="bkmk_restore"></a>SDN インフラストラクチャをバックアップから復元します。

復元は、すべての必要なコンポーネントを SDN 環境を運用状態に戻すへのバックアップから復元するプロセスです。  手順については、復元されるコンポーネントの量によって若干異なります。

1. 必要に応じて、Hyper-V ホストと必要な記憶域を再展開します。

2. 必要に応じて、ネットワーク コントローラー Vm、RAS ゲートウェイ Vm および Mux Vm をバックアップから復元します。 

3. すべての Hyper-V ホスト上の NC ホスト エージェントと SLB ホスト エージェントを停止します。

    ```
    stop-service slbhostagent

    stop-service nchostagent
    ```

4. RAS ゲートウェイ Vm を停止します。

5. SLB Mux Vm を停止します。

6. 新しい networkcontrollerrestore コマンドレットを使用して、ネットワーク コントローラーを復元します。

 #### <a name="example-restoring-a-network-controller-database"></a>例: ネットワーク コントローラー データベースを復元します。
 
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

7. 復元 ProvisioningState を復元が正常に完了したときに知ることを確認します。

 #### <a name="example-checking-the-status-of-a-network-controller-database-restore"></a>例: ネットワーク コントローラーのデータベースの復元の状態を確認します。

    ```
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

8. SCVMM を使用している場合は、ネットワーク コントローラーのバックアップとして同時に作成されたバックアップを使用して SCVMM データベースを復元します。

9. ワークロード Vm は、バックアップから復元中場合を行うようになりました。

10. システムのヘルスを確認するのにには、デバッグ networkcontrollerconfigurationstate コマンドレットを使用します。

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

表示される構成の状態メッセージについては、次を参照してください。[、Windows Server 2016 ソフトウェア定義ネットワーク スタックのトラブルシューティングを行う](https://docs.microsoft.com/windows-server/networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack)します。