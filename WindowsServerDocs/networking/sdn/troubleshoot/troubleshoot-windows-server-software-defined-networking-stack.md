---
title: Windows Server ソフトウェア定義ネットワーク スタックのトラブルシューティング
description: この Windows Server のガイドでは、ソフトウェア定義ネットワーク (SDN) の一般的なエラーおよび障害シナリオを調査し、使用可能な診断ツールを活用してトラブルシューティングのワークフローの概要を説明します。
manager: ravirao
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 9be83ed2-9e62-49e8-88e7-f52d3449aac5
ms.author: pashort
author: JMesser81
ms.date: 08/14/2018
ms.openlocfilehash: eeb0c335e4afd3c6835a04421a15073aeab6cdc6
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446242"
---
# <a name="troubleshoot-the-windows-server-software-defined-networking-stack"></a>Windows Server ソフトウェア定義ネットワーク スタックのトラブルシューティング

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このガイドでは、一般的なソフトウェアによるネットワーク制御 (SDN) エラーと障害のシナリオを検証し、使用可能な診断ツールを活用してトラブルシューティングのワークフローを概説します。  

マイクロソフトのソフトウェアがネットワーク定義の詳細については、次を参照してください。 [ソフトウェア定義されるネットワーク](../../sdn/Software-Defined-Networking--SDN-.md)します。  

## <a name="error-types"></a>エラーの種類  
次の一覧は、市場投入までの運用環境のデプロイメントから Windows Server 2012 R2 で HYPER-V ネットワーク仮想化 (HNVv1) が最も多く見られますの問題のクラスを表し、さまざまな方法で同じ種類の新しいソフトウェア ネットワーク (SDN) スタックでの Windows Server 2016 HNVv2 で表示される問題と一致します。  

ほとんどのエラーは、少数のクラスに分類できます。   
* **無効またはサポートされていない構成**  
   ユーザーは、誤って、または無効なポリシーを使用して、NorthBound API を呼び出します。   

* **ポリシー アプリケーションのエラー**  
     ネットワーク コント ローラーからのポリシーは、大幅に遅延および/またはない最新の状態 (たとえば、ライブ マイグレーションを実行) 後のすべての HYPER-V ホストで HYPER-V ホストに配信されませんでした。  
* **構成の誤差またはソフトウェアのバグ**  
  破棄されたパケットのデータ パスの問題です。  

* **NIC のハードウェアに関連する外部エラー/ドライバーや、アンダーレイ ネットワーク ファブリック**  
  (VMQ) などの作業負荷を軽減または (MTU) などの構成が間違っているアンダーレイ ネットワーク ファブリックを適切に動作しません。   

  このトラブルシューティング ガイドでは、これらのエラー カテゴリの各検証し、ベスト プラクティスを特定し、エラーの解決に使用できる診断ツールをお勧めします。  

## <a name="diagnostic-tools"></a>診断ツール  

各この種のエラーのトラブルシューティングのワークフローを説明する前に使用できる診断ツールを調べてみましょう。   

ネットワーク コント ローラー (コントロール パス) の診断ツールを使用するのには、最初 RSAT NetworkController 機能をインストールし、インポートする必要があります、 ``NetworkControllerDiagnostics`` モジュール。  

```  
Add-WindowsFeature RSAT-NetworkController -IncludeManagementTools  
Import-Module NetworkControllerDiagnostics  
```  

インポートする必要があります (データ パス) の HNV 診断診断ツールを使用する、 ``HNVDiagnostics`` モジュール。

```  
# Assumes RSAT-NetworkController feature has already been installed
Import-Module hnvdiagnostics   
```  

### <a name="network-controller-diagnostics"></a>ネットワーク コント ローラーの診断  
Technet の「これらのコマンドレットについては、 [ネットワーク コント ローラー診断コマンドレット トピック](https://docs.microsoft.com/powershell/module/networkcontrollerdiagnostics/)します。 コントロール パスとネットワーク コント ローラーと HYPER-V ホストで実行されている NC ホスト エージェントの間にネットワーク コント ローラーのノード間でネットワーク ポリシーの整合性に問題を特定するのに役立ちます。

 _デバッグ ServiceFabricNodeStatus_ と _Get NetworkControllerReplica_ ネットワーク コント ローラーのノードのバーチャル マシンのいずれかのコマンドレットを実行する必要があります。 その他のすべての NC 診断コマンドレットは、ネットワーク コント ローラーに接続し、ネットワーク コント ローラーの管理セキュリティ グループ (Kerberos) のいずれかが、またはネットワーク コント ローラーを管理するための X.509 証明書にアクセスするすべてのホストから実行できます。 

### <a name="hyper-v-host-diagnostics"></a>HYPER-V ホストでの診断  
Technet の「これらのコマンドレットについては、 [Hyper-v ネットワーク仮想化 (HNV) 診断コマンドレット トピック](https://docs.microsoft.com/powershell/module/hnvdiagnostics/)します。 テナント仮想マシン (東または西) 間のデータ パスの問題を特定できると SLB VIP (北または南) からトラフィックを受信します。 

_デバッグ VirtualMachineQueueOperation_, 、_Get CustomerRoute_, 、_Get PACAMapping_, 、_Get ProviderAddress_, 、_Get VMNetworkAdapterPortId_, 、_Get VMSwitchExternalPortId_, 、および _テスト EncapOverheadSettings_ すべての HYPER-V ホストから実行できるすべてのローカル テストします。 その他のコマンドレットでは、ネットワーク コント ローラーを介してデータ パスのテストを呼び出すし、したがって上 descried としてネットワーク コント ローラーへのアクセスを必要です。

### <a name="github"></a>GitHub
[Microsoft/SDN GitHub リポジトリ](https://github.com/microsoft/sdn) が数多くサンプル スクリプトとワークフロー内のこれらのコマンドレットの上に構築する必要があります。 具体的には、診断のスクリプトは記載されて、 [診断](https://github.com/Microsoft/sdn/diagnostics) フォルダーです。 プル要求を送信することでこれらのスクリプトへの協力にご協力します。

## <a name="troubleshooting-workflows-and-guides"></a>ワークフローおよびガイドのトラブルシューティング  

### <a name="hoster-validate-system-health"></a>[ホスト]システム正常性を検証します。
という名前の埋め込みリソースがある _構成状態_ ネットワーク コント ローラーのリソースのいくつか。 構成の状態は、ネットワーク コント ローラーの構成と HYPER-V ホスト上の実際の (実行中) 状態の一貫性を含むシステム正常性に関する情報を提供します。 

構成の状態を確認するには、ネットワーク コント ローラーへの接続にすべての HYPER-V ホストから、次を実行します。

>[!NOTE] 
>値、 *NetworkController* パラメーターと、"X.509 のサブジェクト名に基づく FQDN または IP アドレスである"か > ネットワーク コント ローラー用に証明書。
>
>*資格情報* パラメーターのみをネットワーク コント ローラーが Kerberos 認証 (VMM の展開で標準) を使用するかどうかに指定する必要があります。 ネットワーク コント ローラーの管理セキュリティ グループに属するユーザーの資格情報があります。

```none
Debug-NetworkControllerConfigurationState -NetworkController <FQDN or NC IP> [-Credential <PS Credential>]

# Healthy State Example - no status reported
$cred = Get-Credential
Debug-NetworkControllerConfigurationState -NetworkController 10.127.132.211 -Credential $cred

Fetching ResourceType:     accessControlLists
Fetching ResourceType:     servers
Fetching ResourceType:     virtualNetworks
Fetching ResourceType:     networkInterfaces
Fetching ResourceType:     virtualGateways
Fetching ResourceType:     loadbalancerMuxes
Fetching ResourceType:     Gateways
```

サンプル構成の状態メッセージは、以下に示します。

```none
Fetching ResourceType:     servers
---------------------------------------------------------------------------------------------------------
ResourcePath:     https://10.127.132.211/Networking/v1/servers/4c4c4544-0056-4b10-8058-b8c04f395931
Status:           Warning

Source:           SoftwareLoadBalancerManager
Code:             HostNotConnectedToController
Message:          Host is not Connected.
----------------------------------------------------------------------------------------------------------
```

>[!NOTE]
> SLB Mux 転送中の VM NIC のネットワーク インターフェイス リソースは「仮想スイッチ-ホスト接続をコント ローラー以外」のエラーで失敗状態にあるシステムのバグがあります。 VM の NIC のリソースの IP 構成が転送中の論理ネットワークの IP プールから IP アドレスに設定されている場合は、このエラーを無視しても問題ありません。 "仮想スイッチ-PortBlocked"のエラーで失敗状態で、ゲートウェイ HNV プロバイダーの VM の Nic のネットワーク インターフェイス リソースのあるシステムでは、2 番目のバグがあります。 このエラーも無視しても安全 VM の NIC のリソースの IP 構成が設定されている場合 (デザイン) によって null にします。


次の表には、監視構成の状態に基づいて実行するには、エラー コード、メッセージ、およびフォロー アップのアクションの一覧が表示されます。


| **コード**| **メッセージ**| **操作**|  
|--------|-----------|----------|  
| Unknown| 不明なエラー| |  
| HostUnreachable                       | ホスト コンピューターが到達可能ではありません。 | ネットワーク コント ローラーとホスト間での管理ネットワーク接続を確認します。 |  
| PAIpAddressExhausted                  | PA Ip アドレスの不足 | HNV プロバイダー論理サブネットの IP プールのサイズを増やす |  
| PAMacAddressExhausted                 | PA の Mac アドレスをすべて使用しました。 | Mac プールの範囲を広げる |  
| PAAddressConfigurationFailure         | ホストの PA アドレスを組み込むために失敗しました | ネットワーク コント ローラーとホスト間の管理ネットワーク接続を確認します。 |  
| CertificateNotTrusted                 | 証明書が信頼されていません。  |ホストとの通信に使用される証明書を修正します。 |  
| CertificateNotAuthorized              | 証明書が承認されていません。 | ホストとの通信に使用される証明書を修正します。 |  
| PolicyConfigurationFailureOnVfp       | VFP ポリシーの構成の失敗 | これは、実行時エラーです。  なしの確実な回避策です。 ログを収集します。 |  
| PolicyConfigurationFailure            | 通信エラーまたはその他のユーザーによる、ホストへのポリシーのプッシュの障害、NetworkController のエラーです。| 確実な操作はありません。  これは、目標とする状態、ネットワーク コント ローラー モジュールの処理のエラーが原因です。 ログを収集します。 |  
| HostNotConnectedToController          | ホストがネットワーク コント ローラーにまだ接続されていません。 | ポート プロファイルが適用されない、または、ホスト上では、ネットワーク コント ローラーから到達できません。 ホスト Id のレジストリ キーにサーバー リソースのインスタンス ID が一致することを検証します。 |  
| MultipleVfpEnabledSwitches            | 複数 VFp が、ホストでスイッチを有効には  | ネットワーク コント ローラーのホストのエージェントでは、VFP 拡張を有効化と 1 つの vSwitch のみがサポートされているので、スイッチのいずれかを削除します。 |  
| PolicyConfigurationFailure            | 証明書のエラーまたは接続エラーのため VmNic の VNet のポリシーをプッシュできませんでした。  | 確認して適切な証明書が展開されているかどうか (証明書サブジェクト名は、ホストの FQDN を一致する必要があります)。 また、ホストと接続を確認、ネットワーク コント ローラー |  
| PolicyConfigurationFailure            | 証明書のエラーまたは接続エラーのため VmNic の vSwitch ポリシーをプッシュできませんでした。  | 確認して適切な証明書が展開されているかどうか (証明書サブジェクト名は、ホストの FQDN を一致する必要があります)。 また、ホストと接続を確認、ネットワーク コント ローラー|
| PolicyConfigurationFailure            | 証明書のエラーまたは接続エラーのため VmNic のファイアウォール ポリシーをプッシュできませんでした。 | 確認して適切な証明書が展開されているかどうか (証明書サブジェクト名は、ホストの FQDN を一致する必要があります)。 また、ホストと接続を確認、ネットワーク コント ローラー|
| DistributedRouterConfigurationFailure | ホスト vNic の分散ルーター設定を構成できませんでした。                          | TCP/IP スタックのエラーです。 このエラーが報告されたサーバー上の PA と災害復旧ホスト Vnic のクリーンアップが必要な場合があります。 |
| DhcpAddressAllocationFailure          | VMNic の DHCP アドレス割り当てに失敗しました                                                    | NIC のリソースに静的 IP アドレス属性が構成されているかどうかは確認します。 |  
| CertificateNotTrusted<br>CertificateNotAuthorized | ネットワークまたは証明書のエラーにより Mux に接続できませんでした。 | エラー メッセージのコードで提供されている数値コードを確認します。 これは winsock エラー コードに対応します。 きめ細かいものでは証明書のエラー (たとえば、証明書を確認することはできません、証明書が承認されていないなどです)。 |  
| HostUnreachable                       | MUX に問題があります (一般的なケースは切断 BGPRouter) | BGP ピア RRAS (BGP 仮想マシン) または上部ラック (ToR) スイッチでは、正常に到達できないまたはいないピアリングです。 ソフトウェア ロード バランサー マルチプレクサー リソースと BGP ピア (ToR または RRAS 仮想マシン) の両方で BGP 設定を確認します。 |  
| HostNotConnectedToController          | SLB ホスト エージェントが接続されていません。  | SLB ホスト エージェント サービスが実行されていることを確認上の理由から、SLB ホスト エージェントのログ (自動実行) を参照してください、SLBM (NC) が実行されているホストのエージェントによって提示される証明書を拒否された場合に状態情報が表示されます微妙  |  
| PortBlocked                           | VNET がないことによる、VFP ポートがブロックされている/ACL ポリシー | ポリシーを構成しない場合があります、その他のエラーがあることを確認します。 |  
| 過負荷                            | Loadbalancer MUX はオーバー ロードします。  | MUX のパフォーマンスに関する問題 |  
| RoutePublicationFailure               | Loadbalancer MUX が BGP ルーターに接続されていません。 | 正しくセットアップされているチェック、MUX BGP ルーターおよびその BGP ピアリングとの接続がある場合 |  
| VirtualServerUnreachable              | Loadbalancer MUX が SLB マネージャーに接続されていません。 | SLBM とマルチプレクサー間の接続を確認します。 |  
| QosConfigurationFailure               | QOS ポリシーの構成に失敗しました | 十分な帯域幅は、QOS の予約を使用する場合はすべての仮想マシン用に使用可能なかどうかを参照してください。 |


#### <a name="check-network-connectivity-between-the-network-controller-and-hyper-v-host-nc-host-agent-service"></a>ネットワーク コント ローラーと HYPER-V ホスト (NC ホスト エージェント サービス) の間のネットワーク接続を確認します。
実行、 *netstat* NC ホスト エージェントとネットワーク コント ローラーのノードと HYPER-V ホスト上の 1 つのリッスン ソケットの間の 3 つの確立した接続があることを検証する次のコマンド
- HYPER-V ホスト (NC ホスト エージェント サービス) にポート TCP:6640 でリッスンしています。
- HYPER-V から確立されている 2 つの接続をホストに一時的なポート (> 32000) の NC ノードの IP ポート 6640 で IP
- ネットワーク コント ローラー REST ip ポート 6640 で一時的なポートでの HYPER-V ホストの IP から 1 つに確立された接続

>[!NOTE]
>ある可能性がありますのみ HYPER-V ホスト上で確立されている 2 つの接続を特定のホストに展開されているテナントのバーチャル マシンがない場合。

```none
netstat -anp tcp |findstr 6640

# Successful output
  TCP    0.0.0.0:6640           0.0.0.0:0              LISTENING
  TCP    10.127.132.153:6640    10.127.132.213:50095   ESTABLISHED
  TCP    10.127.132.153:6640    10.127.132.214:62514   ESTABLISHED
  TCP    10.127.132.153:50023   10.127.132.211:6640    ESTABLISHED
```
#### <a name="check-host-agent-services"></a>ホスト エージェント サービスを確認します。
ネットワーク コント ローラーは、HYPER-V ホスト上の 2 つのホスト エージェント サービスと通信します。SLB ホスト エージェントと NC ホスト エージェント。 これらのサービスの一方または両方が実行されていないことことができます。 その状態を確認し、それらを実行していない場合は再起動します。

```none
Get-Service SlbHostAgent
Get-Service NcHostAgent

# (Re)start requires -Force flag
Start-Service NcHostAgent -Force
Start-Service SlbHostAgent -Force
```

#### <a name="check-health-of-network-controller"></a>ネットワーク コント ローラーの状態を確認します。
次の 3 つの確立した接続がある場合、またはネットワーク コント ローラーが応答していない場合は、すべてのノードおよびサービス モジュールが稼働している次のコマンドレットを使用して、確認します。 

```none
# Prints a DIFF state (status is automatically updated if state is changed) of a particular service module replica 
Debug-ServiceFabricNodeStatus [-ServiceTypeName] <Service Module>
```
ネットワーク コント ローラー サービス モジュールは次のとおりです。
- ControllerService
- ApiService
- SlbManagerService
- ServiceInsertion
- FirewallService
- VSwitchService
- GatewayManager
- FnmService
- HelperService
- UpdateService

ReplicaStatus はあることを確認 **準備** HealthState は **Ok**します。

実稼働で展開が、複数ノードのネットワーク コント ローラーと各サービスのプライマリになっているノードと個々 のレプリカの状態を確認することもできます。

```none  
Get-NetworkControllerReplica

# Sample Output for the API service module 
Replicas for service: ApiService

ReplicaRole   : Primary
NodeName      : SA18N30NC3.sa18.nttest.microsoft.com
ReplicaStatus : Ready

```
レプリカの状態が準備完了であることを確認サービスごとにします。

#### <a name="check-for-corresponding-hostids-and-certificates-between-network-controller-and-each-hyper-v-host"></a>対応するホストの Id とネットワーク コント ローラーと各 HYPER-V ホスト間で証明書の確認 
HYPER-V ホストでは、ホスト Id がネットワーク コント ローラー上のサーバー リソースのインスタンス Id に対応しているかを確認するには、次のコマンドを実行します

```none
Get-ItemProperty "hklm:\system\currentcontrolset\services\nchostagent\parameters" -Name HostId |fl HostId

HostId : **162cd2c8-08d4-4298-8cb4-10c2977e3cfe**

Get-NetworkControllerServer -ConnectionUri $uri |where { $_.InstanceId -eq "162cd2c8-08d4-4298-8cb4-10c2977e3cfe"}

Tags             :
ResourceRef      : /servers/4c4c4544-0056-4a10-8059-b8c04f395931
InstanceId       : **162cd2c8-08d4-4298-8cb4-10c2977e3cfe**
Etag             : W/"50f89b08-215c-495d-8505-0776baab9cb3"
ResourceMetadata : Microsoft.Windows.NetworkController.ResourceMetadata
ResourceId       : 4c4c4544-0056-4a10-8059-b8c04f395931
Properties       : Microsoft.Windows.NetworkController.ServerProperties
```

*修復* SDNExpress を使用してスクリプトまたは手動展開の更新サーバー リソースのインスタンス Id に一致するようにレジストリ内のホスト Id キーです。 VMM を使用して、HYPER-V サーバーを VMM から削除する場合は、HYPER-V ホスト (物理サーバー) 上のネットワーク コント ローラー ホスト エージェントを再起動し、ホスト Id のレジストリ キーを削除します。 次に、VMM を使用してサーバーを再度追加します。


(SouthBound) 間の通信、HYPER-V ホスト (NC ホスト エージェント サービス) とネットワーク コント ローラーのノード (ホスト名は証明書のサブジェクト名になります) から HYPER-V ホストによって使用される X.509 証明書の拇印が同じであることを確認します。 あることを確認、ネットワーク コント ローラーの残りの部分の証明書のサブジェクト名 *CN =<FQDN or IP>* します。

```  
# On Hyper-V Host
dir cert:\\localmachine\my  

Thumbprint                                Subject
----------                                -------
2A3A674D07D8D7AE11EBDAC25B86441D68D774F9  CN=SA18n30-4.sa18.nttest.microsoft.com
...

dir cert:\\localmachine\root

Thumbprint                                Subject
----------                                -------
30674C020268AA4E40FD6817BA6966531FB9ADA4  CN=10.127.132.211 **# NC REST IP ADDRESS**

# On Network Controller Node VM
dir cert:\\localmachine\root  

Thumbprint                                Subject
----------                                -------
2A3A674D07D8D7AE11EBDAC25B86441D68D774F9  CN=SA18n30-4.sa18.nttest.microsoft.com
30674C020268AA4E40FD6817BA6966531FB9ADA4  CN=10.127.132.211 **# NC REST IP ADDRESS**
...
```  

各証明書サブジェクト名は何だかどうかを確認するは、次のパラメーターを確認することもできます (ホスト名または NC REST FQDN または IP) が必要な証明書がまだ失効していない、および信頼されたルート証明機関に証明書チェーン内のすべての証明機関が含まれています。

- サブジェクト名  
- 失効日  
- 信頼されるルート証明機関  

*修復* 複数の証明書では、HYPER-V ホストに同じサブジェクト名がある、ネットワーク コント ローラーのホストのエージェントは無作為に選択ネットワーク コント ローラーに表示する 1 つです。 これが、既知のネットワーク コント ローラーにサーバー リソースのサムプリントとは一致しません。 この場合、HYPER-V ホスト上の同じサブジェクト名を持つ証明書のいずれかを削除し、ネットワーク コント ローラーのホストのエージェント サービスを再開します。 まだ、接続は確立されません、HYPER-V ホスト上の同じサブジェクト名を持つその他の証明書を削除し、VMM での対応するサーバー リソースを削除します。 次に、vmm は新しい X.509 証明書を生成し、HYPER-V ホストにインストールされるサーバー リソースを再作成します。


#### <a name="check-the-slb-configuration-state"></a>SLB 構成状態を確認します。
デバッグ NetworkController コマンドレットに出力の一部として、SLB 構成の状態を確認できます。 このコマンドレットは、JSON ファイル、各 HYPER-V ホスト (サーバー) からのすべての IP 構成とホスト エージェントのデータベース テーブルからローカル ネットワーク ポリシーでネットワーク コント ローラーのリソースの現在のセットも出力されます。 

その他のトレースは、既定で収集されます。 トレースを収集しない追加の IncludeTraces: $false のパラメーターです。

```none
Debug-NetworkController -NetworkController <FQDN or IP> [-Credential <PS Credential>] [-IncludeTraces:$false]

# Don't collect traces
$cred = Get-Credential 
Debug-NetworkController -NetworkController 10.127.132.211 -Credential $cred -IncludeTraces:$false

Transcript started, output file is C:\\NCDiagnostics.log
Collecting Diagnostics data from NC Nodes
```

>[!NOTE]
>既定の出力場所は、< working_directory > \NCDiagnostics\ ディレクトリになります。 使用して既定の出力ディレクトリを変更できる、 `-OutputDirectory` パラメーター。 

SLB 構成の状態については記載されて、 _診断 slbstateResults.Json_ このディレクトリ内のファイルです。

この JSON ファイルは、次のセクションに分けることができます。
 * ファブリック
   * SlbmVips - このセクションでは、coodinate 構成と状態 SLB Muxes と SLB ホストのエージェントの間にネットワーク コント ローラーで使用される SLB Manager の VIP アドレスの IP アドレスを一覧表示します。
   * MuxState - このセクションには 1 つの値の一覧各 SLB Mux 展開、mux の状態を与える
   * ルーターの構成 - このセクションで、上流のルーターの (BGP ピア) ボックスの一覧は自律システム番号 (ASN)、転送中の IP アドレス、および ID SLB Muxes ASN および転送中の IP も表示されます。
   * ホスト情報のこのセクションで接続されている、管理 ip アドレス ボックスの一覧のすべてのワークロードの負荷分散を実行できるように HYPER-V ホスト アドレスします。
   * Vip 範囲 - このセクションには、パブリックとプライベートの VIP IP プールの範囲が表示されます。 SLBM VIP は割り当てられている IP からこれらの範囲のいずれかとして含まれます。 
   * Mux ルート - このセクションには 1 つの値の一覧各 SLB Mux 展開されているすべての特定のマルチプレクサーのルートのアドバタイズを含みます。
 * テナント
   * VipConsolidatedState - このセクションには接続状態の一覧アドバタイズされたルート プレフィックス、HYPER-V ホストおよび DIP エンドポイントを含む各テナント VIP です。

> [!NOTE]
> 使用して直接 SLB 状態を確認できる、 [DumpSlbRestState](https://github.com/Microsoft/SDN/blob/master/Diagnostics/DumpSlbRestState.ps1) スクリプトで使用できる、 [Microsoft SDN GitHub リポジトリ](https://github.com/microsoft/sdn)です。 

#### <a name="gateway-validation"></a>ゲートウェイの検証

**ネットワーク コント ローラー: から**
```
Get-NetworkControllerLogicalNetwork
Get-NetworkControllerPublicIPAddress
Get-NetworkControllerGatewayPool
Get-NetworkControllerGateway
Get-NetworkControllerVirtualGateway
Get-NetworkControllerNetworkInterface
```

**ゲートウェイ VM: から**
```
Ipconfig /allcompartments /all
Get-NetRoute -IncludeAllCompartments -AddressFamily
Get-NetBgpRouter
Get-NetBgpRouter | Get-BgpPeer
Get-NetBgpRouter | Get-BgpRouteInformation
```

**トップ オブ ラック (ToR) スイッチ: から**

`sh ip bgp summary (for 3rd party BGP Routers)`

**Windows BGP ルーター**
```
Get-BgpRouter
Get-BgpPeer
Get-BgpRouteInformation
```

これらの問題を解決します (特にで SDNExpress ベースの展開の場合)、これまできましたが、に加えて GW Vm 上で構成を取得されていないテナント コンパートメントの最も一般的な理由と思われる FabricConfig.psd1 で GW 容量が TenantConfig.psd1 にしようとするどのような人々 (S2S トンネル) のネットワーク接続に割り当てるよりも少なくします。 これは、次のコマンドの出力を比較することによって簡単にチェックすることができます。

```
PS > (Get-NetworkControllerGatewayPool -ConnectionUri $uri).properties.Capacity
PS > (Get-NetworkControllerVirtualgatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "TenantName").properties.OutboundKiloBitsPerSecond
PS > (Get-NetworkControllerVirtualgatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "TenantName").property
```

### <a name="hoster-validate-data-plane"></a>[ホスト]平面データを検証します。
ネットワーク コント ローラーが展開されている、テナントの仮想ネットワークとサブネットを作成し、Vm が仮想サブネットに関連付けられる後、は、テナント接続を確認したり、ホスト側によって追加のファブリック レベルのテストを実行することができます。

#### <a name="check-hnv-provider-logical-network-connectivity"></a>HNV プロバイダーの論理ネットワーク接続を確認します。
HYPER-V ホストで実行されている VM がテナントの仮想ネットワークに接続された最初のゲストの後にネットワーク コント ローラーは、HYPER-V ホストに 2 つの HNV プロバイダー IP アドレス (PA IP アドレス) を割り当てます。 これらの Ip では、HNV プロバイダー論理ネットワークの IP プールから取得され、ネットワーク コント ローラーで管理します。  これら 2 つの HNV の IP アドレスを調べるの

```none
PS > Get-ProviderAddress

# Sample Output
ProviderAddress : 10.10.182.66
MAC Address     : 40-1D-D8-B7-1C-04
Subnet Mask     : 255.255.255.128
Default Gateway : 10.10.182.1
VLAN            : VLAN11

ProviderAddress : 10.10.182.67
MAC Address     : 40-1D-D8-B7-1C-05
Subnet Mask     : 255.255.255.128
Default Gateway : 10.10.182.1
VLAN            : VLAN11
```

これら HNV プロバイダー IP アドレス (PA Ip) が独立した TCPIP ネットワーク コンパートメントで作成したイーサネット アダプターに割り当てられておりのアダプターの名前を付ける _VLANX_ X は HNV プロバイダー (トランスポート) の論理ネットワークに割り当てられている VLAN です。

論理ネットワークを行う追加のコンパートメントを持つ ping HNV プロバイダーを使用して 2 つの HYPER-V ホスト間の接続 (-c Y) Y が、PAhostVNICs が作成された TCPIP ネットワーク コンパートメントのパラメーターです。 このコンパートメントは、実行することで決定できます。

```none
C:\> ipconfig /allcompartments /all

<snip> ...
==============================================================================
Network Information for *Compartment 3*
==============================================================================
   Host Name . . . . . . . . . . . . : SA18n30-2
<snip> ...

Ethernet adapter VLAN11:

   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : Microsoft Hyper-V Network Adapter
   Physical Address. . . . . . . . . : 40-1D-D8-B7-1C-04
   DHCP Enabled. . . . . . . . . . . : No
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::5937:a365:d135:2899%39(Preferred)
   IPv4 Address. . . . . . . . . . . : 10.10.182.66(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.128
   Default Gateway . . . . . . . . . : 10.10.182.1
   NetBIOS over Tcpip. . . . . . . . : Disabled

Ethernet adapter VLAN11:

   Connection-specific DNS Suffix  . :
   Description . . . . . . . . . . . : Microsoft Hyper-V Network Adapter
   Physical Address. . . . . . . . . : 40-1D-D8-B7-1C-05
   DHCP Enabled. . . . . . . . . . . : No
   Autoconfiguration Enabled . . . . : Yes
   Link-local IPv6 Address . . . . . : fe80::28b3:1ab1:d9d9:19ec%44(Preferred)
   IPv4 Address. . . . . . . . . . . : 10.10.182.67(Preferred)
   Subnet Mask . . . . . . . . . . . : 255.255.255.128
   Default Gateway . . . . . . . . . : 10.10.182.1
   NetBIOS over Tcpip. . . . . . . . : Disabled

*Ethernet adapter vEthernet (PAhostVNic):*
<snip> ...
```

>[!NOTE]
> PA ホスト vNIC アダプターでは、データ パスで使用されていないと、そのため、「vEthernet (PAhostVNic) アダプター」に割り当てられている ip アドレスはありません。

たとえば、HYPER-V ホスト 1 と 2 は、HNV プロバイダー (PA) の IP アドレスであるとします。

|HYPER-V のホスト:|-1 PA IP アドレス|-2 PA IP アドレス|
|---             |---            |---             |
|ホスト 1 | 10.10.182.64 | 10.10.182.65 |
|ホスト 2 | 10.10.182.66 | 10.10.182.67 |

次のコマンドを使用して HNV プロバイダーの論理ネットワークの接続をチェックする 2 つの ping を実行します。

```none
# Ping the first PA IP Address on Hyper-V Host 2 from the first PA IP address on Hyper-V Host 1 in compartment (-c) 3
C:\> ping -c 3 10.10.182.66 -S 10.10.182.64

# Ping the second PA IP Address on Hyper-V Host 2 from the first PA IP address on Hyper-V Host 1 in compartment (-c) 3
C:\> ping -c 3 10.10.182.67 -S 10.10.182.64

# Ping the first PA IP Address on Hyper-V Host 2 from the second PA IP address on Hyper-V Host 1 in compartment (-c) 3
C:\> ping -c 3 10.10.182.66 -S 10.10.182.65

# Ping the second PA IP Address on Hyper-V Host 2 from the second PA IP address on Hyper-V Host 1 in compartment (-c) 3
C:\> ping -c 3 10.10.182.67 -S 10.10.182.65
```

*修復* 場合の HNV プロバイダー ping にありません作業は、VLAN の構成を含め、物理的なネットワーク接続を確認します。 各 HYPER-V ホスト上の物理 Nic は、割り当てられていない特定の VLAN をトランク モードにする必要があります。 管理ホスト vNIC は、管理の論理ネットワークの VLAN に分離する必要があります。

```none
PS C:\> Get-NetAdapter "Ethernet 4" |fl

Name                       : Ethernet 4
InterfaceDescription       : <NIC> Ethernet Adapter
InterfaceIndex             : 2
MacAddress                 : F4-52-14-55-BC-21
MediaType                  : 802.3
PhysicalMediaType          : 802.3
InterfaceOperationalStatus : Up
AdminStatus                : Up
LinkSpeed(Gbps)            : 10
MediaConnectionState       : Connected
ConnectorPresent           : True
*VlanID                     : 0*
DriverInformation          : Driver Date 2016-08-28 Version 5.25.12665.0 NDIS 6.60

# VMM uses the older PowerShell cmdlet <Verb>-VMNetworkAdapterVlan to set VLAN isolation
PS C:\> Get-VMNetworkAdapterVlan -ManagementOS -VMNetworkAdapterName <Mgmt>

VMName VMNetworkAdapterName Mode     VlanList
------ -------------------- ----     --------
<snip> ...        
       Mgmt                 Access   7
<snip> ...

# SDNExpress deployments use the newer PowerShell cmdlet <Verb>-VMNetworkAdapterIsolation to set VLAN isolation
PS C:\> Get-VMNetworkAdapterIsolation -ManagementOS

<snip> ...

IsolationMode        : Vlan
AllowUntaggedTraffic : False
DefaultIsolationID   : 7
MultiTenantStack     : Off
ParentAdapter        : VMInternalNetworkAdapter, Name = 'Mgmt'
IsTemplate           : True
CimSession           : CimSession: .
ComputerName         : SA18N30-2
IsDeleted            : False

<snip> ...
```

#### <a name="check-mtu-and-jumbo-frame-support-on-hnv-provider-logical-network"></a>HNV のプロバイダーの論理ネットワーク上の MTU およびジャンボ フレームのサポートを確認します。

HNV のプロバイダーの論理ネットワーク内の別の一般的な問題は、物理ネットワーク ポートおよびイーサネット カードが VXLAN (NVGRE) カプセル化によるオーバーヘッドを処理するように構成するのに十分な大きさ MTU を持っていないことです。 
>[!NOTE]
> 一部のイーサネット カードとドライバー サポート、新しい * EncapOverhead キーワードである数値 160、ネットワーク コント ローラー ホスト エージェントによって自動的に設定されます。 この値は、の値には追加し、* JumboPacket キーワードの合計は、アドバタイズされた MTU として使用されます。
> 例: * EncapOverhead = 160 と * JumboPacket 1514 の = = > MTU 1674B =

```none
# Check whether or not your Ethernet card and driver support *EncapOverhead
PS C:\ > Test-EncapOverheadSettings

Verifying Physical Nic : <NIC> Ethernet Adapter #2
Physical Nic  <NIC> Ethernet Adapter #2 can support SDN traffic. Encapoverhead value set on the nic is  160
Verifying Physical Nic : <NIC> Ethernet Adapter
Physical Nic  <NIC> Ethernet Adapter can support SDN traffic. Encapoverhead value set on the nic is  160
```

HNV のプロバイダーの論理ネットワークが、大きい MTU サイズ エンド ツー エンドをサポートしているかどうかをテストするには、使用、 _テスト LogicalNetworkSupportsJumboPacket_ コマンドレット。
```none
# Get credentials for both source host and destination host (or use the same credential if in the same domain)
$sourcehostcred = Get-Credential
$desthostcred = Get-Credential

# Use the Management IP Address or FQDN of the Source and Destination Hyper-V hosts
Test-LogicalNetworkSupportsJumboPacket -SourceHost sa18n30-2 -DestinationHost sa18n30-3 -SourceHostCreds $sourcehostcred -DestinationHostCreds $desthostcred

# Failure Results
SourceCompartment : 3
pinging Source PA: 10.10.182.66 to Destination PA: 10.10.182.64 with Payload: 1632
pinging Source PA: 10.10.182.66 to Destination PA: 10.10.182.64 with Payload: 1472
Checking if physical nics support jumbo packets on host
Physical Nic  <NIC> Ethernet Adapter #2 can support SDN traffic. Encapoverhead value set on the nic is  160
Cannot send jumbo packets to the destination. Physical switch ports may not be configured to support jumbo packets.
Checking if physical nics support jumbo packets on host
Physical Nic  <NIC> Ethernet Adapter #2 can support SDN traffic. Encapoverhead value set on the nic is  160
Cannot send jumbo packets to the destination. Physical switch ports may not be configured to support jumbo packets.

# TODO: Success Results aftering updating MTU on physical switch ports
```

*修復*
* 以上である物理スイッチ ポートで MTU サイズを調整する 1674B (14B イーサネット ヘッダーとトレーラーを含む)
* NIC カードが EncapOverhead キーワードをサポートしていない場合は、少なくとも、JumboPacket キーワードを調整する 1674B


#### <a name="check-tenant-vm-nic-connectivity"></a>テナント VM の NIC の接続を確認します。
ゲスト VM に割り当てられている各 VM の NIC には、プライベート カスタマー アドレス (CA) と HNV プロバイダー アドレス (PA) 空間の間で CA と PA マッピングがあります。 これらのマッピングが各 HYPER-V ホストで OVSDB server のテーブルに保持され、次のコマンドレットを実行することによって検出されたことができます。

```none
# Get all known PA-CA Mappings from this particular Hyper-V Host
PS > Get-PACAMapping

CA IP Address CA MAC Address    Virtual Subnet ID PA IP Address
------------- --------------    ----------------- -------------
10.254.254.2  00-1D-D8-B7-1C-43              4115 10.10.182.67
10.254.254.3  00-1D-D8-B7-1C-43              4115 10.10.182.67
192.168.1.5   00-1D-D8-B7-1C-07              4114 10.10.182.65
10.254.254.1  40-1D-D8-B7-1C-06              4115 10.10.182.66
192.168.1.1   40-1D-D8-B7-1C-06              4114 10.10.182.66
192.168.1.4   00-1D-D8-B7-1C-05              4114 10.10.182.66
```
>[!NOTE]
> 期待する CA と PA のマッピングは、特定のテナント VM 用の出力ではない場合、は、ネットワーク コント ローラーを使用して、上の VM NIC と ip アドレス構成のリソースを確認してください、 _Get NetworkControllerNetworkInterface_ コマンドレットです。 また、NC ホスト エージェントとネットワーク コント ローラーのノード間で確立された接続を確認してください。

この情報は、テナントの VM ping できるネットワーク コント ローラーを使用して、ホスト側によって起動されるよう、 _テスト VirtualNetworkConnection_ コマンドレットです。

## <a name="specific-troubleshooting-scenarios"></a>具体的なトラブルシューティング シナリオ

次のセクションでは、特定のシナリオのトラブルシューティングのガイダンスを提供します。

### <a name="no-network-connectivity-between-two-tenant-virtual-machines"></a>2 つのテナント仮想マシン間のネットワーク接続なし

1.  [テナント]テナントのバーチャル マシンで Windows ファイアウォールがトラフィックをブロックしていないことを確認します。  
2.  [テナント]IP アドレスがテナントの仮想マシンに実行して、割り当てられたことを確認して _ipconfig_します。 
3.  [ホスト]実行**テスト VirtualNetworkConnection**問題の 2 つのテナント仮想マシン間の接続を検証する HYPER-V ホストから。 

>[!NOTE]
>VSID と仮想サブネット ID には VXLAN の場合これは、VXLAN ネットワーク識別子 (VNI) です。 実行して、この値を見つけることができます、 **Get PACAMapping**コマンドレット。

#### <a name="example"></a>例

    $password = ConvertTo-SecureString -String "password" -AsPlainText -Force
    $cred = New-Object pscredential -ArgumentList (".\administrator", $password) 

"Sa18n30-2.sa18.nttest.microsoft.com"10.127.132.153 ListenerCA IP への管理 ip アドレス 192.168.1.5 を仮想サブネット (VSID) 4114 アタッチされている両方の CA の ping 間"緑 Web VM 1"のホスト上の 192.168.1.4 SenderCA ip を作成します。

    Test-VirtualNetworkConnection -OperationId 27 -HostName sa18n30-2.sa18.nttest.microsoft.com -MgmtIp 10.127.132.153 -Creds $cred -VMName "Green Web VM 1" -VMNetworkAdapterName "Green Web VM 1" -SenderCAIP 192.168.1.4 -SenderVSID 4114 -ListenerCAIP 192.168.1.5 -ListenerVSID 4114

    Test-VirtualNetworkConnection at command pipeline position 1

CA 空間 ping テストの開始アドレス 192.168.1.4 から成功 192.168.1.5 をトレース セッション Ping を開始する Rtt = 0 ミリ秒


CA のルーティング情報:

    Local IP: 192.168.1.4
    Local VSID: 4114
    Remote IP: 192.168.1.5
    Remote VSID: 4114
    Distributed Router Local IP: 192.168.1.1
    Distributed Router Local MAC: 40-1D-D8-B7-1C-06
    Local CA MAC: 00-1D-D8-B7-1C-05
    Remote CA MAC: 00-1D-D8-B7-1C-07
    Next Hop CA MAC Address: 00-1D-D8-B7-1C-07

ルーティング情報の PA:

    Local PA IP: 10.10.182.66
    Remote PA IP: 10.10.182.65

 <snip> ...

4. [テナント]仮想サブネットまたはトラフィックをブロックする VM ネットワーク インターフェイスで指定された分散型のファイアウォール ポリシーがないことを確認します。    

Sa18.nttest.microsoft.com ドメイン内で sa18n30nc デモ環境でのネットワーク コント ローラーの REST API のクエリを実行します。

    $uri = "https://sa18n30nc.sa18.nttest.microsoft.com"
    Get-NetworkControllerAccessControlList -ConnectionUri $uri 

# <a name="look-at-ip-configuration-and-virtual-subnets-which-are-referencing-this-acl"></a>IP 構成と仮想サブネットをこの ACL を参照しています

1. [ホスト]実行 ``Get-ProviderAddress`` 両方の HYPER-V でホストをホストしている 2 つの質問の仮想マシンをテナントし、実行 ``Test-LogicalNetworkConnection`` または ``ping -c <compartment>`` HNV プロバイダーの論理ネットワーク上の接続を検証できる HYPER-V ホストから
2.  [ホスト]MTU 設定が HYPER-V ホスト上で正しいことと、レイヤー 2 HYPER-V ホストの間にデバイスを切り替えることを確認します。 実行 ``Test-EncapOverheadValue`` 対象のすべての HYPER-V ホストにします。 また間にあるすべてのレイヤー 2 スイッチが MTU 160 バイトの最大のオーバーヘッドを考慮する最小限の 1674 バイトに設定をあることを確認します。  
3.  [ホスト]PA IP アドレスが存在しない CA 接続を確立できない場合や場合、は、ネットワーク ポリシーが受信されたことを確認することを確認します。 実行 ``Get-PACAMapping`` をカプセル化のルールと仮想ネットワークのオーバーレイを作成するために必要な CA と PA のマッピングが正しく確立されるかどうかを参照してください。  
4.  [ホスト]ネットワーク コント ローラーにネットワーク コント ローラーのホストのエージェントが接続されていることを確認してください。 実行 ``netstat -anp tcp |findstr 6640`` かどうかを   
5.  [ホスト]ホストが HKLM に ID チェック テナントのバーチャル マシンをホストしているサーバーのリソースのインスタンス ID と一致します。  
6. [ホスト]ポート プロファイルの ID に、テナントのバーチャル マシンの VM ネットワーク インターフェイスのインスタンス ID が一致することを確認してください。  

## <a name="logging-tracing-and-advanced-diagnostics"></a>ログ、トレース、および高度な診断

次のセクションでは、高度な診断でログ記録、およびトレース情報を提供します。

### <a name="network-controller-centralized-logging"></a>ネットワーク コント ローラーがログ記録を集中管理 

ネットワーク コント ローラーを自動的にデバッガーのログを収集し、一元的な場所に保管します。 後でいつでも、初めてのネットワーク コント ローラーを展開するときに、ログの収集を有効にできます。 ログを選択して、ネットワーク コント ローラーから収集されるネットワーク ネットワーク コント ローラーで管理されている要素: コンピューター、ソフトウェアによる負荷分散 (SLB) とゲートウェイのマシンをホストします。 

これらのログには、ネットワーク コント ローラー クラスター、ネットワーク コント ローラー アプリケーション、ゲートウェイのログ、SLB、仮想ネットワークおよび分散型のファイアウォールのデバッグ ログが含まれます。 ネットワーク コント ローラーに新しいホスト/SLB/ゲートウェイを追加するたびにそれらのコンピューターのログ記録が開始されます。 同様に、ネットワーク コント ローラーからホスト/SLB/ゲートウェイが削除されると、それらのコンピューターのログが停止されました。

#### <a name="enable-logging"></a>ログを有効にする

ネットワーク コント ローラーを使用してクラスターをインストールするときに、ログ記録が自動的に有効になって、**インストール NetworkControllerCluster**コマンドレット。 既定では、ログ収集されます。 ローカルでのネットワーク コント ローラーのノードに *%systemdrive%\SDNDiagnostics*します。 **を強くお勧め** (ローカルではありません)、リモート ファイル共有にするには、この場所を変更することです。 

ネットワーク コント ローラーのクラスター ログが格納されている *%programData%\Windows Fabric\log\Traces*します。 ログ コレクションに対して一元的な場所を指定することができます、 **DiagnosticLogLocation**もこれは推奨事項にパラメーターをリモート ファイル共有にします。 

この場所へのアクセスを制限する場合は、アクセス資格情報を行うことができます、 **LogLocationCredential**パラメーター。 指定する必要がある、ログの場所へのアクセスに資格情報を提供する場合、 **CredentialEncryptionCertificate**パラメーターで、ネットワーク コント ローラーのノードでローカルに格納されている資格情報を暗号化するために使用します。  

既定の設定であるかローカル ノードの中央の場所、および 25 GB の空き領域の 75 GB 以上 (中央の場所を使用していない) 場合 3 ノード クラスターのネットワーク コント ローラーをお勧めします。

#### <a name="change-logging-settings"></a>ログ設定を変更します。

使用して任意のログ設定を変更することができます、 ``Set-NetworkControllerDiagnostic`` コマンドレットです。 次の設定を変更できます。

- **ログの場所を集中管理**します。  すべてのログを保存する場所を変更する、 ``DiagnosticLogLocation`` パラメーター。  
- **ログの場所へのアクセスに資格情報**します。  ログの場所を表示する資格情報を変更することができます、 ``LogLocationCredential`` パラメーター。  
- **ローカル ログに移動**します。  ログの保存先の一元的な場所を指定した場合、戻すことができますとネットワーク コント ローラーのノードのローカル ログインに、 ``UseLocalLogLocation`` パラメーター (大容量のディスク領域の要件によっては推奨されません)。  
- **ログ記録のスコープ**します。  既定では、すべてのログが収集されます。 唯一のネットワーク コント ローラーがクラスター ログを収集するスコープを変更することができます。  
- **ログ記録レベル**します。  既定のログ レベルは Informational です。 エラー、警告、または詳細を変更することができます。  
- **時間のエージング ログ**します。  ログは、循環形式で格納されます。 ローカル ログまたは集中ログを使用するかどうかは、既定では、ログ データの 3 日間があります。 この時間の制限を変更することができます**LogTimeLimitInDays**パラメーター。  
- **ログのサイズをエージング**します。  既定では、ローカルのログを使用した場合は、集中ログと 25 GB を使用する場合、ログ データの場合は、最大 75 GB があります。 この制限を変更することができます、 **LogSizeLimitInMBs**パラメーター。

#### <a name="collecting-logs-and-traces"></a>収集するログとトレース

VMM の展開は、既定では、ネットワーク コント ローラーの集中ログを使用します。 これらのログのファイル共有の場所は、ネットワーク コント ローラーのサービス テンプレートを展開するときに指定します。

ファイルの場所が指定すると、ローカルはされていない場合は、C:\Windows\tracing\SDNDiagnostics 保存されたログとネットワーク コント ローラーの各ノードのログ記録が使用されます。 これらのログは、次の階層を使用して保存されます。

- CrashDumps
- NCApplicationCrashDumps
- NCApplicationLogs
- PerfCounters
- SDNDiagnostics
- トレース

ネットワーク コント ローラーは、(Azure) の Service Fabric を使用します。 Service Fabric のログは、特定の問題のトラブルシューティングを行う場合、必要なことがあります。 これらのログは C:\ProgramData\Microsoft\Service Fabric の場合は、各ネットワーク コント ローラー ノードにあります。

ユーザー実行している場合、 _デバッグ NetworkController_ コマンドレットでは、追加のログはネットワーク コント ローラーでサーバー リソースが指定されている各 HYPER-V ホストでの表示されます。 これらのログ (およびトレースが有効な場合) が C:\NCDiagnostics 下に置いておく

### <a name="slb-diagnostics"></a>SLB 診断

#### <a name="slbm-fabric-errors-hosting-service-provider-actions"></a>SLBM ファブリック エラー (ホスティング サービス プロバイダーの操作)

1.  ソフトウェア ロード バランサー マネージャー (SLBM) が機能していることと、オーケストレーション レイヤーを相互に通信できることを確認します。SLBM SLB Mux]-> [し、SLBM SLB ホスト エージェント]-> [です。 実行 [DumpSlbRestState](https://github.com/Microsoft/SDN/blob/master/Diagnostics/DumpSlbRestState.ps1) ネットワーク コント ローラーの REST エンドポイントにアクセス権を持つ任意のノードから。  
2.  検証、 *SDNSLBMPerfCounters* ネットワーク コント ローラーのノードの Vm (可能であれば、プライマリ ネットワーク コント ローラー ノード - Get NetworkControllerReplica) のいずれかのパフォーマンス モニターにします。
    1.  ロード バランサー (LB) エンジンが SLBM に接続されているでしょうか。 (*SLBM LBEngine 構成合計* > 0)  
    2.  SLBM 少なくともの認識して、独自のエンドポイントですか。 (*VIP エンドポイント合計* > = 2)  
    3.  HYPER-V (DIP) のホストが SLBM に接続されているでしょうか。 (*接続されている HP クライアント*  num サーバー = =)   
    4.  SLBM は Muxes に接続されているか。 (*Muxes が接続されている* == *SLBM に正常な Muxes* == *Muxes が正常なレポート作成* = # SLB Muxes Vm)。  
3.  BGP ルーターに構成されては SLB MUX とピアリング正常にすることを確認します。  
    1.  RRAS を使用して、リモート アクセス (つまり BGP 仮想マシン) に: 場合  
        1.  Get BgpPeer が接続されている表示する必要があります。  
        2.  Get BgpRouteInformation は、少なくともルートを表示、SLBM の自己 VIP  
    2.  BGP ピアとして別の物理 - Top-of-rack (ToR) を使用して場合、は、ドキュメントを参照してください。  
        1.  例: # bgp インスタンスを表示します。  
4.  検証、 *SlbMuxPerfCounters* と *SLBMUX* SLB Mux VM でのパフォーマンス モニターのカウンター
5.  ソフトウェア ロード バランサー マネージャー リソース VIP 範囲と構成の状態を確認します。  
    1.  Get NetworkControllerLoadBalancerConfiguration ConnectionUri < https://<FQDN or IP>| convertto json の深さ 8 (SLBM self VIP を確認して、IP プール内の VIP 範囲 (*LoadBalanacerManagerIPAddress*) し、すべてのテナントに接続する Vip は、これらの範囲内で)  
        1. "< 公開/秘密 VIP 論理ネットワーク リソース ID >"を get NetworkControllerIpPool ネットワーク Id SubnetId"< 公開/秘密 VIP 論理サブネット リソース ID >"- ResourceId"<IP Pool Resource Id>"ConnectionUri $uri | convertto json の深さ 8 
    2.  デバッグ NetworkControllerConfigurationState-  

チェックのいずれか、失敗の上場合、は、テナント SLB 状態が障害モードでもできます。  

**修復**   
表示される次の診断情報に基づきは、次を修正します。  
* SLB Multiplexers が接続されていることを確認します。  
  * 証明書の問題を修正します。  
  * ネットワーク接続の問題を修正します  
* BGP ピアリング情報が正常に構成されていることを確認します。  
* レジストリでのホスト ID がサーバー リソース内のサーバー インスタンスの ID と一致することを確認 (については、付録を参照 *HostNotConnected* エラー コード)  
* ログの収集  

#### <a name="slbm-tenant-errors-hosting-service-provider--and-tenant-actions"></a>SLBM テナント エラー (ホスティング サービス プロバイダーおよびテナント アクション)

1.  [ホスト]確認 *デバッグ NetworkControllerConfigurationState* LoadBalancer リソースがエラー状態を確認します。 次のアクション アイテム付録内のテーブルで軽減しようとしてください。   
    1.  VIP エンドポイントが存在し、広告のルートのことを確認します。  
    2.  VIP エンドポイントの探索された DIP エンドポイントの数を確認します。  
2.  [テナント]検証ロード バランサーのリソースが正しく指定されています  
    1.  DIP を検証 SLBM で登録されているエンドポイントが LoadBalancer バック エンド アドレス プールの IP 構成に対応するテナントのバーチャル マシンをホストしています。  
3.  [ホスト]DIP エンドポイントの検出または接続されていない: 場合   
    1.  確認 *デバッグ NetworkControllerConfigurationState*  
        1.  NC を検証および SLB ホスト エージェントが正常を使用して、ネットワーク コント ローラー イベント コーディネーターに接続されています。 ``netstat -anp tcp |findstr 6640)``  
    2.  確認 *HostId* で *nchostagent* サービス レジストリ キー (参照 *HostNotConnected* 、付録の内容のエラー コード)、対応するサーバー リソースのインスタンス Id と一致する (``Get-NCServer |convertto-json -depth 8``)  
    3.  仮想マシンのポートのポート プロファイルの id に対応するバーチャル マシンの NIC のリソースのインスタンス Id と一致するを確認します。   
4.  [ホスティング プロバイダー]ログを収集します。   

#### <a name="slb-mux-tracing"></a>SLB Mux トレース

ソフトウェア ロード バランサー Muxes からの情報は、イベント ビューアーからも判断できます。 
1. イベント ビューアーの表示] メニューで [「を表示する分析とデバッグ ログの」
2. [アプリケーションとサービス ログ] に移動 > Microsoft > Windows > SlbMuxDriver > イベント ビューアーでのトレース 
3. これを右クリックし、"ログを有効にする を選択

>[!NOTE]
>短い形式の時刻を有効になっている問題を再現しようとしているときに、このログ記録のみがあることをお勧め

### <a name="vfp-and-vswitch-tracing"></a>VFP と vSwitch のトレース

Hyper-v ホストからホスト、ゲスト仮想マシンをテナントの仮想ネットワークに接続をホストする、問題がある箇所を確認するときに、VFP トレースを収集することができます。

```
netsh trace start provider=Microsoft-Windows-Hyper-V-VfpExt overwrite=yes tracefile=vfp.etl report=disable provider=Microsoft-Windows-Hyper-V-VmSwitch 
netsh trace stop
netsh trace convert .\vfp.etl ov=yes 
```
