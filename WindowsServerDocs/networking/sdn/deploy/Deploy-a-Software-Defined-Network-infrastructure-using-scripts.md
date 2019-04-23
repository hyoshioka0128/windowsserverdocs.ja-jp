---
title: スクリプトを使用してソフトウェア定義ネットワーク インフラストラクチャをデプロイします。
description: このトピックでは、Windows Server 2016 でスクリプトを使用して、Microsoft ソフトウェア定義ネットワーク (SDN) インフラストラクチャをデプロイする方法について説明します。
manager: dougkim
ms.prod: windows-server-threshold
ms.service: virtual-network
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 5ba5bb37-ece0-45cb-971b-f7149f658d19
ms.author: pashort
author: shortpatti
ms.date: 08/23/2018
ms.openlocfilehash: dabfe3de4cc307723ff7e614fb73e3903e74aeb2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844623"
---
# <a name="deploy-a-software-defined-network-infrastructure-using-scripts"></a>スクリプトを使用してソフトウェア定義ネットワーク インフラストラクチャを展開する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、スクリプトを使用して、Microsoft ソフトウェア定義ネットワーク (SDN) インフラストラクチャをデプロイします。 インフラストラクチャに高可用性 (HA) ネットワーク コント ローラー、HA ソフトウェア ロード バランサー (SLB) が含まれています/MUX、仮想ネットワーク、および関連するアクセス制御リスト (Acl)。 さらに、別のスクリプトは、SDN インフラストラクチャを検証するためのテナントのワークロードをデプロイします。  
  
仮想ネットワークの外部通信するために、テナントのワークロードを実行する場合に、SLB の NAT 規則、サイト対サイト ゲートウェイのトンネルまたは仮想および物理ワークロード間でルーティングするレイヤー 3 の転送をセットアップできます。  
  
Virtual Machine Manager (VMM) を使用して SDN インフラストラクチャをデプロイすることもできます。 詳細については、次を参照してください。 [VMM ファブリックでソフトウェア定義ネットワーク (SDN) インフラストラクチャをセットアップ](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-overview)します。  

  
## <a name="pre-deployment"></a>配置前  
  
> [!IMPORTANT]  
> 展開を開始する前に、計画し、ホストと物理ネットワーク インフラストラクチャを構成する必要があります。 詳細については、[ソフトウェア定義ネットワーク インフラストラクチャの計画](../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)に関する記事を参照してください。  
  
Windows Server 2016 がインストールされているすべての HYPER-V ホストが必要です。  
  
## <a name="deployment-steps"></a>展開の手順  
まず、HYPER-V ホスト (物理サーバー)、HYPER-V 仮想スイッチと IP アドレスの割り当てを構成します。 HYPER-V、共有またはローカルと互換性があるストレージの種類を使用できます。  

### <a name="install-host-networking"></a>ネットワーク ホストをインストールします。  

1. NIC ハードウェアの利用可能な最新のネットワーク ドライバをインストールします。  
2. すべてのホストで HYPER-V の役割をインストール (詳細については、次を参照してください。 [Windows Server 2016 で Hyper-v の概要](https://docs.microsoft.com/windows-server/virtualization/hyper-v/get-started/Get-started-with-Hyper-V-on-Windows)します。   
  
   ```PowerShell
   Install-WindowsFeature -Name Hyper-V -ComputerName <computer_name> -IncludeManagementTools -Restart
   ```  
    
3. HYPER-V 仮想スイッチを作成します。<p>たとえば、すべてのホスト、同じスイッチ名を使用して**sdnSwitch**します。 少なくとも 1 つのネットワーク アダプターを構成または、セットを使用して、少なくとも 2 つのネットワーク アダプターを構成します。 します。 最大受信展開するには、2 つの Nic を使用する場合に発生します。  

   ```PowerShell
   New-VMSwitch "<switch name>" -NetAdapterName "<NetAdapter1>" [, "<NetAdapter2>" -EnableEmbeddedTeaming $True] -AllowManagementOS $True
   ```  
   >[!TIP] 
   >個別の管理 Nic がある場合は、手順 4. と 5. を省略できます。

3. 計画に関するトピックを参照してください ([ソフトウェア定義ネットワーク インフラストラクチャを計画](../../sdn/plan/../../sdn/plan/../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)) と管理の VLAN の VLAN ID を取得する、ネットワーク管理者と連携します。 管理の VLAN に新しく作成された仮想スイッチの管理の vNIC をアタッチします。 お客様の環境では、VLAN タグを使用していない場合、この手順を省略できます。  
   
   ```PowerShell
   Set-VMNetworkAdapterIsolation -ManagementOS -IsolationMode Vlan -DefaultIsolationID <Management VLAN> -AllowUntaggedTraffic $True
   ```  
 
4. 計画に関するトピックを参照してください ([ソフトウェア定義ネットワーク インフラストラクチャを計画](../../sdn/plan/../../sdn/plan/../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)) か、DHCP を使用して、ネットワーク管理者または新しく作成された管理 vNIC に IP アドレスを割り当てる静的 IP 割り当てと連携し、vSwitch します。 次の例では、静的 IP アドレスを作成し、vSwitch の管理の vNIC に割り当てる方法を示します。  
 
   ```PowerShell
   New-NetIPAddress -InterfaceAlias "vEthernet (<switch name>)" -IPAddress <IP> -DefaultGateway <Gateway IP> -AddressFamily IPv4 -PrefixLength <Length of Subnet Mask - for example: 24>
   ```  
      
5. [省略可能]Active Directory Domain Services のホストにバーチャル マシンを展開 ([Active Directory Domain Services をインストール (レベル 100)](https://technet.microsoft.com/library/hh472162.aspx)と DNS サーバー。  
   
    a.  Active Directory と DNS サーバーの仮想マシンを管理 VLAN に接続します。
    
       ```PowerShell
       Set-VMNetworkAdapterIsolation -VMName "<VM Name>" -Access -VlanId <Management VLAN> -AllowUntaggedTraffic $True  
       ```   

   b.  Active Directory Domain Services と DNS をインストールします。  

   >[!NOTE]
   >ネットワーク コント ローラーでは、認証に Kerberos と X.509 証明書をサポートしています。 このガイドでは、さまざまな目的で両方の認証メカニズムが使用されます (が 1 つだけが必要です)。  
        
6. すべての HYPER-V ホストをドメインに参加させます。 ドメイン名を解決できる DNS サーバーに管理ネットワーク ポイントに割り当てられた IP アドレスを持つネットワーク アダプターの DNS サーバー エントリを確認してください。 

   ```PowerShell   
   Set-DnsClientServerAddress -InterfaceAlias "vEthernet (<switch name>)" -ServerAddresses <DNS Server IP>  
   ```
   
   a.  右クリックして**開始**、 をクリックして**システム**、順にクリックします**設定の変更**します。  
   b.  **[変更]** をクリックします。  
   c. クリックして**ドメイン**し、ドメイン名を指定します。  
   d. **[OK]** をクリックします。  
   e. ユーザー名とパスワード資格情報が表示されたらを入力します。  
   f. サーバーを再起動します。  
  
### <a name="validation"></a>［確認］  
そのホストのネットワークを検証するには、次の手順を正しくセットアップを使用します。  

1. VM スイッチが正常に作成されたことを確認します。  
      
   ```PowerShell
   Get-VMSwitch "<switch name>"
   ```  

2. 管理の VLAN に VM スイッチの管理の vNIC が接続されていることを確認します。  

   >[!NOTE]
   >管理およびテナントのトラフィックが同じ NIC を共有する場合にのみ該当    
      
   ```PowerShell
   Get-VMNetworkAdapterIsolation -ManagementOS
   ```

3. すべての HYPER-V ホストと外部管理のリソース、たとえば、DNS サーバーを検証します。<p>管理 IP アドレスまたは完全修飾ドメイン名 (FQDN) を使用して ping を使用してアクセスできることを確認します。   
      
   ``ping <Hyper-V Host IP>``  
   ``ping <Hyper-V Host FQDN>``  

4. 配置ホストで、次のコマンドを実行し、使用する Kerberos 資格情報を確認するには、各 HYPER-V ホストの FQDN は、すべてのサーバーへのアクセスを提供します。 を指定します。  
      
   ``winrm id -r:<Hyper-V Host FQDN>``  
      
### <a name="nano-installation-requirements-and-notes"></a>Nano インストール要件および注意事項  

展開するため、HYPER-V ホスト (物理サーバー) として Nano を使用する場合は、次の追加要件で。  

1. Nano のすべてのノードは、DSC パッケージを言語パックをインストールする必要があります。  
   
    - Microsoft-NanoServer-DSC-Package.cab  
    - Microsoft-NanoServer-DSC-Package_en-us.cab
   
    ``dism /online /add-package /packagepath:<Path> /loglevel:4``  

2. 非 Nano ホスト (Windows Server Core または GUI を使用した Windows Server) からは、SDN Express スクリプトを実行する必要があります。 Nano では、PowerShell ワークフローはサポートされていません。  

3.  ネットワーク コント ローラーの NorthBound API を呼び出す PowerShell または NC REST ラッパー (Invoke-webrequest および Invoke-restmethod 依存) を使用する必要がありますいない Nano ホストから。  
   
         
### <a name="run-sdn-express-scripts"></a>SDN Express スクリプトを実行します。  
  
1. 移動して、 [Microsoft SDN GitHub リポジトリ](https://github.com/Microsoft/SDN.git)インストール ファイル。

2. 指定された配置先のコンピューターにリポジトリからインストール ファイルをダウンロードします。 クリックして**複製またはダウンロード** をクリックし、 **ZIP のダウンロード**します。  
 
   >[!NOTE]
   >2016 以降により、指定された配置先のコンピューターに Windows Server を実行する必要があります。
 
3. Zip ファイルとコピーを展開し、 **SDNExpress**配置先のコンピューターのフォルダー`C:\`フォルダー。  
  
4. 共有、`C:\SDNExpress`フォルダーとして"**SDNExpress**"のアクセス許可を持つ**Everyone**に**読み取り/書き込み**します。  
  
5. 移動し、`C:\SDNExpress`フォルダー。<p>次のフォルダーを参照してください。  

   |フォルダー名|説明|  
   |---------------|---------------|  
   |AgentConf|プログラムのネットワーク ポリシーには、各 Windows Server 2016 の HYPER-V ホストでの SDN のホスト エージェントによって使用される OVSDB スキーマの新しいコピーを保持します。|  
   |証明書|NC 証明書ファイルの一時的な共有場所。|  
   |画像|空の、Windows Server 2016 の vhdx イメージをここに配置|  
   |ツール|トラブルシューティングとデバッグのためのユーティリティです。  ホストとバーチャル マシンにコピーされます。  または配置するネットワーク モニター Wireshark は、ここに必要な場合に使用できるようにすることをお勧めします。|  
   |スクリプト|配置スクリプトです。<br /><br />-   **SDNExpress.ps1**<br />    展開し、ネットワーク コント ローラーの仮想マシン、SLB Mux 仮想マシン、ゲートウェイ プール、プールに対応する HNV ゲートウェイ仮想マシンなど、ファブリックを構成します。<br />-   **FabricConfig.psd1**<br />    SDNExpress スクリプト用の構成ファイル テンプレート。  環境には、これをカスタマイズします。<br />-   **SDNExpressTenant.ps1**<br />    負荷分散された VIP と仮想ネットワーク上のサンプル テナント ワークロードをデプロイします。<br />    1 つまたは複数のネットワーク接続 (IPSec S2S VPN、GRE、L3) は、以前に作成したテナントのワークロードに接続されているサービス プロバイダーのエッジ ゲートウェイでも準備されます。 IPSec と GRE ゲートウェイが接続に使用できる、対応する VIP の IP アドレスと L3 転送ゲートウェイ経由で、対応するアドレス プール経由でします。<br />    元に戻すオプションも、対応する構成を削除するのには、このスクリプトを使用できます。<br />-   **TenantConfig.psd1**<br />    テナントのワークロードと S2S ゲートウェイの構成用のテンプレート構成ファイル。<br />-   **SDNExpressUndo.ps1**<br />    Fabric の環境がクリーンアップし、開始状態にリセットされます。<br />-   **SDNExpressEnterpriseExample.ps1**<br />    1 つのリモート アクセス ゲートウェイと (必要に応じて) 1 つの対応するエンタープライズ仮想マシン 1 サイトあたり 1 つまたは複数のエンタープライズ サイト環境を準備します。 IPSec または GRE エンタープライズ ゲートウェイは、S2S トンネルを確立するために、サービス プロバイダーのゲートウェイの対応する VIP の IP アドレスに接続します。 L3 転送ゲートウェイは、対応するピアの IP アドレスで接続します。 <br />            元に戻すオプションも、対応する構成を削除するのには、このスクリプトを使用できます。<br />-   **EnterpriseConfig.psd1**<br />    エンタープライズ サイト対サイト ゲートウェイとクライアント VM の構成用のテンプレート構成ファイル。|  
   |TenantApps|ファイルの例のテナントのワークロードをデプロイするために使用します。|  
   ---
  
6. Windows Server 2016 の VHDX ファイルが確認します、**イメージ**フォルダー。  
  
7. 変更することで、SDNExpress\scripts\FabricConfig.psd1 ファイルをカスタマイズ、 **<< 置換 >>** に合わせて、ラボ インフラストラクチャのホスト名、ドメイン名、ユーザー名およびパスワードを含む特定の値を持つタグとネットワークの計画トピックにあるネットワークのネットワークの情報。  

8. NetworkControllerRestName (FQDN) と NetworkControllerRestIP の dns ホスト A レコードを作成します。  

9. ドメイン管理者の資格情報を持つユーザーとして、スクリプトを実行します。  
      
   ``SDNExpress\scripts\SDNExpress.ps1 -ConfigurationDataFile FabricConfig.psd1 -Verbose``  
      
10. すべての操作を元に戻すには、次のコマンドを実行します。  
      
    ``SDNExpress\scripts\SDNExpressUndo.ps1 -ConfigurationDataFile FabricConfig.psd1 -Verbose``  
      
#### <a name="validation"></a>［確認］  

SDN Express スクリプトのすべてのエラーを報告することがなく完了するまで実行すると仮定した場合は、ファブリックのリソースが正しく展開されているし、テナントの配置に使用できることを確認するには、次の手順を実行できます。  

使用[診断ツール](https://docs.microsoft.com/windows-server/networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack)にエラーがない任意のファブリック リソースのネットワーク コント ローラーのことを確認します。  
      
   ``Debug-NetworkControllerConfigurationState -NetworkController <FQDN of Network Controller Rest Name>``  
        
   
### <a name="deploy-a-sample-tenant-workload-with-the-software-load-balancer"></a>ソフトウェア ロード バランサーをサンプル テナント ワークロードをデプロイします。  
    
ファブリックのリソースがデプロイされると、これで、サンプル テナントのワークロードをデプロイすることで、SDN 展開エンド ツー エンドを検証できます。 このテナント ワークロードは、2 つの仮想サブネット (web 層とデータベース層) 分散 SDN ファイアウォールを使用してアクセス制御リスト (ACL) 規則によって保護されているので構成されます。 Web 層の仮想サブネットは仮想 IP (VIP) アドレスを使用して SLB/MUX を介してアクセスできます。 スクリプトは自動的に 2 つの web 層の仮想マシンと 1 つのデータベース層の仮想マシンを展開し、仮想サブネットに接続します。  
  
1.  SDNExpress\scripts\TenantConfig.psd1 ファイルを変更することでカスタマイズ、 **<< 置換 >>** 特定の値を持つタグ (例。VHD イメージの名前、ネットワーク コント ローラー REST 名、vSwitch の名前、前に思われる FabricConfig.psd1 ファイルで定義されているなど)  

2.  スクリプトを実行します。 例:  

    ``SDNExpress\scripts\SDNExpressTenant.ps1 -ConfigurationDataFile TenantConfig.psd1 -Verbose``  

3.  構成を元に戻すには、同じスクリプトを実行、**を元に戻す**パラメーター。 次に、例を示します。  

    ``SDNExpress\scripts\SDNExpressTenant.ps1 -Undo -ConfigurationDataFile TenantConfig.psd1 -Verbose``  

#### <a name="validation"></a>［確認］  

テナントのデプロイが成功したことを検証するには、次の操作を行います。

1. データベース層の仮想マシンにログインし、web 層の仮想マシン (web 層の仮想マシンで Windows ファイアウォールがになっていることを確認) のいずれかの IP アドレスに ping を実行しようとしてください。  

2. ネットワーク コント ローラーのテナント リソースのエラーを確認します。 ネットワーク コント ローラーに、レイヤー 3 接続のすべての HYPER-V ホストから、次を実行します。  
      
   ``Debug-NetworkControllerConfigurationState -NetworkController <FQDN of Network Controller REST Name>``

3. ロード バランサーが正しく実行されていることを確認するには、すべての HYPER-V ホストから、次を実行します。
    
   ``wget <VIP IP address>/unique.htm -disablekeepalive -usebasicparsing``
   
   場所`<VIP IP address>`は web 層 TenantConfig.psd1 ファイルで構成した VIP の IP アドレスです。 

   >[!TIP]
   >検索、 `VIPIP` TenantConfig.psd1 変数。

   ロード バランサーが使用可能な Dip 間の切り替えを確認するには、この複数回実行します。 また、web ブラウザーを使用してこの動作を確認できます。 `<VIP IP address>/unique.htm` を参照します。 ブラウザーを閉じて新しいインスタンスを開くし、再度参照します。 青色のページと、キャッシュがタイムアウトするまでに、ブラウザーがページをキャッシュする場合を除き、代替の緑色のページが表示されます。

---