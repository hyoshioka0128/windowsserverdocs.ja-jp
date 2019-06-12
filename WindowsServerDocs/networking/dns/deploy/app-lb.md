---
title: アプリケーションの負荷分散に DNS ポリシーを使用する
description: このトピックは、DNS ポリシー シナリオ ガイドの Windows Server 2016 の一部です。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: f9c313ac-bb86-4e48-b9b9-de5004393e06
ms.author: pashort
author: shortpatti
ms.openlocfilehash: dca60fc0e216b1b873bd4f94dd1b01174d80fc14
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446442"
---
# <a name="use-dns-policy-for-application-load-balancing"></a>アプリケーションの負荷分散に DNS ポリシーを使用する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用すると、アプリケーションの負荷分散を実行するのに DNS ポリシーを構成するのに方法について説明します。

以前のバージョンの Windows Server DNS は、ラウンド ロビンの反応を使用して負荷分散のみ提供されています。Windows Server 2016 で DNS に DNS のポリシーをアプリケーションの負荷分散を構成できます。

アプリケーションの複数のインスタンスを展開している場合は、それによって動的にアプリケーションのトラフィックの負荷を割り当て、別のアプリケーション インスタンス間でトラフィックの負荷を分散する DNS ポリシーを使用できます。

## <a name="example-of-application-load-balancing"></a>アプリケーションの負荷分散の例

アプリケーションの負荷分散に DNS ポリシーを使用する方法の例を次に示します。

この例は、1 つ架空の会社 Contoso ギフト サービス - オンライン gifing のサービスを提供して、という名前の Web サイトを使用して**contosogiftservices.com**します。

Contosogiftservices.com web サイトは、異なる IP アドレスがある複数のデータ センターでホストされます。

Contoso ギフト サービスのプライマリの市場には、北米の Web サイトは、次の 3 つのデータ センターでホストされます。イリノイ州シカゴ、テキサス州ダラスおよび、ワシントン州シアトルです。

シアトルの Web サーバーは、最適なハードウェア構成を備え、他の 2 つのサイトとして 2 倍の負荷を処理することができます。 Contoso ギフト サービスには、次のようにアプリケーションのトラフィックが希望しています。

- シアトルの Web サーバーには、その他のリソースが含まれているために、アプリケーションのクライアントの半分はこのサーバーに送られます。
- アプリケーションのクライアントの 4 分の 1 は、テキサス州ダラスのデータ センターに送られます
- アプリケーションのクライアントの 4 分の 1 は、イリノイ州シカゴのデータ センターに送られます

次の図は、このシナリオを示しています。

![DNS アプリケーションの負荷分散と DNS のポリシー](../../media/Dns-App-Lb/dns-app-lb.jpg)


### <a name="how-application-load-balancing-works"></a>アプリケーションの負荷分散の動作

構成した後アプリケーション用の DNS ポリシーを持つ DNS サーバー負荷分散を使用してこのシナリオ例では、DNS サーバー、シアトル Web サーバー アドレス、ダラス Web サーバー アドレスでは、時間の 25% から 25% 以上の時間で時間の 50% の応答シカゴの Web サーバーのアドレス。

そのための DNS サーバーが 4 つのクエリごとに、応答した 2 つの応答シアトルと Dallas とシカゴの 1 つずつです。

DNS のポリシーでの負荷分散と考えられる問題の 1 つは、DNS クライアントおよびクライアントまたは競合回避モジュールでは、DNS サーバーに、クエリは送信しないため、負荷分散に干渉する競合回避モジュール/LDNS によって DNS レコードのキャッシュです。

短い時刻を使用してこの動作の影響を軽減する\-に\-Live \(TTL\)値、DNS レコードをする負荷を分散する必要があります。

### <a name="how-to-configure-application-load-balancing"></a>アプリケーションの負荷分散を構成する方法

次のセクションでは、アプリケーションの負荷分散用の DNS ポリシーを構成する方法を説明します。

#### <a name="create-the-zone-scopes"></a>ゾーンのスコープを作成します。

まず、ホストされているデータ センターのゾーン contosogiftservices.com のスコープを作成する必要があります。

ゾーンのスコープは、ゾーンの一意のインスタンスです。 DNS ゾーンは、独自の DNS レコード セットを格納している各ゾーンのスコープを持つ、複数のゾーン スコープを持つことができます。 同じレコードは、別の IP アドレスを持つ、複数のスコープまたは同じ IP アドレスに存在することができます。

>[!NOTE]
>既定では、ゾーンのスコープは、DNS ゾーンに存在します。 このゾーンのスコープでは、ゾーンと同じ名前と、従来の DNS の機能がこのスコープで動作します。

次の Windows PowerShell コマンドを使用すると、ゾーンのスコープを作成します。
    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "SeattleZoneScope"
    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DallasZoneScope"
    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "ChicagoZoneScope"

詳細については、次を参照してください [追加 DnsServerZoneScope。](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)

#### <a name="bkmk_records"></a>レコードをゾーンのスコープに追加します。

今すぐゾーン スコープに web サーバーのホストを表すレコードを追加する必要があります。

**SeattleZoneScope**シアトルのデータ センターにある IP アドレス、192.0.0.1 レコード www.contosogiftservices.com を追加することができます。

**ChicagoZoneScope**、同じレコードを追加する\(www.contosogiftservices.com\) 182.0.0.1 シカゴのデータ センターの IP アドレスします。

同様に、 **DallasZoneScope**、レコードを追加する\(www.contosogiftservices.com\) 162.0.0.1 シカゴのデータ センターの IP アドレスします。

次の Windows PowerShell コマンドを使用して、レコードをゾーンのスコープに追加することができます。
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "SeattleZoneScope
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "182.0.0.1" -ZoneScope "ChicagoZoneScope"
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "162.0.0.1" -ZoneScope "DallasZoneScope"
    

詳細については、次を参照してください。 [追加 DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)します。

#### <a name="bkmk_policies"></a>DNS ポリシーを作成します。

パーティション (ゾーン スコープ) を作成したレコードを追加した後は、50% の contosogiftservices.com に対するクエリの応答が IP アドレスを持つ、Web のように、これらのスコープ全体で着信クエリを分散する DNS ポリシーを作成する必要があります。シアトルのデータ センターおよびその他のサーバーは、シカゴとダラスのデータ センター間で均等に分散されます。

次の Windows PowerShell コマンドを使用すると、これら 3 つのデータ センター間でのアプリケーション トラフィックを分散する DNS ポリシーを作成します。

>[!NOTE]
>次に、式の例で – ゾーン範囲ゾーン"SeattleZoneScope、2 です。ChicagoZoneScope、1 になります。DallasZoneScope、1"DNS サーバーを構成パラメーターの組み合わせを含む配列を持つ\<ゾーン範囲ゾーン\>、\<重み\>します。
    
    Add-DnsServerQueryResolutionPolicy -Name "AmericaPolicy" -Action ALLOW -ZoneScope "SeattleZoneScope,2;ChicagoZoneScope,1;DallasZoneScope,1" -ZoneName "contosogiftservices.com"
    

詳細については、次を参照してください。 [追加 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)します。  

次の 3 つの異なるデータ センター内の Web サーバー間で分散アプリケーションの負荷を提供する DNS ポリシーは正常に作成されました。

何千もの DNS のポリシーに合わせて作成できます、トラフィック管理の要件、DNS サーバーを再起動しなくても - 受信したクエリで、すべての新しいポリシーが動的 - 適用されます。
