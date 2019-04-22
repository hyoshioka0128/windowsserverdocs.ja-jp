---
title: DNS ポリシーの概要
description: このトピックは、DNS ポリシー シナリオ ガイドの Windows Server 2016 の一部です。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 566bc270-81c7-48c3-a904-3cba942ad463
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ad8fa904f43bb51871e5063eaddedd0762d54d95
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814303"
---
# <a name="dns-policies-overview"></a>DNS ポリシーの概要

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用すると、Windows Server 2016 の新機能は、DNS のポリシーについて説明します。 DNS のポリシーを使用するには、地理的場所ベースの管理トラフィック分割用に構成された 1 つの DNS サーバーを管理する、1 日の時間に基づくインテリジェントの DNS 応答の\-ブレイン展開、DNS クエリでは、その他にフィルターを適用します。 次のものでは、これらの機能について詳しく説明します。

-   **アプリケーションの負荷を分散します。** 異なる場所にあるアプリケーションの複数のインスタンスを展開している場合は、アプリケーションのトラフィックの負荷を動的に割り当て、別のアプリケーション インスタンス間でトラフィックの負荷を分散する DNS ポリシーを使用できます。

-   **Geo\-場所ベースのトラフィック管理します。** クライアントに提供する、最も近いの IP アドレス、クライアントとクライアントが接続しようとするのにリソースの両方の地理的な場所に基づいて、DNS クライアント クエリに応答するのにプライマリとセカンダリの DNS サーバーを許可するのに DNS ポリシーを使用することができます。リソースです。 

-   **DNS の脳に分割します。** 分割は\-ブレイン DNS では、DNS レコードは、同じ DNS サーバー上の別のゾーン スコープに分割され、DNS クライアントは、クライアントは、内部または外部クライアントかどうかに基づいて応答を受信します。 分割を構成する\-Active Directory 統合ゾーンやスタンドアロン DNS サーバーでゾーンに対する DNS の脳です。

-   **フィルター処理します。** 指定した条件に基づくクエリ フィルターを作成する DNS ポリシーを構成することができます。 DNS のポリシーでのクエリ フィルターを使用すると、カスタムの DNS クエリを送信する DNS クライアントと DNS クエリに基づく方法で応答する DNS サーバーを構成できます。 
-   **科学捜査します。** 非に悪意のある DNS クライアントをリダイレクトする DNS ポリシーを使用することができます\-アクセスしようとしているコンピューターに転送することではなく IP アドレスが存在します。

-   **リダイレクトを時間帯に基づいています。** DNS のポリシーを使用すると、1 日の時間に基づく DNS ポリシーを使用して、アプリケーションの別の地理的に分散インスタンス アプリケーション トラフィックを分散させます。

## <a name="new-concepts"></a>新しい概念  
上記のシナリオをサポートするためのポリシーを作成するには、ゾーン、その他の要素間のネットワーク上のクライアントのグループ内のレコードのグループを識別できるようにする必要があります。 これらの要素は、次の新しい DNS オブジェクトによって表されます。  

- **クライアントのサブネット:** クライアントのサブネット オブジェクトは、クエリが DNS サーバーに送信元 IPv4 または IPv6 サブネットを表します。 後で、要求に由来するサブネットに基づいて適用するポリシーを定義するサブネットを作成することができます。 たとえば、スプリット ブレイン DNS シナリオなどの名前の解決の要求で*www.microsoft.com*から内部サブネットは、クライアントに内部 IP アドレスと外部のクライアントに別の IP アドレスに応答することができますサブネット。

- **再帰のスコープ:** 再帰スコープは、DNS サーバーで再帰を制御する設定のグループの一意のインスタンス。 再帰のスコープは、フォワーダの一覧が含まれていて、再帰が有効になっているかどうかを指定します。 DNS サーバーは、多くの再帰スコープを持つことができます。 DNS サーバーの再帰ポリシーを使用すると、一連のクエリの再帰スコープを選択できます。 特定の DNS サーバーが権限のない場合、クエリ、DNS サーバーの再帰ポリシーを使用すると、これらのクエリを解決する方法を制御できます。 どのフォワーダーを使用し、再帰を使用するかどうかを指定できます。

- **ゾーンのスコープ:** DNS ゾーンは、独自の DNS レコード セットを格納している各ゾーンのスコープを持つ、複数のゾーン スコープを持つことができます。 同じレコードが別の IP アドレスを持つ、複数のスコープ内に存在できます。 また、ゾーン転送は、ゾーンのスコープ レベルで実行されます。 つまり、プライマリ ゾーンのゾーンのスコープからレコードをセカンダリ ゾーンで同じゾーンのスコープに転送されます。

## <a name="types-of-policy"></a>ポリシーの種類

DNS のポリシーは、レベル、および種類別に分類されます。 クエリの処理方法を定義するクエリ解決ポリシーとゾーン転送を行う方法を定義するゾーン転送のポリシーを使用することができます。 各ポリシーの種類、サーバー レベルまたはゾーン レベルで適用できます。
  
### <a name="query-resolution-policies"></a>クエリ解決ポリシー

DNS クエリ解決ポリシーを使用すると、クエリが DNS サーバーによって処理される着信解像度を指定します。 すべての DNS クエリ解決ポリシーには、次の要素が含まれています。  
  
|フィールド|説明|設定可能な値|  
|---------|---------------|-------------------|  
|**名前**|ポリシー名|-256 文字にします。<br />-ファイル名の有効な任意の文字を含めることができます。|  
|**状態**|ポリシーの状態|-(既定値) を有効にします。<br />-無効|  
|**Level**|ポリシー レベル|-サーバー<br />ゾーン|  
|**処理順序**|クエリはレベルによって分類されで適用され、サーバーは、最初にポリシーをクエリは、条件に一致して、クエリに適用されますを検索します|-数値<br />レベルは同じで、値に適用されるポリシーを格納しているごとの一意の値|  
|**操作**|DNS サーバーで実行されるアクション|-(ゾーン レベルの既定値) を許可します。<br />Deny (サーバー レベルの既定値)<br />-無視します。|  
|**条件**|ポリシーの条件 (または) および適用するポリシーを満たすための条件の一覧|条件演算子 (または)<br />-条件 (以下の条件の表を参照してください) の一覧|  
|**Scope**|ゾーンのスコープとスコープごとの加重値の一覧。 加重計算される値は、負荷分散の配布のために使用されます。 たとえば、datacenter1 3 の重みと重みの 5 datacenter2 にこの一覧が含まれている場合、サーバーは応答のレコードを含む 8 つの要求から 3 回 datacentre1 から|ゾーンのスコープ (その名前) と重みのリスト|  

> [!NOTE]
> サーバー レベルのポリシーでは、値を持つことができますのみ**Deny**または**無視**アクションとして。

DNS のポリシーの条件フィールドは、2 つの要素で構成されます。

|名前|説明|サンプルの値|
|--------|---------------|-----------------|
|**クライアントのサブネット**|定義済みのクライアントのサブネットの名前です。 クエリの送信元となるサブネットを確認するために使用します。|-   **EQ、スペイン、フランス**-スペインまたはフランスのいずれかとして、サブネットが識別される場合は true に解決されます。<br />-   **NE、カナダ、メキシコ**-クライアントのサブネットがカナダ、メキシコ以外の任意のサブネットである場合は true に解決されます|  
|**トランスポート プロトコル**|トランスポート プロトコル クエリで使用をします。 可能なエントリは**UDP**と**TCP**|-   **EQ、TCP**<br />-   **EQ、UDP**|  
|**インターネット プロトコル**|クエリで使用されるネットワーク プロトコルです。 可能なエントリは**IPv4**と**IPv6**|-   **EQ、IPv4**<br />-   **EQ、IPv6**|  
|**サーバーのインターフェイスの IP アドレス**|受信した DNS サーバーのネットワーク インターフェイスの IP アドレス|-   **EQ、10.0.0.1**<br />-   **EQ、192.168.1.1**|  
|**FQDN**|ワイルドカードを使用する可能性があります、クエリ内のレコードの FQDN|-   **EQ、www.contoso.com** -解決数 rue クエリが解決するのにはしようとした場合にのみ、 *www.contoso.com* FQDN<br />-   **EQ、\*. contoso.com、\*. woodgrove.com** -クエリが任意のレコードで終わる場合は true に解決される*contoso.com***または***woodgrove.com*|  
|**クエリの種類**|(A、SVR、TXT) に照会しているレコードの種類|-   **EQ、TXT、SRV** -クエリは、TXT を要求している場合は true に解決される**または**SRV レコード<br />-   **EQ、MX** -クエリが MX レコードを要求している場合は true に解決されます|  
|**1 日の時間**|クエリが受信した時刻|-   **EQ、10時 00分-12時 00分 22時 00分-23時 00分**-クエリが午前 10 時と正午、間に受信した場合は true に解決される**または**午後 10 時と午後 11 時間|  
  
上記の表を使用して、開始点として、次の表にされる可能性がありますを任意の種類のレコードが 8 を午後 10 時の間に TCP 経由で 10.0.0.0/24 のサブネット内のクライアントから送信される、contoso.com ドメインの SRV レコードのクエリに一致するように使用する条件を定義します。インターフェイス 10.0.0.3:  
  
|名前|値|  
|--------|---------|  
|クライアントのサブネット|EQ,10.0.0.0/24|  
|トランスポート プロトコル|EQ、TCP|  
|サーバーのインターフェイスの IP アドレス|EQ、10.0.0.3|  
|FQDN|EQ、*.contoso.com|  
|クエリの種類|NE、SRV|  
|1 日の時間|EQ、20時 00分-22時 00分|  
  
処理順序の異なる値がある限りは、複数のクエリ、同じレベルの解決ポリシーを作成することができます。 複数のポリシーが使用できる場合は、DNS サーバーは、次のように着信クエリを処理します。  
  
![DNS のポリシーの処理](../../media/DNS-Policies-Overview/DNSQueryResolutionPolicyFlowchart.png)  
  
### <a name="recursion-policies"></a>再帰ポリシー  
再帰ポリシーは、特別な**型**のサーバー レベルのポリシー。 再帰ポリシーでは、DNS サーバーがクエリの再帰を実行する方法を制御します。 再帰ポリシーでは、クエリの処理が再帰パスに達した場合にのみ適用されます。 再帰クエリのセットを拒否または無視の値を選択できます。 また、一連のクエリのフォワーダーのセットを選択できます。  
  
再帰ポリシーを使用して、Split-brain DNS 構成を実装することができます。 この構成で DNS サーバーがそのクエリの他のクライアントの再帰を実行しないときに、DNS サーバーは一連のクエリの場合、クライアントの再帰を実行します。  
  
再帰ポリシーには、通常の DNS クエリ解決ポリシーが含まれています、次の表に、要素と同じ要素が含まれています。  
  
|名前|説明|  
|--------|---------------|  
|**再帰を適用します。**|このポリシーは再帰のみ使用する必要がありますを指定します。|  
|**再帰のスコープ**|再帰のスコープの名前。|  
  
> [!NOTE]  
> 再帰ポリシーは、サーバー レベルでのみ作成できます。  
  
### <a name="zone-transfer-policies"></a>ゾーン転送のポリシー  
ゾーン転送のポリシーは、ゾーン転送が許可されるかどうか、または、DNS サーバーではなくを制御します。 サーバー レベルまたはゾーン レベルのいずれかでは、ゾーン転送のポリシーを作成できます。 サーバー レベル ポリシーは、DNS サーバー上で発生するすべてのゾーン転送クエリに適用されます。 ゾーン レベルのポリシーは、DNS サーバーでホストされているゾーンのクエリにのみ適用されます。 ゾーン レベルのポリシーの最も一般的な用途では、ブロックされているまたはセーフ リストを実装します。  
  
> [!NOTE]  
> ゾーン転送のポリシーは、アクションとして、拒否または無視を使用できますのみ。  
  
サーバー レベルのゾーン転送ポリシーを使用すると、指定されたサブネットからの contoso.com ドメインのゾーン転送を拒否します。  
  
```  
Add-DnsServerZoneTransferPolicy -Name DenyTransferOfContosoToFabrikam -Zone contoso.com -Action DENY -ClientSubnet "EQ,192.168.1.0/24"  
```  
  
処理順序の異なる値がある限りは、複数のゾーン転送、同じレベルのポリシーを作成することができます。 複数のポリシーが使用できる場合は、DNS サーバーは、次のように着信クエリを処理します。  
  
![複数のゾーン転送のポリシーの DNS のプロセス](../../media/DNS-Policies-Overview/DNSPolicyZone.png)  
  
## <a name="managing-dns-policies"></a>DNS のポリシーを管理します。  
作成し、PowerShell を使用して DNS のポリシーを管理できます。 次の例では、DNS のポリシーを構成できるさまざまなサンプル シナリオを参照してください。  
  
### <a name="traffic-management"></a>トラフィックの管理  
DNS クライアントの場所によって異なるサーバーに FQDN に基づいてトラフィックを指示することができます。 次の例では、トラフィックを北米地域のデータ センターに特定のサブネットとヨーロッパ データ センターにもう 1 つのサブネットからお客様に出力するための管理ポリシーを作成する方法を示します。  
  
```  
Add-DnsServerClientSubnet -Name "NorthAmericaSubnet" -IPv4Subnet "172.21.33.0/24"  
Add-DnsServerClientSubnet -Name "EuropeSubnet" -IPv4Subnet "172.17.44.0/24"  
Add-DnsServerZoneScope -ZoneName "Contoso.com" -Name "NorthAmericaZoneScope"  
Add-DnsServerZoneScope -ZoneName "Contoso.com" -Name "EuropeZoneScope"  
Add-DnsServerResourceRecord -ZoneName "Contoso.com" -A -Name "www" -IPv4Address "172.17.97.97" -ZoneScope "EuropeZoneScope"  
Add-DnsServerResourceRecord -ZoneName "Contoso.com" -A -Name "www" -IPv4Address "172.21.21.21" -ZoneScope "NorthAmericaZoneScope"  
Add-DnsServerQueryResolutionPolicy -Name "NorthAmericaPolicy" -Action ALLOW -ClientSubnet "eq,NorthAmericaSubnet" -ZoneScope "NorthAmericaZoneScope,1" -ZoneName "Contoso.com"  
Add-DnsServerQueryResolutionPolicy -Name "EuropePolicy" -Action ALLOW -ClientSubnet "eq,EuropeSubnet" -ZoneScope "EuropeZoneScope,1" -ZoneName contoso.com  
```  
  
スクリプトの最初の 2 つの行は、クライアントに北米とヨーロッパのサブネット オブジェクトを作成します。 その後の 2 つの行では、リージョンごとに 1 つずつ、contoso.com ドメイン内のゾーン スコープを作成します。 その後の 2 つの行を別の IP アドレス、1 つはヨーロッパ、北米のもう 1 つに ww.contoso.com を関連付ける各ゾーンでレコードを作成します。 最後に、スクリプトの最後の行は、2 つ DNS クエリ解決ポリシー別、ヨーロッパのサブネットに北米のサブネットに適用される 1 つを作成します。  
  
### <a name="block-queries-for-a-domain"></a>ドメインのクエリがブロック  
ドメインにクエリがブロックに DNS クエリ解決ポリシーを使用することができます。 次の例では、treyresearch.net に対するすべてのクエリをブロックします。  
  
```  
Add-DnsServerQueryResolutionPolicy -Name "BlackholePolicy" -Action IGNORE -FQDN "EQ,*.treyresearch.com"  
```  
  
### <a name="block-queries-from-a-subnet"></a>サブネットからのブロックのクエリ  
特定のサブネットから送信されるクエリをブロックすることもできます。 以下のスクリプトでは、172.0.33.0/24 のサブネットを作成し、し、そのサブネットから送信されるすべてのクエリを無視するポリシーを作成します。  
  
```  
Add-DnsServerClientSubnet -Name "MaliciousSubnet06" -IPv4Subnet 172.0.33.0/24  
Add-DnsServerQueryResolutionPolicy -Name "BlackholePolicyMalicious06" -Action IGNORE -ClientSubnet  "EQ,MaliciousSubnet06"  
```  
  
### <a name="allow-recursion-for-internal-clients"></a>内部クライアントの再帰を許可します。  
DNS クエリ解決ポリシーを使用して、再帰を制御できます。 スプリット ブレイン シナリオでの外部のクライアントを無効にすること、内部クライアントの再帰を有効にするのには、以下のサンプルを使用できます。  
  
```  
Set-DnsServerRecursionScope -Name . -EnableRecursion $False   
Add-DnsServerRecursionScope -Name "InternalClients" -EnableRecursion $True  
Add-DnsServerQueryResolutionPolicy -Name "SplitBrainPolicy" -Action ALLOW -ApplyOnRecursion -RecursionScope "InternalClients" -ServerInterfaceIP  "EQ,10.0.0.34"  
```  
  
スクリプトの最初の行だけという既定の再帰スコープを変更する"."(ドット) 再帰を無効にします。 2 番目の行では、という名前の再帰スコープを作成します。 *InternalClients*再帰では有効にします。 3 番目の行を適用するポリシーを作成して、新しく作成された再帰スコープを IP アドレスとして 10.0.0.34 を持つサーバー インターフェイス通過するすべてのクエリにします。  
  
### <a name="create-a-server-level-zone-transfer-policy"></a>サーバー レベルのゾーン転送のポリシーを作成します。  
DNS ゾーン転送のポリシーを使用してより詳細な形式でゾーン転送を制御できます。 次のサンプル スクリプトは、特定のサブネット上の任意のサーバーのゾーン転送を許可を使用できます。  
  
```  
Add-DnsServerClientSubnet -Name "AllowedSubnet" -IPv4Subnet 172.21.33.0/24  
Add-DnsServerZoneTransferPolicy -Name "NorthAmericaPolicy" -Action IGNORE -ClientSubnet "ne,AllowedSubnet"  
```  
  
スクリプトの最初の行は、という名前のサブネット オブジェクトを作成します。 *AllowedSubnet* IP を持つ 172.21.33.0/24 をブロックします。 2 番目の行では、任意の DNS サーバーを以前に作成したサブネット上のゾーン転送を許可するゾーン転送のポリシーを作成します。  
  
### <a name="create-a-zone-level-zone-transfer-policy"></a>ゾーン レベルのゾーン転送のポリシーを作成します。  
ゾーン レベルのゾーン転送のポリシーを作成することもできます。 次の例では、contoso.com を 10.0.0.33 の IP アドレスを持つサーバー インターフェイスからのゾーン転送のすべての要求を無視します。  
  
```  
Add-DnsServerZoneTransferPolicy -Name "InternalTransfers" -Action IGNORE -ServerInterfaceIP "ne,10.0.0.33" -PassThru -ZoneName "contoso.com"  
```  
  
## <a name="dns-policy-scenarios"></a>DNS ポリシー シナリオ

特定のシナリオ用の DNS のポリシーを使用する方法については、このガイドでは、次のトピックを参照してください。

- [Geo ロケーションの DNS ポリシーを使用するプライマリ サーバーのトラフィック管理のベース](primary-geo-location.md)  
- [地理的場所ベースのプライマリ セカンダリ展開でのトラフィック管理用に DNS ポリシーを使用します。](primary-secondary-geo-location.md)  
- [1 日の時間に基づくインテリジェント DNS 応答の DNS ポリシーを使用します。](dns-tod-intelligent.md)
- [Azure の 1 日の時間に基づく DNS 応答のクラウド アプリケーション サーバー](dns-tod-azure-cloud-app-server.md)
- [スプリット ブレイン DNS 展開の DNS ポリシーを使用します。](split-brain-DNS-deployment.md)
- [Active Directory でスプリット ブレイン DNS の DNS ポリシーを使用します。](dns-sb-with-ad.md)
- [DNS クエリのフィルターを適用するために DNS ポリシーを使用します。](apply-filters-on-dns-queries.md)
- [アプリケーションの負荷分散に DNS ポリシーを使用します。](app-lb.md)
- [アプリケーションの負荷分散位置認識での DNS ポリシーを使用します。](app-lb-geo.md)

## <a name="using-dns-policy-on-read-only-domain-controllers"></a>読み取り専用ドメイン コント ローラーに DNS ポリシーを使用

DNS のポリシーは読み取り専用ドメイン コント ローラーとの互換性です。 DNS サーバー サービスの再起動が読み取り専用ドメイン コント ローラーに読み込まれる新しい DNS のポリシーに必要なことに注意してください。 これは、書き込み可能なドメイン コント ローラーの必要はありません。
