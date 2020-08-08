---
title: Azure クラウド アプリケーション サーバーを使用した 1 日の時間に基づく DNS 応答
description: このトピックは、Windows Server 2016 の DNS ポリシーシナリオガイドに含まれています。
manager: brianlic
ms.topic: article
ms.assetid: 4846b548-8fbc-4a7f-af13-09e834acdec0
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d7df84e26ef86f553d57b2019d4d46581d7c17fa
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996894"
---
# <a name="dns-responses-based-on-time-of-day-with-an-azure-cloud-app-server"></a>Azure クラウド アプリケーション サーバーを使用した 1 日の時間に基づく DNS 応答

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、1 日の時間に基づき、DNS のポリシーを使用して、アプリケーションの別の地理的に分散インスタンス間でアプリケーションのトラフィックを分散するのに方法について説明します。

このシナリオは、別のタイムゾーンに配置されている Microsoft Azure でホストされている Web サーバーなど、1つのタイムゾーンのトラフィックを別のアプリケーションサーバーに転送する場合に便利です。 これにより、トラフィックを負荷分散アプリケーションのインスタンス間でのピーク時のトラフィックがプライマリ サーバーが、いつ過負荷の期間します。

> [!NOTE]
> Azure を使用せずにインテリジェントな DNS 応答に DNS ポリシーを使用する方法については、「[時間に基づくインテリジェント Dns 応答に Dns ポリシーを使用](./dns-tod-intelligent.md)する」を参照してください。

## <a name="example-of-intelligent-dns-responses-based-on-the-time-of-day-with-azure-cloud-app-server"></a>Azure Cloud App Server での時間に基づくインテリジェント DNS 応答の例

1 日の時間に基づくアプリケーションのトラフィックを分散する DNS ポリシーを使用する方法の例を次に示します。

この例は、1 つ架空の会社の Web サイトを通じて、世界各地でオンライン gifting ソリューションを提供する Contoso ギフト サービスを使用して contosogiftservices.com します。

Contosogiftservices.com web サイトは、シアトルの1つのオンプレミスデータセンター (パブリック IP 192.68.30.2) でのみホストされています。

DNS サーバーは、オンプレミスのデータセンターにも配置されます。

ビジネスで最近が急増したとき、contosogiftservices.com が訪問者の数を増やす、毎日とサービスの可用性に関する問題を報告した顧客の一部です。

Contoso ギフトサービスはサイト分析を実行し、午後6時から午後9時までの間に、シアトルの Web サーバーへのトラフィックが急増していることを検出します。 Web サーバーは、これらのピーク時間で増加したトラフィックを処理するように拡張することはできません。その結果、顧客へのサービス拒否が発生します。

Contosogiftservices.com のお客様が Web サイトから応答性の高いエクスペリエンスを得られるように、Contoso ギフト Services は、この時間内に Microsoft Azure 上の仮想マシン VM をレンタルし、 \( \) web サーバーのコピーをホストすることを決定します。

Contoso のギフトサービスは VM (192.68.31.44) の Azure からパブリック IP アドレスを取得し、毎日5-10 の間に Azure で Web サーバーをデプロイするための自動化を開発します。これにより、1時間のコンティンジェンシー期間が可能になります。

> [!NOTE]
> Azure Vm の詳細については、 [Virtual Machines のドキュメント](https://azure.microsoft.com/documentation/services/virtual-machines/)を参照してください。

DNS サーバーはゾーンスコープと DNS ポリシーを使用して構成されます。これにより、毎日 5-9 PM に、Azure で実行されている Web サーバーのインスタンスにクエリの30% が送信されます。

次の図は、このシナリオを示しています。

![時間帯応答の DNS ポリシー](../../media/DNS-Policy-Tod2/dns_policy_tod2.jpg)

## <a name="how-intelligent-dns-responses-based-on-time-of-day-with-azure-app-server-works"></a>Azure アプリ Server での時間帯に基づくインテリジェント DNS 応答のしくみ

この記事では、2つの異なるアプリケーションサーバー IP アドレスを使用して dns クエリに応答するように DNS サーバーを構成する方法について説明します。一方の web サーバーはシアトルにあり、もう1つは Azure データセンターにあります。

シアトルの午後6時から午後9時までのピーク時間に基づいて新しい DNS ポリシーを構成した後、DNS サーバーは、シアトルの Web サーバーの IP アドレスを含むクライアントに対して、dns 応答の1秒あたり70を送信します。また、Azure Web サーバーの IP アドレスを含むクライアントに対して、DNS 応答の1% を行います。これにより、クライアントトラフィックが新しい Azure Web サーバーに転送され、シアトルの Web サーバーが過負荷になるのを防ぐことができます。

それ以外の時間は、通常のクエリ処理が実行され、応答が既定のゾーンスコープから送信されます。これには、オンプレミスデータセンター内の web サーバーのレコードが含まれます。

Azure レコードの TTL を10分にすると、Azure から VM が削除される前に、レコードが LDNS キャッシュから期限切れになります。 このようなスケーリングの利点の1つは、DNS データをオンプレミスに保持し、必要に応じて Azure へのスケールアウトを維持できることです。

## <a name="how-to-configure-dns-policy-for-intelligent-dns-responses-based-on-time-of-day-with-azure-app-server"></a>Azure アプリ Server での時刻に基づいてインテリジェント DNS 応答の DNS ポリシーを構成する方法

分散アプリケーションの負荷を 1 日の時間ベースのクエリの応答の DNS のポリシーを構成するには、次の手順を実行する必要があります。

- [ゾーンのスコープを作成します。](#create-the-zone-scopes)
- [レコードをゾーンのスコープに追加します。](#add-records-to-the-zone-scopes)
- [DNS のポリシーを作成します。](#create-the-dns-policies)

> [!NOTE]
> 構成する場合、ゾーンに対して権限のある DNS サーバーでは、これらの手順を実行する必要があります。 メンバーシップ DnsAdmins, 、または同等の権限が必要で、次の手順を実行します。

次のセクションでは、詳細な構成手順を説明します。

> [!IMPORTANT]
> 以下のセクションには、多くのパラメーターの値の例を含む Windows PowerShell コマンドの例が含まれています。 これらのコマンドで値の例は、これらのコマンドを実行する前に、展開に対応する値を置き換えることを確認します。


### <a name="create-the-zone-scopes"></a>ゾーンのスコープを作成します。

ゾーンのスコープは、ゾーンの一意のインスタンスです。 DNS ゾーンは複数のゾーンスコープを持つことができ、各ゾーンスコープには独自の DNS レコードセットが含まれます。 同じレコードが複数のスコープに存在し、異なる IP アドレスまたは同じ IP アドレスを持つことができます。

> [!NOTE]
> 既定では、ゾーンのスコープは、DNS ゾーンに存在します。 このゾーンのスコープでは、ゾーンと同じ名前と、従来の DNS の機能がこのスコープで動作します。

次のコマンド例を使用すると、Azure レコードをホストするゾーンスコープを作成できます。

```
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "AzureZoneScope"
```

詳細については、次を参照してください [追加 DnsServerZoneScope。](/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)

### <a name="add-records-to-the-zone-scopes"></a>レコードをゾーンのスコープに追加します。
次の手順では、Web サーバーホストを表すレコードをゾーンのスコープに追加します。

AzureZoneScope では、レコード www.contosogiftservices.com は、Azure パブリッククラウド内にある IP アドレス192.68.31.44 を使用して追加されます。

同様に、既定のゾーンスコープ contosogiftservices.com では、 \( \) シアトルの \( \) オンプレミスデータセンターで実行されている Web サーバーの IP アドレス192.68.30.2 を使用して、レコード www.contosogiftservices.com が追加されます。

次の2番目のコマンドレットでは、–ゾーン範囲ゾーンパラメーターは含まれていません。 このため、レコードは既定のゾーン範囲ゾーンに追加されます。

さらに、Azure Vm のレコードの TTL は600秒 (10 分) に保持されるため、LDNS はそれを長時間キャッシュしないようにして、負荷分散に干渉します。 また、キャッシュされたレコードを持つクライアントでも解決できるように、コンティンジェンシーとして1時間分の Azure Vm を使用できます。

```
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.68.31.44" -ZoneScope "AzureZoneScope" –TimeToLive 600

Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.68.30.2"
```

詳細については、次を参照してください。 [追加 DnsServerResourceRecord](/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)します。

### <a name="create-the-dns-policies"></a>DNS のポリシーを作成します。
ゾーンスコープが作成されたら、次のように、これらのスコープに対して受信クエリを分散する DNS ポリシーを作成できます。

1. 午後6時から午後9時までの間、クライアントの30% は DNS 応答で Azure データセンター内の Web サーバーの IP アドレスを受け取りますが、クライアントの70% はシアトルのオンプレミス Web サーバーの IP アドレスを受け取ります。
2. それ以外の場合、すべてのクライアントは、シアトルのオンプレミス Web サーバーの IP アドレスを受け取ります。

その日の時刻は、DNS サーバーのローカル時刻で表される必要があります。

DNS ポリシーを作成するには、次のコマンド例を使用します。

```
Add-DnsServerQueryResolutionPolicy -Name "Contoso6To9Policy" -Action ALLOW -ZoneScope "contosogiftservices.com,7;AzureZoneScope,3" –TimeOfDay “EQ,18:00-21:00” -ZoneName "contosogiftservices.com" –ProcessingOrder 1
```

詳細については、次を参照してください。 [追加 DnsServerQueryResolutionPolicy](/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)します。

これで、DNS サーバーは、時間に基づいて Azure Web サーバーにトラフィックをリダイレクトするために必要な DNS ポリシーを使用して構成されます。

式に注意してください。

`
 -ZoneScope "contosogiftservices.com,7;AzureZoneScope,3" –TimeOfDay “EQ,18:00-21:00”
`

この式では、ゾーン範囲ゾーンと weight の組み合わせを使用して DNS サーバーを構成します。これは、Azure Web サーバーの ip アドレスを時間の経過と共に30分ごとに送信すると同時に、シアトルの Web サーバー70の IP アドレスを送信するように DNS サーバーに指示します。

何千もの DNS のポリシーに合わせて作成できます、トラフィック管理の要件、DNS サーバーを再起動しなくても - 受信したクエリで、すべての新しいポリシーが動的 - 適用されます。