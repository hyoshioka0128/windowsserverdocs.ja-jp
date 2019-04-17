---
title: アプリケーションの負荷分散に DNS ポリシーを使用します。
description: このトピックでは、DNS ポリシー シナリオ ガイドの Windows Server 2016 の一部
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: f9c313ac-bb86-4e48-b9b9-de5004393e06
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d156c258b971c45bf1c4c20739440bd5cc9e239f
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-application-load-balancing"></a>アプリケーションの負荷分散に DNS ポリシーを使用します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、アプリケーションの負荷分散を実行するのに DNS ポリシーを構成するのに方法について説明します。

以前のバージョンの Windows Server DNS ラウンド ロビンの反応を使用して、負荷分散に用意したものDNS では Windows Server 2016 では、アプリケーションの負荷分散に DNS ポリシーを構成することができます。

アプリケーションの複数のインスタンスを展開したときに DNS ポリシーを使用するアプリケーションのトラフィックの負荷をこれにより動的に割り当てる、別のアプリケーションのインスタンス間でトラフィックの負荷を分散することができます。

## <a name="example-of-application-load-balancing"></a>アプリケーションの負荷分散の例

アプリケーションの負荷分散に DNS ポリシーを使用する方法の例を次に示します。

この例は、1 つ架空の会社の Contoso ギフト サービス - gifing オンライン サービスを提供して、という名前の Web サイトを使用して**contosogiftservices.com**します。

Contosogiftservices.com web サイトは、複数の IP アドレスがある複数のデータ センターでホストされています。

Contoso ギフト サービスのプライマリ市場には、北米では、Web サイトは次の 3 つのデータ センターでホストされて: イリノイ州シカゴ、米国テキサス州ダラスおよびワシントン州シアトルします。

シアトルの Web サーバーが最適なハードウェア構成と、その他の 2 つのサイトとして倍の負荷を処理できます。 Contoso ギフト サービスは、次のようにアプリケーションのトラフィックを希望しています。

- アプリケーションのクライアントの半分はこのサーバーに転送シアトル Web サーバーより多くのリソースが含まれているため
- アプリケーションのクライアントの四半期を 1 つは、米国テキサス州ダラス データ センターに転送します。
- アプリケーションのクライアントの四半期を 1 つは、イリノイ州シカゴのデータ センターに転送します。

次の図は、このシナリオを示しています。

![DNS アプリケーションで負荷分散の DNS のポリシー](../../media/Dns-App-Lb/dns-app-lb.jpg)


### <a name="how-application-load-balancing-works"></a>アプリケーションの負荷分散の動作

構成した後アプリケーションの DNS ポリシーを持つ DNS サーバー負荷分散を使用してこのシナリオ例では、DNS サーバーは、シアトルの Web サーバー アドレス、ダラス Web サーバーのアドレス、時間の 25%、シカゴの Web サーバーのアドレスで時刻の 25% で時間の 50% です。

したがっての DNS サーバーが受信する 4 つのクエリごとに、応答する 2 つの応答でシアトルとダラスおよびシカゴに対して 1 つずつのします。

DNS のポリシーを使用した負荷分散と考えられる問題の 1 つは、DNS クライアントとの競合回避モジュール/LDNS、負荷分散のため、クライアントまたはリゾルバー送信しないクエリを DNS サーバーに干渉することができる DNS レコードのキャッシュです。

負荷分散をする必要がある DNS レコードの time \ へ記述 Live \(TTL\) 小さい値を使用してこの動作の影響を軽減できます。

### <a name="how-to-configure-application-load-balancing"></a>アプリケーションの負荷分散を構成する方法

次のセクションでは、アプリケーションの負荷分散に DNS ポリシーを構成する方法を説明します。

#### <a name="create-the-zone-scopes"></a>ゾーンのスコープを作成します。

ホストされているデータ センターのゾーン contosogiftservices.com のスコープを作成する必要があります。

ゾーンのスコープは、ゾーンの一意のインスタンスです。 DNS ゾーンには、複数のゾーンのスコープ、DNS レコードの独自セットが含まれている各ゾーンのスコープを持つことができます。 同じレコードは、別の IP アドレスを持つ複数のスコープまたは同じ IP アドレスに存在することができます。

>[!NOTE]
>既定では、ゾーンのスコープは、DNS ゾーンに存在します。 このゾーンのスコープは、ゾーンと同じ名前を持つし、従来の DNS 操作は、このスコープで動作します。

次の Windows PowerShell コマンドを使用すると、ゾーンのスコープを作成します。
    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "SeattleZoneScope"
    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DallasZoneScope"
    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "ChicagoZoneScope"

詳細については、次を参照してください[追加 DnsServerZoneScope。](https://technet.microsoft.com/library/mt126267.aspx)

####<a name="bkmk_records"></a>レコードをゾーンのスコープに追加します。

ゾーンのスコープに web サーバーのホストを表すレコードを追加する必要がありますようになりました。

**SeattleZoneScope**、シアトルのデータ センターにある IP アドレス、192.0.0.1 レコード www.contosogiftservices.com を追加することができます。

**ChicagoZoneScope**、シカゴのデータ センターで IP アドレス 182.0.0.1 で同じレコード \(www.contosogiftservices.com\) を追加することができます。

同様に、 **DallasZoneScope**、シカゴのデータ センターで 162.0.0.1 の IP アドレスを持つレコード \(www.contosogiftservices.com\) を追加することができます。

次の Windows PowerShell コマンドを使用して、レコードをゾーンのスコープに追加することができます。
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "SeattleZoneScope
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "182.0.0.1" -ZoneScope "ChicagoZoneScope"
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "162.0.0.1" -ZoneScope "DallasZoneScope"
    

詳細については、次を参照してください。[追加 DnsServerResourceRecord](https://technet.microsoft.com/library/jj649925.aspx)します。

####<a name="bkmk_policies"></a>DNS ポリシーを作成します。

パーティション (ゾーン スコープ) を作成したレコードを追加した後、contosogiftservices.com に対するクエリの 50% はシアトルのデータ センター内の Web サーバーの IP アドレスに応答して、残りの部分はシカゴとダラス データ センター間で均等に分散できるように、これらのスコープに受信したクエリを分散する DNS ポリシーを作成する必要があります。

次の Windows PowerShell コマンドを使用すると、これら 3 つのデータ センター間でアプリケーションのトラフィックを分散する DNS ポリシーを作成します。

>[!NOTE]
>式の下の例で – ゾーン範囲ゾーン"SeattleZoneScope、2、ChicagoZoneScope、1 になります。DallasZoneScope、1"DNS サーバーを構成パラメーターの組み合わせを含む配列で \ < ZoneScope\ > \ < weight\ > します。
    
    Add-DnsServerQueryResolutionPolicy -Name "AmericaPolicy" -Action ALLOW – -ZoneScope "SeattleZoneScope,2;ChicagoZoneScope,1;DallasZoneScope,1" -ZoneName "contosogiftservices.com"
    

詳細については、次を参照してください。[追加 DnsServerQueryResolutionPolicy](https://technet.microsoft.com/library/mt126273.aspx)します。  

次の 3 つの異なるデータ センター内の Web サーバー間で分散アプリケーションの負荷を提供する DNS のポリシーは正常に作成できるようになりました。

要件を作成できます何千もの DNS のポリシーに従って、トラフィックの管理、および DNS サーバーを再起動しなくても - 受信したクエリで、すべての新しいポリシーが動的 - 適用します。