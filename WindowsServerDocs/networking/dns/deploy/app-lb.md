---
title: アプリケーションの負荷分散に DNS ポリシーを使用する
description: このトピックは、Windows Server 2016 の DNS ポリシーシナリオガイドに含まれています。
manager: brianlic
ms.topic: article
ms.assetid: f9c313ac-bb86-4e48-b9b9-de5004393e06
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 0af8a819494754fc45392116230edad808835e80
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87964238"
---
# <a name="use-dns-policy-for-application-load-balancing"></a>アプリケーションの負荷分散に DNS ポリシーを使用する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、アプリケーションの負荷分散を実行するように DNS ポリシーを構成する方法について説明します。

以前のバージョンの Windows Server DNS では、ラウンドロビン応答を使用した負荷分散のみが提供されていました。しかし、Windows Server 2016 の DNS では、アプリケーションの負荷分散に DNS ポリシーを構成できます。

アプリケーションの複数のインスタンスをデプロイした場合は、DNS ポリシーを使用して、異なるアプリケーションインスタンス間でトラフィックの負荷を分散し、アプリケーションのトラフィック負荷を動的に割り当てることができます。

## <a name="example-of-application-load-balancing"></a>アプリケーションの負荷分散の例

次に、アプリケーションの負荷分散に DNS ポリシーを使用する方法の例を示します。

この例では、架空の会社である Contoso ギフトサービスを使用します。これは、オンライン gifing サービスを提供し、 **contosogiftservices.com**という名前の Web サイトを持っています。

Contosogiftservices.com web サイトは、それぞれが異なる IP アドレスを持つ複数のデータセンターでホストされています。

Contoso ギフトサービスの主要市場である北米では、Web サイトはシカゴ、IL、ダラス、TX、シアトル、ワシントンという3つのデータセンターでホストされています。

シアトルの Web サーバーは最適なハードウェア構成を備えており、他の2つのサイトと同様に2倍の負荷を処理できます。 Contoso ギフトサービスは、次のようにアプリケーショントラフィックを送信します。

- シアトルの Web サーバーにはより多くのリソースが含まれているため、アプリケーションの半分のクライアントがこのサーバーに送られます。
- アプリケーションのクライアントの1四半期がダラス、TX datacenter に送られます。
- アプリケーションのクライアントの1四半期がシカゴ、IL、データセンターに送信されます。

次の図は、このシナリオを示しています。

![Dns ポリシーを使用した DNS アプリケーションの負荷分散](../../media/Dns-App-Lb/dns-app-lb.jpg)


### <a name="how-application-load-balancing-works"></a>アプリケーションの負荷分散のしくみ

このシナリオ例を使用して、アプリケーションの負荷分散の dns ポリシーを使用して DNS サーバーを構成した後、DNS サーバーは、シアトルの Web サーバーアドレス、ダラス Web サーバーのアドレスでは25%、シカゴの Web サーバーアドレスでは25% の時間のうち、50% の時間を返します。

これにより、DNS サーバーが受信する4つのクエリごとに、シアトルの2つの応答と、ダラスとシカゴ用の2つの応答が返されます。

DNS ポリシーを使用した負荷分散で考えられる1つの問題は、dns クライアントおよびリゾルバー/LDNS による DNS レコードのキャッシュです。これは、クライアントまたはリゾルバーがクエリを DNS サーバーに送信しないため、負荷分散に干渉する可能性があります。

\- \- \( \) 負荷分散する必要がある DNS レコードに対して、[有効期限-有効期間の TTL 値を使用することによって、この動作の影響を軽減することができます。

### <a name="how-to-configure-application-load-balancing"></a>アプリケーションの負荷分散を構成する方法

次のセクションでは、アプリケーションの負荷分散に DNS ポリシーを構成する方法について説明します。

#### <a name="create-the-zone-scopes"></a>ゾーンのスコープを作成します。

最初に、ホストされているデータセンターのゾーン contosogiftservices.com のスコープを作成する必要があります。

ゾーンのスコープは、ゾーンの一意のインスタンスです。 DNS ゾーンは複数のゾーンスコープを持つことができ、各ゾーンスコープには独自の DNS レコードセットが含まれます。 同じレコードが複数のスコープに存在し、異なる IP アドレスまたは同じ IP アドレスを持つことができます。

>[!NOTE]
>既定では、ゾーンのスコープは、DNS ゾーンに存在します。 このゾーンのスコープでは、ゾーンと同じ名前と、従来の DNS の機能がこのスコープで動作します。

次の Windows PowerShell コマンドを使用すると、ゾーンのスコープを作成します。

```powershell
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "SeattleZoneScope"
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DallasZoneScope"
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "ChicagoZoneScope"
```

詳細については、次を参照してください [追加 DnsServerZoneScope。](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)

#### <a name="add-records-to-the-zone-scopes"></a><a name="bkmk_records"></a>レコードをゾーンのスコープに追加します。

次に、web サーバーホストを表すレコードをゾーンのスコープに追加する必要があります。

**SeattleZoneScope**では、シアトルのデータセンターにある IP address 192.0.0.1 を使用して、レコード www.contosogiftservices.com を追加できます。

**ChicagoZoneScope**では、 \( シカゴの \) データセンターに IP アドレス182.0.0.1 を持つ同じレコード www.contosogiftservices.com を追加できます。

同様に、 **DallasZoneScope**では、シカゴの \( \) データセンターに IP アドレス162.0.0.1 のレコード www.contosogiftservices.com を追加できます。

次の Windows PowerShell コマンドを使用して、レコードをゾーンのスコープに追加することができます。

```powershell
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "SeattleZoneScope"
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "182.0.0.1" -ZoneScope "ChicagoZoneScope"
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "162.0.0.1" -ZoneScope "DallasZoneScope"
```

詳細については、次を参照してください。 [追加 DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)します。

#### <a name="create-the-dns-policies"></a><a name="bkmk_policies"></a>DNS のポリシーを作成します。

パーティション (ゾーンのスコープ) を作成し、レコードを追加したら、これらのスコープに対して受信クエリを分散する DNS ポリシーを作成する必要があります。これにより、contosogiftservices.com に対するクエリの50% がシアトルのデータセンターの Web サーバーの IP アドレスで応答するようになります

次の Windows PowerShell コマンドを使用すると、これら3つのデータセンター間でアプリケーショントラフィックを分散する DNS ポリシーを作成できます。

>[!NOTE]
>次の例のコマンドでは、式–ゾーン範囲ゾーン "SeattleZoneScope, 2;ChicagoZoneScope, 1;DallasZoneScope, 1 "は、パラメーターの組み合わせを含む配列を使用して DNS サーバーを構成し `<ZoneScope>` `<weight>` ます。

```powershell
Add-DnsServerQueryResolutionPolicy -Name "AmericaPolicy" -Action ALLOW -ZoneScope "SeattleZoneScope,2;ChicagoZoneScope,1;DallasZoneScope,1" -ZoneName "contosogiftservices.com"
```

詳細については、次を参照してください。 [追加 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)します。

これで、3つの異なるデータセンター内の Web サーバー間でのアプリケーションの負荷分散を実現する DNS ポリシーが作成されました。

何千もの DNS のポリシーに合わせて作成できます、トラフィック管理の要件、DNS サーバーを再起動しなくても - 受信したクエリで、すべての新しいポリシーが動的 - 適用されます。
