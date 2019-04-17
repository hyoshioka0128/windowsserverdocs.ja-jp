---
title: Windows Server ソフトウェア定義ネットワーク スタックをトラブルシューティングします。
description: この Windows Server のガイドでは、一般的なソフトウェアによるネットワーク制御 (SDN) エラーおよび障害のシナリオを調べ、使用可能な診断ツールを活用してトラブルシューティングのワークフローの概要を示します。
manager: ravirao
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 9be83ed2-9e62-49e8-88e7-f52d3449aac5
ms.author: pashort
author: JMesser81
ms.openlocfilehash: af59ae6746467f9aecf384d1b3cf9af1e8baeb9a
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="troubleshoot-the-windows-server-software-defined-networking-stack"></a>Windows Server ソフトウェア定義ネットワーク スタックをトラブルシューティングします。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このガイドでは、一般的なソフトウェアによるネットワーク制御 (SDN) エラーと障害のシナリオが調べられ、使用可能な診断ツールを活用してトラブルシューティングのワークフローの概要を示します。  

Microsoft のソフトウェア定義ネットワークの詳細については、次を参照してください。[ソフトウェアがネットワーク定義](../../sdn/Software-Defined-Networking--SDN-.md)します。  

## <a name="error-types"></a>エラーの種類  
次の一覧は市場での実稼働展開から Windows Server 2012 R2 で Hyper-V ネットワーク仮想化 (HNVv1) が最も多く見られますの問題のクラスを表すし、さまざまな方法で問題が発生 hnvv2 新しいソフトウェア定義ネットワーク (SDN) スタックで表示される Windows Server 2016 での同じの種類と一致します。  

ほとんどのエラーは、少数のクラスに分類できます。   
* **無効またはサポートされない構成**  
   ユーザーは、誤って、または無効なポリシーを使って、NorthBound API を呼び出します。   

* **ポリシー アプリケーションのエラー**  
     ネットワーク コントローラーからのポリシーが大幅に遅延および/またはない最新の状態 (たとえば、ライブ マイグレーションを実行) 後のすべての Hyper-V ホスト上の Hyper-V ホストに配信されませんでした。  
* **構成の誤差またはソフトウェアのバグ**  
 破棄されたパケットのデータ パスの問題です。  

* **NIC のハードウェアに関連する外部エラー/ドライバーや、アンダーレイ ネットワーク ファブリック**  
 (VMQ) などの作業負荷を軽減または (MTU) などの構成が間違っているアンダーレイ ネットワーク ファブリックを適切に動作しません   

 このトラブルシューティングのガイドでは、これらのエラー カテゴリの各検証し、ベスト プラクティスとを識別し、エラーの解決に使用できる診断ツールをお勧めします。  

## <a name="diagnostic-tools"></a>診断ツール  

各種のエラーのトラブルシューティングのワークフローを説明する前に使用できる診断ツールを調べてみましょう。   
  
ネットワーク コントローラー (コントロール パス) の診断ツールを使用するは、最初 RSAT NetworkController 機能をインストールし、インポートする必要があります、``NetworkControllerDiagnostics``モジュール。  

```  
Add-WindowsFeature RSAT-NetworkController -IncludeManagementTools  
Import-Module NetworkControllerDiagnostics  
```  

インポートする必要があります (データ パス) の HNV 診断診断ツールを使用する、``HNVDiagnostics``モジュール。
  
```  
# Assumes RSAT-NetworkController feature has already been installed
Import-Module hnvdiagnostics   
```  

### <a name="network-controller-diagnostics"></a>ネットワーク コントローラーの診断  
これらのコマンドレットについては、technet の「、[ネットワーク コントローラー診断コマンドレット トピック](https://docs.microsoft.com/en-us/powershell/module/networkcontrollerdiagnostics/)します。 コントロール パスと、ネットワーク コントローラーと Hyper-V ホストで実行されている NC ホスト エージェントの間でネットワーク コントローラーのノード間でネットワーク ポリシーの整合性に問題を特定できます。

 _デバッグ ServiceFabricNodeStatus_と_Get NetworkControllerReplica_からネットワーク コントローラーのノードの仮想マシンのいずれかのコマンドレットを実行する必要があります。 その他のすべての NC 診断コマンドレットは、ネットワーク コントローラーに接続し、ネットワーク コントローラーの管理セキュリティ グループ (Kerberos) のいずれかがまたはネットワーク コントローラーを管理するための X.509 証明書にアクセスするすべてのホストから実行できます。 
   
### <a name="hyper-v-host-diagnostics"></a>Hyper-V ホストでの診断  
これらのコマンドレットについては、technet の「、[Hyper-v ネットワーク仮想化 (HNV) 診断コマンドレット トピック](https://docs.microsoft.com/en-us/powershell/module/hnvdiagnostics/)します。 テナント仮想マシン (東または西) 間のデータ パスの問題を特定できると SLB VIP (北または南) からトラフィックを受信します。 

_デバッグ VirtualMachineQueueOperation_、_Get CustomerRoute_、_Get PACAMapping_、_Get ProviderAddress_、_Get VMNetworkAdapterPortId_、_Get VMSwitchExternalPortId_、および_テスト EncapOverheadSettings_はすべての Hyper-V ホストから実行できるすべてのローカル テストします。 その他のコマンドレットでは、ネットワーク コントローラーを介してデータ パスのテストを呼び出すし、したがって上 descried としてネットワーク コントローラーへのアクセスを必要があります。
 
### <a name="github"></a>GitHub
[MICROSOFT/SDN GitHub リポジトリ](https://github.com/microsoft/sdn)、数多くのサンプル スクリプトとワークフロー ボックスでのこれらのコマンドレットの上に構築します。 具体的には、診断のスクリプトは記載されて、[診断](https://github.com/Microsoft/sdn/diagnostics)フォルダー。 ご協力くださいプル要求を送信することでこれらのスクリプトに投稿します。

## <a name="troubleshooting-workflows-and-guides"></a>ワークフローおよびガイドのトラブルシューティング  

### <a name="hoster-validate-system-health"></a>[ホスト]システム正常性を検証します。
という名前の埋め込みリソースがある_構成状態_のネットワーク コントローラーのリソースのいくつか。 構成の状態は、ネットワーク コントローラーの構成と Hyper-V ホスト上の実際の (実行中) 状態の間で一貫性を含むシステム正常性に関する情報を提供します。 

構成の状態を確認するには、ネットワーク コントローラーに接続を備えたすべての Hyper-V ホストから、次を実行します。

>[!NOTE] 
>値、*NetworkController*パラメーター必要がありますか、X.509 のサブジェクト名に基づく FQDN または IP アドレスである > ネットワーク コントローラー用に作成された証明書。
>
>*Credential*パラメーターのみをネットワーク コントローラーが Kerberos 認証 (VMM の展開で標準) を使用するかどうかに指定する必要があります。 ネットワーク コントローラーの管理セキュリティ グループ内であるユーザーの資格情報があります。

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

サンプル構成の状態メッセージは、次に示します。

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
> SLB Mux 転送中の VM NIC のネットワーク インターフェイス リソースは「仮想スイッチ-ホストいない接続をコントローラー」のエラーで失敗状態であるシステムには、バグがあります。 IP 構成の VM NIC のリソース転送中の論理ネットワークの IP プールから IP アドレスに設定されている場合は、このエラーを無視しても問題ありません。 "仮想スイッチ-PortBlocked"のエラーで失敗状態で、ゲートウェイ HNV プロバイダーの VM Nic のネットワーク インターフェイス リソースが、システムには、2 番目のバグがあります。 このエラーも無視してかまいませんの VM NIC のリソースの IP 構成が設定されている場合 (デザイン) によって null にします。


次の表は、監視構成の状態に基づいて実行するには、エラー コード、メッセージ、およびフォロー アップのアクションの一覧を示します。

  
| **コード**| **メッセージ**| **アクション**|  
|:--------:|:-----------:|----------:|  
| [不明]| 不明なエラー| |  
| HostUnreachable                       | ホスト コンピューターが到達不可 | ネットワーク コントローラーとホスト間での管理ネットワーク接続を確認します。 |  
| PAIpAddressExhausted                  | PA Ip アドレスの不足 | HNV プロバイダー論理サブネットの IP プールのサイズを増やす |  
| PAMacAddressExhausted                 | PA の Mac アドレスの不足 | Mac プールの範囲を増やす |  
| PAAddressConfigurationFailure         | ホストの PA アドレスを組み込むために失敗しました | ネットワーク コントローラーとホスト間での管理ネットワーク接続を確認します。 |  
| CertificateNotTrusted                 | 証明書が信頼されていません  |ホストとの通信に使用される証明書を修正します。 |  
| CertificateNotAuthorized              | 証明書が承認されていません。 | ホストとの通信に使用される証明書を修正します。 |  
| PolicyConfigurationFailureOnVfp       | VFP ポリシーの構成の失敗 | これは、ランタイム エラーです。  確実な回避策がありません。 ログを収集します。 |  
| PolicyConfigurationFailure            | 通信エラーまたはその他のユーザーによる、ホストにポリシーをプッシュの障害、NetworkController のエラーです。| 確実な操作はありません。  これは、目標とする状態、ネットワーク コントローラー モジュールの処理でエラーが原因です。 ログを収集します。 |  
| HostNotConnectedToController          | ホストが、ネットワーク コントローラーにまだ接続されていません。 | ポート プロファイルが適用されない、または、ホスト上では、ネットワーク コントローラーから到達できません。 ホスト ID のレジストリ キーにサーバー リソースのインスタンス ID が一致することを検証します。 |  
| MultipleVfpEnabledSwitches            | 複数 VFp が、ホストでスイッチを有効には  | ネットワーク コントローラー ホスト エージェントでは、VFP 拡張を有効化と 1 つの vSwitch のみがサポートされているので、スイッチのいずれかを削除します。 |  
| PolicyConfigurationFailure            | 証明書のエラーまたは接続エラーのため VmNic の VNet のポリシーをプッシュできませんでした。  | 適切な証明書が展開されているかどうかをチェック (証明書のサブジェクト名は、ホストの FQDN を一致する必要があります)。 また、ホスト、ネットワーク コントローラーと接続を確認します。 |  
| PolicyConfigurationFailure            | 証明書のエラーまたは接続エラーのため VmNic の vSwitch ポリシーをプッシュできませんでした。  | 適切な証明書が展開されているかどうかをチェック (証明書のサブジェクト名は、ホストの FQDN を一致する必要があります)。 また、ホスト、ネットワーク コントローラーと接続を確認します。|
| PolicyConfigurationFailure            | 証明書のエラーまたは接続エラーのため VmNic のファイアウォール ポリシーをプッシュできませんでした。 | 適切な証明書が展開されているかどうかをチェック (証明書のサブジェクト名は、ホストの FQDN を一致する必要があります)。 また、ホスト、ネットワーク コントローラーと接続を確認します。|
| DistributedRouterConfigurationFailure | ホスト vNic の分散ルーター設定を構成できませんでした。                          | TCP/IP スタックのエラーです。 このエラーが報告されたサーバー上の PA と災害復旧ホスト Vnic のクリーンアップする必要があります。 |
| DhcpAddressAllocationFailure          | VMNic の DHCP アドレス割り当てに失敗しました                                                    | NIC のリソースに静的 IP アドレス属性が構成されているかどうかはチェックします。 |  
| CertificateNotTrusted<br>CertificateNotAuthorized | ネットワークまたは証明書のエラーにより Mux に接続できませんでした。 | エラー メッセージのコードで提供される数値コードを確認します。これは winsock エラー コードに対応します。 きめ細かいものでは証明書のエラー (たとえば、証明書を検証できない、承認されていないなどです)。 |  
| HostUnreachable                       | MUX に問題があります (一般的なケースは切断 BGPRouter) | BGP ピア RRAS (BGP 仮想マシン) または上部ラック (ToR) スイッチでは、正常に到達できないまたはいないピアリングです。 ソフトウェア ロード バランサー マルチプレクサー リソースと BGP ピア (ToR または RRAS 仮想マシン) の両方で BGP 設定を確認します。 |  
| HostNotConnectedToController          | SLB ホスト エージェントが接続されていません。  | SLB ホスト エージェント サービスが実行されていることを確認します。上の理由から、SLB ホスト エージェントのログ (自動実行) を参照してください、SLBM (NC) を実行しているホスト エージェントによって提示される証明書を拒否された場合に状態情報が表示されます微妙  |  
| PortBlocked                           | VNET がないことによる、VFP ポートがブロックされている//ACL ポリシー | 他のエラー、しない構成するポリシーを引き起こす可能性があるかを確認します。 |  
| 過負荷の状態                            | Loadbalancer MUX が過負荷の状態します。  | MUX のパフォーマンスに関する問題 |  
| RoutePublicationFailure               | Loadbalancer MUX が BGP ルーターに接続されていません | MUX が BGP ルーターとの接続性を持つかどうか、BGP ピアリングが正しく設定されているとを確認します。 |  
| VirtualServerUnreachable              | Loadbalancer MUX が SLB マネージャーに接続されていません | SLBM とマルチプレクサー間の接続を確認します。 |  
| QosConfigurationFailure               | QOS ポリシーの構成に失敗しました | 十分な帯域幅は QOS の予約を使用する場合はすべての仮想マシン用に利用可能なかどうかを参照してください。 |


#### <a name="check-network-connectivity-between-the-network-controller-and-hyper-v-host-nc-host-agent-service"></a>ネットワーク コントローラーと Hyper-V ホスト (NC ホスト エージェント サービス) の間のネットワーク接続を確認します。
実行、*netstat* NC ホスト エージェントとネットワーク コントローラーのノードと Hyper-V ホスト上の 1 つのリッスン ソケットの間の 3 つの確立した接続があることを検証する次のコマンド
- Hyper-V ホスト (NC ホスト エージェント サービス) にポート TCP:6640 でリッスンしています。
- Hyper-V から確立されている接続の 2 つのホストに一時的なポート (> 32000) の NC ノードの IP ポート 6640 で IP
- ネットワーク コントローラー REST IP ポート 6640 で一時的なポートでの Hyper-V ホストの IP から 1 つに確立された接続

>[!NOTE]
>ある可能性がありますのみ Hyper-V ホスト上の 2 つの確立された接続を特定のホストに展開されているテナントのバーチャル マシンがない場合。

```none
netstat -anp tcp |findstr 6640

# Successful output
  TCP    0.0.0.0:6640           0.0.0.0:0              LISTENING
  TCP    10.127.132.153:6640    10.127.132.213:50095   ESTABLISHED
  TCP    10.127.132.153:6640    10.127.132.214:62514   ESTABLISHED
  TCP    10.127.132.153:50023   10.127.132.211:6640    ESTABLISHED
```
#### <a name="check-host-agent-services"></a>ホスト エージェント サービスを確認します。
ネットワーク コントローラーは、Hyper-V ホスト上の 2 つのホスト エージェント サービスと通信します。SLB ホスト エージェントと NC ホスト エージェント。 これらのサービスの一方または両方が実行されていないことことができます。 その状態を確認し、それらが実行されていない場合に再起動します。

```none
Get-Service SlbHostAgent
Get-Service NcHostAgent

# (Re)start requires -Force flag
Start-Service NcHostAgent -Force
Start-Service SlbHostAgent -Force
```

#### <a name="check-health-of-network-controller"></a>ネットワーク コントローラーの正常性を確認します。
次の 3 つの確立した接続がある場合、または、ネットワーク コントローラーが応答しない場合は、すべてのノードおよびサービス モジュールが起動して実行中である次のコマンドレットを使用して確認します。 

```none
# Prints a DIFF state (status is automatically updated if state is changed) of a particular service module replica 
Debug-ServiceFabricNodeStatus [-ServiceTypeName] <Service Module>
```
ネットワーク コントローラー サービス モジュールは次のとおりです。
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

ReplicaStatus はチェック**準備ができて**HealthState は**OK**します。

実稼働で展開は、複数ノードのネットワーク コントローラーと各サービスのプライマリになっているノードと個々 のレプリカの状態を確認することもできます。

```none  
Get-NetworkControllerReplica

# Sample Output for the API service module
Replicas for service: ApiService

ReplicaRole   : Primary
NodeName      : SA18N30NC3.sa18.nttest.microsoft.com
ReplicaStatus : Ready

```
レプリカの状態が準備完了であることを確認サービスごとにします。
 
#### <a name="check-for-corresponding-hostids-and-certificates-between-network-controller-and-each-hyper-v-host"></a>対応する ID とネットワーク コントローラーと各 Hyper-V ホスト間で証明書の確認します。 
Hyper-V ホストでは、ホスト ID がネットワーク コントローラー上のサーバー リソースのインスタンス ID に対応していることを確認するには、次のコマンドを実行します

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

*修復*かどうか SDNExpress を使用してスクリプトまたは手動展開は、更新サーバー リソースのインスタンス ID が一致するようにレジストリ内のホスト ID キー。 VMM を使用して、VMM からは、Hyper-V サーバーを削除する場合は、Hyper-V ホスト (物理サーバー) 上のネットワーク コントローラー ホスト エージェントを再起動し、ホスト ID のレジストリ キーを削除します。 次に、VMM を使用してサーバーを再度追加します。


(SouthBound) 間の通信、Hyper-V ホスト (NC ホスト エージェント サービス) とネットワーク コントローラーのノード (ホスト名は証明書のサブジェクト名になります)、Hyper-V ホストによって使用される X.509 証明書の拇印が同じであることを確認します。 あることを確認、ネットワーク コントローラーの残りの部分の証明書のサブジェクト名*CN =<FQDN or IP>*します。

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

各証明書、サブジェクト名はどのようなことを確認するは、次のパラメーターを確認することもできます (ホスト名または NC REST FQDN または IP) を想定証明書がまだ失効して、信頼されたルート証明機関に証明書チェーン内のすべての証明機関が含まれているとします。

- サブジェクト名  
- 有効期限日  
- ルート証明機関によって信頼  

*修復*複数の証明書では、Hyper-V ホスト上の同じサブジェクト名がある、ネットワーク コントローラー ホスト エージェントは無作為に選択ネットワーク コントローラーに表示する 1 つです。 これが、既知のネットワーク コントローラーにサーバー リソースのサムプリントとは一致しません。 この場合は、Hyper-V ホスト上の同じサブジェクト名を持つ証明書のいずれかを削除し、ネットワーク コントローラー ホスト エージェント サービスを再開します。 まだ、接続は行われず、Hyper-V ホスト上の同じサブジェクト名を持つその他の証明書を削除し、VMM での対応するサーバー リソースを削除します。 次に、vmm は新しい X.509 証明書を生成し、Hyper-V ホストにインストールするサーバーのリソースを再作成します。
  

#### <a name="check-the-slb-configuration-state"></a>SLB 構成状態を確認します。
Debug-NetworkController コマンドレットに出力の一部として、SLB 構成の状態を特定できます。 このコマンドレットは、現在の JSON ファイル、各 Hyper-V ホスト (サーバー) からのすべての IP 構成とホストのエージェントのデータベース テーブルからローカル ネットワーク ポリシーでネットワーク コントローラーのリソースのセットも出力します。 

既定では、その他のトレースが収集されます。 トレースを収集しない追加の IncludeTraces: $false のパラメーターです。

```none
Debug-NetworkController -NetworkController <FQDN or IP> [-Credential <PS Credential>] [-IncludeTraces:$false]

# Don't collect traces
$cred = Get-Credential 
Debug-NetworkController -NetworkController 10.127.132.211 -Credential $cred -IncludeTraces:$false

Transcript started, output file is C:\\NCDiagnostics.log
Collecting Diagnostics data from NC Nodes
```

>[!NOTE]
>既定の出力場所は、< working_directory > \NCDiagnostics\ ディレクトリになります。 使用して既定の出力ディレクトリを変更することができます、`-OutputDirectory`パラメーター。 

SLB 構成の状態の詳細については記載されて、_診断 slbstateResults.Json_このディレクトリ内のファイル。

この JSON ファイルは、次のセクションに分けることができます。
 * ファブリック
   * SlbmVips - このセクションでは、coodinate 構成と状態 SLB Muxes と SLB ホスト エージェントの間にネットワーク コントローラーで使用される SLB Manager の VIP アドレスの IP アドレスを示します。
   * MuxState - このセクションでは 1 つの値の一覧各 SLB mux 展開、mux の状態を与える
   * ルーターの構成 - このセクションで、上流のルーターの (BGP ピア) ボックスの一覧は自律システム番号 (ASN)、転送中の IP アドレス、および ID 転送中の IP と SLB Muxes ASN も表示されます。
   * ホスト情報のこのセクションで接続されているが、管理 IP のリストのすべてのワークロードの負荷分散を実行できるようにインストールされた Hyper-v ホスト アドレスします。
   * Vip 範囲 - このセクションには、パブリックおよびプライベートの VIP IP プールの範囲が表示されます。 SLBM VIP は割り当てられている IP からこれらの範囲のいずれかとして含まれます。 
   * Mux ルート] - このセクションでは 1 つの値の一覧各 SLB mux 展開されているその特定のマルチプレクサーのルート アドバタイズのすべてを含みます。
 * テナント
   * VipConsolidatedState - このセクションでを一覧表示接続状態アドバタイズされたルート プレフィックス、Hyper-V ホストおよび DIP エンドポイントを含む各テナント VIP です。
    
> [!NOTE]
> 使用して直接 SLB 状態を確認できる、[DumpSlbRestState](https://github.com/Microsoft/SDN/blob/master/Diagnostics/DumpSlbRestState.ps1)スクリプトで使用できる、[Microsoft SDN GitHub リポジトリ](https://github.com/microsoft/sdn)します。 

#### <a name="gateway-validation"></a>ゲートウェイの検証

**ネットワーク コントローラー: から**
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

これらの問題を解決します (特にで SDNExpress ベースの展開)、これまできました、に加えて GW Vm 上で構成を取得するされていないテナント コンパートメントの最も一般的な原因と思われるという事実を思われる FabricConfig.psd1 で GW 容量が TenantConfig.psd1 にしようとどのような人々 (S2S トンネル) のネットワーク接続に割り当てる小さいと比較します。 これは、次のコマンドの出力を比較することによって簡単にチェックすることができます。

```
PS > (Get-NetworkControllerGatewayPool -ConnectionUri $uri).properties.Capacity
PS > (Get-NetworkControllerVirtualgatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "TenantName").properties.OutboundKiloBitsPerSecond
PS > (Get-NetworkControllerVirtualgatewayNetworkConnection -ConnectionUri $uri -VirtualGatewayId "TenantName").property
```

### <a name="hoster-validate-data-plane"></a>[ホスト]データ プレーンを検証します。
ネットワーク コントローラーが展開されているし、テナントの仮想ネットワークとサブネットを作成すると、Vm が仮想サブネットにアタッチされているが、テナント接続を確認する、ホスト側によって追加のファブリック レベルのテストを実行できます。

#### <a name="check-hnv-provider-logical-network-connectivity"></a>HNV プロバイダー論理ネットワークの接続を確認します。
Hyper-V ホスト上で実行されている VM がテナントの仮想ネットワークに接続された最初のゲストの後に、ネットワーク コントローラーは、Hyper-V ホストを 2 つの HNV プロバイダー IP アドレス (PA IP アドレス) を割り当てます。 これらの Ip では、HNV プロバイダー論理ネットワークの IP プールから取得され、ネットワーク コントローラーで管理します。  これら 2 つの HNV の IP アドレスを調べるの

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

これら HNV プロバイダー IP アドレス (PA Ip) が独立した TCPIP ネットワーク コンパートメントで作成したイーサネット アダプターに割り当てられているし、アダプターの名前の_VLANX_ X は HNV プロバイダー (トランスポート) の論理ネットワークに割り当てられている VLAN です。

論理ネットワークを行う追加のコンパートメントを持つ ping HNV プロバイダーを使用して 2 つの Hyper-V ホスト間の接続 (--c Y) Y が、PAhostVNICs が作成された TCPIP ネットワーク コンパートメントのパラメーターです。 このコンパートメントを実行して決定できます。

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
> PA ホスト vNIC アダプターでは、データ パスで使用されていない、ので、「vEthernet (PAhostVNic) アダプター」に割り当てられている IP はありません。

たとえば、Hyper-V ホスト 1 と 2 は、HNV プロバイダー (PA) の IP アドレスであると仮定します。

|-Hyper-V ホスト:|PA IP アドレス 1|PA IP アドレス 2|
|---             |---            |---             |
|ホスト 1 | 10.10.182.64 | 10.10.182.65 |
|ホスト 2 | 10.10.182.66 | 10.10.182.67 |

次のコマンドを使用して HNV プロバイダー論理ネットワークの接続を確認する 2 つの ping を実行します。

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

*修復*場合の HNV プロバイダー ping が動作、VLAN の構成を含む、物理的なネットワーク接続を確認していません。 各 Hyper-V ホスト上の物理 Nic は、割り当てられていない特定の VLAN をトランク モードにする必要があります。 管理ホスト vNIC は、管理の論理ネットワークの VLAN に分離する必要があります。

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
 
#### <a name="check-mtu-and-jumbo-frame-support-on-hnv-provider-logical-network"></a>HNV プロバイダー論理ネットワーク上の MTU およびジャンボ フレームのサポートを確認します。

HNV プロバイダー論理ネットワーク内の別の一般的な問題は、物理ネットワーク ポートおよびイーサネット カードが VXLAN (NVGRE) カプセル化によるオーバーヘッドを処理するように構成するのに十分な大きさ MTU がないことです。 
>[!NOTE]
> 一部のイーサネット カードとドライバーをサポートして、新しい * EncapOverhead キーワードである数値 160 にネットワーク コントローラー ホスト エージェントによって自動的に設定されます。 この値は、の値に追加されますが、* JumboPacket キーワードの合計は、アドバタイズされた MTU として使用します。
> 例: * EncapOverhead = 160 と * JumboPacket 1514 の = = > MTU 1674B =

```none
# Check whether or not your Ethernet card and driver support *EncapOverhead
PS C:\ > Test-EncapOverheadSettings

Verifying Physical Nic : <NIC> Ethernet Adapter #2
Physical Nic  <NIC> Ethernet Adapter #2 can support SDN traffic. Encapoverhead value set on the nic is  160
Verifying Physical Nic : <NIC> Ethernet Adapter
Physical Nic  <NIC> Ethernet Adapter can support SDN traffic. Encapoverhead value set on the nic is  160
```

HNV プロバイダー論理ネットワークが、大きい MTU サイズ エンド ツー エンドをサポートしているかどうかをテストするには、使用、_テスト LogicalNetworkSupportsJumboPacket_コマンドレット。
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
* 少なくとも、物理スイッチ ポートで MTU サイズを調整する 1674B (14 b イーサネット ヘッダーとトレーラーを含む)
* NIC カードが EncapOverhead キーワードをサポートしていない場合は、少なくとも、JumboPacket キーワードを調整する 1674B


#### <a name="check-tenant-vm-nic-connectivity"></a>テナント VM の NIC の接続を確認します
ゲスト VM に割り当てられている各 VM の NIC には、プライベート カスタマー アドレス (CA) と HNV プロバイダー アドレス (PA) 空間の間で CA と PA のマッピングがあります。 これらのマッピングは、各 Hyper-V ホストで OVSDB server のテーブルに保存しが見つかった場合、次のコマンドレットを実行します。

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
> 期待する CA と PA のマッピングは、指定したテナント VM 用の出力ではない場合、は、ネットワーク コントローラーを使用して、VM の NIC と ip アドレス構成のリソースを確認してください、_Get NetworkControllerNetworkInterface_コマンドレット。 また、NC ホスト エージェントとネットワーク コントローラーのノード間で確立された接続を確認します。

この情報は、テナントの VM ping できる、ネットワーク コントローラーを使用して、ホスト側によって起動されるよう、_テスト VirtualNetworkConnection_コマンドレット。

## <a name="specific-troubleshooting-scenarios"></a>具体的なトラブルシューティング シナリオ

次のセクションでは、特定のシナリオのトラブルシューティングのガイダンスを提供します。

### <a name="no-network-connectivity-between-two-tenant-virtual-machines"></a>次の 2 つのテナント仮想マシン間のネットワーク接続なし

1.  [テナント]テナントのバーチャル マシンで Windows ファイアウォールがトラフィックをブロックしていないことを確認します。  
2.  [テナント]IP アドレスがテナントの仮想マシンを実行して、割り当てられたことを確認して_ipconfig_します。 
3.  [ホスト]実行**テスト VirtualNetworkConnection**問題の 2 つのテナント仮想マシン間の接続を検証する Hyper-V ホストからです。 

>[!NOTE]
>VSID と仮想サブネット ID VXLAN の場合これは、VXLAN ネットワーク識別子 (VNI) です。 この値を検索するを実行している、**Get PACAMapping**コマンドレット。

#### <a name="example"></a>使用例

    $password = ConvertTo-SecureString -String "password" -AsPlainText -Force
    $cred = New-Object pscredential -ArgumentList (".\administrator", $password) 

ホスト上で"sa18n30-2.sa18.nttest.microsoft.com"管理 ip 10.127.132.153 の ListenerCA ip 192.168.1.5 両方に仮想サブネット (VSID) 4114 をアタッチの 192.168.1.4 の SenderCA IP を"緑 Web 1 の VM"の間で CA に ping を作成します。

    Test-VirtualNetworkConnection -OperationId 27 -HostName sa18n30-2.sa18.nttest.microsoft.com -MgmtIp 10.127.132.153 -Creds $cred -VMName "Green Web VM 1" -VMNetworkAdapterName "Green Web VM 1" -SenderCAIP 192.168.1.4 -SenderVSID 4114 -ListenerCAIP 192.168.1.5 -ListenerVSID 4114

    Test-VirtualNetworkConnection at command pipeline position 1

CA 空間 ping テストの開始アドレス 192.168.1.4 Rtt からが成功した 192.168.1.5 にトレース セッション Ping を開始 = 0 の ms


CA のルーティング情報があります。

    Local IP: 192.168.1.4
    Local VSID: 4114
    Remote IP: 192.168.1.5
    Remote VSID: 4114
    Distributed Router Local IP: 192.168.1.1
    Distributed Router Local MAC: 40-1D-D8-B7-1C-06
    Local CA MAC: 00-1D-D8-B7-1C-05
    Remote CA MAC: 00-1D-D8-B7-1C-07
    Next Hop CA MAC Address: 00-1D-D8-B7-1C-07

PA のルーティング情報があります。

    Local PA IP: 10.10.182.66
    Remote PA IP: 10.10.182.65
 
 <snip> ...

4.  [テナント]仮想サブネットまたはトラフィックをブロックする VM ネットワーク インターフェイスで指定された分散型のファイアウォール ポリシーがないことを確認します。    

sa18.nttest.microsoft.com ドメインで sa18n30nc のデモ環境で見つかったネットワーク コントローラー REST API をクエリします。

    $uri = "https://sa18n30nc.sa18.nttest.microsoft.com"
    Get-NetworkControllerAccessControlList -ConnectionUri $uri 

# <a name="look-at-ip-configuration-and-virtual-subnets-which-are-referencing-this-acl"></a>IP 構成と、この ACL を参照している仮想サブネットを見る

1. [ホスト]実行``Get-ProviderAddress``両方の Hyper-V でホストをホストしている 2 つの質問に仮想マシンをテナントし、実行``Test-LogicalNetworkConnection``または``ping -c <compartment>``HNV プロバイダー論理ネットワーク上の接続を検証する Hyper-V ホストから
2.  [ホスト]MTU 設定が Hyper-V ホスト上で正しいと、レイヤー 2 Hyper-V ホストの間にデバイスを切り替えることを確認します。 実行``Test-EncapOverheadValue``問題のすべての Hyper-V ホスト上でします。 また間にすべてのレイヤー 2 スイッチが MTU 160 バイトの最大のオーバーヘッドを考慮する最小限の 1674 バイトに設定があることを確認します。  
3.  [ホスト]PA IP アドレスが存在しない CA 接続が切断された場合は、ネットワーク ポリシーが受信されたことを確認することを確認します。 実行``Get-PACAMapping``をカプセル化のルールと仮想ネットワークのオーバーレイを作成するために必要な CA と PA のマッピングが正しく確立されるかどうかを参照してください。  
4.  [ホスト]ネットワーク コントローラー ホスト エージェントがネットワーク コントローラーに接続されていることを確認します。 実行``netstat -anp tcp |findstr 6640``かどうかを   
5.  [ホスト]ホストが HKLM に ID チェック テナントのバーチャル マシンをホストしているサーバーのリソースのインスタンス ID と一致する/します。  
6. [ホスト]ポート プロファイルの ID に、テナントの仮想マシンの VM ネットワーク インターフェイスのインスタンス ID が一致することを確認します。  

## <a name="logging-tracing-and-advanced-diagnostics"></a>ログ、トレース、および高度な診断

次のセクションでは、高度な診断、ログ、およびトレースの情報を提供します。

### <a name="network-controller-centralized-logging"></a>ネットワーク コントローラーの集中ログの記録 
 
ネットワーク コントローラーは自動的にデバッガーのログを収集し、一元的な場所に保管します。 後でいつでも、初めてのネットワーク コントローラーを展開するときに、ログの収集を有効にすることができます。 ログがネットワーク コントローラーから収集され、ネットワークのネットワーク コントローラーによって管理されている要素: コンピューター、ソフトウェアによる負荷分散 (SLB) とゲートウェイのマシンをホストします。 

これらのログには、ネットワーク コントローラー クラスター、ネットワーク コントローラー アプリケーション、ゲートウェイのログ、SLB、仮想ネットワークおよび分散型のファイアウォールのデバッグ ログが含まれます。 ネットワーク コントローラーに、新しいホスト/SLB/ゲートウェイを追加するたびにそれらのコンピューターのログ記録が開始されます。 同様に、ネットワーク コントローラーから、ホスト/SLB/ゲートウェイが削除されると、それらのコンピューターのログが停止されました。

#### <a name="enable-logging"></a>ログ記録を有効にします。

ログを自動的に有効に、ネットワーク コントローラーを使用してクラスターをインストールするときに、**インストール NetworkControllerCluster**コマンドレット。 既定では、ログは、収集にローカルでネットワーク コントローラーのノード*%systemdrive%\SDNDiagnostics*します。 **強くお勧め**(ローカルではありません)、リモート ファイル共有にするには、この場所を変更することです。 

ネットワーク コントローラーのクラスター ログが格納されている*%programData%\Windows fabric \log\traces*します。 ログ コレクションに対して一元的な場所を指定することができます、**DiagnosticLogLocation**もこれは推奨事項にパラメーターが、リモート ファイル共有を指定します。 

この場所へのアクセスを制限する場合は、アクセス資格情報を提供できます、**LogLocationCredential**パラメーター。 ログの場所にアクセスする資格情報を提供する場合もを入力してください、**CredentialEncryptionCertificate**パラメーターで、ネットワーク コントローラーのノードでローカルに保存された資格情報を暗号化するために使用します。  

既定の設定であるかローカル ノードの中央の場所、および 25 GB の空き領域の 75 GB 以上 (中央の場所を使用していない) 場合 3 ノード クラスターのネットワーク コントローラーをお勧めします。

#### <a name="change-logging-settings"></a>ログ設定を変更します。

使用して任意のログ設定を変更することができます、``Set-NetworkControllerDiagnostic``コマンドレット。 次の設定を変更することができます。

- **ログの場所を集中管理**します。  すべてのログを保存する場所を変更することができます、``DiagnosticLogLocation``パラメーター。  
- **ログの場所にアクセスする資格情報**します。  ログの場所にアクセスする資格情報を変更することができます、``LogLocationCredential``パラメーター。  
- **ローカル ログに移動**します。  ログの保存を一元的な場所を指定した場合、戻すことができますとネットワーク コントローラーのノードのローカル ログインに、``UseLocalLogLocation``パラメーター (大容量のディスク領域の要件によっては推奨されません)。  
- **ログ記録のスコープ**します。  既定では、すべてのログが収集されます。 唯一のネットワーク コントローラー クラスター ログを収集するスコープを変更することができます。  
- **ログ出力レベル**します。  既定のログ レベルは Informational です。 エラー、警告、または Verbose に変更することができます。  
- **時間のエージング ログ**します。  ログは、循環形式で保存されます。 ローカル ログまたは集中ログを使用するかどうか、既定では、3 日間のログ データがあります。 この時間の制限を変更する**LogTimeLimitInDays**パラメーター。  
- **ログ サイズをエージング**します。  既定では、ローカル ログを使用する場合は、集中ログと 25 GB を使用する場合にログ データの最大 75 GB があります。 この制限を変更することができます、**LogSizeLimitInMBs**パラメーター。

#### <a name="collecting-logs-and-traces"></a>ログし、トレースを収集します。

VMM の展開では、既定で、ネットワーク コントローラーを集中ログを使用します。 ネットワーク コントローラーのサービス テンプレートを展開するときに、これらのログ ファイルの共有の場所を指定します。

ファイルの場所が指定すると、ローカルはされていない場合は、下にある C:\Windows\tracing\SDNDiagnostics 保存されたログとネットワーク コントローラー ノードごとにログが使用されます。 これらのログは、次の階層を使用して保存されます。

- CrashDumps
- NCApplicationCrashDumps
- NCApplicationLogs
- PerfCounters
- SDNDiagnostics
- トレース

ネットワーク コントローラーは、(Azure) の Service Fabric を使用します。 特定の問題をトラブルシューティングするときに、Service Fabric のログが必要な可能性があります。 これらのログは C:\ProgramData\Microsoft\Service ファブリックでは、各ネットワーク コントローラー ノードにあります。

ユーザー実行している場合、_デバッグ NetworkController_コマンドレット、追加のログは、ネットワーク コントローラーでサーバー リソースが指定されている各 Hyper-V ホストでの利用可能ななります。 これらのログ (およびトレースが有効な場合) が C:\NCDiagnostics 下に保持されます。

### <a name="slb-diagnostics"></a>SLB 診断

#### <a name="slbm-fabric-errors-hosting-service-provider-actions"></a>SLBM ファブリック エラー (ホスティング サービス プロバイダーの操作)

1.  ソフトウェア ロード バランサー マネージャー (SLBM) が機能していることと、オーケストレーションのレイヤーが互いに通信できることを確認します。SLBM SLB Mux]-> [と SLBM SLB ホスト エージェント]-> [します。 実行[DumpSlbRestState](https://github.com/Microsoft/SDN/blob/master/Diagnostics/DumpSlbRestState.ps1)ネットワーク コントローラーの REST エンドポイントへのアクセスを持つ任意のノードから。  
2.  検証、*SDNSLBMPerfCounters*ネットワーク コントローラー ノードの Vm (可能であれば、プライマリ ネットワーク コントローラー ノード - Get-NetworkControllerReplica) のいずれかで。
    1.  ロード バランサー (LB) エンジンが SLBM に接続されているか。 (*SLBM LBEngine 構成合計*> 0)  
    2.  SLBM 少なくともの認識、独自のエンドポイントですか。 (*VIP エンドポイント合計*> = 2)  
    3.  Hyper-V (DIP) のホストが SLBM に接続されているか。 (*接続している HP クライアント*num サーバー = =)   
    4.  SLBM は Muxes に接続されているか。 (*Muxes が接続されている* == *SLBM に正常な Muxes* == *Muxes が正常なレポート*= # SLB Muxes Vm)。  
3.  BGP ルーターに構成されては SLB MUX とピアリング正常にすることを確認します。  
    1.  RRAS をリモート アクセス (つまり BGP 仮想マシン) を使用して: 場合  
        1.  Get-BgpPeer が接続されている表示する必要があります。  
        2.  Get-BgpRouteInformation は、少なくともルートを表示、SLBM の自己 VIP  
    2.  BGP ピアとして別の物理上部ラック (ToR) を使用して場合のドキュメントを参照してください。  
        1.  例: # bgp インスタンスを表示します。  
4.  検証、*SlbMuxPerfCounters*と*SLBMUX* SLB Mux VM 上でパフォーマンス モニター カウンター
5.  ソフトウェア ロード バランサー マネージャー リソース VIP 範囲と構成の状態を確認します。  
    1.  Get-NetworkControllerLoadBalancerConfiguration ConnectionUri < https://<FQDN or IP>|convertto json の深さ 8 (SLBM self VIP を確認して IP プール内の VIP 範囲 (*LoadBalanacerManagerIPAddress*) し、任意のテナントに接続する Vip は、これらの範囲内で)  
        1. "< 公開/秘密 VIP 論理ネットワーク リソース ID >"を Get-NetworkControllerIpPool ネットワーク ID SubnetId"< 公開/秘密 VIP 論理サブネット リソース ID >"- ResourceId"<IP Pool Resource Id>"ConnectionUri $uri | convertto json の深さ 8 
    2.  Debug-NetworkControllerConfigurationState-  

失敗の上場チェックのいずれか場合、は、テナント SLB 状態が障害モードでもできます。  

**修復**   
表示、次の診断情報に基づきは、次の修正します。  
* SLB Multiplexers が接続されていることを確認します。  
  * 証明書の問題を修正します。  
  * ネットワーク接続の問題を修正します。  
* BGP ピアリング情報が正常に構成されていることを確認します。  
* レジストリでのホスト ID がサーバー リソース内のサーバー インスタンスの ID と一致することを確認 (については、付録を参照*HostNotConnected*エラー コード)  
* ログを収集します。  

#### <a name="slbm-tenant-errors-hosting-service-provider--and-tenant-actions"></a>SLBM テナント エラー (ホスティング サービス プロバイダーおよびテナント アクション)

1.  [ホスト]確認*デバッグ NetworkControllerConfigurationState* LoadBalancer リソースがエラー状態のかどうかを確認してください。 次のアクション アイテム付録内のテーブルで軽減しようとしてください。   
    1.  VIP エンドポイントが存在し、広告のルートであることを確認します。  
    2.  VIP エンドポイントの探索された DIP エンドポイントの数を確認します。  
2.  [テナント]検証ロード バランサーのリソースが正しく指定されています。  
    1.  DIP を検証 SLBM で登録されているエンドポイントが LoadBalancer バック エンド アドレス プールの IP 構成に対応するテナントのバーチャル マシンをホストしています。  
3.  [ホスト]DIP エンドポイントの検出または接続されていない: 場合   
    1.  確認*デバッグ NetworkControllerConfigurationState*  
        1.  NC を検証および SLB ホスト エージェントが正常を使用して、ネットワーク コントローラー イベント コーディネーターに接続されています。 ``netstat -anp tcp |findstr 6640)``  
    2.  確認*HostId*で*nchostagent*サービス レジストリ キー (参照*HostNotConnected*付録のエラー コード)、対応するサーバー リソースのインスタンス ID と一致する (``Get-NCServer |convertto-json -depth 8``)  
    3.  仮想マシンのポートのポート プロファイルの ID が対応する仮想マシン NIC のリソースのインスタンス ID と一致するを確認します。   
4.  [ホスティング プロバイダー]ログを収集します。   

#### <a name="slb-mux-tracing"></a>SLB Mux トレース

ソフトウェア ロード バランサー Muxes からの情報は、イベント ビューアーからも判断できます。 
1. [イベント ビューアーの表示] メニュー「を表示する分析とデバッグ ログの」をクリックします。
2. "アプリケーションとサービス ログ] に移動 > Microsoft > Windows > SlbMuxDriver > イベント ビューアーでのトレース 
3. それを右クリックし、"ログを有効にする] を選択します。

>[!NOTE]
>このログの問題を再現しようとしているときに、短時間の有効化だけがあることをお勧め

### <a name="vfp-and-vswitch-tracing"></a>VFP と vSwitch のトレース

Hyper-v ホストからホスト、ゲスト仮想マシンをテナントの仮想ネットワークに接続されているをホストしている、問題がある可能性がありますを確認するときに VFP トレースを収集することができます。

```
netsh trace start provider=Microsoft-Windows-Hyper-V-VfpExt overwrite=yes tracefile=vfp.etl report=disable provider=Microsoft-Windows-Hyper-V-VmSwitch 
netsh trace stop
netsh trace convert .\vfp.etl ov=yes 
```
