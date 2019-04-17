---
title: DNS ポリシーを使用しての地理的な場所ベースのプライマリ サーバーのトラフィック管理
description: このトピックでは、DNS ポリシー シナリオ ガイドの Windows Server 2016 の一部
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: ef9828f8-c0ad-431d-ae52-e2065532e68f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bd72e13cd3d2d7f3ca886afcdcf97e824ef227f5
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-geo-location-based-traffic-management-with-primary-servers"></a>DNS ポリシーを使用しての地理的な場所ベースのプライマリ サーバーのトラフィック管理

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックは、クライアントに提供する、最も近いリソースの IP アドレス、クライアントと、クライアントが、接続しようとするのにリソースの両方の地理的な場所に基づいて、DNS クライアント クエリに応答するのにプライマリの DNS サーバーを許可するように DNS ポリシーを構成するのに方法については、使用できます。  
  
>[!IMPORTANT]  
>このシナリオでは、のみプライマリ DNS サーバーを使用しているときに、地理的な場所ベースのトラフィック管理用の DNS ポリシーを展開する方法を示します。 プライマリとセカンダリの両方の DNS サーバーがある場合は、地理的な場所ベースのトラフィック管理を行うこともできます。 プライマリ セカンダリ展開を使っている場合、このトピックの手順を完了し、「」トピックに記載されている手順に従います[プライマリ セカンダリ展開での地理的な場所ベースのトラフィック管理用の DNS ポリシーを使用して](primary-secondary-geo-location.md)します。

新しい DNS ポリシーを使用するには、Web サーバーの IP アドレスの入力を求めるクライアント クエリに応答する DNS サーバーを許可する DNS ポリシーを作成できます。 Web サーバーのインスタンスは、物理的に異なる場所でさまざまなデータ センターに存在する可能性があります。 DNS は、クライアントと Web サーバーの場所を評価し、クライアントに提供する Web サーバーの IP アドレスに物理的に近くにあるクライアントの Web サーバーによってクライアントの要求に応答します。  

次の DNS ポリシー パラメーターを使用して、DNS クライアントからのクエリには、DNS サーバーの応答を制御することができます。 

- **クライアントのサブネット**します。 定義済みのクライアントのサブネットの名前です。 クエリの送信元となるサブネットを確認するために使用します。
- **トランスポート プロトコル**します。 トランスポート プロトコルのクエリで使用します。 可能なエントリは**UDP**と**TCP**します。
- **インターネット プロトコル**します。 クエリで使用されるネットワーク プロトコルです。 可能なエントリは**IPv4**と**IPv6**します。
- **サーバーのインターフェイスの IP アドレス**します。 DNS 要求を受信する DNS サーバーのネットワーク インターフェイスの IP アドレスです。
- **FQDN**します。 完全修飾ドメイン名 (FQDN)、クエリ内のレコードのワイルドカードを使用する可能性です。
- **クエリの種類**します。 (A、SRV、TXT など) に照会しているレコードの種類。
- **1 日の時間**します。 クエリを受信した時刻。 
  
ポリシーの式を考案するために、論理演算子 (/) は、次の条件を組み合わせることができます。 これらの式に一致するとき、次の操作のいずれかを実行するポリシーが必要です。
 
- **無視**します。 DNS サーバーは、サイレント モードでクエリを削除します。          
- **拒否**します。 DNS サーバーでは、エラー応答には、そのクエリが応答します。          
- **許可**します。 DNS サーバーは、管理トラフィックの応答の応答で応答します。          
  
##  <a name="bkmk_example"></a>地理的な場所ベースのトラフィック管理の例

DNS クエリを実行するクライアントの物理的な場所に基づいてトラフィックのリダイレクトを実現するために DNS ポリシーを使用する方法の例を次に示します。   
  
この例は、次の 2 つ架空の会社の Web とドメイン ホスティング ソリューションを提供する Contoso クラウド サービスを使用してください。Woodgrove 食品サービスは世界中で複数の市区町村の食品の配信サービスを提供し、woodgrove.com という名前の Web サイトを持ちます。  
  
Contoso クラウド サービスとは、米国内のいずれかとヨーロッパに 2 つのデータ センターです。 ヨーロッパ データ センターでは、woodgrove.com 用のポータルを順序付け食品をホストします。   
  
woodgrove.com 顧客が Web サイトから応答性の高いエクスペリエンスを取得することを確認するには、Woodgrove では、ヨーロッパ データ センターに送らヨーロッパ言語のクライアントと u. S. データ センターに送らアメリカのクライアントを希望しています。 世界中の他の場所にあるお客様は、データ センターのいずれかに送信できます。   
  
次の図は、このシナリオを示しています。  
  
![地理的な場所ベースのトラフィック管理の例](../../media/DNS-Policy-Geo1/dns_policy_geo1.png)  
  
##  <a name="bkmk_works"></a>DNS 名前解決の処理を動作します。  
  
名前解決の処理中に、ユーザーは www.woodgrove.com に接続しようとします。これにより、ユーザーのコンピューターにネットワーク接続のプロパティで構成されている DNS サーバーに送信される DNS 名前解決の要求されます。 通常、これは、リゾルバーをキャッシュとして機能する地域の ISP によって提供される DNS サーバーであり、LDNS と呼びます。   
  
DNS 名が LDNS のローカル キャッシュに存在しない場合は、LDNS サーバーは woodgrove.com に対して権限のある DNS サーバーにクエリを転送します。権威 DNS サーバーは、さらに、レコードが、ユーザーのコンピューターに送信する前にローカルでキャッシュされている LDNS サーバーに要求されたレコード (www.woodgrove.com) 応答します。  
  
Contoso クラウド サービスでは、DNS サーバーのポリシーを使用するため、地理的な位置を取得するホスト contoso.com が構成されている権限のある DNS サーバーは管理のトラフィックの応答を基づいています。 これは、結果、ヨーロッパ言語のクライアントの方向へヨーロッパ データ センターと u. S. データ センターにアメリカのクライアントの方向の図に示すようにします。  
  
このシナリオで、権威 DNS サーバーでは、LDNS サーバーおよびから、ごくまれには、ユーザーのコンピューターを近日公開名前解決の要求が通常は表示されます。 このため、権威 DNS サーバーから見た場合に、名前解決の要求の発信元 IP アドレスは、LDNS サーバーの値と、ユーザーのコンピューターです。 ただし、地理的な場所を構成するときに、LDNS サーバーの IP アドレスを使用してに基づくクエリの応答が、ユーザーの地理的な場所の公正な見積もりを提供、ユーザーが自分のローカルの ISP の DNS サーバーを照会するためです。  
  
>[!NOTE]  
>DNS のポリシーは、DNS クエリを含む UDP と TCP パケットの送信元 IP を使用します。 クエリでは、複数の競合回避モジュール/LDNS ホップを使用してプライマリ サーバーに達すると、ポリシーは DNS サーバーがクエリを受信する最後の競合回避モジュールの IP アドレスのみを検討します。  
  
##  <a name="bkmk_config"></a>地理的な場所ベースのクエリ応答の DNS ポリシーを構成する方法  
地理的な場所ベースのクエリの応答の DNS ポリシーを構成するのには、次の手順を実行する必要があります。  
  
1. [DNS クライアントのサブネットを作成します。](#bkmk_subnets)  
2. [ゾーンのスコープを作成します](#bkmk_scopes)  
3. [レコードをゾーンのスコープに追加します。](#bkmk_records)  
4. [ポリシーを作成します。](#bkmk_policies)  
  
>[!NOTE]  
>構成する場合、ゾーンの権限のある DNS サーバーでは、これらの手順を実行する必要があります。 メンバーシップ**DnsAdmins**、またはそれと同等は、次の手順を実行する必要です。  
  
次のセクションでは、詳細な構成手順を提供します。  
  
>[!IMPORTANT]  
>次のセクションでには、多くのパラメーターの値例にはが含まれている Windows PowerShell コマンド例にはが含まれます。 これらのコマンドを実行する前に、展開に適切な値を持つこれらのコマンドで値の例を置き換えることを確認します。  
  
### <a name="bkmk_subnets"></a>DNS クライアントのサブネットを作成します。  
  
最初の手順では、サブネットまたは IP アドレス空間のトラフィックをリダイレクトする領域を特定します。 たとえば、米国およびヨーロッパのトラフィックをリダイレクトする場合は、サブネットまたは IP アドレスのスペースがこれらの領域を識別する必要があります。  
  
この情報は、地理的な IP のマップから取得できます。 これらの地理的な IP のディストリビューションに基づき、「DNS クライアント サブネット」を作成する必要があります DNS クライアントのサブネットは、DNS サーバーにクエリの送信元 IPv4 または IPv6 サブネットの論理グループです。  
  
次の Windows PowerShell コマンドを使用して、DNS クライアントのサブネットを作成することができます。  
  
      
    Add-DnsServerClientSubnet -Name "USSubnet" -IPv4Subnet "192.0.0.0/24"  
      
    Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet "141.1.0.0/24"  
      
  
詳細については、次を参照してください。[追加 DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps)します。  
  
### <a name="bkmk_scopes"></a>ゾーンのスコープを作成します。  
構成後は、クライアントのサブネットは、次の 2 つの異なるゾーン スコープにリダイレクトするトラフィックの 1 つのスコープを構成している DNS クライアントのサブネットごとのゾーンのパーティションを作成する必要があります。   
  
たとえば、www.woodgrove.com DNS 名のトラフィックをリダイレクトする場合は、woodgrove.com ゾーン、米国およびヨーロッパの 2 つの異なるゾーン スコープを作成する必要があります。  
  
ゾーンのスコープは、ゾーンの一意のインスタンスです。 DNS ゾーンには、複数のゾーンのスコープ、DNS レコードの独自セットが含まれている各ゾーンのスコープを持つことができます。 同じレコードは、別の IP アドレスを持つ複数のスコープまたは同じ IP アドレスに存在することができます。  
  
>[!NOTE]  
>既定では、ゾーンのスコープは、DNS ゾーンに存在します。 このゾーンのスコープは、ゾーンと同じ名前を持つし、従来の DNS 操作は、このスコープで動作します。   
  
次の Windows PowerShell コマンドを使用すると、ゾーンのスコープを作成します。  
  
      
    Add-DnsServerZoneScope -ZoneName "woodgrove.com" -Name "USZoneScope"  
      
    Add-DnsServerZoneScope -ZoneName "woodgrove.com" -Name "EuropeZoneScope"  

詳細については、次を参照してください。[追加 DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)します。  
  
### <a name="bkmk_records"></a>レコードをゾーンのスコープに追加します。  
次の 2 つのゾーン スコープに Web サーバーのホストを表すレコードを追加する必要がありますようになりました。   
  
たとえば、**USZoneScope**と**。EuropeZoneScope**します。 Uszonescope、u. S. データ センター; にある 192.0.0.1、IP アドレスを持つレコード www.woodgrove.com に追加できます。。EuropeZoneScope ヨーロッパ データ センター内の IP アドレス 141.1.0.1 で同じレコード (www.woodgrove.com) を追加できます。   
  
次の Windows PowerShell コマンドを使用して、レコードをゾーンのスコープに追加することができます。  
  
      
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "USZoneScope  
      
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "141.1.0.1" -ZoneScope "EuropeZoneScope"  
  
  
  
この例では、世界の残りの部分ことも、2 つのデータ センターのどちらからでもアクセス、woodgrove.com Web サーバーを確認するのにゾーンの既定のスコープにレコードを追加するのに、次の Windows PowerShell コマンドを使用する必要があります。  
    
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "192.0.0.1"   
      
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "141.1.0.1"
      
 
**ゾーン範囲ゾーン**パラメーターが含まれていない、既定のスコープでレコードを追加するとします。 これは、標準の DNS ゾーンにレコードを追加すると同じです。  
  
詳細については、次を参照してください。[追加 DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)します。  
  
### <a name="bkmk_policies"></a>ポリシーを作成します。  
サブネットを作成した後は、パーティション (ゾーン スコープ) を追加したレコード、できるように、クエリの応答が、ゾーンの正しい範囲から返される DNS クライアントのサブネットのいずれかのソースからクエリする際は、サブネット、およびパーティションに接続するポリシーを作成する必要があります。 ポリシーの既定のゾーンのスコープをマッピングするため必要はありません。   
  
次の Windows PowerShell コマンドを使用して、DNS クライアントのサブネットをリンクして、ゾーンのスコープ、DNS のポリシーを作成することができます。   
  
      
    Add-DnsServerQueryResolutionPolicy -Name "USPolicy" -Action ALLOW -ClientSubnet "eq,USSubnet" -ZoneScope "USZoneScope,1" -ZoneName "woodgrove.com"  
      
    Add-DnsServerQueryResolutionPolicy -Name "EuropePolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "EuropeZoneScope,1" -ZoneName "woodgrove.com"  
     
詳細については、次を参照してください。[追加 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)します。  
  
DNS サーバーが、必要な DNS ポリシーを地理的な場所に基づいて、トラフィックをリダイレクトするよう構成されました。  
  
DNS サーバーは名前解決クエリを受け取った場合、DNS サーバーは、DNS 要求に対して構成された DNS ポリシー内のフィールドを評価します。 名前解決の要求の発信元 IP アドレスには、任意のポリシーが一致すると、関連付けられているゾーンのスコープは、クエリに応答するために使用し、それらに地理的に最も近いリソースに、ユーザーを誘導します。   
  
要件を作成できます何千もの DNS のポリシーに従って、トラフィックの管理、および DNS サーバーを再起動しなくても - 受信したクエリで、すべての新しいポリシーが動的 - 適用します。  
  
  
