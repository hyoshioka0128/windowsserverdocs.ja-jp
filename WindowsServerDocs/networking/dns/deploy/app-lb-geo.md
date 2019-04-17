---
title: アプリケーションで負荷分散を地理的な位置認識に DNS ポリシーを使用します。
description: このトピックでは、DNS ポリシー シナリオ ガイドの Windows Server 2016 の一部
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: b6e679c6-4398-496c-88bc-115099f3a819
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7637d927c7b22b83053e7f9100b07581c11bafc0
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-application-load-balancing-with-geo-location-awareness"></a>アプリケーションで負荷分散を地理的な位置認識に DNS ポリシーを使用します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、負荷を分散アプリケーションに地理的な場所を認識するのに DNS ポリシーを構成するのに方法について説明します。

このガイドでは、前のトピック[アプリケーションの負荷分散に DNS ポリシーを使用して](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/app-lb)、例の架空の会社の Contoso ギフト サービス - オンライン gifting を提供するサービスの使用、およびこれが、Web サイト名前 contosogiftservices.com します。Contoso ギフト サービスはオンラインの Web アプリケーションのワシントン州シアトル、イリノイ州シカゴと米国テキサス州ダラスである北アメリカのデータ センター内のサーバー間で分散します。

>[!NOTE]
>理解して、「」トピックをお勧め[アプリケーションの負荷分散に DNS ポリシーを使用して](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/app-lb)このシナリオで」手順を実行する前にします。

このトピックは、同じ架空の企業とネットワーク インフラストラクチャを地理的な場所を認識が含まれる新しい展開例については基礎として使用します。

この例では Contoso ギフト サービスが正常に展開されて、プレゼンス世界各地います。

北米と同様に、会社のヨーロッパ データ センターでホストされる web サーバーできます。

Contoso ギフト サービスの DNS 管理者は、ヨーロッパ データ センターの分散が Dublin、アイルランド、アムステルダム、オランダ、および他の場所に配置されている Web サーバー間で分散アプリケーションのトラフィックと、米国で DNS のポリシーの実装と同様の方法でアプリケーションの負荷を構成するとします。

DNS 管理者は、すべてのデータ センター間で均等に分散世界の他の場所からのすべてのクエリを必要もあります。

次のセクションでは、独自のネットワーク上で Contoso の DNS 管理者のような目標を達成する方法を説明します。

## <a name="how-to-configure-application-load-balancing-with-geo-location-awareness"></a>アプリケーションで負荷分散を地理的な場所を認識を構成する方法

次のセクションでは、アプリケーションで負荷分散を地理的な位置認識に DNS ポリシーを構成する方法を説明します。

>[!IMPORTANT]
>次のセクションでには、多くのパラメーターの値例にはが含まれている Windows PowerShell コマンド例にはが含まれます。 これらのコマンドを実行する前に、展開に適切な値を持つこれらのコマンドで値の例を置き換えることを確認します。

###<a name="bkmk_clientsubnets"></a>DNS クライアントのサブネットを作成します。

まず、サブネットまたは IP アドレス空間の北米とヨーロッパの地域を識別する必要があります。

この情報は、地理的な IP のマップから取得できます。 これらの地理的な IP のディストリビューションに基づき、DNS クライアントのサブネットを作成する必要があります。

DNS クライアントのサブネットは、DNS サーバーにクエリの送信元 IPv4 または IPv6 サブネットの論理グループです。

次の Windows PowerShell コマンドを使用して、DNS クライアントのサブネットを作成することができます。 

    
    Add-DnsServerClientSubnet -Name "AmericaSubnet" -IPv4Subnet 192.0.0.0/24,182.0.0.0/24
    Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet 141.1.0.0/24,151.1.0.0/24
    
詳細については、次を参照してください。[追加 DnsServerClientSubnet](https://technet.microsoft.com/library/mt126261.aspx)します。

###<a name="bkmk_zscopes2"></a>ゾーンのスコープを作成します。

クライアントのサブネットがあると、後に各データ センターの別のゾーン スコープにゾーン contosogiftservices.com のパーティションを作成する必要があります。

ゾーンのスコープは、ゾーンの一意のインスタンスです。 DNS ゾーンには、複数のゾーンのスコープ、DNS レコードの独自セットが含まれている各ゾーンのスコープを持つことができます。 同じレコードは、別の IP アドレスを持つ複数のスコープまたは同じ IP アドレスに存在することができます。

>[!NOTE]
>既定では、ゾーンのスコープは、DNS ゾーンに存在します。 このゾーンのスコープは、ゾーンと同じ名前を持つし、従来の DNS 操作は、このスコープで動作します。

アプリケーションの負荷分散では、前のシナリオでは、北米でデータ センターの 3 つのゾーンのスコープを構成する方法について説明します。

以下のコマンドを使用してダブリンとアムステルダムのデータ センターの 1 つずつ 2 つの複数ゾーン スコープを作成することができます。 

これらのゾーンのスコープを変更せず、次の 3 つ既存北アメリカのゾーンのスコープが同じゾーンに追加できます。 さらに、これらのゾーンのスコープを作成した後、DNS サーバーを再起動する必要はありません。

次の Windows PowerShell コマンドを使用すると、ゾーンのスコープを作成します。

    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DublinZoneScope"
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "AmsterdamZoneScope"
    

詳細については、次を参照してください[追加 DnsServerZoneScope。](https://technet.microsoft.com/library/mt126267.aspx)

###<a name="bkmk_records2"></a>レコードをゾーンのスコープに追加します。

ゾーンのスコープに web サーバーのホストを表すレコードを追加する必要がありますようになりました。

アメリカ データ センターの記録は、前のシナリオで追加されました。 次の Windows PowerShell コマンドを使用すると、ヨーロッパ データ センターのゾーンのスコープにレコードを追加します。
 
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "151.1.0.1" -ZoneScope "DublinZoneScope”
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "141.1.0.1" -ZoneScope "AmsterdamZoneScope"
    

詳細については、次を参照してください。[追加 DnsServerResourceRecord](https://technet.microsoft.com/library/jj649925.aspx)します。

###<a name="bkmk_policies2"></a>DNS ポリシーを作成します。

パーティション (ゾーン スコープ) を作成したレコードを追加した後、これらのスコープに受信したクエリを分散する DNS ポリシーを作成する必要があります。

この例では、さまざまなデータ センター内のアプリケーション サーバーの間でクエリの配布は、次の条件を満たしています。

1. DNS 応答の 50% が、シアトルのデータ センターを指す北アメリカのクライアントのサブネットでは、移行元から DNS クエリが受信したときに、応答の 25% が、シカゴのデータ センターをポイントして、応答の残りの 25% がダラス データ センターをポイントします。
2. ヨーロッパのクライアントのサブネット内のソースから受信した場合、DNS クエリは、DNS 応答の 50% が Dublin データ センターをポイントし、DNS 応答の 50% がアムステルダムのデータ センターにポイントします。
3. クエリは、世界中の他の場所からは、DNS 応答が 5 つすべてのデータ センターに分散します。

次の Windows PowerShell コマンドを使用して、これらの DNS ポリシーを実装することができます。

    
    Add-DnsServerQueryResolutionPolicy -Name "AmericaLBPolicy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,2;ChicagoZoneScope,1; TexasZoneScope,1" -ZoneName "contosogiftservices.com" –ProcessingOrder 1
    
    Add-DnsServerQueryResolutionPolicy -Name "EuropeLBPolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "DublinZoneScope,1;AmsterdamZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 2
    
    Add-DnsServerQueryResolutionPolicy -Name "WorldWidePolicy" -Action ALLOW -FQDN "eq,*.contoso.com" -ZoneScope "SeattleZoneScope,1;ChicagoZoneScope,1; TexasZoneScope,1;DublinZoneScope,1;AmsterdamZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 3
    
    

詳細については、次を参照してください。[追加 DnsServerQueryResolutionPolicy](https://technet.microsoft.com/library/mt126273.aspx)します。

複数の大陸で 5 つの異なるデータ センターに配置されている Web サーバー間で分散アプリケーションの負荷を提供する DNS のポリシーは正常に作成できるようになりました。

要件を作成できます何千もの DNS のポリシーに従って、トラフィックの管理、および DNS サーバーを再起動しなくても - 受信したクエリで、すべての新しいポリシーが動的 - 適用します。
