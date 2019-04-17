---
title: スクリプトを使用してソフトウェア定義ネットワーク インフラストラクチャを展開します。
description: このトピックでは、Windows Server 2016 でスクリプトを使用した Microsoft ソフトウェア定義ネットワーク (SDN) インフラストラクチャを展開する方法について説明します。
manager: brianlic
ms.prod: windows-server-threshold
ms.service: virtual-network
ms.technology: networking-sdn
ms.topic: get-started-article
ms.assetid: 5ba5bb37-ece0-45cb-971b-f7149f658d19
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4428ad73ab8933510d5a759ec4fa7377ea222ebd
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-a-software-defined-network-infrastructure-using-scripts"></a>スクリプトを使用してソフトウェア定義ネットワーク インフラストラクチャを展開します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、スクリプトを使用した Microsoft ソフトウェア定義ネットワーク (SDN) インフラストラクチャを展開する方法について説明します。 インフラストラクチャに高可用性 (HA) ネットワーク コントローラーを HA ソフトウェア ロード バランサー (SLB) が含まれています/MUX、仮想ネットワーク、およびアクセス制御リスト (Acl) に関連付けられました。 さらに、別のスクリプトは、SDN インフラストラクチャを検証するためのテナント ワークロードを展開します。  
  
外部仮想ネットワークと通信するテナント ワークロードを実行する場合に、ワークロードの仮想および物理間でルーティングする SLB NAT 規則、サイト間ゲートウェイ トンネル、またはレイヤー 3 の転送を設定できます。  
  
Virtual Machine Manager (VMM) を使用して、SDN インフラストラクチャを展開することもできます。 詳細については、次を参照してください。[VMM ファブリック内のソフトウェア定義ネットワーク (SDN) インフラストラクチャをセットアップ](https://technet.microsoft.com/system-center-docs/vmm/scenario/sdn-overview)します。  
  
## <a name="pre-deployment"></a>展開前  
  
> [!IMPORTANT]  
> 展開を開始する前に計画し、ホストおよび物理ネットワーク インフラストラクチャを構成する必要があります。 詳細については、次を参照してください。[ソフトウェア定義ネットワーク インフラストラクチャを計画する](../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)します。  
  
すべての Hyper-V ホストには、Windows Server 2016 がインストールされている必要があります。  
  
## <a name="deployment-steps"></a>展開の手順  
Hyper-V ホスト (物理サーバー) Hyper-V 仮想スイッチと IP アドレスの割り当てを構成して起動します。 Hyper-V を共有またはローカルと互換性がある記憶域の種類を使用することがあります。  
### <a name="install-host-networking"></a>ネットワーク ホストをインストールします。  
1. NIC ハードウェアで利用可能な最新のネットワーク ドライバをインストールします。  
2. すべてのホストで Hyper-V の役割をインストールする (詳細については、次を参照してください。[Windows Server 2016 にインストールされた Hyper-v の概要](https://technet.microsoft.com/en-us/library/mt126159.aspx)します。   
  
   管理者特権の Windows PowerShellcommand プロンプト。  
   ``Install-WindowsFeature -Name Hyper-V -ComputerName <computer_name> -IncludeManagementTools -Restart``  
    
    します。 Hyper-V 仮想スイッチ (すべてのホストに対して同じスイッチ名を使用します作成します。 たとえば: **sdnSwitch**)。 少なくとも 1 つのネットワーク アダプターを構成または、スイッチ埋め込みチーミングを使用している場合に、少なくとも 2 つのネットワーク アダプターを構成します。 最大入力方向の展開は、2 つの Nic を使用する場合に発生します。  
 `` New-VMSwitch "<switch name>" -NetAdapterName "<NetAdapter1>" [, "<NetAdapter2>" -EnableEmbeddedTeaming $True] -AllowManagementOS $True``  
 
 >[!NOTE] 
 >管理の独立した Nic がある場合は、手順 3. および 4. をスキップできます。

3. 計画に関するトピックを参照してください ([ソフトウェア定義ネットワーク インフラストラクチャを計画する](../../sdn/plan/../../sdn/plan/../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)) と連携して、ネットワーク管理者に管理 VLAN の VLAN ID を取得します。 新しく作成した仮想スイッチの管理 vNIC を管理 VLAN にアタッチします。 お客様の環境では、VLAN タグを使用していない場合、この手順を省略できます。  
 `` Set-VMNetworkAdapterIsolation -ManagementOS -IsolationMode Vlan -DefaultIsolationID <Management VLAN> -AllowUntaggedTraffic $True``  
 
4. 計画に関するトピックを参照してください ([ソフトウェア定義ネットワーク インフラストラクチャを計画する](../../sdn/plan/../../sdn/plan/../../sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)) と DHCP のいずれかを使用して、ネットワーク管理者と静的 IP の割り当てを新しく作成された vSwitch の管理 vNIC を IP アドレスを割り当てる作業します。 次の例では、静的 IP アドレスを作成し、vSwitch の管理 vNIC に割り当てる方法を示します。  
 ``New-NetIPAddress -InterfaceAlias "vEthernet (<switch name>)" -IPAddress <IP> -DefaultGateway <Gateway IP> -AddressFamily IPv4 -PrefixLength <Length of Subnet Mask - for example: 24>``  
      
5. [オプション]Active Directory ドメイン サービスのホストにバーチャル マシンを展開 ([Active Directory Domain Services をインストール (レベル 100)](https://technet.microsoft.com/library/hh472162.aspx)と DNS サーバー。  
   
    します。 Active Directory と DNS サーバーの仮想マシンを管理 VLAN に接続します。
    
            Set-VMNetworkAdapterIsolation -VMName "<VM Name>" -Access -VlanId <Management VLAN> -AllowUntaggedTraffic $True  
   
   B します。 Active Directory ドメイン サービスと DNS をインストールします。  
      >[!NOTE]
      >ネットワーク コントローラーでは、認証に Kerberos と X.509 の両方の証明書をサポートしています。 このガイドでは、(ただし、1 つだけが必要です) にさまざまな目的の両方の認証メカニズムを使用します。  
        
6. すべての Hyper-V ホストをドメインに参加します。 ネットワークの管理ポイントで、ドメイン名を解決できる DNS サーバーに割り当てられている IP アドレスが割り当てられたネットワーク アダプターの DNS サーバーのエントリを確認します。 例えば：

        Set-DnsClientServerAddress -InterfaceAlias "vEthernet (<switch name>)" -ServerAddresses <DNS Server IP>  
   
   します。 右クリック**開始**、] をクリックして**システム**、] をクリックし、**設定を変更する**します。  
   B します。 をクリックして**変更**します。  
   C です。 をクリックして**ドメイン**し、ドメイン名を指定します。  
   D します。 をクリックして**OK**します。  
   E します。 ユーザー名とパスワードされたら、資格情報を入力します。  
   F します。 サーバーを再起動します。  
  
### <a name="validation"></a>検証  
ホストするネットワークを検証する次の手順が正しく設定を使用します。  
1. VM スイッチが正常に作成されたことを確認します。  
      
    ``Get-VMSwitch "<switch name>"``  
2. VM スイッチで管理 vNIC が管理 VLAN に接続されていることを確認します。  
    >[!NOTE]
    >管理およびテナントのトラフィックが同一の NIC を共有する場合にのみ関連    
      
    ``Get-VMNetworkAdapterIsolation -ManagementOS``  
3. 確認してすべての Hyper-V ホスト (と外部管理リソースの例: DNS サーバー) は、管理 IP アドレスまたは完全修飾ドメイン名 (FQDN) を使用して ping を使用してアクセスします。   
      
   ``ping <Hyper-V Host IP>``  
   ``ping <Hyper-V Host FQDN>``  
4. 展開のホスト上で、次のコマンドを実行し、すべてのサーバーへのアクセスを提供するを使用した Kerberos 資格情報を確認するには、各 Hyper-V ホストの FQDN を指定します。  
      
   ``winrm id -r:<Hyper-V Host FQDN>``  
      
### <a name="nano-installation-requirements-and-notes"></a>Nano インストール要件と注意事項  
Nano として、Hyper-V ホスト (物理サーバー) の展開を使用する場合は、次の追加要件で。  
1. Nano のすべてのノードでは、DSC パッケージを言語パックをインストールする必要があります。  
   
   * Microsoft-NanoServer-DSC-Package.cab  
   * Microsoft-NanoServer-DSC-Package_en-us.cab
   
        ``dism /online /add-package /packagepath:<Path> /loglevel:4``  
2. SDN Express スクリプトは、Nano 以外のホスト (Windows Server Core または GUI での Windows サーバー) から実行する必要があります。 PowerShell ワークフローは、Nano でサポートされていません。  
3.  ネットワーク コントローラーの NorthBound API を呼び出す PowerShell または NC REST ラッパー (Invoke-WebRequest と Invoke-RestMethod に依存) を使用して行う必要があります Nano 以外のホストからです。  
   
         
### <a name="run-sdn-express-scripts"></a>SDN の高速スクリプトを実行します。  
  
1.  GitHub では、インストール ファイルが存在します。 Zip ファイルをダウンロード、[Microsoft SDN GitHub リポジトリ](https://github.com/Microsoft/SDN.git)します。 Microsoft SDN リポジトリ] ページで、をクリックして**複製またはダウンロード**] をクリックし、**Download ZIP**します。  
  
2.  展開コンピューターとして 1 台のコンピューターを指定します。  このコンピューターでは、Windows Server 2016 が実行されている必要があります。 Zip ファイルとコピー] を展開、**SDNExpress**配置先のコンピューターのフォルダー`C:\`フォルダー。  
  
3.  共有、`C:\SDNExpress`フォルダーとして"**SDNExpress**"のアクセス許可を持つ**Everyone**に**読み取り/書き込み**します。  
  
4.  移動、`C:\SDNExpress`フォルダー。

 次のフォルダーが表示されます。  

|フォルダ名|説明|  
|---------------|---------------|  
|AgentConf|ネットワーク ポリシーのプログラムに各 Windows Server 2016 の Hyper-V ホスト上の SDN ホスト エージェントによって使用される OVSDB スキーマの新しいコピーを保持します。|  
|証明書|NC の証明書ファイルの一時的な共有場所。|  
|イメージ|空の次のとおり、Windows Server 2016 の vhdx イメージを配置|  
|ツール|トラブルシューティングとデバッグに関するユーティリティです。  ホストとバーチャル マシンにコピーされます。  配置するネットワーク モニターまたは Wireshark ここして必要な場合に使用できるようにすることをお勧めします。|  
|スクリプト|展開スクリプトです。<br /><br />-   **SDNExpress.ps1**<br />    展開し、ネットワーク コントローラーの仮想マシン、SLB Mux 仮想マシン、ゲートウェイ プールのプールに対応する、HNV ゲートウェイ仮想マシンなど、ファブリックを構成します。<br />-   **思われる FabricConfig.psd1**<br />    SDNExpress スクリプトの構成ファイル テンプレート。  これは、環境にカスタマイズします。<br />-   **SDNExpressTenant.ps1**<br />    負荷分散の VIP と仮想ネットワーク上のサンプル テナント ワークロードを展開します。<br />    また、以前に作成したテナントのワークロードに接続されているサービス プロバイダーのエッジ ゲートウェイで 1 つまたは複数のネットワーク接続 (IPSec S2S VPN、GRE、L3) を準備します。 IPSec および GRE ゲートウェイが接続に使用できる、対応する VIP IP アドレス、および、L3 転送ゲートウェイ経由で、対応するアドレス プール経由でします。<br />    このスクリプトは、構成を削除する、対応する元に戻すオプションを使用しても使用できます。<br />-   **TenantConfig.psd1**<br />    テナント ワークロードと S2S ゲートウェイの構成用のテンプレート構成ファイル。<br />-   **SDNExpressUndo.ps1**<br />    ファブリックの環境をクリーンアップし、開始時の状態にリセットします。<br />-   **SDNExpressEnterpriseExample.ps1**<br />    1 つのリモート アクセス ゲートウェイと (必要に応じて) 1 つの対応するエンタープライズ仮想マシン サイトごとに 1 つまたは複数のエンタープライズ サイト環境を準備します。 IPSec や GRE エンタープライズ ゲートウェイは、対応する S2S トンネルを確立するために、サービス プロバイダー ゲートウェイの VIP IP アドレスに接続します。 L3 転送ゲートウェイは、対応するピアの IP アドレスを介して接続します。 <br />            このスクリプトは、構成を削除する、対応する元に戻すオプションを使用しても使用できます。<br />-   **EnterpriseConfig.psd1**<br />    エンタープライズ サイト間ゲートウェイと VM のクライアント構成用のテンプレート構成ファイル。|  
|TenantApps|ファイルの例のテナント ワークロードを展開するために使用します。|  
  
5.  Windows Server 2016 の VHDX ファイルを確認、**イメージ**フォルダー。  
  
6. SDNExpress\scripts\FabricConfig.psd1 ファイルを変更することでカスタマイズして、**<< 置換 >>**ネットワークの計画トピックの「ホスト名、ドメイン名、ユーザー名とパスワードを含む、ラボ インフラストラクチャを合わせるネットワークの情報ネットワーク特定値を持つタグが一覧表示します。  
7. NetworkControllerRestName (FQDN) と NetworkControllerRestIP dns ホスト A レコードを作成します。  
8. ドメイン管理者の資格情報を持つユーザーとして、スクリプトを実行します。  
      
    ``SDNExpress\scripts\SDNExpress.ps1 -ConfigurationDataFile FabricConfig.psd1 -Verbose``  
      
9.  すべての操作を元に戻すには、次のコマンドを実行します。  
      
    ``SDNExpress\scripts\SDNExpressUndo.ps1 -ConfigurationDataFile FabricConfig.psd1 -Verbose``  
      
#### <a name="validation"></a>検証  
SDN Express スクリプトはすべてのエラーを報告することがなく完了するまで実行するものと仮定のファブリック リソースを正しく展開されているされ、テナント展開の適用できるようにする、次の手順を実行できます。  

- 使用[診断ツール](https://docs.microsoft.com/windows-server/networking/sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack)にエラーがない、ファブリックのリソースにネットワーク コントローラーのことを確認します。  
      
    ``Debug-NetworkControllerConfigurationState -NetworkController <FQDN of Network Controller Rest Name>``  
        
   
### <a name="deploy-a-sample-tenant-workload-with-the-software-load-balancer"></a>ソフトウェア ロード バランサーとサンプルのテナント ワークロードを展開します。  
    
ファブリックのリソースが展開されていて、これで、サンプルのテナント ワークロードを展開することにより、SDN 展開エンド ツー エンドを検証できます。 このテナント ワークロードは、次の 2 つの仮想サブネット (Web 層およびデータベース層) 分散 SDN ファイアウォールを使用してアクセス制御リスト (ACL) ルールによって保護で構成されます。 Web 層の仮想サブネットは、仮想 IP (VIP) アドレスを使用して SLB/MUX を介してアクセスすることです。 スクリプトは自動的に 2 つの Web 層のバーチャル マシンと 1 つのデータベース層のバーチャル マシンを展開し、これらの仮想サブネットに接続します。  
  
1.  SDNExpress\scripts\TenantConfig.psd1 ファイルを変更することでカスタマイズ、**<< 置換 >>**特定の値を持つタグ (例: VHD イメージ、ネットワーク コントローラー、残りの部分名、vSwitch の名前、以前と思われる FabricConfig.psd1 ファイルで定義されているなど)  
2.  スクリプトを実行します。 例えば：  
``SDNExpress\scripts\SDNExpressTenant.ps1 -ConfigurationDataFile TenantConfig.psd1 -Verbose``  
3.  構成を元に戻すには、同じスクリプトを実行、**を元に戻す**パラメーター。 例えば：  
``SDNExpress\scripts\SDNExpressTenant.ps1 -Undo -ConfigurationDataFile TenantConfig.psd1 -Verbose``  

#### <a name="validation"></a>検証  
テナントの展開が成功したことを検証するには、次の操作を行います。
1.  データベース層のバーチャル マシンにログインし、(Web 層のバーチャル マシンで Windows ファイアウォールがになってことを確認して) Web 層のバーチャル マシンの 1 つの IP アドレスに対して ping を実行します。  
2.  ネットワーク コントローラーのテナント リソースのエラーを確認します。 ネットワーク コントローラーに、レイヤー 3 の接続でのすべての Hyper-V ホストから、次を実行します。  
      
    ``Debug-NetworkControllerConfigurationState -NetworkController <FQDN of Network Controller REST Name>``
3. ロード バランサーが正しく実行されていることを確認するには、すべての Hyper-V ホストから、次を実行します。
    
        wget <VIP IP address>/unique.htm -disablekeepalive -usebasicparsing
   
   ここで`<VIP IP address>`Web 層 TenantConfig.psd1 ファイルで構成した VIP IP アドレスは、します。 検索、`VIPIP`TenantConfig.psd1 に変数がします。

   利用可能な Dip を切り替える、ロード バランサーを表示するには、この複数回実行します。 また、Web ブラウザーを使用してこの動作を確認できます。 参照`<VIP IP address>/unique.htm`します。 ブラウザーを閉じて、新しいインスタンスを開きもう一度します。 Blue 社のページとを除き、ブラウザーが、ページのキャッシュとキャッシュがタイムアウトになる前に、代替緑色のページが表示されます。