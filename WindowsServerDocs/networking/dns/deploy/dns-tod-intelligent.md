---
title: 1 日の時間に基づくインテリジェント DNS 応答の DNS ポリシーを使用します。
description: このトピックでは、DNS ポリシー シナリオ ガイドの Windows Server 2016 の一部
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 161446ff-a072-4cc4-b339-00a04857ff3a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 46821daff4a0046bf78d7f56dc7c5deabcc437e4
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-intelligent-dns-responses-based-on-the-time-of-day"></a>1 日の時間に基づくインテリジェント DNS 応答の DNS ポリシーを使用します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、アプリケーションの別の地理的に分散インスタンス間で 1 日の時間に基づく DNS ポリシーを使用してアプリケーションのトラフィックを分散するのに方法について説明します。  
  
このシナリオは、別のタイム ゾーンに格納されている Web サーバーなどの別のアプリケーション サーバーを 1 つのタイム ゾーンでトラフィックを送信する場合に便利です。 これにより、トラフィックの負荷分散アプリケーションのインスタンス間でのピーク時にトラフィックがプライマリ サーバーが、いつ過負荷の期間します。   
  
### <a name="bkmk_example1"></a>1 日の時間に基づくインテリジェント DNS 応答の例  
1 日の時間に基づくアプリケーションのトラフィックを分散する DNS ポリシーを使用する方法の例を次に示します。  
  
この例では、1 つ架空の会社の Web サイト、contosogiftservices.com を通じて、世界各地でオンライン gifting ソリューションを提供する Contoso ギフト サービスを使用します。   
  
contosogiftservices.com Web サイトは、次の 2 つのデータ センター、シアトル (北米のみ) の 1 つとダブリン (ヨーロッパ) でホストされます。 地理的な場所に DNS ポリシーを使用して対応応答を送信するため、DNS サーバーが構成されます。 ビジネスで最近急増したとき、contosogiftservices.com が訪問者の数を増やす、毎日とサービスの可用性に関する問題を報告した顧客の一部です。  
  
Contoso ギフト サービスは、サイトの分析を実行し、毎日午後 6 時と午後 9 時のローカル時刻との間が急増したとき、Web サーバーへのトラフィックを検出します。 Web サーバーを顧客にサービス拒否攻撃の結果として、これらのピーク時に増加したトラフィックを処理するスケールことはできません。 ピーク時間トラフィックの同じオーバー ロードは、ヨーロッパと米国のデータのセンターで発生します。 その他の時間帯では、サーバーは、トラフィックの量が最大能力も下にあるを処理します。  
  
シアトル アプリケーション サーバーをダブリン; の午後 6 時と午後 9 時の間にある程度の Dublin トラフィックをリダイレクトする contosogiftservices.com お客様が、Web サイトから応答性の高いエクスペリエンスを取得するためには、Contoso ギフト サービスを求めています対象とする午後 6 時とシアトルの午後 9 時の Dublin のアプリケーション サーバーをある程度のシアトル トラフィックをリダイレクトします。  
  
次の図は、このシナリオを示しています。  
  
![時刻の日 DNS ポリシーの例](../../media/DNS-Policy-Tod1/dns_policy_tod1.jpg)  
  
### <a name="bkmk_works1"></a>日の作業時間に基づくインテリジェントの DNS 応答  
  
時間が午後 6 時と各地理的な場所での午後 9 時の間の日 DNS ポリシーの DNS サーバーが構成されている場合、DNS サーバーは、次のします。  
  
- ローカル データ センター内の Web サーバーの IP アドレスを持つ受信最初の 4 つのクエリに応答します。  
- リモート データ センター内の Web サーバーの IP アドレスを持つ受信 5 番目のクエリに応答します。   
  
このポリシー ベースの動作は、ローカル アプリケーション サーバー上の負担を軽減し、顧客のサイト パフォーマンスの向上はリモートの Web サーバーにローカルの Web サーバーのトラフィックの負荷の約 20% をオフロードします。  
  
、ピーク時以外には、DNS サーバーは、通常の地理的な場所ベースのトラフィック管理を実行します。 さらに、北米またはヨーロッパ以外の場所からクエリを送信している DNS クライアントは、DNS サーバーの負荷は、シアトルとダブリン データ センター間のトラフィックを分散します。  
  
DNS では、複数の DNS ポリシーが構成されているとは、順序付けされた一連の規則によって処理される DNS 最高の優先順位と優先順位が最もします。 DNS は、1 日の時間を含むような場合に一致する最初のポリシーを使用します。 このため、個別のポリシーに優先順位の高いことが必要です。 ポリシーの 1 日の時間を作成してポリシーの一覧で、優先度の高いを与える場合、DNS は処理し、パラメーターの DNS クライアント クエリと、ポリシーで定義されている条件に一致した場合、まずこれらのポリシーを使用します。 ハッシュが一致しない DNS は一致するものが見つかるまで、既定のポリシーの処理ポリシーの一覧を下に移動します。  
  
ポリシーの種類と条件の詳細については、次を参照してください。[DNS のポリシーの概要](../../dns/deploy/DNS-Policies-Overview.md)します。  
  
### <a name="bkmk_how1"></a>1 日の時間に基づくインテリジェント DNS 応答の DNS ポリシーを構成する方法  
DNS のポリシー ベースの分散アプリケーションの負荷を 1 日の時間のクエリの応答を構成するのには、次の手順を実行する必要があります。  
  
- [DNS クライアントのサブネットを作成します。](#bkmk_subnets)  
- [ゾーンのスコープを作成します。](#bkmk_zscopes)  
- [レコードをゾーンのスコープに追加します。](#bkmk_records)  
- [DNS ポリシーを作成します。](#bkmk_policies)  
  
>[!NOTE]
>構成する場合、ゾーンの権限のある DNS サーバーでは、これらの手順を実行する必要があります。 メンバーシップ**DnsAdmins**、またはそれと同等は、次の手順を実行する必要です。  
  
次のセクションでは、詳細な構成手順を提供します。  
  
>[!IMPORTANT]
>次のセクションでには、多くのパラメーターの値例にはが含まれている Windows PowerShell コマンド例にはが含まれます。 これらのコマンドを実行する前に、展開に適切な値を持つこれらのコマンドで値の例を置き換えることを確認します。  
  
#### <a name="bkmk_subnets"></a>DNS クライアントのサブネットを作成します。  
最初の手順では、サブネットまたは IP アドレス空間のトラフィックをリダイレクトする領域を特定します。 たとえば、米国およびヨーロッパのトラフィックをリダイレクトする場合は、サブネットまたは IP アドレスのスペースがこれらの領域を識別する必要があります。  
  
この情報は、地理的な IP のマップから取得できます。 これらの地理的な IP のディストリビューションに基づき、「DNS クライアント サブネット」を作成する必要があります DNS クライアントのサブネットは、DNS サーバーにクエリの送信元 IPv4 または IPv6 サブネットの論理グループです。  
  
次の Windows PowerShell コマンドを使用して、DNS クライアントのサブネットを作成することができます。  
  
```  
Add-DnsServerClientSubnet -Name "AmericaSubnet" -IPv4Subnet "192.0.0.0/24, 182.0.0.0/24"  
  
Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet "141.1.0.0/24, 151.1.0.0/24"  
  
```  
詳細については、次を参照してください。[追加 DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps)します。  
  
#### <a name="bkmk_zscopes"></a>ゾーンのスコープを作成します。  
構成後は、クライアントのサブネットは、次の 2 つの異なるゾーン スコープにリダイレクトするトラフィックの 1 つのスコープを構成している DNS クライアントのサブネットごとのゾーンのパーティションを作成する必要があります。  
  
たとえば、www.contosogiftservices.com DNS 名のトラフィックをリダイレクトする場合は、contosogiftservices.com ゾーン、米国およびヨーロッパの 2 つの異なるゾーン スコープを作成する必要があります。  
  
ゾーンのスコープは、ゾーンの一意のインスタンスです。 DNS ゾーンには、複数のゾーンのスコープ、DNS レコードの独自セットが含まれている各ゾーンのスコープを持つことができます。 同じレコードは、別の IP アドレスを持つ複数のスコープまたは同じ IP アドレスに存在することができます。  
  
>[!NOTE]
>既定では、ゾーンのスコープは、DNS ゾーンに存在します。 このゾーンのスコープは、ゾーンと同じ名前を持つし、従来の DNS 操作は、このスコープで動作します。  
  
次の Windows PowerShell コマンドを使用すると、ゾーンのスコープを作成します。  
  
```  
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "SeattleZoneScope"  
  
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DublinZoneScope"  
  
```  
詳細については、次を参照してください。[追加 DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)します。  
  
#### <a name="bkmk_records"></a>レコードをゾーンのスコープに追加します。  
次の 2 つのゾーン スコープに Web サーバーのホストを表すレコードを追加する必要がありますようになりました。  
  
たとえば、**SeattleZoneScope**、レコード**www.contosogiftservices.com**がシアトルのデータ センターにある 192.0.0.1、IP アドレスを追加します。 同様に、[ **DublinZoneScope**、レコード**www.contosogiftservices.com** Dublin データ センターの IP アドレス 141.1.0.3 の追加  
  
次の Windows PowerShell コマンドを使用して、レコードをゾーンのスコープに追加することができます。  
  
```  
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "SeattleZoneScope  
  
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "141.1.0.3" -ZoneScope "DublinZoneScope"  
  
```  
既定のスコープでレコードを追加すると、ゾーン範囲ゾーン パラメーターが含まれていません。 これは、標準の DNS ゾーンにレコードを追加すると同じです。  
  
詳細については、次を参照してください。[追加 DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)します。  
  
#### <a name="bkmk_policies"></a>DNS ポリシーを作成します。  
サブネットを作成した後は、パーティション (ゾーン スコープ) を追加したレコード、できるように、クエリの応答が、ゾーンの正しい範囲から返される DNS クライアントのサブネットのいずれかのソースからクエリする際は、サブネット、およびパーティションに接続するポリシーを作成する必要があります。 ポリシーの既定のゾーンのスコープをマッピングするため必要はありません。  
  
これらの DNS ポリシーを構成した後、DNS サーバーの動作が次に示します。  
  
1. ヨーロッパの DNS クライアントは、その DNS クエリの応答で Dublin データ センターで、Web サーバーの IP アドレスを受け取ります。  
2. アメリカの DNS クライアントは、シアトルのデータ センターの DNS クエリの応答で、Web サーバーの IP アドレスを受け取ります。  
3. 午後 6 時とダブリンの午後 9 時、間は、ヨーロッパ言語のクライアントからのクエリの 20% は、シアトルのデータ センターの DNS クエリの応答で、Web サーバーの IP アドレスを受け取ります。  
4. 午後 6 時とシアトルの午後 9 時、間は、アメリカのクライアントからのクエリの 20% は、その DNS クエリの応答で Dublin データ センターで、Web サーバーの IP アドレスを受け取ります。  
5. シアトルのデータ センターの IP アドレスを受け取る、世界の残りの部分からのクエリの半分と残りの半分が Dublin データ センターの IP アドレスを受け取ります。  
  
  
次の Windows PowerShell コマンドを使用して、DNS クライアントのサブネットをリンクして、ゾーンのスコープ、DNS のポリシーを作成することができます。  
  
>[!NOTE]
>この例では、DNS サーバーは GMT のタイム ゾーンでピーク期間は同等の GMT 時刻で表現する必要があります。  
  
```  
Add-DnsServerQueryResolutionPolicy -Name "America6To9Policy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,4;DublinZoneScope,1" -TimeOfDay "EQ,01:00-04:00" -ZoneName "contosogiftservices.com" -ProcessingOrder 1  
  
Add-DnsServerQueryResolutionPolicy -Name "Europe6To9Policy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "SeattleZoneScope,1;DublinZoneScope,4" -TimeOfDay "EQ,17:00-20:00" -ZoneName "contosogiftservices.com" -ProcessingOrder 2  
  
Add-DnsServerQueryResolutionPolicy -Name "AmericaPolicy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 3  
  
Add-DnsServerQueryResolutionPolicy -Name "EuropePolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "DublinZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 4  
  
Add-DnsServerQueryResolutionPolicy -Name "RestOfWorldPolicy" -Action ALLOW --ZoneScope "DublinZoneScope,1;SeattleZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 5  
  
```  
詳細については、次を参照してください。[追加 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)します。  
  
DNS サーバーが、必要な DNS ポリシーを地理的な場所および 1 日の時間に基づいてトラフィックをリダイレクトするよう構成されました。  
  
DNS サーバーは名前解決クエリを受け取った場合、DNS サーバーは、DNS 要求に対して構成された DNS ポリシー内のフィールドを評価します。 名前解決の要求の発信元 IP アドレスには、任意のポリシーが一致すると、関連付けられているゾーンのスコープは、クエリに応答するために使用し、それらに地理的に最も近いリソースに、ユーザーを誘導します。  
  
要件を作成できます何千もの DNS のポリシーに従って、トラフィックの管理、および DNS サーバーを再起動しなくても - 受信したクエリで、すべての新しいポリシーが動的 - 適用します。


