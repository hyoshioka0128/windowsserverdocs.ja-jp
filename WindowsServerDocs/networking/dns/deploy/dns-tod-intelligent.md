---
title: 1 日の時間に基づくインテリジェントなDNS 応答に DNS ポリシーを使用する
description: このトピックは、Windows Server 2016 の DNS ポリシーシナリオガイドに含まれています。
manager: brianlic
ms.topic: article
ms.assetid: 161446ff-a072-4cc4-b339-00a04857ff3a
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 771b87776e6530f330e68f1f06b39fef191cb7c7
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996886"
---
# <a name="use-dns-policy-for-intelligent-dns-responses-based-on-the-time-of-day"></a>1 日の時間に基づくインテリジェントなDNS 応答に DNS ポリシーを使用する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、1 日の時間に基づき、DNS のポリシーを使用して、アプリケーションの別の地理的に分散インスタンス間でアプリケーションのトラフィックを分散するのに方法について説明します。

このシナリオは、別のタイム ゾーンに配置されている Web サーバーなどの別のアプリケーション サーバーに 1 つのタイム ゾーンでトラフィックを転送場合に便利です。 これにより、トラフィックを負荷分散アプリケーションのインスタンス間でのピーク時のトラフィックがプライマリ サーバーが、いつ過負荷の期間します。

### <a name="example-of-intelligent-dns-responses-based-on-the-time-of-day"></a><a name="bkmk_example1"></a>1 日の時間に基づくインテリジェント DNS 応答の例
1 日の時間に基づくアプリケーションのトラフィックを分散する DNS ポリシーを使用する方法の例を次に示します。

この例は、1 つ架空の会社の Web サイトを通じて、世界各地でオンライン gifting ソリューションを提供する Contoso ギフト サービスを使用して contosogiftservices.com します。

Contosogiftservices.com Web サイトは、2 つのデータ センター、シアトル (北米のみ) の 1 つとダブリン (ヨーロッパ) でホストされています。 DNS サーバーは、応答を送信地理的な場所に注意してください DNS ポリシーを使用して構成されます。 ビジネスで最近が急増したとき、contosogiftservices.com が訪問者の数を増やす、毎日とサービスの可用性に関する問題を報告した顧客の一部です。

Contoso ギフト サービスは、サイトの分析を実行し、毎日午後 6 時から午後 9 時のローカル時間の間が急増したときに Web サーバーへのトラフィックを検出します。 Web サーバーは、その結果サービス拒否が起こるよう顧客にこれらのピーク時に増加したトラフィックを処理するスケールことはできません。 ピーク時間トラフィックの同じオーバー ロードは、ヨーロッパと米国のデータのセンターで発生します。 他の時間帯では、サーバーは、トラフィックの量が最大能力も下にあるを処理します。

シアトル アプリケーション サーバーをダブリン; の午後 6 時から午後 9 時の間にある程度の Dublin トラフィックをリダイレクトする、contosogiftservices.com 顧客が Web サイトから応答性の高いエクスペリエンスを取得することを確認するには、Contoso ギフト サービスを求めています午後 6 時とシアトルの午後 9 時の Dublin のアプリケーション サーバーにある程度のシアトル トラフィックをリダイレクトします。

次の図は、このシナリオを示しています。

![1 日の DNS のポリシーの例の時間](../../media/DNS-Policy-Tod1/dns_policy_tod1.jpg)

### <a name="how-intelligent-dns-responses-based-on-time-of-day-works"></a><a name="bkmk_works1"></a>日の作業時間に基づくインテリジェントの DNS 応答

DNS サーバーがで時間が午後 6 時と各地理的な場所での午後 9 時の間の日 DNS ポリシーで構成されている DNS サーバーは次のです。

- ローカル データ センター内の Web サーバーの IP アドレスを持つ受信最初の 4 つのクエリに応答します。
- リモート データ センター内の Web サーバーの IP アドレスを持つ受信 5 番目のクエリに応答します。

このポリシー ベースの動作は、ローカル アプリケーション サーバー上の負担を軽減し、顧客のサイト パフォーマンスの向上はリモートの Web サーバーにローカル Web サーバーのトラフィックの負荷の約 20% をオフロードします。

オフピーク時間中には、DNS サーバーは、通常の地理的場所ベースのトラフィック管理を実行します。 さらに、北米またはヨーロッパ以外の場所からクエリを送信する DNS クライアントは、DNS サーバーの負荷は、シアトルとダブリン データ センター間で、トラフィックを分散します。

DNS では、複数の DNS ポリシーが構成されていると順序付けられた一連の規則が優先順位が最も優先度の高い DNS で処理されるは。 DNS は、1 日の時間も含めて、状況に一致する最初のポリシーを使用します。 このため、個別のポリシーに優先順位が高いことが必要です。 ポリシーの 1 日の時刻を作成してポリシーの一覧で優先度の高いを与える場合、DNS は処理し、DNS クライアント クエリと、ポリシーで定義された条件のパラメーター値が一致した場合は、まずこれらのポリシーを使用します。 ハッシュが一致しない場合、DNS は一致を検出するまで、既定のポリシーの処理ポリシーの一覧を下へ移動します。

ポリシーの種類と条件の詳細については、次を参照してください。 [DNS のポリシーの概要](../../dns/deploy/DNS-Policies-Overview.md)します。

### <a name="how-to-configure-dns-policy-for-intelligent-dns-responses-based-on-time-of-day"></a><a name="bkmk_how1"></a>1 日の時間に基づくインテリジェント DNS 応答に DNS のポリシーを構成する方法
分散アプリケーションの負荷を 1 日の時間ベースのクエリの応答の DNS のポリシーを構成するには、次の手順を実行する必要があります。

- [DNS クライアントのサブネットを作成します。](#bkmk_subnets)
- [ゾーンのスコープを作成します。](#bkmk_zscopes)
- [レコードをゾーンのスコープに追加します。](#bkmk_records)
- [DNS のポリシーを作成します。](#bkmk_policies)

>[!NOTE]
>構成する場合、ゾーンに対して権限のある DNS サーバーでは、これらの手順を実行する必要があります。 メンバーシップ **DnsAdmins**, 、または同等の権限が必要で、次の手順を実行します。

次のセクションでは、詳細な構成手順を説明します。

>[!IMPORTANT]
>以下のセクションには、多くのパラメーターの値の例を含む Windows PowerShell コマンドの例が含まれています。 これらのコマンドで値の例は、これらのコマンドを実行する前に、展開に対応する値を置き換えることを確認します。

#### <a name="create-the-dns-client-subnets"></a><a name="bkmk_subnets"></a>DNS クライアントのサブネットを作成します。
最初の手順では、サブネットまたは IP アドレス空間のトラフィックをリダイレクトする領域を識別します。 たとえば、米国およびヨーロッパのトラフィックをリダイレクトする場合は、サブネットまたは IP アドレス空間がこれらの領域を識別する必要があります。

この情報は、地理的 IP のマップから取得できます。 これらの地理的 IP のディストリビューションに基づき、「DNS クライアント サブネット」を作成する必要があります。 DNS クライアントのサブネットは、クエリが DNS サーバーに送信元 IPv4 または IPv6 サブネットの論理グループです。

次の Windows PowerShell コマンドを使用すると、DNS クライアントのサブネットを作成します。

```
Add-DnsServerClientSubnet -Name "AmericaSubnet" -IPv4Subnet "192.0.0.0/24, 182.0.0.0/24"

Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet "141.1.0.0/24, 151.1.0.0/24"

```
詳細については、次を参照してください。 [追加 DnsServerClientSubnet](/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps)します。

#### <a name="create-the-zone-scopes"></a><a name="bkmk_zscopes"></a>ゾーンのスコープを作成します。
クライアントのサブネットを構成した後は、2 つの異なるゾーン スコープにリダイレクトするトラフィックの 1 つのスコープに構成されている DNS クライアントのサブネットごとのゾーンをパーティション分割する必要があります。

など DNS 名 www.contosogiftservices.com のトラフィックをリダイレクトする場合は、contosogiftservices.com ゾーン、米国およびヨーロッパの 2 つの別のゾーン スコープを作成する必要があります。

ゾーンのスコープは、ゾーンの一意のインスタンスです。 DNS ゾーンは複数のゾーンスコープを持つことができ、各ゾーンスコープには独自の DNS レコードセットが含まれます。 同じレコードが複数のスコープに存在し、異なる IP アドレスまたは同じ IP アドレスを持つことができます。

>[!NOTE]
>既定では、ゾーンのスコープは、DNS ゾーンに存在します。 このゾーンのスコープでは、ゾーンと同じ名前と、従来の DNS の機能がこのスコープで動作します。

次の Windows PowerShell コマンドを使用すると、ゾーンのスコープを作成します。

```
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "SeattleZoneScope"

Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DublinZoneScope"

```
詳細については、「 [DnsServerZoneScope](/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)」を参照してください。

#### <a name="add-records-to-the-zone-scopes"></a><a name="bkmk_records"></a>レコードをゾーンのスコープに追加します。
2 つのゾーンのスコープに web サーバーのホストを表すレコードを追加する必要があります。

たとえば、 **SeattleZoneScope**, 、レコード <strong>www.contosogiftservices.com</strong> はシアトルのデータ センターにある IP アドレス、192.0.0.1 で追加します。 同様に、[ **DublinZoneScope**, 、レコード <strong>www.contosogiftservices.com</strong> Dublin データ センター内の IP アドレス 141.1.0.3 の追加

次の Windows PowerShell コマンドを使用して、レコードをゾーンのスコープに追加することができます。

```
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "SeattleZoneScope

Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "141.1.0.3" -ZoneScope "DublinZoneScope"

```
既定のスコープでレコードを追加すると、ゾーン範囲ゾーン パラメーターは含まれません。 これは、標準の DNS ゾーンにレコードを追加すると同じです。

詳細については、次を参照してください。 [追加 DnsServerResourceRecord](/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)します。

#### <a name="create-the-dns-policies"></a><a name="bkmk_policies"></a>DNS のポリシーを作成します。
サブネットを作成した後は、しパーティション (ゾーン スコープ) には、レコードを追加した、サブネット、およびパーティションに接続しているポリシーは、DNS クライアントのサブネットのいずれかのソースから、クエリの結果が、クエリの応答が、ゾーンの正しい範囲から返されます。 を作成する必要があります。 ポリシーの既定のゾーンのスコープをマッピングするため必要はありません。

これらの DNS のポリシーを構成した後、DNS サーバーの動作は次に示します。

1. ヨーロッパの DNS クライアントは、その DNS クエリの応答で Dublin データ センターの Web サーバーの IP アドレスを受け取ります。
2. アメリカの DNS クライアントは、シアトルのデータ センターの DNS クエリの応答での Web サーバーの IP アドレスを受け取ります。
3. 、午後 6 時とダブリンの午後 9 時の間は、ヨーロッパのクライアントからのクエリの 20% は、シアトルのデータ センターの DNS クエリの応答での Web サーバーの IP アドレスを受け取ります。
4. 、午後 6 時とシアトルの午後 9 時の間は、アメリカのクライアントからのクエリの 20% は、その DNS クエリの応答で Dublin データ センターの Web サーバーの IP アドレスを受け取ります。
5. シアトルのデータ センターの IP アドレスを受信、その他の国からのクエリの半分と残りの半分が Dublin データ センターの IP アドレスを受信します。


次の Windows PowerShell コマンドを使用すると、DNS クライアントのサブネットへのリンクとゾーン スコープに、DNS のポリシーを作成します。

>[!NOTE]
>この例では、DNS サーバーは GMT のタイム ゾーンでピーク時の期間は同等の GMT 時刻で表現できる必要があります。

```
Add-DnsServerQueryResolutionPolicy -Name "America6To9Policy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,4;DublinZoneScope,1" -TimeOfDay "EQ,01:00-04:00" -ZoneName "contosogiftservices.com" -ProcessingOrder 1

Add-DnsServerQueryResolutionPolicy -Name "Europe6To9Policy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "SeattleZoneScope,1;DublinZoneScope,4" -TimeOfDay "EQ,17:00-20:00" -ZoneName "contosogiftservices.com" -ProcessingOrder 2

Add-DnsServerQueryResolutionPolicy -Name "AmericaPolicy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 3

Add-DnsServerQueryResolutionPolicy -Name "EuropePolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "DublinZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 4

Add-DnsServerQueryResolutionPolicy -Name "RestOfWorldPolicy" -Action ALLOW --ZoneScope "DublinZoneScope,1;SeattleZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 5

```
詳細については、次を参照してください。 [追加 DnsServerQueryResolutionPolicy](/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)します。

DNS サーバーが、必要な DNS のポリシーに地理的な場所と時間に基づいてトラフィックをリダイレクトするよう構成されました。

DNS サーバーは、名前解決のクエリを受信すると、DNS サーバーは、DNS 要求に対して構成された DNS ポリシー内のフィールドを評価します。 名前解決の要求の送信元 IP アドレスには、任意のポリシーが一致すると、関連付けられているゾーンのスコープは、クエリに応答するために使用し、地理的に最も近いリソースにユーザーを誘導します。

何千もの DNS のポリシーに合わせて作成できます、トラフィック管理の要件、DNS サーバーを再起動しなくても - 受信したクエリで、すべての新しいポリシーが動的 - 適用されます。