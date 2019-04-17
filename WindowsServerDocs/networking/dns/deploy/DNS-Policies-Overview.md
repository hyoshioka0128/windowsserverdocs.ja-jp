---
title: DNS のポリシーの概要
description: このトピックでは、DNS ポリシー シナリオ ガイドの Windows Server 2016 の一部
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 566bc270-81c7-48c3-a904-3cba942ad463
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 06086bbd7edc2fa489805eb5075062332e002ab4
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="dns-policies-overview"></a>DNS のポリシーの概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、Windows Server 2016 の新機能は、DNS のポリシーについて説明します。 地理的な場所ベースのトラフィック管理を 1 日の時間に基づくインテリジェント DNS 応答の DNS ポリシーを使用する DNS クエリにフィルターを適用する、split\ ブレイン展開用に構成された 1 台の DNS サーバーを管理することができます。 次の項目では、これらの機能について詳しく説明します。

-   **アプリケーションの負荷を分散します。** 異なる場所にあるアプリケーションの複数のインスタンスを展開したときに DNS ポリシーを使用するアプリケーションのトラフィックの負荷を動的に割り当てる、別のアプリケーションのインスタンス間でトラフィックの負荷を分散することができます。

-   **Geo\ 場所ベースのトラフィック管理をします。** 最も近いリソースの IP アドレスを持つクライアントに提供する、クライアントと、クライアントが、接続しようとするのにリソースの両方の地理的な場所に基づいて、DNS クライアント クエリに応答するのにプライマリとセカンダリの DNS サーバーを許可するように、DNS のポリシーを使用することができます。 

-   **ブレイン DNS を分割します。** 、Split\ ブレイン DNS に DNS レコードは、同じ DNS サーバーで、別のゾーンのスコープに分割 DNS クライアント応答を受信するかどうかに基づいて、クライアントの内部または外部のクライアント。 スタンドアロン DNS サーバーで、Active Directory 統合ゾーンやゾーンに対する split\ ブレイン DNS を構成できます。

-   **フィルタ リングします。** 指定した条件に基づいてクエリ フィルターを作成する DNS ポリシーを構成することができます。 DNS ポリシーでクエリ フィルターを使用すると、DNS クエリと、DNS クエリを送信する DNS クライアントに基づくカスタムの方法で応答する DNS サーバーを構成できます。 
-   **フォレンジックします。** アクセスしようとしているコンピューターに誘導するのではなく、以外、存在しない IP アドレスに悪意のある DNS クライアントをリダイレクトする DNS ポリシーを使用することができます。

-   **リダイレクトを 1 日の時間に基づいています。** アプリケーションの別の地理的に分散インスタンス間で 1 日の時間に基づく DNS ポリシーを使用してアプリケーションのトラフィックを分散する DNS ポリシーを使用することができます。

## <a name="new-concepts"></a>新しい概念  
上記のシナリオをサポートするためにポリシーを作成するためには、ゾーン、その他の要素間のネットワーク上のクライアントのグループ内のレコードのグループを識別できる必要があります。 これらの要素は、次の新しい DNS オブジェクトによって表されます。  

- **クライアントのサブネット:**クライアントのサブネット オブジェクトが元のクエリが DNS サーバーに送信された、IPv4 または IPv6 サブネットを表します。 後で、要求に由来サブネットに基づいて適用するポリシーを定義するサブネットを作成することができます。 たとえば、スプリット ブレイン DNS シナリオなどの名前の解決の要求で*www.microsoft.com*内部サブネットからクライアントに内部 IP アドレスとサブネットの外部でクライアントを別の IP アドレスに回答できます。

- **再帰スコープ:**再帰のスコープは、DNS サーバーで再帰を制御する設定のグループの一意のインスタンス。 再帰スコープは、フォワーダの一覧が含まれていて、再帰が有効になっているかどうかを指定します。 DNS サーバーは、多くの再帰スコープを持つことができます。 DNS サーバーの再帰ポリシーを使用すると、クエリのセットに対して再帰適用範囲を選択できます。 特定の DNS サーバーは権限がない場合、クエリの場合、DNS サーバーの再帰ポリシーを使用すると、それらのクエリを解決する方法を制御できます。 どのフォワーダを使用し、再帰を使用するかどうかを指定することができます。

- **ゾーンのスコープ:** DNS ゾーンで DNS レコードの独自セットが含まれている各ゾーンのスコープを持つ、複数のゾーン スコープを持つことができます。 同じレコードは、異なる IP アドレスを持つ複数のスコープに存在することができます。 また、ゾーン転送がゾーン スコープ レベルで行われます。 つまり、プライマリ ゾーンのゾーンのスコープからのレコードは、セカンダリ ゾーンで同じゾーンのスコープに転送されます。

## <a name="types-of-policy"></a>ポリシーの種類

DNS のポリシーは、レベルと入力して分類されます。 クエリの処理方法を定義するクエリ解決ポリシーとゾーン転送を行う方法を定義するゾーン転送のポリシーを使用することができます。 各ポリシーの種類、サーバー レベルまたはゾーン レベルで適用できます。
  
### <a name="query-resolution-policies"></a>クエリ解決ポリシー

DNS クエリ解決ポリシーを使用すると、クエリが DNS サーバーによって処理される着信解像度を指定します。 すべての DNS クエリ解決ポリシーには、次の要素が含まれています。  
  
|フィールド|説明|指定可能な値|  
|---------|---------------|-------------------|  
|**名**|ポリシー名|-を 256 文字以内<br />のファイル名の有効な任意の文字を含めることができます。|  
|**状態**|ポリシーの状態|-(既定) を有効にします。<br />-無効|  
|**レベル**|ポリシー レベル|-サーバー<br />ゾーン|  
|**処理順序**|サーバーは、最初のポリシーをクエリ条件に一致し、適用を照会することを検索クエリのレベルによって分類されに適用される、|-数値<br />のポリシーを含む同じレベルの値に適用されるごと一意の値|  
|**アクション**|DNS サーバーで実行されるアクション|-(ゾーン レベルの既定値) を許可します。<br />-(サーバー レベルの既定値) の拒否します。<br />-を無視します。|  
|**条件**|ポリシーの条件 (/) と条件を満たす必要があるポリシーを適用するための一覧|条件演算子 (/)<br />-(次の条件の表を参照してください) 条件の一覧|  
|**スコープ**|ゾーンのスコープとスコープごとの重み付け値の一覧です。 加重値は、負荷分散の配布に使用されます。 たとえば、この一覧には、3 の重み付き datacenter1 と 5 の重み付き datacenter2 が含まれている場合、サーバーが応答レコードに 8 つの要求を 3 回 datacentre1 から|(名) をゾーンのスコープと重みのリスト|  

> [!NOTE]
> サーバー レベルのポリシーでは、値を持つことができますのみ**拒否**または**無視**として動作します。

DNS のポリシーの条件のフィールドは、2 つの要素で構成されます。

|名|説明|値の例|
|--------|---------------|-----------------|
|**クライアントのサブネット**|トランスポート プロトコルのクエリで使用します。 可能なエントリは**UDP**と**TCP**|-   **EQ、スペイン、フランス**-サブネットがスペインまたはフランスのいずれかとして識別された場合は true に解決<br />-   **NE、カナダ、メキシコ**-クライアントのサブネットがどのサブネット カナダおよびメキシコ以外の場合は true に解決|  
|**トランスポート プロトコル**|トランスポート プロトコルのクエリで使用します。 可能なエントリは**UDP**と**TCP**|-   **EQ、TCP**<br />-   **EQ、UDP**|  
|**インターネット プロトコル**|クエリで使用されるネットワーク プロトコルです。 可能なエントリは**IPv4**と**IPv6**|-   **EQ、IPv4**<br />-   **EQ、IPv6**|  
|**サーバーのインターフェイスの IP アドレス**|入力方向の DNS サーバーのネットワーク インターフェイスの IP アドレス|-   **EQ、10.0.0.1**<br />-   **EQ、192.168.1.1**|  
|**FQDN**|ワイルドカードを使用する可能性はありますが、クエリ内のレコードの FQDN|-   **EQ、www.contoso.com** -解決 >.30 rue 場合にのみ、クエリはしようとして解決するには、*www.contoso.com* FQDN<br />-   **EQ,\*.contoso.com,\*.woodgrove.com** -クエリで終わるすべてのレコードの場合は true に解決*contoso.com***または***woodgrove.com*|  
|**クエリの種類**|(A、SVR、TXT) に照会しているレコードの種類|-   **EQ、TXT、SRV** -クエリが、TXT を要求している場合、解決 >.30 rue**または**SRV レコード<br />-   **EQ、MX** -クエリで MX レコードを要求している場合、解決 >.30 rue|  
|**1 日の時間**|クエリが受信した時刻|-   **EQ、10時 00分-12時 00分: 00 22-23時 00分**の午前 10 時と正午間でクエリを受信した場合、解決 >.30 rue**または**午後 10 時と午後 11 時間|  
  
上のテーブルを使用して開始点として、レコードが 8、インターフェイス 10.0.0.3 から午後 10 時の間で TCP 経由で 10.0.0.0/24 サブネット内のクライアントから送ら contoso.com ドメインの SRV レコードの種類のクエリに一致するために使用する条件を定義する次の表を使用できます。  
  
|名|値|  
|--------|---------|  
|クライアントのサブネット|EQ、10.0.0.0/24|  
|トランスポート プロトコル|EQ、TCP|  
|サーバーのインターフェイスの IP アドレス|EQ、10.0.0.3|  
|FQDN|EQ、*. contoso.com|  
|クエリの種類|NE、SRV|  
|1 日の時間|EQ、20時 00分-22時 00分|  
  
処理順序に別の値を持っていればは、複数のクエリ、同じレベルの解像度のポリシーを作成することができます。 複数のポリシーが使用できる場合は、DNS サーバーは、次のように受信したクエリを処理します。  
  
![DNS のポリシーの処理](../../media/DNS-Policies-Overview/DNSQueryResolutionPolicyFlowchart.png)  
  
### <a name="recursion-policies"></a>再帰ポリシー  
再帰ポリシーは、特別な**種類**サーバー レベルのポリシーのします。 再帰ポリシーでは、DNS サーバーがクエリに対して再帰を実行する方法を制御します。 再帰ポリシーは、クエリの処理が再帰のパスに達したときにのみ適用されます。 再帰クエリのセットを拒否または無視の値を選択できます。 または、一連のクエリのフォワーダのセットを選択できます。  
  
実装に再帰ポリシーを使用することができます、Split-brain DNS 構成します。 この構成では、DNS サーバーがそのクエリの他のクライアントの再帰を実行していないときに、DNS サーバーは一連のクエリ、クライアントの再帰を実行します。  
  
再帰ポリシーでは、正規の DNS クエリ解決ポリシーが含まれている次の表に、要素と共に、同じ要素があります。  
  
|名|説明|  
|--------|---------------|  
|**再帰を適用します。**|このポリシーは再帰に対してのみ使用する必要がありますを指定します。|  
|**再帰のスコープ**|再帰のスコープの名前です。|  
  
> [!NOTE]  
> 再帰ポリシーは、サーバー レベルでのみ作成できます。  
  
### <a name="zone-transfer-policies"></a>ゾーン転送のポリシー  
ゾーン転送のポリシーは、ゾーン転送が許可されているかどうか、または、DNS サーバーではなくを制御します。 サーバー レベルまたはゾーン レベルのいずれかでゾーン転送のポリシーを作成することができます。 サーバー レベルのポリシーは、DNS サーバーで発生するすべてのゾーン転送クエリを適用します。 ゾーン レベルのポリシーは、DNS サーバーでホストされているゾーンのクエリにのみ適用されます。 ゾーン レベルのポリシーの最も一般的な用途は、ブロックされているか安全のリストを実装します。  
  
> [!NOTE]  
> ゾーン転送のポリシーのみ使用できます拒否するか無視する動作として。  
  
サーバー レベルのゾーン転送ポリシーを使用して、特定のサブネットから contoso.com ドメインのゾーン転送を拒否できます。  
  
```  
Add-DnsServerZoneTransferPolicy -Name DenyTransferOfCOnsotostoFabrikam -Zone contoso.com -Action DENY -ClientSubnet "EQ,192.168.1.0/24"  
```  
  
処理順序に別の値を持っていればは、複数のゾーン転送、同じレベルのポリシーを作成することができます。 複数のポリシーが使用できる場合は、DNS サーバーは、次のように受信したクエリを処理します。  
  
![複数のゾーン転送のポリシーの DNS プロセス](../../media/DNS-Policies-Overview/DNSPolicyZone.png)  
  
## <a name="managing-dns-policies"></a>DNS のポリシーの管理  
作成し、PowerShell を使用して DNS のポリシーを管理することができます。 次の例は、DNS のポリシーで構成できる別のサンプル シナリオを参照してください。  
  
### <a name="traffic-management"></a>トラフィックの管理  
DNS クライアントの場所に応じて、異なるサーバーに FQDN に基づいて、トラフィックを送信できます。 次の例は、トラフィックの北アメリカ データ センターに特定のサブネットとヨーロッパ データ センターに別のサブネットからのユーザーに誘導して管理ポリシーを作成する方法を示しています。  
  
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
  
最初の 2 つの行のスクリプトは、クライアントに北米とヨーロッパで活動のサブネット オブジェクトを作成します。 その後、次の 2 つの行は、各地域の 1 つ、contoso.com ドメイン内のゾーンのスコープを作成します。 その後、次の 2 つの行は、別の IP アドレス、ヨーロッパの 1 つ、North America 用 ww.contoso.com に関連付けている各ゾーンにレコードを作成します。 最後に、最後の行のスクリプトは、次の 2 つ DNS クエリ解決ポリシー、北米サブネットは、ヨーロッパのサブネットに別に適用される 1 つを作成します。  
  
### <a name="block-queries-for-a-domain"></a>ドメインのブロックのクエリ  
ドメインにブロック クエリを DNS クエリ解決ポリシーを使用することができます。 次の例では、treyresearch.net すべてのクエリをブロックします。  
  
```  
Add-DnsServerQueryResolutionPolicy -Name "BlackholePolicy" -Action IGNORE -FQDN "EQ,*.treyresearch.com"  
```  
  
### <a name="block-queries-from-a-subnet"></a>サブネットからブロック クエリ  
特定のサブネットからクエリをブロックすることもできます。 次のスクリプトは、172.0.33.0/24 サブネットを作成し、そのサブネットから送られているすべてのクエリを無視するポリシーを作成します。  
  
```  
Add-DnsServerClientSubnet -Name "MaliciousSubnet06" -IPv4Subnet 172.0.33.0/24  
Add-DnsServerQueryResolutionPolicy -Name "BlackholePolicyMalicious06" -Action IGNORE -ClientSubnet  "EQ,MaliciousSubnet06"  
```  
  
### <a name="allow-recursion-for-internal-clients"></a>内部クライアントの再帰を許可します。  
DNS クエリ解決ポリシーを使用して、再帰を制御できます。 スプリット ブレイン シナリオでは外部クライアントの無効にしているときに、内部クライアントの再帰を有効にするのには、以下のサンプルを使用できます。  
  
```  
Set-DnsServerRecursionScope -Name . -EnableRecursion $False   
Add-DnsServerRecursionScope -Name "InternalClients" -EnableRecursion $True  
Add-DnsServerQueryResolutionPolicy -Name "SplitBrainPolicy" -Action ALLOW -ApplyOnRecursion -RecursionScope "InternalClients" -ServerInterfaceIP  "EQ,10.0.0.34"  
```  
  
スクリプトの最初の行は、単にという名前の既定の再帰スコープを変更"です"。(ドット) 再帰を無効にします。 2 行目をという名前の再帰スコープを作成*InternalClients*再帰が有効になっているとします。 3 番目の行を適用するポリシーを作成して、新しくを IP アドレスとして 10.0.0.34 を持つサーバー インターフェイスを介して取り込まれたすべてのクエリを再帰スコープを作成します。  
  
### <a name="create-a-server-level-zone-transfer-policy"></a>サーバー レベルのゾーン転送のポリシーを作成します。  
DNS ゾーン転送のポリシーを使用してより詳細な形式でゾーン転送を制御できます。 次のサンプル スクリプトは、特定のサブネット上の任意のサーバーのゾーン転送を許可するように使用できます。  
  
```  
Add-DnsServerClientSubnet -Name "AllowedSubnet" -IPv4Subnet 172.21.33.0/24  
Add-DnsServerZoneTransferPolicy -Name "NorthAmericaPolicy" -Action IGNORE -ClientSubnet "ne,AllowedSubnet"  
```  
  
スクリプトの最初の行をという名前のサブネット オブジェクトを作成*AllowedSubnet* ip アドレス ブロック 172.21.33.0/24 です。 2 行目では、任意の DNS サーバーに以前に作成した、サブネット上のゾーン転送を許可するように、ゾーン転送のポリシーを作成します。  
  
### <a name="create-a-zone-level-zone-transfer-policy"></a>ゾーン レベルのゾーン転送のポリシーを作成します。  
ゾーン レベルのゾーン転送のポリシーを作成することもできます。 次の例では、contoso.com 10.0.0.33 の IP アドレスが割り当てられたサーバーのインターフェイスからのゾーン転送のすべての要求を無視します。  
  
```  
Add-DnsServerZoneTransferPolicy -Name "InternalTransfers" -Action IGNORE -ServerInterfaceIP "ne,10.0.0.33" -PassThru -ZoneName "contoso.com"  
```  
  
## <a name="dns-policy-scenarios"></a>DNS ポリシー シナリオ

特定のシナリオの DNS のポリシーを使用する方法については、このガイドの次のトピックを参照してください。

- [DNS ポリシーを使用しての地理的な場所ベースのプライマリ サーバーのトラフィック管理](primary-geo-location.md)  
- [地理的な場所ベースのプライマリ セカンダリ展開でのトラフィック管理に DNS ポリシーを使用します。](primary-secondary-geo-location.md)  
- [1 日の時間に基づくインテリジェント DNS 応答の DNS ポリシーを使用します。](dns-tod-intelligent.md)
- [クラウド アプリケーション サーバーを Azure で 1 日の時間に基づく DNS 応答](dns-tod-azure-cloud-app-server.md)
- [DNS のポリシーを使用して Split-Brain DNS の展開](split-brain-DNS-deployment.md)
- [DNS のポリシーを使用して Split-Brain Active Directory 内の DNS](dns-sb-with-ad.md)
- [DNS クエリにフィルターを適用するために DNS ポリシーを使用します。](apply-filters-on-dns-queries.md)
- [アプリケーションの負荷分散に DNS ポリシーを使用します。](app-lb.md)
- [アプリケーションで負荷分散を地理的な位置認識に DNS ポリシーを使用します。](app-lb-geo.md)


