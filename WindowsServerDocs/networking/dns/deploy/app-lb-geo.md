---
title: 地理的な場所を認識するアプリケーションの負荷分散に DNS ポリシーを使用する
description: このトピックは、DNS ポリシー シナリオ ガイドの Windows Server 2016 の一部です。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: b6e679c6-4398-496c-88bc-115099f3a819
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 806c0cdeedb44db44fc0ec5218124f516a6f70e5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852553"
---
# <a name="use-dns-policy-for-application-load-balancing-with-geo-location-awareness"></a>地理的な場所を認識するアプリケーションの負荷分散に DNS ポリシーを使用する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用すると、地理的位置認識と負荷分散アプリケーションに DNS ポリシーを構成するのに方法について説明します。

このガイドでは、前のトピック[DNS ポリシーを使用するアプリケーションの負荷分散の](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/app-lb)、使用してオンライン贈答を提供する架空の会社 Contoso ギフト サービス - の例のサービス、およびという名前の Web サイトを持つcontosogiftservices.com します。 Contoso ギフト サービスはオンラインの Web アプリケーション、ワシントン州シアトル、イリノイ州シカゴ、テキサス州ダラスにあるデータ センターを北米のサーバー間で分散します。

>[!NOTE]
>理解するおくと、そのトピックには勧め[DNS ポリシーを使用するアプリケーションの負荷分散の](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/app-lb)このシナリオでは、手順を実行する前にします。

このトピックでは、同じ架空の企業とネットワーク インフラストラクチャを地理的場所の認識を含む新しい展開例については、単位として使用します。

この例で、Contoso ギフト サービスは、世界各地で存在しているを正常に展開が。

北米と同様に、会社になりましたヨーロッパ データ センターでホストされる web サーバー。

Contoso ギフト サービスの DNS 管理者がアプリケーションの負荷に配置されている Web サーバー間で分散アプリケーションのトラフィックを米国で DNS のポリシーの実装と同様の方法でヨーロッパのデータ センターの分散を構成します。アイルランドのダブリン、アムステルダム、オランダ、および他の場所。

DNS 管理者は、すべてのデータ センターの間に均等に分散環境で他の場所からすべてのクエリもします。

次のセクションでは、独自のネットワーク上の Contoso の DNS 管理者のような目標を達成する方法を学習できます。

## <a name="how-to-configure-application-load-balancing-with-geo-location-awareness"></a>アプリケーションの負荷分散と地理的場所の認識を構成する方法

次のセクションでは、地理的位置認識と分散アプリケーションの負荷の DNS ポリシーを構成する方法を示します。

>[!IMPORTANT]
>次のセクションでには、多くのパラメーターの値例にはが含まれている Windows PowerShell コマンド例にはが含まれます。 これらのコマンドで値の例は、これらのコマンドを実行する前に、展開に対応する値を置き換えることを確認します。

###<a name="bkmk_clientsubnets"></a>DNS クライアントのサブネットを作成します。

まず、サブネットまたは北米およびヨーロッパのリージョンの IP アドレス空間を識別する必要があります。

この情報は、地理的 IP のマップから取得できます。 これらの地理的 IP のディストリビューションに基づき、DNS クライアントのサブネットを作成する必要があります。

DNS クライアントのサブネットは、クエリが DNS サーバーに送信元 IPv4 または IPv6 サブネットの論理グループです。

次の Windows PowerShell コマンドを使用すると、DNS クライアントのサブネットを作成します。 

    
    Add-DnsServerClientSubnet -Name "AmericaSubnet" -IPv4Subnet 192.0.0.0/24,182.0.0.0/24
    Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet 141.1.0.0/24,151.1.0.0/24
    
詳細については、次を参照してください。 [追加 DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps)します。

###<a name="bkmk_zscopes2"></a>ゾーンのスコープを作成します。

クライアントのサブネットがあると後、各データ センターの別のゾーン スコープにゾーン contosogiftservices.com をパーティション分割する必要があります。

ゾーンのスコープは、ゾーンの一意のインスタンスです。 DNS ゾーンは、独自の DNS レコード セットを格納している各ゾーンのスコープを持つ、複数のゾーン スコープを持つことができます。 同じレコードは、別の IP アドレスを持つ、複数のスコープまたは同じ IP アドレスに存在することができます。

>[!NOTE]
>既定では、ゾーンのスコープは、DNS ゾーンに存在します。 このゾーンのスコープでは、ゾーンと同じ名前と、従来の DNS の機能がこのスコープで動作します。

アプリケーションの負荷分散では、前のシナリオでは、北米でのデータ センターの次の 3 つのゾーンのスコープを構成する方法を示します。

次のコマンドでは、ダブリン、アムステルダム データ センターに対して 1 つずつ 2 つの詳細についてゾーン スコープを作成できます。 

同じゾーンで 3 つ既存北米ゾーン スコープには、何も変更せずのこれらのゾーン スコープを追加できます。 さらに、これらのゾーンのスコープを作成した後、DNS サーバーを再起動する必要はありません。

次の Windows PowerShell コマンドを使用すると、ゾーンのスコープを作成します。

    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DublinZoneScope"
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "AmsterdamZoneScope"
    

詳細については、次を参照してください [追加 DnsServerZoneScope。](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)

###<a name="bkmk_records2"></a>レコードをゾーンのスコープに追加します。

今すぐゾーン スコープに web サーバーのホストを表すレコードを追加する必要があります。

上記のシナリオでは、アメリカのデータ センターのレコードが追加されました。 次の Windows PowerShell コマンドを使用すると、ヨーロッパ データ センターのゾーンのスコープにレコードを追加します。
 
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "151.1.0.1" -ZoneScope "DublinZoneScope”
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "141.1.0.1" -ZoneScope "AmsterdamZoneScope"
    

詳細については、次を参照してください。 [追加 DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)します。

###<a name="bkmk_policies2"></a>DNS ポリシーを作成します。

パーティション (ゾーン スコープ) を作成したレコードを追加した後は、着信クエリをこれらのスコープに分散する DNS ポリシーを作成する必要があります。

この例では、さまざまなデータ センター内のアプリケーション サーバー間でクエリの分布は、次の条件を満たしています。

1. DNS 応答の 50% が、シアトルのデータ センターを指す北アメリカのクライアントのサブネットでは、ソースから DNS クエリが受信したときに、応答の 25% が、シカゴのデータ センターをポイントし、応答の残りの 25% がダラス データ センターにポイントします。
2. ヨーロッパのクライアントのサブネット内のソースから受信した場合、DNS クエリは、DNS 応答の 50% が Dublin データ センターをポイントし、DNS 応答の 50% がアムステルダム データ センターにポイントします。
3. クエリは、その他の場所からの世界では、ときに、DNS 応答は、5 つすべてのデータ センターに分散されます。

これらの DNS ポリシーを実装するために、次の Windows PowerShell コマンドを使用することができます。

    
    Add-DnsServerQueryResolutionPolicy -Name "AmericaLBPolicy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,2;ChicagoZoneScope,1; TexasZoneScope,1" -ZoneName "contosogiftservices.com" –ProcessingOrder 1
    
    Add-DnsServerQueryResolutionPolicy -Name "EuropeLBPolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "DublinZoneScope,1;AmsterdamZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 2
    
    Add-DnsServerQueryResolutionPolicy -Name "WorldWidePolicy" -Action ALLOW -FQDN "eq,*.contoso.com" -ZoneScope "SeattleZoneScope,1;ChicagoZoneScope,1; TexasZoneScope,1;DublinZoneScope,1;AmsterdamZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 3
    
    

詳細については、次を参照してください。 [追加 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)します。

複数の大陸で 5 つの異なるデータ センターに配置されている Web サーバー間で分散アプリケーションの負荷を提供する DNS ポリシーは正常に作成されました。

何千もの DNS のポリシーに合わせて作成できます、トラフィック管理の要件、DNS サーバーを再起動しなくても - 受信したクエリで、すべての新しいポリシーが動的 - 適用されます。
