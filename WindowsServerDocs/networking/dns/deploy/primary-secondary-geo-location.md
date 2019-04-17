---
title: 地理的な場所ベースのプライマリ セカンダリ展開でのトラフィック管理に DNS ポリシーを使用します。
description: このトピックでは、DNS ポリシー シナリオ ガイドの Windows Server 2016 の一部
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: a9ee7a56-f062-474f-a61c-9387ff260929
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4c78a0198e29fb59f30fd8ad776c7f200312d014
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-geo-location-based-traffic-management-with-primary-secondary-deployments"></a>地理的な場所ベースのプライマリ セカンダリ展開でのトラフィック管理に DNS ポリシーを使用します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、プライマリとセカンダリの両方の DNS サーバーが、DNS の展開に含まれている場合は、地理的な場所ベースのトラフィック管理用の DNS ポリシーを作成するのに方法について説明します。  

前のシナリオでは、[地理的な場所ベースのトラフィック管理のプライマリ サーバーの DNS ポリシーを使用して](primary-geo-location.md)、プライマリ DNS サーバーの地理的な場所ベースのトラフィック管理用の DNS ポリシーを構成するための指示を提供します。 インターネット インフラストラクチャにただし、DNS サーバーは広く展開モデルでは、プライマリ セカンダリ、場所を選択し、セキュリティで保護されたプライマリ サーバーでゾーンの書き込み可能なコピーが格納されているし、ゾーンの読み取り専用のコピーが複数のセカンダリ サーバーに保存されます。   
  
セカンダリ サーバーを要求して、プライマリ DNS サーバー上のゾーンへの新しい変更を含むゾーンの更新プログラムを受信する権限を持つ転送 (AXFR) と増分ゾーン転送 (IXFR) は、ゾーン転送のプロトコルを使用します。   
  
>[!NOTE]
>AXFR に関する詳細については、インターネット技術標準化委員会 (IETF) を参照してください。[コメント 5936 要求](https://tools.ietf.org/rfc/rfc5936.txt)します。 IXFR に関する詳細については、インターネット技術標準化委員会 (IETF) を参照してください。[コメント 1995 の要求](https://tools.ietf.org/html/rfc1995)します。  
  
## <a name="bkmk_example"></a>プライマリ-セカンダリの地理的な場所ベースのトラフィック管理の例  
DNS クエリを実行するクライアントの物理的な場所に基づいてトラフィックのリダイレクトを実現するために、プライマリ セカンダリ配置で DNS のポリシーを使用する方法の例を次に示します。  
  
この例は、次の 2 つ架空の会社の Web とドメイン ホスティング ソリューションを提供する Contoso クラウド サービスを使用してください。Woodgrove 食品サービスは世界中で複数の市区町村の食品の配信サービスを提供し、woodgrove.com という名前の Web サイトを持ちます。  
  
woodgrove.com 顧客が Web サイトから応答性の高いエクスペリエンスを取得することを確認するには、Woodgrove では、ヨーロッパ データ センターに送らヨーロッパ言語のクライアントと u. S. データ センターに送らアメリカのクライアントを希望しています。 世界中の他の場所にあるお客様は、データ センターのいずれかに送信できます。  
  
Contoso クラウド サービスとは、2 つのデータ センター、ヨーロッパ、Contoso が woodgrove.com 用のポータルを順序付け、食品をホストして、米国内のいずれかです。  
  
Contoso の DNS 展開にはで 2 つのセカンダリ サーバーが含まれています: **SecondaryServer1**、10.0.0.2; IP アドレスを持つ**SecondaryServer2**、10.0.0.3 IP アドレスを使用します。 これらのセカンダリ サーバーは、次の 2 つのさまざまな地域内のネーム サーバーとして、ヨーロッパと米国 SecondaryServer2 SecondaryServer1 で動作しています。
  
プライマリの書き込み可能なゾーンのコピーがある**PrimaryServer** (IP アドレス 10.0.0.1) ゾーンの変更が行われる場所です。 セカンダリ サーバーへの転送を正規のゾーン、セカンダリ サーバーも、PrimaryServer のゾーンに新しい変更で最新の状態されます。
  
次の図は、このシナリオを示しています。
  
![プライマリ-セカンダリの地理的な場所ベースのトラフィック管理の例](../../media/Dns-Policy_PS1/dns_policy_primarysecondary1.jpg)  
   
## <a name="bkmk_works"></a>DNS プライマリ セカンダリ システムの動作方法

プライマリ-セカンダリ DNS 展開での地理的な場所ベースのトラフィック管理を展開するときに、ゾーン転送をスコープ レベルについて学習する前に転送を行う方法の通常のプライマリ セカンダリ ゾーンを理解する必要があります。 次のセクションでは、ゾーンとゾーン転送をスコープ レベルの情報を提供します。  
  
- [DNS プライマリ セカンダリ展開でゾーン転送](#bkmk_zone)  
- [ゾーン転送をスコープ レベルで DNS プライマリ セカンダリ展開](#bkmk_scope)  
  
### <a name="bkmk_zone"></a>DNS プライマリ セカンダリ展開でゾーン転送

DNS プライマリ セカンダリ展開を作成し、次の手順でゾーンを同期できます。  
1. DNS をインストールするときにプライマリ DNS サーバーにプライマリ ゾーンを作成します。  
2. セカンダリ サーバーで、ゾーンを作成し、プライマリ サーバーを指定します。   
3. プライマリ サーバーで、プライマリ ゾーンの信頼されているセカンダリとしてセカンダリ サーバーを追加できます。   
4. セカンダリ ゾーンは、ゾーンの完全転送要求 (AXFR) を行い、ゾーンのコピーを受信します。   
5. 必要な場合、プライマリ サーバーはゾーンの更新はセカンダリ サーバーに通知を送信します。  
6. セカンダリ サーバーは、増分ゾーン転送要求 (IXFR) を作成します。 このため、セカンダリ サーバーは、プライマリ サーバーと同期を保ちます。   
  
### <a name="bkmk_scope"></a>ゾーン転送をスコープ レベルで DNS プライマリ セカンダリ展開

トラフィック管理のシナリオでは、ゾーン別のゾーン スコープに分割する追加の手順が必要です。 このため、追加の手順は、セカンダリ サーバーにゾーンのスコープ内のデータを転送し、ポリシーおよび DNS クライアントのサブネットをセカンダリ サーバーに転送する必要です。   
  
プライマリおよびセカンダリ サーバーで、DNS インフラストラクチャを構成した後、次の手順を使用して、DNS によって、ゾーン転送をスコープ レベルが自動的に実行されます。  
  
スコープ レベルのゾーン転送を確実には、DNS サーバーは DNS (EDNS0) 選択 RR の拡張メカニズムを使用します。 スコープを持つゾーンからのすべてのゾーン転送 (AXFR または IXFR) 要求は、EDNS0 OPT RR、ID を持つオプションは既定で「65433」に設定で発生します。 EDNSO の詳細については、IETF を参照してください。[コメント 6891 要求](https://tools.ietf.org/html/rfc6891)します。  
  
OPT RR の値は、要求が送信されているゾーンのスコープの名前です。 プライマリ DNS サーバーは、信頼されたセカンダリ サーバーからこのパケットを受信するときに、そのゾーンのスコープ用と、要求を解釈します。   
  
プライマリ サーバーがそのゾーンのスコープを持つ場合そのスコープからデータを転送 (xfr を発売) で応答します。 応答には、RR オプションと同じ ID「65433」を選択し、、値が同じゾーン スコープ設定が含まれていますいます。 セカンダリ サーバーは、この応答を受信するには、応答からスコープ情報を取得および特定のゾーンのスコープを更新します。  
  
このプロセスの後は、プライマリ サーバーは、このようなゾーン スコープ要求の通知が送信される信頼されたセカンダリの一覧を保持します。   
  
ゾーンのスコープでさらに、更新プログラムは、同じ OPT RR で、セカンダリ サーバーへ IXFR 通知が送信されます。 通知を受けるゾーンのスコープは、その選択 RR を含む IXFR request と同じように上記で説明した次のとおりです。  
  
## <a name="bkmk_config"></a>プライマリ-セカンダリの地理的な場所ベースのトラフィック管理用の DNS のポリシーを構成する方法

開始する前に、すべてのトピックの手順を完了したことを確認[地理的な場所ベースのトラフィック管理のプライマリ サーバーの DNS ポリシーを使用して](../../dns/deploy/Scenario--Use-DNS-Policy-for-Geo-Location-Based-Traffic-Management-with-Primary-Servers.md)、プライマリ DNS サーバーがゾーン、ゾーンのスコープ、DNS クライアントのサブネット、および DNS のポリシーで構成されているとします。  
  
>[!NOTE]
> このトピックの「DNS のプライマリ サーバーからセカンダリの DNS サーバーに DNS クライアントのサブネット ゾーンのスコープ、および DNS のポリシーをコピーする手順については、最初の DNS 設定と検証です。 今後の DNS クライアントのサブネット、ゾーンのスコープ、およびプライマリ サーバー上のポリシー設定を変更する可能性があります。 この状況では、プライマリ サーバーと同期セカンダリ サーバーに保つために自動化スクリプトを作成できます。  
  
プライマリ-セカンダリの地理的な場所ベースのクエリ応答の DNS のポリシーを構成するのには、次の手順を実行する必要があります。  
  
- [セカンダリ ゾーンを作成します。](#bkmk_secondary)  
- [プライマリ ゾーンのゾーン転送設定を構成します。](#bkmk_zonexfer)  
- [DNS クライアントのサブネットをコピーします。](#bkmk_client)  
- [セカンダリ サーバーでゾーンのスコープを作成します。](#bkmk_zonescopes)  
- [DNS のポリシーを構成します。](#bkmk_dnspolicy)  
  
次のセクションでは、詳細な構成手順を提供します。  
  
>[!IMPORTANT]
>次のセクションでには、多くのパラメーターの値例にはが含まれている Windows PowerShell コマンド例にはが含まれます。 これらのコマンドを実行する前に、展開に適切な値を持つこれらのコマンドで値の例を置き換えることを確認します。  
><br>メンバーシップ**DnsAdmins**、またはそれと同等は、次の手順を実行する必要です。  
  
### <a name="bkmk_secondary"></a>セカンダリ ゾーンを作成します。

SecondaryServer1 と SecondaryServer2 にレプリケートするゾーンのセカンダリ コピーを作成することができます (コマンドレットと仮定して実行されているリモート 1 つの管理クライアントから)。   
  
たとえば、SecondaryServer1 および SecondarySesrver2 www.woodgrove.com のセカンダリ コピーを作成することができます。  
  
次の Windows PowerShell コマンドを使用して、セカンダリ ゾーンを作成することができます。  
  
    
    Add-DnsServerSecondaryZone -Name "woodgrove.com" -ZoneFile "woodgrove.com.dns" -MasterServers 10.0.0.1 -ComputerName SecondaryServer1  
      
    Add-DnsServerSecondaryZone -Name "woodgrove.com" -ZoneFile "woodgrove.com.dns" -MasterServers 10.0.0.1 -ComputerName SecondaryServer2  
      

詳細については、次を参照してください。[追加 DnsServerSecondaryZone](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserversecondaryzone?view=win10-ps)します。  
  
### <a name="bkmk_zonexfer"></a>プライマリ ゾーンのゾーン転送設定を構成します。

プライマリ ゾーンの設定を構成する必要がありますようにします。

1. 指定されたセカンダリ サーバーにプライマリ サーバーからゾーン転送が許可されます。  
2. ゾーンの更新通知は、プライマリ サーバーで、セカンダリ サーバーに送信されます。  
  
次の Windows PowerShell コマンドを使用して、プライマリ ゾーンのゾーン転送設定を構成することができます。
  
>[!NOTE]
>次の例のコマンドでパラメーター **-通知**プライマリ サーバーがセカンダリの選択のリストを更新プログラムに関する通知を送信するように指定します。  
  
    
    Set-DnsServerPrimaryZone -Name "woodgrove.com" -Notify Notify -SecondaryServers "10.0.0.2,10.0.0.3" -SecureSecondaries TransferToSecureServers -ComputerName PrimaryServer  
     
  
詳細については、次を参照してください。[セット デモンストレーション](https://https://docs.microsoft.com/powershell/module/dnsserver/set-dnsserverprimaryzone?view=win10-ps)します。  
  
  
### <a name="bkmk_client"></a>DNS クライアントのサブネットをコピーします。

セカンダリ サーバーにプライマリ サーバーから DNS クライアントのサブネットをコピーする必要があります。
  
次の Windows PowerShell コマンドを使用して、サブネットをセカンダリ サーバーにコピーすることができます。
  
    
    Get-DnsServerClientSubnet -ComputerName PrimaryServer | Add-DnsServerClientSubnet -ComputerName SecondaryServer1  
      
    Get-DnsServerClientSubnet -ComputerName PrimaryServer | Add-DnsServerClientSubnet -ComputerName SecondaryServer2  
      

詳細については、次を参照してください。[追加 DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps)します。  
  
### <a name="bkmk_zonescopes"></a>セカンダリ サーバーでゾーンのスコープを作成します。

セカンダリ サーバーでゾーンのスコープを作成する必要があります。 DNS では、ゾーンのスコープを開始も xfr 可能をプライマリ サーバーから要求します。 プライマリ サーバーでゾーンのスコープの変更、ゾーンのスコープ情報を含む通知は、セカンダリ サーバーに送信されます。 セカンダリ サーバーは、増分の変更で、ゾーンのスコープを更新できます。  
  
次の Windows PowerShell コマンドを使用して、セカンダリ サーバーでゾーンのスコープを作成することができます。  
  
    
    Get-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName PrimaryServer|Add-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName SecondaryServer1 -ErrorAction Ignore  
      
    Get-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName PrimaryServer|Add-DnsServerZoneScope -ZoneName "woodgrove.com" -ComputerName SecondaryServer2 -ErrorAction Ignore  
  

>[!NOTE]
>これらの例のコマンドで、**-erroraction を無視する**すべてのゾーンに既定のゾーンのスコープが存在するためにパラメーターが含まれています。 ゾーンの既定のスコープを作成または削除することはできません。 パイプライン処理と、そのスコープを作成しようとしは失敗します。 または、2 つのセカンダリ ゾーンの既定以外のゾーンのスコープを作成することができます。  
  
詳細については、次を参照してください。[追加 DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)します。  
  
### <a name="bkmk_dnspolicy"></a>DNS のポリシーを構成します。

サブネットを作成した後は、パーティション (ゾーン スコープ) を追加したレコード、できるように、クエリの応答が、ゾーンの正しい範囲から返される DNS クライアントのサブネットのいずれかのソースからクエリする際は、サブネット、およびパーティションに接続するポリシーを作成する必要があります。 ポリシーの既定のゾーンのスコープをマッピングするため必要はありません。  
  
次の Windows PowerShell コマンドを使用して、DNS クライアントのサブネットをリンクして、ゾーンのスコープ、DNS のポリシーを作成することができます。   
    
    $policy = Get-DnsServerQueryResolutionPolicy -ZoneName "woodgrove.com" -ComputerName PrimaryServer  
      
    $policy | Add-DnsServerQueryResolutionPolicy -ZoneName "woodgrove.com" -ComputerName SecondaryServer1  
      
    $policy | Add-DnsServerQueryResolutionPolicy -ZoneName "woodgrove.com" -ComputerName SecondaryServer2  
      

詳細については、次を参照してください。[追加 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)します。  
  
今すぐセカンダリ DNS サーバーは、地理的な場所に基づいてトラフィックをリダイレクトする必要な DNS ポリシーで構成されます。  
  
DNS サーバーは名前解決クエリを受け取った場合、DNS サーバーは、DNS 要求に対して構成された DNS ポリシー内のフィールドを評価します。 名前解決の要求の発信元 IP アドレスには、任意のポリシーが一致すると、関連付けられているゾーンのスコープは、クエリに応答するために使用し、それらに地理的に最も近いリソースに、ユーザーを誘導します。   
  
要件を作成できます何千もの DNS のポリシーに従って、トラフィックの管理、および DNS サーバーを再起動しなくても - 受信したクエリで、すべての新しいポリシーが動的 - 適用します。
