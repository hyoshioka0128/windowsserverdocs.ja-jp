---
title: スクリプトを使用してソフトウェアで定義されたネットワークインフラストラクチャを展開する
description: このトピックでは、Windows Server 2016 のスクリプトを使用して、Microsoft ソフトウェア定義ネットワーク (SDN) インフラストラクチャを展開する方法について説明します。 '
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 5ba5bb37-ece0-45cb-971b-f7149f658d19
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/23/2018
ms.openlocfilehash: 522c4c640daf438f122857154fed2b0ec8138bec
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855725"
---
# <a name="deploy-a-software-defined-network-infrastructure-using-scripts"></a>スクリプトを使用してソフトウェア定義ネットワーク インフラストラクチャを展開する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016 ' このトピックでは、スクリプトを使用して Microsoft ソフトウェア定義ネットワーク (SDN) インフラストラクチャを展開します。 インフラストラクチャには、高可用性 (HA) ネットワークコントローラー、HA ソフトウェア Load Balancer (SLB)/MUX、仮想ネットワーク、および関連する Access Control リスト (Acl) が含まれています。 また、別のスクリプトによって、SDN インフラストラクチャを検証するためのテナントワークロードがデプロイされます。  

テナントのワークロードが仮想ネットワークの外部で通信できるようにする場合は、SLB NAT 規則、サイト間ゲートウェイトンネル、またはレイヤー3転送を設定して、仮想ワークロードと物理ワークロード間をルーティングできます。  

Virtual Machine Manager (VMM) を使用して SDN インフラストラクチャを展開することもできます。 詳細については、「 [VMM ファブリックでのソフトウェア定義ネットワーク (SDN) インフラストラクチャのセットアップ](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-overview)」を参照してください。  


## <a name="pre-deployment"></a>配置前  

> [!IMPORTANT]  
> 展開を開始する前に、ホストと物理ネットワークインフラストラクチャを計画して構成する必要があります。 詳細については、[ソフトウェア定義ネットワーク インフラストラクチャの計画](../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)に関する記事を参照してください。  

すべての Hyper-v ホストに Windows Server 2016 がインストールされている必要があります。  

## <a name="deployment-steps"></a>展開の手順  
まず、hyper-v ホストの (物理サーバー) Hyper-v 仮想スイッチと IP アドレスの割り当てを構成します。 Hyper-v、shared、または local と互換性のあるストレージの種類を使用できます。  

### <a name="install-host-networking"></a>ホストネットワークのインストール  

1. NIC ハードウェアで使用可能な最新のネットワークドライバーをインストールします。  
2. Hyper-v の役割をすべてのホストにインストールします (詳細については、「 [Windows Server 2016 で hyper-v の使用を開始](https://docs.microsoft.com/windows-server/virtualization/hyper-v/get-started/Get-started-with-Hyper-V-on-Windows)する」を参照してください)。   

   ```PowerShell
   Install-WindowsFeature -Name Hyper-V -ComputerName <computer_name> -IncludeManagementTools -Restart
   ```  

3. Hyper-v 仮想スイッチを作成します。<p>すべてのホストに対して同じスイッチ名を使用します ( **Sdnswitch**など)。 少なくとも1つのネットワークアダプターを構成するか、SET を使用する場合は、少なくとも2つのネットワークアダプターを構成します。 2つの Nic を使用した場合、最大受信拡散が発生します。  

   ```PowerShell
   New-VMSwitch "<switch name>" -NetAdapterName "<NetAdapter1>" [, "<NetAdapter2>" -EnableEmbeddedTeaming $True] -AllowManagementOS $True
   ```  
   >[!TIP] 
   >個別の管理 Nic がある場合は、手順 4. および 5. を省略できます。

3. 計画に関するトピック ([ソフトウェアで定義されたネットワークインフラストラクチャを計画](../../sdn/plan/../../sdn/plan/../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)する) を参照し、ネットワーク管理者と協力して、管理 VLAN の vlan ID を取得します。 新しく作成した仮想スイッチの管理 vNIC を管理 VLAN に接続します。 環境で VLAN タグが使用されていない場合は、この手順を省略できます。  

   ```PowerShell
   Set-VMNetworkAdapterIsolation -ManagementOS -IsolationMode Vlan -DefaultIsolationID <Management VLAN> -AllowUntaggedTraffic $True
   ```  

4. 計画に関するトピック ([ソフトウェアで定義されたネットワークインフラストラクチャを計画](../../sdn/plan/../../sdn/plan/../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)する) を参照し、ネットワーク管理者と協力して、DHCP または静的 ip の割り当てを使用して、新しく作成した VSwitch の管理 VNIC に ip アドレスを割り当てます。 次の例では、静的 IP アドレスを作成し、vSwitch の Management vNIC に割り当てる方法を示します。  

   ```PowerShell
   New-NetIPAddress -InterfaceAlias "vEthernet (<switch name>)" -IPAddress <IP> -DefaultGateway <Gateway IP> -AddressFamily IPv4 -PrefixLength <Length of Subnet Mask - for example: 24>
   ```  

5. Optionalバーチャルマシンをホスト Active Directory Domain Services に展開します ([Active Directory Domain Services (レベル 100)](https://technet.microsoft.com/library/hh472162.aspx)と DNS サーバーをインストールします。  

    a. Active Directory/DNS サーバー仮想マシンを管理 VLAN に接続します。

       ```PowerShell
       Set-VMNetworkAdapterIsolation -VMName "<VM Name>" -Access -VlanId <Management VLAN> -AllowUntaggedTraffic $True  
       ```   

   b. Active Directory Domain Services と DNS をインストールします。  

   >[!NOTE]
   >ネットワークコントローラーは、認証に Kerberos と x.509 の両方の証明書をサポートしています。 このガイドでは、さまざまな目的で両方の認証メカニズムを使用します (ただし、1つだけが必要です)。  

6. すべての Hyper-v ホストをドメインに参加させます。 管理ネットワークに割り当てられた IP アドレスを持つネットワークアダプターの DNS サーバーエントリが、ドメイン名を解決できる DNS サーバーを指していることを確認します。 

   ```PowerShell   
   Set-DnsClientServerAddress -InterfaceAlias "vEthernet (<switch name>)" -ServerAddresses <DNS Server IP>  
   ```

   a. **[スタート]** ボタンを右クリックし、 **[システム]** をクリックして、 **[設定の変更]** をクリックします。  
   b. **[変更]** をクリックします。  
   c. **[ドメイン]** をクリックし、ドメイン名を指定します。  "" "" d. **[OK]** をクリックすると、  
   e. プロンプトが表示されたら、ユーザー名とパスワードの資格情報を入力します。  
   f. サーバーを再起動します。  

### <a name="validation"></a>Validation  
ホストネットワークが正しくセットアップされていることを確認するには、次の手順に従います。  

1. VM スイッチが正常に作成されたことを確認します。  

   ```PowerShell
   Get-VMSwitch "<switch name>"
   ```  

2. VM スイッチの Management vNIC が管理 VLAN に接続されていることを確認します。  

   >[!NOTE]
   >管理とテナントのトラフィックが同じ NIC を共有している場合にのみ関連します。    

   ```PowerShell
   Get-VMNetworkAdapterIsolation -ManagementOS
   ```

3. すべての Hyper-v ホストと外部管理リソース (たとえば、DNS サーバー) を検証します。<p>管理 IP アドレスまたは完全修飾ドメイン名 (FQDN) を使用して ping でアクセスできることを確認します。   

   ``ping <Hyper-V Host IP>``  
   ``ping <Hyper-V Host FQDN>``  

4. 展開ホストで次のコマンドを実行し、各 Hyper-v ホストの FQDN を指定して、使用する Kerberos 資格情報がすべてのサーバーにアクセスできるようにします。  

   ``winrm id -r:<Hyper-V Host FQDN>``  

### <a name="nano-installation-requirements-and-notes"></a>Nano のインストール要件と注意事項  

Nano を Hyper-v ホスト (物理サーバー) として展開に使用する場合は、次の追加要件があります。  

1. すべての Nano ノードには、次の言語パックと共に DSC パッケージがインストールされている必要があります。  

   - Microsoft-NanoServer-DSC-Package  
   - NanoServer (Microsoft-DSC-Package_en)

     ``dism /online /add-package /packagepath:<Path> /loglevel:4``  

2. SDN Express スクリプトは、Nano 以外のホスト (Windows Server Core または Windows Server/GUI) から実行する必要があります。 PowerShell ワークフローは、Nano ではサポートされていません。  

3. PowerShell または NC REST ラッパー (Invoke-restmethod とに依存します) を使用したネットワークコントローラー NorthBound API の呼び出しは、Nano 以外のホストから実行する必要があります。  


### <a name="run-sdn-express-scripts"></a>SDN Express スクリプトを実行する  

1. インストールファイルについては、 [MICROSOFT SDN GitHub リポジトリ](https://github.com/Microsoft/SDN.git)を参照してください。

2. 指定された展開コンピューターにリポジトリからインストールファイルをダウンロードします。 **[複製またはダウンロード]** をクリックし、 **[ZIP のダウンロード]** をクリックします。  

   >[!NOTE]
   >指定された展開コンピューターは、Windows Server 2016 以降を実行している必要があります。

3. Zip ファイルを展開し、 **Sdnexpress**フォルダーを展開コンピューターの `C:\` フォルダーにコピーします。  

4. **すべてのユーザー**が**読み取り/書き込み**可能なアクセス許可を持つ "**sdnexpress**" として `C:\SDNExpress` フォルダーを共有します。  

5. `C:\SDNExpress` フォルダーに移動します。<p>次のフォルダーが表示されます。  


   | Folder Name |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              説明                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
   |-------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |  AgentConf  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   は、各 Windows Server 2016 Hyper-v ホスト上の SDN ホストエージェントが使用する、ネットワークポリシーをプログラムするために使用される、保存されていないスキーマの新しいコピーを保持します。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
   |    証明書    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         NC 証明書ファイルの一時的な共有の場所。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
   |   [画像]    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         空の場合は、Windows Server 2016 vhdx イメージをここに配置します                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
   |    ツール    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            トラブルシューティングとデバッグのためのユーティリティ。  ホストと仮想マシンにコピーされます。  ネットワークモニターまたは Wireshark をここに配置して、必要に応じて使用できるようにすることをお勧めします。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
   |   スクリプト   | 配置スクリプト。<p>-   **Sdnexpress ps1**<br />    ネットワークコントローラー仮想マシン、SLB Mux 仮想マシン、ゲートウェイプール、およびプールに対応する HNV ゲートウェイ仮想マシンを含む、ファブリックをデプロイして構成します。<br />-   **Fabricconfig. .psd1**<br />    SDNExpress スクリプト用の構成ファイルテンプレート。  これは、環境に合わせてカスタマイズします。<br />-   **SDNExpressTenant**<br />    負荷分散された VIP を使用して、仮想ネットワーク上にサンプルテナントワークロードをデプロイします。<br />    また、は、以前に作成されたテナントワークロードに接続されているサービスプロバイダーのエッジゲートウェイに対して、1つまたは複数のネットワーク接続 (IPSec S2S VPN、GRE、L3) をプロビジョニングします。 IPSec と GRE ゲートウェイは、対応する VIP IP アドレスと、対応するアドレスプール上の L3 転送ゲートウェイを介して接続するために使用できます。<br />    このスクリプトを使用すると、[元に戻す] オプションを使用して、対応する構成を削除することもできます。<br />-   **Tenantconfig. .psd1**<br />    テナントワークロードと S2S ゲートウェイ構成用のテンプレート構成ファイル。<br />-   **SDNExpressUndo**<br />    Fabric 環境をクリーンアップし、開始状態にリセットします。<br />-   **SDNExpressEnterpriseExample**<br />    1つのリモートアクセスゲートウェイと (必要に応じて) サイトごとに1つの対応するエンタープライズ仮想マシンを使用して、1つまたは複数のエンタープライズサイト環境をプロビジョニングします。 IPSec または GRE エンタープライズゲートウェイは、サービスプロバイダーゲートウェイの対応する VIP IP アドレスに接続して、S2S トンネルを確立します。 L3 転送ゲートウェイは、対応するピア IP アドレスを介して接続します。 <br />            このスクリプトを使用すると、[元に戻す] オプションを使用して、対応する構成を削除することもできます。<br />-   **EnterpriseConfig .psd1**<br />    エンタープライズサイト間ゲートウェイとクライアント VM 構成用のテンプレート構成ファイル。 |
   | TenantApps  |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             テナントのワークロード例をデプロイするために使用されるファイル。                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |

   ---

6. Windows Server 2016 VHDX ファイルが**Images**フォルダーにあることを確認します。  

7. < を変更して SDNExpress\scripts\FabricConfig.psd1 ファイルをカスタマイズします。そのためには、ホスト名、ドメイン名、ユーザー名とパスワード、計画ネットワークに記載されているネットワークのネットワーク情報を含むラボインフラストラクチャに合わせて、> > タグを特定の値に**置き換え <** ます。  

8. NetworkControllerRestName (FQDN) と NetworkControllerRestIP の DNS にホスト A レコードを作成します。  

9. ドメイン管理者の資格情報を持つユーザーとしてスクリプトを実行します。  

   ``SDNExpress\scripts\SDNExpress.ps1 -ConfigurationDataFile FabricConfig.psd1 -Verbose``  

10. すべての操作を元に戻すには、次のコマンドを実行します。  

    ``SDNExpress\scripts\SDNExpressUndo.ps1 -ConfigurationDataFile FabricConfig.psd1 -Verbose``  

#### <a name="validation"></a>Validation  

SDN Express スクリプトがエラーを報告せずに完了するようにした場合は、次の手順を実行して、ファブリックのリソースが正しくデプロイされ、テナントのデプロイに使用できるようにすることができます。  

[診断ツール](https://docs.microsoft.com/windows-server/networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack)を使用して、ネットワークコントローラー内のファブリックリソースにエラーがないことを確認します。  

   ``Debug-NetworkControllerConfigurationState -NetworkController <FQDN of Network Controller Rest Name>``  


### <a name="deploy-a-sample-tenant-workload-with-the-software-load-balancer"></a>ソフトウェアロードバランサーを使用してサンプルテナントのワークロードをデプロイする  

ファブリックリソースがデプロイされたので、サンプルのテナントワークロードをデプロイして、SDN デプロイをエンドツーエンドで検証できます。 このテナントワークロードは、SDN 分散ファイアウォールを使用して Access Control リスト (ACL) 規則によって保護されている2つの仮想サブネット (web 層とデータベース層) で構成されます。 Web 層の仮想サブネットには、仮想 IP (VIP) アドレスを使用して SLB/MUX 経由でアクセスできます。 このスクリプトは、2つの web 層仮想マシンと1つのデータベース層仮想マシンを自動的にデプロイし、仮想サブネットに接続します。  

1.  **< <** を変更して SDNExpress\scripts\TenantConfig.psd1 ファイルをカスタマイズし、> タグ > を特定の値 (たとえば、.psd1 ファイルで定義した VHD イメージ名、ネットワークコントローラー REST 名、vSwitch 名など) に置き換えます。  

2.  スクリプトを実行します。 例 :  

    ``SDNExpress\scripts\SDNExpressTenant.ps1 -ConfigurationDataFile TenantConfig.psd1 -Verbose``  

3.  構成を元に戻すには、 **undo**パラメーターを指定して同じスクリプトを実行します。 例 :  

    ``SDNExpress\scripts\SDNExpressTenant.ps1 -Undo -ConfigurationDataFile TenantConfig.psd1 -Verbose``  

#### <a name="validation"></a>Validation  

テナントの展開が成功したことを確認するには、次の手順を実行します。

1. データベース層の仮想マシンにログインし、web 層の仮想マシンのいずれかの IP アドレスに対して ping を実行します (web 層の仮想マシンで Windows ファイアウォールが無効になっていることを確認してください)。  

2. ネットワークコントローラーのテナントリソースにエラーがないかどうかを確認します。 ネットワークコントローラーへのレイヤー3接続を使用して、任意の Hyper-v ホストから次を実行します。  

   ``Debug-NetworkControllerConfigurationState -NetworkController <FQDN of Network Controller REST Name>``

3. ロードバランサーが正常に実行されていることを確認するには、任意の Hyper-v ホストから次のように実行します。

   ``wget <VIP IP address>/unique.htm -disablekeepalive -usebasicparsing``

   ここで `<VIP IP address>` は、.psd1 ファイルで構成した web 層の VIP IP アドレスです。 

   >[!TIP]
   >.Psd1 で `VIPIP` 変数を検索します。

   この複数を実行して、使用可能な Dip 間のロードバランサーの切り替えを確認します。 Web ブラウザーを使用して、この動作を確認することもできます。 `<VIP IP address>/unique.htm`を参照します。 ブラウザーを閉じ、新しいインスタンスを開いて、もう一度参照します。 キャッシュがタイムアウトする前にブラウザーがページをキャッシュしている場合を除き、青いページと緑色のページが表示されます。

---