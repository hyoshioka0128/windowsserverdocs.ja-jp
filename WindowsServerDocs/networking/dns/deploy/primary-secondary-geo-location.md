---
title: プライマリ-セカンダリの展開での地理的な場所ベースのトラフィック管理に DNS ポリシーを使用する
description: このトピックは、Windows Server 2016 の DNS ポリシーシナリオガイドに含まれています。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: a9ee7a56-f062-474f-a61c-9387ff260929
ms.author: lizross
author: eross-msft
ms.openlocfilehash: f9bc1a35016ca5946eddeada2088a83f1fa8ca05
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80317751"
---
# <a name="use-dns-policy-for-geo-location-based-traffic-management-with-primary-secondary-deployments"></a>プライマリ-セカンダリの展開での地理的な場所ベースのトラフィック管理に DNS ポリシーを使用する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、プライマリとセカンダリの両方の DNS サーバーが、DNS の展開に含まれている場合は、地理的な場所ベースのトラフィック管理用の DNS ポリシーを作成するのに方法について説明します。  

前のシナリオでは、プライマリサーバーでの地理的な場所[ベースのトラフィック管理に Dns ポリシーを使用](primary-geo-location.md)します。これは、プライマリ dns サーバーで地理的な場所ベースのトラフィック管理用の dns ポリシーを構成するための手順を示しています。 インターネット インフラストラクチャにただし、DNS サーバーは広く導入されているモデルでは、プライマリ セカンダリ、場所を選択し、セキュリティで保護されたプライマリ サーバーでゾーンの書き込み可能なコピーが格納されているし、ゾーンの読み取り専用のコピーが複数のセカンダリ サーバーに保存します。   
  
セカンダリ サーバーは、要求およびプライマリ DNS サーバー上のゾーンへの新しい変更を含むゾーンの更新を受信する権限を持つ転送 (AXFR) と増分ゾーン転送 (IXFR) は、ゾーン転送のプロトコルを使用します。   
  
> [!NOTE]
> AXFR に関する詳細については、インターネット技術標準化委員会 (IETF) を参照してください。 [コメント 5936 要求](https://tools.ietf.org/rfc/rfc5936.txt)します。 IXFR に関する詳細については、インターネット技術標準化委員会 (IETF) を参照してください。 [コメント 1995 の要求](https://tools.ietf.org/html/rfc1995)します。  
  
## <a name="primary-secondary-geo-location-based-traffic-management-example"></a>プライマリ セカンダリ地理的な場所ベースのトラフィック管理の例  
DNS クエリを実行するクライアントの物理的な場所に基づいてトラフィックのリダイレクトを実現するために、プライマリ セカンダリ配置で DNS のポリシーを使用する方法の例を次に示します。  
  
この例は架空の 2 つの会社の Contoso クラウド サービスは、web とドメイン ホスティング ソリューションを提供Woodgrove 食品サービス、世界中で複数の市区町村の食品の配信サービスを提供し、Web サイトを持つ woodgrove.com の名前します。  
  
Woodgrove.com お客様が企業の web サイトから応答性の高いエクスペリエンスを入手することを確認、Woodgrove では、ヨーロッパのデータ センターに送られますヨーロッパ言語のクライアントと u. s. データ センターに送られますアメリカのクライアントを希望しています。 世界中の他の場所にあるお客様は、データ センターのいずれかに送信できます。  
  
Contoso クラウド サービスとは、米国とヨーロッパ、Contoso が woodgrove.com 用のポータルを順序付け、食品をホストするのに 2 つのデータ センターです。  
  
Contoso の DNS の展開には、2 つのセカンダリ サーバーが含まれています: **SecondaryServer1**, 、10.0.0.2; IP アドレスを持つと **SecondaryServer2**, を IP アドレス 10.0.0.3 します。 これらのセカンダリ サーバーは、2 つの異なるリージョン内のネーム サーバーとして、ヨーロッパと米国 SecondaryServer2 SecondaryServer1 で動作しています。
  
プライマリの書き込み可能なゾーンのコピーがある **PrimaryServer** (IP アドレス 10.0.0.1) ゾーンの変更が行われる場所です。 セカンダリ サーバーへの転送を正規のゾーン、セカンダリ サーバーも、PrimaryServer のゾーンに新しいデータを最新されます。
  
次の図は、このシナリオを示しています。
  
![プライマリ セカンダリ地理的な場所ベースのトラフィック管理の例](../../media/Dns-Policy_PS1/dns_policy_primarysecondary1.jpg)  
   
## <a name="how-the-dns-primary-secondary-system-works"></a>DNS のプライマリ セカンダリ システムの動作

プライマリ-セカンダリ DNS 展開での地理的な場所ベースのトラフィック管理を展開するときに、ゾーン転送をスコープ レベルについて学習する前に転送を行う方法の通常のプライマリ セカンダリ ゾーンを理解する必要があります。 次のセクションでは、ゾーンとゾーン転送をスコープ レベルについてを説明します。  
  
- [DNS プライマリセカンダリ展開でのゾーン転送](#zone-transfers-in-a-dns-primary-secondary-deployment)  
- [DNS プライマリセカンダリ展開でのゾーンスコープレベルの転送](#zone-scope-level-transfers-in-a-dns-primary-secondary-deployment)  
  
### <a name="zone-transfers-in-a-dns-primary-secondary-deployment"></a>プライマリ-セカンダリの DNS 展開でゾーン転送

DNS プライマリ セカンダリ展開を作成して、次の手順でゾーンを同期することができます。  
1. DNS をインストールするときにプライマリ DNS サーバーにプライマリ ゾーンを作成します。  
2. セカンダリ サーバーでゾーンを作成し、プライマリ サーバーを指定します。   
3. プライマリ サーバーでは、プライマリ ゾーンの信頼されているセカンダリとしてセカンダリ サーバーを追加できます。   
4. セカンダリ ゾーンは、ゾーンの完全転送要求 (AXFR) を行い、ゾーンのコピーを受信します。   
5. 必要な場合、プライマリ サーバーはゾーンの更新はセカンダリ サーバーに通知を送信します。  
6. セカンダリ サーバーでは、増分ゾーン転送要求 (IXFR) を作成します。 このため、セカンダリ サーバーは、プライマリ サーバーと同期を保ちます。   
  
### <a name="zone-scope-level-transfers-in-a-dns-primary-secondary-deployment"></a>スコープ レベルのゾーンを DNS プライマリ セカンダリ配置の転送します。

トラフィック管理のシナリオでは、別のゾーンのスコープのゾーンに分割する追加の手順が必要です。 このため、追加の手順は、セカンダリ サーバーにゾーンのスコープ内のデータを転送し、ポリシーおよび DNS クライアントのサブネットのセカンダリ サーバーに転送する必要があります。   
  
プライマリおよびセカンダリ サーバーで、DNS インフラストラクチャを構成した後、次の手順を使用して、DNS によって、ゾーン転送をスコープ レベルが自動的に実行されます。  
  
スコープ レベルのゾーン転送を確実には、DNS サーバーは、DNS (EDNS0) 選択 RR の拡張メカニズムを使用します。 スコープを持つゾーンからのすべてのゾーン転送 (AXFR または IXFR) 要求から始まったもので、EDNS0 OPT RR、ID を持つオプションは既定で「65433」に設定します。 EDNSO の詳細については、IETF を参照してください。 [コメント 6891 要求](https://tools.ietf.org/html/rfc6891)します。  
  
OPT RR の値は、要求が送信されるゾーンのスコープの名前です。 プライマリの DNS サーバーは、信頼されたセカンダリ サーバーからこのパケットを受信したときに、そのゾーンの範囲内にあると、要求を解釈します。   
  
プライマリ サーバーがそのゾーンのスコープを持つ場合、スコープからデータを転送 (xfr を発売) で応答します。 応答には、オプションと同じ id「65433」RR を選択し、値が同じゾーンのスコープに設定が含まれています。 セカンダリ サーバーは、この応答を受信して、応答からスコープ情報を取得して、ゾーンの特定のスコープを更新します。  
  
このプロセスの後は、プライマリ サーバーは、このようなゾーン スコープ要求の通知が送信される信頼されたセカンダリの一覧を保持します。   
  
ゾーンのスコープでさらに、更新プログラムは、同じ OPT RR で、セカンダリ サーバーへ IXFR 通知が送信されます。 通知を受けるゾーンのスコープは、その選択 RR を含む IXFR request と同じように上記で説明した次のとおりです。  
  
## <a name="how-to-configure-dns-policy-for-primary-secondary-geo-location-based-traffic-management"></a>プライマリ-セカンダリの地理的な場所ベースのトラフィック管理用の DNS のポリシーを構成する方法

開始する前に、すべてのトピックの手順を完了したことを確認 [のプライマリ サーバーの地理的な場所ベースのトラフィック管理用の DNS ポリシーを使用して](../../dns/deploy/Scenario--Use-DNS-Policy-for-Geo-Location-Based-Traffic-Management-with-Primary-Servers.md), 、ゾーン、ゾーンのスコープ、DNS クライアントのサブネット、および DNS のポリシーで、プライマリ DNS サーバーが構成されているとします。  
  
> [!NOTE]
> DNS のプライマリ サーバーからセカンダリの DNS サーバーに DNS クライアントのサブネット、ゾーンのスコープ、および DNS のポリシーをコピーするは、このトピックの手順は、最初の DNS 設定と検証です。 今後、DNS クライアントのサブネット、ゾーンのスコープ、およびプライマリ サーバー上のポリシー設定を変更することができます。 このような状況では、セカンダリ サーバーをプライマリ サーバーと同期を保つために自動化スクリプトを作成できます。  
  
プライマリ-セカンダリの地理的な場所ベースのクエリ応答の DNS のポリシーを構成するには、次の手順を実行する必要があります。  
  
- [セカンダリゾーンを作成する](#create-the-secondary-zones)  
- [プライマリゾーンのゾーン転送設定を構成する](#configure-the-zone-transfer-settings-on-the-primary-zone)  
- [DNS クライアントのサブネットをコピーする](#copy-the-dns-client-subnets)  
- [セカンダリサーバーでゾーンのスコープを作成する](#create-the-zone-scopes-on-the-secondary-server)  
- [DNS ポリシーの構成](#configure-dns-policy)  
  
次のセクションでは、詳細な構成手順を説明します。  
  
> [!IMPORTANT]
> 以下のセクションには、多くのパラメーターの値の例を含む Windows PowerShell コマンドの例が含まれています。 これらのコマンドで値の例は、これらのコマンドを実行する前に、展開に対応する値を置き換えることを確認します。  
> 
> メンバーシップ **DnsAdmins**, 、または同等の権限が必要で、次の手順を実行します。  
  
### <a name="create-the-secondary-zones"></a>セカンダリ ゾーンを作成します。

SecondaryServer1 と SecondaryServer2 にレプリケートするゾーンのセカンダリ コピーを作成することができます (コマンドレットと仮定して実行されているリモートから 1 つの管理クライアントから)。   
  
たとえば、SecondaryServer1 および SecondarySesrver2 www.woodgrove.com のセカンダリ コピーを作成できます。  
  
次の Windows PowerShell コマンドを使用すると、セカンダリ ゾーンを作成します。  
  
    
    Add-DnsServerSecondaryZone -Name "woodgrove.com" -ZoneFile "woodgrove.com.dns" -MasterServers 10.0.0.1 -ComputerName SecondaryServer1  
      
    Add-DnsServerSecondaryZone -Name "woodgrove.com" -ZoneFile "woodgrove.com.dns" -MasterServers 10.0.0.1 -ComputerName SecondaryServer2  
      

詳細については、次を参照してください。 [追加 DnsServerSecondaryZone](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserversecondaryzone?view=win10-ps)します。  
  
### <a name="configure-the-zone-transfer-settings-on-the-primary-zone"></a>プライマリ ゾーンのゾーン転送設定を構成します。

プライマリ ゾーンの設定を構成する必要がありますようにします。

1. プライマリ サーバーから、指定したセカンダリ サーバーへのゾーン転送が許可されています。  
2. ゾーンの更新通知は、セカンダリ サーバーに、プライマリ サーバーによって送信されます。  
  
次の Windows PowerShell コマンドを使用して、プライマリ ゾーンのゾーン転送設定を構成することができます。
  
> [!NOTE]
> 次の例のコマンドをパラメーターで **-通知** プライマリ サーバーから更新プログラムに関する通知をセカンダリの選択リストに送信されるかを指定します。  
  
    
    Set-DnsServerPrimaryZone -Name "woodgrove.com" -Notify Notify -SecondaryServers "10.0.0.2,10.0.0.3" -SecureSecondaries TransferToSecureServers -ComputerName PrimaryServer  
     
  
詳細については、次を参照してください。 [セット デモンストレーション](https://docs.microsoft.com/powershell/module/dnsserver/set-dnsserverprimaryzone?view=win10-ps)します。  
  
  
### <a name="copy-the-dns-client-subnets"></a>DNS クライアントのサブネットをコピーします。

セカンダリ サーバーには、プライマリ サーバーから DNS クライアントのサブネットをコピーする必要があります。
  
次の Windows PowerShell コマンドを使用すると、サブネットをセカンダリ サーバーにコピーします。
  
    
    Get-DnsServerClientSubnet -ComputerName PrimaryServer | Add-DnsServerClientSubnet -ComputerName SecondaryServer1  
      
    Get-DnsServerClientSubnet -ComputerName PrimaryServer | Add-DnsServerClientSubnet -ComputerName SecondaryServer2  
      

詳細については、次を参照してください。 [追加 DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps)します。  
  
### <a name="create-the-zone-scopes-on-the-secondary-server"></a>セカンダリ サーバーでゾーンのスコープを作成します。

セカンダリ サーバーでは、ゾーンのスコープを作成する必要があります。 DNS では、ゾーンのスコープによって、プライマリサーバーからの XFRs の要求も開始されます。 プライマリ サーバー上のゾーンのスコープの変更、ゾーンのスコープ情報を含む通知はセカンダリ サーバーに送信されます。 セカンダリ サーバーは、増分の変更で、ゾーンのスコープを更新できます。  
  
次の Windows PowerShell コマンドを使用すると、セカンダリ サーバーでゾーンのスコープを作成します。  
  
    
    Get-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName PrimaryServer|Add-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName SecondaryServer1 -ErrorAction Ignore  
      
    Get-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName PrimaryServer|Add-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName SecondaryServer2 -ErrorAction Ignore  
  

> [!NOTE]
> これらの例のコマンドで、 **-erroraction を無視する** すべてのゾーンに既定のゾーンのスコープが存在するために、パラメーターが含まれています。 既定のゾーンのスコープを作成または削除することはできません。 そのスコープを作成するためのパイプライン処理が発生しは失敗します。 また、2 つのセカンダリ ゾーンの既定以外のゾーンのスコープを作成できます。  
  
詳細については、次を参照してください。 [追加 DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)します。  
  
### <a name="configure-dns-policy"></a>DNS のポリシーを構成します。

サブネットを作成した後は、しパーティション (ゾーン スコープ) には、レコードを追加した、サブネット、およびパーティションに接続しているポリシーは、DNS クライアントのサブネットのいずれかのソースから、クエリの結果が、クエリの応答が、ゾーンの正しい範囲から返されます。 を作成する必要があります。 ポリシーの既定のゾーンのスコープをマッピングするため必要はありません。  
  
次の Windows PowerShell コマンドを使用すると、DNS クライアントのサブネットへのリンクとゾーン スコープに、DNS のポリシーを作成します。   
    
    $policy = Get-DnsServerQueryResolutionPolicy -ZoneName "woodgrove.com" -ComputerName PrimaryServer  
      
    $policy | Add-DnsServerQueryResolutionPolicy -ZoneName "woodgrove.com" -ComputerName SecondaryServer1  
      
    $policy | Add-DnsServerQueryResolutionPolicy -ZoneName "woodgrove.com" -ComputerName SecondaryServer2  
      

詳細については、次を参照してください。 [追加 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)します。  
  
今すぐセカンダリ DNS サーバーは、地理的な場所に基づいて、トラフィックをリダイレクトする必要な DNS ポリシーで構成されます。  
  
DNS サーバーは、名前解決のクエリを受信すると、DNS サーバーは、DNS 要求に対して構成された DNS ポリシー内のフィールドを評価します。 名前解決の要求の送信元 IP アドレスには、任意のポリシーが一致すると、関連付けられているゾーンのスコープは、クエリに応答するために使用し、地理的に最も近いリソースにユーザーを誘導します。   
  
何千もの DNS のポリシーに合わせて作成できます、トラフィック管理の要件、DNS サーバーを再起動しなくても - 受信したクエリで、すべての新しいポリシーが動的 - 適用されます。
