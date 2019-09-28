---
title: 地理的な場所を認識するアプリケーションの負荷分散に DNS ポリシーを使用する
description: このトピックは、Windows Server 2016 の DNS ポリシーシナリオガイドに含まれています。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: b6e679c6-4398-496c-88bc-115099f3a819
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ea3f959612de0f2bc56a887ba73aba47f1d3f141
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406217"
---
# <a name="use-dns-policy-for-application-load-balancing-with-geo-location-awareness"></a>地理的な場所を認識するアプリケーションの負荷分散に DNS ポリシーを使用する

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、geo ロケーションを認識するアプリケーションの負荷を分散するように DNS ポリシーを構成する方法について説明します。

このガイドの前述の「[アプリケーションの負荷分散に DNS ポリシーを使用](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/app-lb)する」では、架空の会社である Contoso ギフトサービスの例を使用します。これは、オンライン贈答サービスを提供し、contosogiftservices.com という名前の Web サイトを持っています。 Contoso ギフト Services は、シアトル、ワシントン州、シカゴ、IL、およびダラス (テキサス州) にある北米データセンターのサーバー間で、オンライン Web アプリケーションの負荷を分散します。

>[!NOTE]
>このシナリオの手順を実行する前に、「[アプリケーションの負荷分散に DNS ポリシーを使用](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/app-lb)する」をよく理解しておくことをお勧めします。

このトピックでは、地理的な場所の認識を含む新しいサンプルデプロイの基礎として、架空の企業およびネットワークインフラストラクチャを使用します。

この例では、Contoso のギフトサービスは地球全体でのプレゼンスの拡張に成功しています。

北米と同様に、会社はヨーロッパのデータセンターでホストされている web サーバーを持つようになりました。

Contoso ギフトサービス DNS 管理者は、米国の DNS ポリシー実装と同様の方法で欧州データセンターのアプリケーション負荷分散を構成する必要があります。アプリケーショントラフィックは、にある Web サーバー間で分散されます。ダブリン、アイルランド、アムステルダム、Holland など。

また、DNS 管理者は、世界中の他の場所からのすべてのクエリを、すべてのデータセンター間で均等に分散させる必要があります。

次のセクションでは、独自のネットワーク上の Contoso の DNS 管理者と同様の目標を達成する方法について説明します。

## <a name="how-to-configure-application-load-balancing-with-geo-location-awareness"></a>Geo ロケーションを認識するアプリケーションの負荷分散を構成する方法

次のセクションでは、地理的な場所を認識するアプリケーションの負荷分散の DNS ポリシーを構成する方法について説明します。

>[!IMPORTANT]
>以下のセクションには、多くのパラメーターの値の例を含む Windows PowerShell コマンドの例が含まれています。 これらのコマンドで値の例は、これらのコマンドを実行する前に、展開に対応する値を置き換えることを確認します。

### <a name="bkmk_clientsubnets"></a>DNS クライアントサブネットを作成する

まず、北米とヨーロッパのリージョンのサブネットまたは IP アドレス空間を特定する必要があります。

この情報は、地理的 IP のマップから取得できます。 これらの Geo IP ディストリビューションに基づいて、DNS クライアントサブネットを作成する必要があります。

DNS クライアントのサブネットは、クエリが DNS サーバーに送信元 IPv4 または IPv6 サブネットの論理グループです。

次の Windows PowerShell コマンドを使用すると、DNS クライアントのサブネットを作成します。 

    
    Add-DnsServerClientSubnet -Name "AmericaSubnet" -IPv4Subnet 192.0.0.0/24,182.0.0.0/24
    Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet 141.1.0.0/24,151.1.0.0/24
    
詳細については、次を参照してください。 [追加 DnsServerClientSubnet](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverclientsubnet?view=win10-ps)します。

### <a name="bkmk_zscopes2"></a>ゾーンのスコープを作成する

クライアントサブネットが配置されたら、ゾーンの contosogiftservices.com をデータセンターごとに異なるゾーンスコープに分割する必要があります。

ゾーンのスコープは、ゾーンの一意のインスタンスです。 DNS ゾーンは複数のゾーンスコープを持つことができ、各ゾーンスコープには独自の DNS レコードセットが含まれます。 同じレコードが複数のスコープに存在し、異なる IP アドレスまたは同じ IP アドレスを持つことができます。

>[!NOTE]
>既定では、ゾーンのスコープは、DNS ゾーンに存在します。 このゾーンのスコープでは、ゾーンと同じ名前と、従来の DNS の機能がこのスコープで動作します。

アプリケーションの負荷分散に関する前のシナリオでは、北米のデータセンターに対して3つのゾーンのスコープを構成する方法を示します。

次のコマンドを使用して、ダブリンとアムステルダムのデータセンター用にそれぞれ1つずつ、さらに2つのゾーンスコープを作成できます。 

これらのゾーンスコープは、同じゾーン内の既存の3つの北米ゾーンスコープに変更を加えることなく追加できます。 また、これらのゾーンスコープを作成した後で、DNS サーバーを再起動する必要はありません。

次の Windows PowerShell コマンドを使用すると、ゾーンのスコープを作成します。

    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DublinZoneScope"
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "AmsterdamZoneScope"
    

詳細については、次を参照してください [追加 DnsServerZoneScope。](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)

### <a name="bkmk_records2"></a>ゾーンのスコープにレコードを追加する

次に、web サーバーホストを表すレコードをゾーンのスコープに追加する必要があります。

米国のデータセンターのレコードは、前のシナリオで追加されました。 次の Windows PowerShell コマンドを使用して、ヨーロッパのデータセンターのゾーンのスコープにレコードを追加できます。
 
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "151.1.0.1" -ZoneScope "DublinZoneScope”
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "141.1.0.1" -ZoneScope "AmsterdamZoneScope"
    

詳細については、次を参照してください。 [追加 DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)します。

### <a name="bkmk_policies2"></a>DNS ポリシーを作成する

パーティション (ゾーンスコープ) を作成し、レコードを追加したら、これらのスコープに対して受信クエリを分散する DNS ポリシーを作成する必要があります。

この例では、異なるデータセンター内のアプリケーションサーバー間でのクエリの分散は、次の条件を満たしています。

1. 北米クライアントサブネットのソースから DNS クエリを受信すると、DNS 応答の 50% がシアトルデータセンターを指し、応答の 25% がシカゴのデータセンターに送信され、さらにその残りの 25% がダラスデータセンターに送信されます。
2. 欧州クライアントサブネットのソースから DNS クエリを受信すると、DNS 応答の 50% がダブリンデータセンターをポイントし、DNS 応答の 50% がアムステルダムデータセンターをポイントします。
3. クエリが世界中の他の場所からのものである場合、DNS 応答は5つのデータセンター全体に分散されます。

これらの DNS ポリシーを実装するには、次の Windows PowerShell コマンドを使用します。

    
    Add-DnsServerQueryResolutionPolicy -Name "AmericaLBPolicy" -Action ALLOW -ClientSubnet "eq,AmericaSubnet" -ZoneScope "SeattleZoneScope,2;ChicagoZoneScope,1; TexasZoneScope,1" -ZoneName "contosogiftservices.com" –ProcessingOrder 1
    
    Add-DnsServerQueryResolutionPolicy -Name "EuropeLBPolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "DublinZoneScope,1;AmsterdamZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 2
    
    Add-DnsServerQueryResolutionPolicy -Name "WorldWidePolicy" -Action ALLOW -FQDN "eq,*.contoso.com" -ZoneScope "SeattleZoneScope,1;ChicagoZoneScope,1; TexasZoneScope,1;DublinZoneScope,1;AmsterdamZoneScope,1" -ZoneName "contosogiftservices.com" -ProcessingOrder 3
    
    

詳細については、次を参照してください。 [追加 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)します。

これで、5つの異なるデータセンターにある複数の大陸に配置されている Web サーバー全体で、アプリケーションの負荷分散を実現する DNS ポリシーが作成されました。

何千もの DNS のポリシーに合わせて作成できます、トラフィック管理の要件、DNS サーバーを再起動しなくても - 受信したクエリで、すべての新しいポリシーが動的 - 適用されます。
