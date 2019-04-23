---
title: プライマリ サーバーでの地理的な場所ベースのトラフィック管理に DNS ポリシーを使用する
description: このトピックは、DNS ポリシー シナリオ ガイドの Windows Server 2016 の一部です。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: ef9828f8-c0ad-431d-ae52-e2065532e68f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 110014adf1e23be574f23efc01e8a4d69397e547
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831983"
---
# <a name="use-dns-policy-for-geo-location-based-traffic-management-with-primary-servers"></a>プライマリ サーバーでの地理的な場所ベースのトラフィック管理に DNS ポリシーを使用する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックは、最も近いリソースの IP アドレスがクライアントに提供する、クライアントと、クライアントが接続しようとするのにリソースの両方の地理的場所に基づいて、DNS クライアント クエリに応答するのにプライマリ DNS サーバーを許可するように DNS のポリシーを構成するのに方法については、使用できます。  
  
>[!IMPORTANT]  
>このシナリオでは、のみプライマリ DNS サーバーを使用しているときに、地理的な場所ベースのトラフィック管理用の DNS のポリシーを展開する方法を示します。 プライマリとセカンダリの両方の DNS サーバーがある場合は、地理的な場所ベースのトラフィック管理を行うこともできます。 プライマリ セカンダリ展開の場合は、最初に、このトピックの手順を完了し、トピックに記載されている手順を完了し、 [のプライマリセカンダリ展開での地理的場所ベースのトラフィック管理用にDNSポリシーを使用する](primary-secondary-geo-location.md).

新しい DNS ポリシーを使用するには、DNS サーバーは、Web サーバーの IP アドレスの入力を求めるクライアントのクエリに応答できるようにする DNS ポリシーを作成することができます。 Web サーバーのインスタンスは、物理的に異なる場所でさまざまなデータ センターに存在する可能性があります。 DNS は、クライアントと Web サーバーの場所を評価し、クライアントに提供する Web サーバーの IP アドレスをクライアントに近い場所に物理的に位置している Web サーバーによって、クライアントの要求に対応します。  

次の DNS ポリシー パラメーターを使用すると、DNS クライアントからのクエリには、DNS サーバーの応答を制御します。 

- **クライアントのサブネット**します。 定義済みのクライアントのサブネットの名前です。 クエリの送信元となるサブネットを確認するために使用します。
- **トランスポート プロトコル**します。 トランスポート プロトコル クエリで使用をします。 可能なエントリは **UDP** と **TCP**します。
- **インターネット プロトコル**します。 クエリで使用されるネットワーク プロトコルです。 可能なエントリは **IPv4** と **IPv6**します。
- **サーバーのインターフェイスの IP アドレス**です。 DNS 要求を受信する DNS サーバーのネットワーク インターフェイスの IP アドレス。
- **FQDN**します。 完全修飾ドメイン名 (FQDN)、クエリ内のレコードのワイルドカードを使用する可能性です。
- **クエリの種類**します。 (A、SRV、TXT など) に照会しているレコードの型。
- **時刻**します。 クエリが受信した時刻。 
  
ポリシーの式を考案するために、論理演算子 (/) は、次の条件を組み合わせることができます。 これらの式に一致すると、ポリシーは、次の操作を実行するに必要です。
 
- **無視**します。 DNS サーバーは、サイレント モードでクエリを削除します。          
- **[拒否]**。 DNS サーバーは、そのクエリのようなエラー応答を返します。          
- **[許可]**。 DNS サーバーは、管理トラフィックの応答で応答します。          
  
##  <a name="bkmk_example"></a>地理的場所ベースのトラフィック管理の例

DNS クエリを実行するクライアントの物理的な場所に基づいてトラフィックのリダイレクトを実現するために、DNS のポリシーを使用する方法の例を次に示します。   
  
この例は架空の 2 つの会社の Contoso クラウド サービスは、web とドメイン ホスティング ソリューションを提供Woodgrove 食品サービス、世界中で複数の市区町村の食品の配信サービスを提供し、Web サイトを持つ woodgrove.com の名前します。  
  
Contoso クラウド サービスとは、米国とヨーロッパに 2 つのデータ センターです。 ヨーロッパのデータ センターでは、woodgrove.com 用のポータルを順序付け食品をホストします。   
  
Woodgrove.com お客様が企業の web サイトから応答性の高いエクスペリエンスを入手することを確認、Woodgrove では、ヨーロッパのデータ センターに送られますヨーロッパ言語のクライアントと u. s. データ センターに送られますアメリカのクライアントを希望しています。 世界中の他の場所にあるお客様は、データ センターのいずれかに送信できます。   
  
次の図は、このシナリオを示しています。  
  
![地理的な場所ベースのトラフィック管理の例](../../media/DNS-Policy-Geo1/dns_policy_geo1.png)  
  
##  <a name="bkmk_works"></a>DNS 名前解決プロセスを動作します。  
  
名前解決の処理中に、ユーザーは www.woodgrove.com に接続しようとします。 これは、結果、ユーザーのコンピューターにネットワーク接続のプロパティで構成されている DNS サーバーに送信される DNS 名前解決の要求。 通常、これはキャッシュの競合回避モジュールとして動作している地域の ISP によって提供される DNS サーバーであり、LDNS と呼びます。   
  
DNS 名が LDNS のローカル キャッシュに存在しない場合、LDNS サーバーは、woodgrove.com に対する権限を持つ DNS サーバーにクエリを転送します。 権限のある DNS サーバーは、さらに、レコードがユーザーのコンピューターに送信する前にローカルにキャッシュされている LDNS サーバーに要求されたレコード (www.woodgrove.com) で応答します。  
  
Contoso のクラウド サービスは、DNS サーバーのポリシーを使用しているためには、地理的な場所ベースの管理のトラフィックの応答を返すため contoso.com をホストしている権限のある DNS サーバーが構成されています。 これは、結果ヨーロッパ言語のクライアントの方向へヨーロッパ データ センターと u. s. データ センターにアメリカ合衆国のクライアントの通信方向の図に示すようにします。  
  
通常、権限のある DNS サーバーではこのシナリオでは、LDNS と、サーバーから、ごくまれには、ユーザーのコンピューターから送信される名前解決の要求が表示されます。 このため、権限のある DNS サーバーから見た場合に、名前解決の要求の発信元 IP アドレスは、LDNS サーバーの値と、ユーザーのコンピューターです。 ただし、LDNS サーバーの IP アドレスを使用して地理的な場所を構成するときに基づくクエリの応答は、ユーザーの地理的場所の公正な見積もりを提供、ユーザーが自分のローカルの ISP の DNS サーバーを照会するためです。  
  
>[!NOTE]  
>DNS のポリシーは、DNS クエリを含む UDP と TCP パケットの送信元 IP を使用します。 クエリでは、複数の競合回避モジュール/LDNS ホップを使用してプライマリ サーバーに達すると、ポリシーは、DNS サーバーがクエリを受信する元となる最後の競合回避モジュールの ip アドレスのみを検討します。  
  
##  <a name="bkmk_config"></a>地理的場所ベースのクエリ応答の DNS のポリシーを構成する方法  
地理的な場所ベースのクエリ応答の DNS のポリシーを構成するには、次の手順を実行する必要があります。  
  
1. [DNS クライアントのサブネットを作成します。](#bkmk_subnets)  
2. [ゾーンのスコープを作成します。](#bkmk_scopes)  
3. [レコードをゾーンのスコープに追加します。](#bkmk_records)  
4. [ポリシーを作成します。](#bkmk_policies)  
  
>[!NOTE]  
>構成する場合、ゾーンに対して権限のある DNS サーバーでは、これらの手順を実行する必要があります。 メンバーシップ **DnsAdmins**, 、または同等の権限が必要で、次の手順を実行します。  
  
次のセクションでは、詳細な構成手順を説明します。  
  
>[!IMPORTANT]  
>次のセクションでには、多くのパラメーターの値例にはが含まれている Windows PowerShell コマンド例にはが含まれます。 これらのコマンドで値の例は、これらのコマンドを実行する前に、展開に対応する値を置き換えることを確認します。  
  
### <a name="bkmk_subnets"></a>DNS クライアントのサブネットを作成します。  
  
最初の手順では、サブネットまたは IP アドレス空間のトラフィックをリダイレクトする領域を識別します。 たとえば、米国およびヨーロッパのトラフィックをリダイレクトする場合は、サブネットまたは IP アドレス空間がこれらの領域を識別する必要があります。  
  
この情報は、地理的 IP のマップから取得できます。 これらの地理的 IP のディストリビューションに基づき、「DNS クライアント サブネット」を作成する必要があります。 DNS クライアントのサブネットは、クエリが DNS サーバーに送信元 IPv4 または IPv6 サブネットの論理グループです。  
  
次の Windows PowerShell コマンドを使用すると、DNS クライアントのサブネットを作成します。  
  
      
    Add-DnsServerClientSubnet -Name "USSubnet" -IPv4Subnet "192.0.0.0/24"  
      
    Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet "141.1.0.0/24"  
      
  
詳細については、次を参照してください。 [追加 DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps)します。  
  
### <a name="bkmk_scopes"></a>ゾーンのスコープを作成します。  
クライアントのサブネットを構成した後は、2 つの異なるゾーン スコープにリダイレクトするトラフィックの 1 つのスコープに構成されている DNS クライアントのサブネットごとのゾーンをパーティション分割する必要があります。   
  
など DNS 名 www.woodgrove.com のトラフィックをリダイレクトする場合は、woodgrove.com ゾーン、米国およびヨーロッパの 2 つの別のゾーン スコープを作成する必要があります。  
  
ゾーンのスコープは、ゾーンの一意のインスタンスです。 DNS ゾーンは、独自の DNS レコード セットを格納している各ゾーンのスコープを持つ、複数のゾーン スコープを持つことができます。 同じレコードは、別の IP アドレスを持つ、複数のスコープまたは同じ IP アドレスに存在することができます。  
  
>[!NOTE]  
>既定では、ゾーンのスコープは、DNS ゾーンに存在します。 このゾーンのスコープでは、ゾーンと同じ名前に、従来の DNS の機能がこのスコープで動作します。   
  
次の Windows PowerShell コマンドを使用すると、ゾーンのスコープを作成します。  
  
      
    Add-DnsServerZoneScope -ZoneName "woodgrove.com" -Name "USZoneScope"  
      
    Add-DnsServerZoneScope -ZoneName "woodgrove.com" -Name "EuropeZoneScope"  

詳細については、次を参照してください。 [追加 DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)します。  
  
### <a name="bkmk_records"></a>レコードをゾーンのスコープに追加します。  
2 つのゾーンのスコープに web サーバーのホストを表すレコードを追加する必要があります。   
  
たとえば、 **USZoneScope** と **EuropeZoneScope**します。 USZoneScope、u. s. データ センター; にある IP アドレス、192.0.0.1 レコード www.woodgrove.com を追加することができます。EuropeZoneScope ヨーロッパ データ センターの IP アドレス 141.1.0.1 で同じレコード (www.woodgrove.com) を追加できます。   
  
次の Windows PowerShell コマンドを使用して、レコードをゾーンのスコープに追加することができます。  
  
      
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "USZoneScope  
      
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "141.1.0.1" -ZoneScope "EuropeZoneScope"  
  
  
  
この例ではアクセスできるように、世界の残りの部分も woodgrove.com web サーバーから 2 つのデータ センターのいずれかに既定のゾーンのスコープ内にレコードを追加するのに、次の Windows PowerShell コマンドを使用することも必要があります。  
    
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "192.0.0.1"   
      
    Add-DnsServerResourceRecord -ZoneName "woodgrove.com" -A -Name "www" -IPv4Address "141.1.0.1"
      
 
**ゾーン範囲ゾーン** パラメーターは、既定のスコープでレコードを追加するときに含まれません。 これは、標準の DNS ゾーンにレコードを追加すると同じです。  
  
詳細については、次を参照してください。 [追加 DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)します。  
  
### <a name="bkmk_policies"></a>ポリシーを作成します。  
サブネットを作成した後は、しパーティション (ゾーン スコープ) には、レコードを追加した、サブネット、およびパーティションに接続しているポリシーは、DNS クライアントのサブネットのいずれかのソースから、クエリの結果が、クエリの応答が、ゾーンの正しい範囲から返されます。 を作成する必要があります。 ポリシーの既定のゾーンのスコープをマッピングするため必要はありません。   
  
次の Windows PowerShell コマンドを使用すると、DNS クライアントのサブネットへのリンクとゾーン スコープに、DNS のポリシーを作成します。   
  
      
    Add-DnsServerQueryResolutionPolicy -Name "USPolicy" -Action ALLOW -ClientSubnet "eq,USSubnet" -ZoneScope "USZoneScope,1" -ZoneName "woodgrove.com"  
      
    Add-DnsServerQueryResolutionPolicy -Name "EuropePolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "EuropeZoneScope,1" -ZoneName "woodgrove.com"  
     
詳細については、次を参照してください。 [追加 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)します。  
  
DNS サーバーが、必要な DNS のポリシーに地理的な場所に基づいて、トラフィックをリダイレクトするよう構成されました。  
  
DNS サーバーは、名前解決のクエリを受信すると、DNS サーバーは、DNS 要求に対して構成された DNS ポリシー内のフィールドを評価します。 名前解決の要求の送信元 IP アドレスには、任意のポリシーが一致すると、関連付けられているゾーンのスコープは、クエリに応答するために使用し、地理的に最も近いリソースにユーザーを誘導します。   
  
何千もの DNS のポリシーに合わせて作成できます、トラフィック管理の要件、DNS サーバーを再起動しなくても - 受信したクエリで、すべての新しいポリシーが動的 - 適用されます。  
  
  
