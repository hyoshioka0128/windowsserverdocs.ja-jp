---
title: DNS ポリシーの概要
description: このトピックは、Windows Server 2016 の DNS ポリシーシナリオガイドに含まれています。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 566bc270-81c7-48c3-a904-3cba942ad463
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 687864619c981b3ab8d24ef540c759bc29314c90
ms.sourcegitcommit: 6f968368c12b9dd699c197afb3a3d13c2211f85b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/26/2019
ms.locfileid: "68544667"
---
# <a name="dns-policies-overview"></a>DNS ポリシーの概要

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Windows Server 2016 で新しく追加された DNS ポリシーについて説明します。 Geo ロケーションベースのトラフィック管理に dns ポリシーを使用したり、時間に基づくインテリジェント DNS 応答を使用して、分割\-ブレイン展開用に構成された単一の dns サーバーを管理したり、dns クエリにフィルターを適用したりできます。 これらの機能の詳細については、次の項目を参照してください。

-   **アプリケーションの負荷分散。** 異なる場所にアプリケーションの複数のインスタンスをデプロイした場合は、DNS ポリシーを使用して、異なるアプリケーションインスタンス間でトラフィックの負荷を分散し、アプリケーションのトラフィック負荷を動的に割り当てることができます。

-   **地理的\-な場所ベースのトラフィック管理。** DNS ポリシーを使用すると、クライアントが接続しようとしているリソースの地理的な場所に基づいて、プライマリおよびセカンダリ DNS サーバーが DNS クライアントクエリに応答できるようになります。クライアントは、最も近いセンター. 

-   **スプリットブレイン DNS。** Split\-ブレイン dns を使用すると、dns レコードは同じ dns サーバー上の異なるゾーンスコープに分割され、dns クライアントが内部クライアントであるか外部クライアントであるかに基づいて応答を受信します。 Active Directory 統合ゾーンまた\-はスタンドアロン dns サーバーのゾーン用に分割ブレイン DNS を構成できます。

-   **除外.** 指定した条件に基づいてクエリフィルターを作成するように DNS ポリシーを構成できます。 Dns ポリシーのクエリフィルターを使用すると、dns クエリを送信する dns クエリと dns クライアントに基づいて、カスタムの方法で応答するように DNS サーバーを構成できます。 
-   **捜査.** Dns ポリシーを使用して、悪意のある dns クライアントを\-、接続しようとしているコンピューターにリダイレクトするのではなく、存在しない IP アドレスにリダイレクトすることができます。

-   **時間ベースのリダイレクト。** DNS ポリシーを使用すると、1日の時間に基づく DNS ポリシーを使用して、アプリケーションの異なる地理的に分散したインスタンスにアプリケーショントラフィックを分散させることができます。

## <a name="new-concepts"></a>新しい概念  
上記のシナリオをサポートするポリシーを作成するには、ゾーン内のレコードのグループ、ネットワーク上のクライアントのグループを、他の要素間で識別できるようにする必要があります。 これらの要素は、次の新しい DNS オブジェクトによって表されます。  

- **クライアントサブネット:** クライアントサブネットオブジェクトは、クエリが DNS サーバーに送信される IPv4 または IPv6 サブネットを表します。 サブネットを作成して、後で要求の送信元のサブネットに基づいて適用するポリシーを定義することができます。 たとえば、スプリットブレイン DNS シナリオでは、 <em>www.microsoft.com</em>などの名前の解決要求に対して、内部サブネットからのクライアントへの内部 IP アドレスと、外部サブネット内のクライアントに対する別の ip アドレスを使用して応答できます。

- **再帰スコープ:** 再帰スコープは、DNS サーバー上の再帰を制御する設定のグループの一意のインスタンスです。 再帰のスコープは、フォワーダの一覧が含まれていて、再帰が有効になっているかどうかを指定します。 DNS サーバーは、多くの再帰スコープを持つことができます。 DNS サーバーの再帰ポリシーを使用すると、一連のクエリの再帰スコープを選択できます。 DNS サーバーが特定のクエリに対して権限を持っていない場合、DNS サーバーの再帰ポリシーを使用して、クエリの解決方法を制御できます。 使用するフォワーダーと再帰を使用するかどうかを指定できます。

- **ゾーンのスコープ:** dns ゾーンには複数のゾーンスコープがあり、それぞれのゾーンスコープには独自の dns レコードセットが含まれます。 同じレコードが複数のスコープに存在し、IP アドレスが異なる場合があります。 また、ゾーンの転送は、ゾーンのスコープレベルで行われます。 つまり、プライマリゾーンのゾーンスコープからのレコードは、セカンダリゾーンの同じゾーンスコープに転送されます。

## <a name="types-of-policy"></a>ポリシーの種類

DNS ポリシーは、レベルと種類で分けられます。 クエリの解決ポリシーを使用して、クエリの処理方法を定義したり、ゾーン転送ポリシーを使用してゾーン転送の実行方法を定義したりできます。 各ポリシーの種類は、サーバーレベルまたはゾーンレベルで適用できます。

### <a name="query-resolution-policies"></a>クエリ解決ポリシー

Dns クエリ解決ポリシーを使用して、DNS サーバーが受信解決クエリを処理する方法を指定できます。 すべての DNS クエリ解決ポリシーには、次の要素が含まれています。  

|フィールド|説明|設定可能な値|  
|---------|---------------|-------------------|  
|**名前**|ポリシー名|-最大256文字<br />-ファイル名に有効な任意の文字を含めることができます。|  
|**State**|ポリシーの状態|-Enable (既定値)<br />-Disabled|  
|**Level**|ポリシーレベル|-サーバー<br />-ゾーン|  
|**処理順序**|クエリがレベル別に分類され、に適用されると、クエリが条件に一致する最初のポリシーがサーバーによって検索され、クエリに適用されます。|-数値<br />-同じレベルを含み、値に適用されるポリシーごとの一意の値|  
|**操作**|DNS サーバーによって実行されるアクション|-Allow (ゾーンレベルの既定値)<br />-Deny (サーバーレベルでは既定)<br />-無視|  
|**条件**|ポリシーの条件 (またはその両方) とポリシーを適用するために満たす条件の一覧|-Condition 演算子 (AND/OR)<br />-条件の一覧 (下の条件表を参照)|  
|**Scope**|スコープごとのゾーンスコープと重み付け値の一覧。 加重値は、負荷分散ディストリビューションに使用されます。 たとえば、この一覧に重み付けが3で、datacenter2 が weight の datacenter1 が含まれている場合、サーバーは8件の要求のうち3倍のレコードで datacentre1 から応答します。|-ゾーンスコープの一覧 (名前別) と重み|  

> [!NOTE]
> サーバーレベルのポリシーでは、アクションとして **[拒否]** または **[無視]** の値のみを指定できます。

DNS ポリシーの条件フィールドは、次の2つの要素で構成されています。


|              名前               |                                         説明                                          |                                                                                                                               サンプル値                                                                                                                               |
|---------------------------------|----------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        **クライアントサブネット**        | 定義済みのクライアントのサブネットの名前です。 クエリの送信元となるサブネットを確認するために使用します。 |                             -   **EQ、スペイン、フランス**-サブネットがスペインまたはフランスとして識別された場合、true に解決されます。<br />-   **NE, カナダ, メキシコ**-クライアントサブネットがカナダとメキシコ以外のサブネットの場合、true に解決されます。                             |
|     **トランスポートプロトコル**      |        トランスポート プロトコル クエリで使用をします。 有効なエントリは**UDP**と**TCP**です。        |                                                                                                                    -   **EQ、TCP**<br />-   **EQ、UDP**                                                                                                                     |
|      **インターネットプロトコル**      |        クエリで使用されるネットワーク プロトコルです。 使用可能なエントリは**IPv4**と**IPv6**です。        |                                                                                                                   -   **EQ、IPv4**<br />-   **EQ、IPv6**                                                                                                                    |
| **サーバーインターフェイスの IP アドレス** |                   受信 DNS サーバーのネットワークインターフェイスの IP アドレス                   |                                                                                                              -   **EQ、10.0.0.1**<br />-   **EQ、192.168.1.1**                                                                                                              |
|            **ここに**             |            クエリ内のレコードの FQDN。ワイルドカードを使用する可能性があります。            | -   **EQ、www. contoso .com** -クエリが<em>www.contoso.com</em> FQDN を解決しようとしている場合にのみ true に解決されます。<br />-   **EQ、\*contoso.com、\*. woodgrove.com** -クエリが*contoso.com***または***woodgrove.com*で終わる任意のレコードに対するものである場合は、true に解決されます。 |
|         **クエリの種類**          |                          クエリ対象のレコードの種類 (A、SRV、TXT)                          |                                                  -   **EQ、txt、srv** -クエリが TXT レコード**また**は srv レコードを要求している場合、true に解決されます。<br />-   **EQ、mx** -クエリが mx レコードを要求している場合は、true に解決されます。                                                   |
|         **時刻**         |                              クエリが受信された時刻                               |                                                                    -   **EQ、10:00-12:00、22:00-23:00** -クエリが午前10時と正午の間、**または**10PM と午後11時の間で受信される場合は、true に解決されます。                                                                    |

上の表を開始点として使用すると、次の表を使用して、任意の種類のレコードのクエリを照合するために使用される条件を定義できますが、10.0.0.0/24 サブネットのクライアントから送信される contoso.com ドメインの SRV レコードは、8から午後10時までの間 TCP 経由で送信されます。interface 10.0.0.3:  

|名前|[値]|  
|--------|---------|  
|クライアントサブネット|EQ、10.0.0.0/24|  
|トランスポートプロトコル|EQ、TCP|  
|サーバーインターフェイスの IP アドレス|EQ、10.0.0.3|  
|FQDN|EQ、*. contoso .com|  
|クエリの種類|NE、SRV|  
|時刻|EQ、20:00-22:00|  

同じレベルの複数のクエリ解決ポリシーを作成するには、処理順序に異なる値が設定されている必要があります。 複数のポリシーを使用できる場合、DNS サーバーは次の方法で受信クエリを処理します。  

![DNS ポリシーの処理](../../media/DNS-Policies-Overview/DNSQueryResolutionPolicyFlowchart.png)  

### <a name="recursion-policies"></a>再帰ポリシー  
再帰ポリシーは、特別な**種類**のサーバーレベルポリシーです。 再帰ポリシーは、DNS サーバーがクエリに対して再帰を実行する方法を制御します。 再帰ポリシーは、クエリ処理が再帰パスに到達した場合にのみ適用されます。 クエリのセットに対して、再帰の値として [拒否] または [無視] を選択できます。 または、一連のクエリに対して一連のフォワーダーを選択することもできます。  

再帰ポリシーを使用すると、スプリットブレイン DNS 構成を実装できます。 この構成では、DNS サーバーはクエリのクライアントのセットに対して再帰を実行しますが、DNS サーバーはそのクエリの他のクライアントに対して再帰を実行しません。  

再帰ポリシーには、次の表に示す要素と共に、通常の DNS クエリ解決ポリシーに含まれるものと同じ要素が含まれています。  

|名前|説明|  
|--------|---------------|  
|**再帰で適用する**|このポリシーが再帰にのみ使用されることを指定します。|  
|**再帰のスコープ**|再帰スコープの名前。|  

> [!NOTE]  
> 再帰ポリシーは、サーバーレベルでのみ作成できます。  

### <a name="zone-transfer-policies"></a>ゾーン転送ポリシー  
ゾーン転送ポリシーは、DNS サーバーでゾーン転送が許可されるかどうかを制御します。 サーバーレベルまたはゾーンレベルのいずれかで、ゾーン転送のポリシーを作成できます。 サーバーレベルのポリシーは、DNS サーバーで実行されるすべてのゾーン転送クエリに適用されます。 ゾーンレベルのポリシーは、DNS サーバーでホストされているゾーンに対するクエリにのみ適用されます。 ゾーンレベルポリシーの最も一般的な用途は、ブロックリストまたはセーフリストを実装することです。  

> [!NOTE]  
> ゾーン転送ポリシーでは、アクションとして、拒否または無視のみを使用できます。  

次のサーバーレベルのゾーン転送ポリシーを使用して、特定のサブネットからの contoso.com ドメインのゾーン転送を拒否できます。  

```  
Add-DnsServerZoneTransferPolicy -Name DenyTransferOfContosoToFabrikam -Zone contoso.com -Action DENY -ClientSubnet "EQ,192.168.1.0/24"  
```  

同じレベルの複数のゾーン転送ポリシーを作成するには、処理順序に異なる値が設定されている必要があります。 複数のポリシーを使用できる場合、DNS サーバーは次の方法で受信クエリを処理します。  

![複数のゾーン転送ポリシーの DNS プロセス](../../media/DNS-Policies-Overview/DNSPolicyZone.png)  

## <a name="managing-dns-policies"></a>DNS ポリシーを管理する  
DNS ポリシーは、PowerShell を使用して作成および管理できます。 次の例では、DNS ポリシーを使用して構成できるさまざまなサンプルシナリオについて説明します。  

### <a name="traffic-management"></a>トラフィック管理  
DNS クライアントの場所に応じて、FQDN に基づいてトラフィックを別のサーバーに転送できます。 次の例では、トラフィック管理ポリシーを作成して、特定のサブネットから北米のデータセンターに、別のサブネットから欧州のデータセンターに顧客を誘導する方法を示します。  

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

スクリプトの最初の2行は、北米とヨーロッパのクライアントサブネットオブジェクトを作成します。 の後の2行で、contoso.com ドメイン内にゾーンスコープを作成します (リージョンごとに1つ)。 その後の2行は、ww.contoso.com を別の IP アドレス (ヨーロッパの場合は1つ) に、もう1つは北米に関連付けられているレコードを各ゾーンに作成します。 最後に、スクリプトの最後の行で、2つの DNS クエリ解決ポリシーを作成します。1つは北米サブネットに適用され、もう1つはヨーロッパサブネットに適用されます。  

### <a name="block-queries-for-a-domain"></a>ドメインのクエリをブロックする  
DNS クエリ解決ポリシーを使用して、ドメインに対するクエリをブロックできます。 次の例では、treyresearch.net に対するすべてのクエリをブロックしています。  

```  
Add-DnsServerQueryResolutionPolicy -Name "BlackholePolicy" -Action IGNORE -FQDN "EQ,*.treyresearch.com"  
```  

### <a name="block-queries-from-a-subnet"></a>サブネットからのクエリをブロックする  
特定のサブネットからのクエリをブロックすることもできます。 次のスクリプトでは、172.0.33.0/24 のサブネットを作成し、そのサブネットからのすべてのクエリを無視するポリシーを作成します。  

```  
Add-DnsServerClientSubnet -Name "MaliciousSubnet06" -IPv4Subnet 172.0.33.0/24  
Add-DnsServerQueryResolutionPolicy -Name "BlackholePolicyMalicious06" -Action IGNORE -ClientSubnet  "EQ,MaliciousSubnet06"  
```  

### <a name="allow-recursion-for-internal-clients"></a>内部クライアントの再帰を許可する  
DNS クエリ解決ポリシーを使用して再帰を制御できます。 次のサンプルを使用すると、内部クライアントの再帰を有効にしながら、スプリットブレインシナリオで外部クライアントに対して無効にすることができます。  

```  
Set-DnsServerRecursionScope -Name . -EnableRecursion $False   
Add-DnsServerRecursionScope -Name "InternalClients" -EnableRecursion $True  
Add-DnsServerQueryResolutionPolicy -Name "SplitBrainPolicy" -Action ALLOW -ApplyOnRecursion -RecursionScope "InternalClients" -ServerInterfaceIP  "EQ,10.0.0.34"  
```  

スクリプトの最初の行では、既定の再帰スコープが変更されます。これは単に "." という名前です。(ドット) を使用して再帰を無効にします。 2行目では、再帰が有効になっている*Internalclients*という名前の再帰スコープを作成します。 3行目では、IP アドレスとして10.0.0.34 を持つサーバーインターフェイスを介して送信されるすべてのクエリに、新しく作成された再帰スコープを適用するポリシーを作成します。  

### <a name="create-a-server-level-zone-transfer-policy"></a>サーバーレベルのゾーン転送ポリシーを作成する  
DNS ゾーン転送ポリシーを使用すると、より詳細な形式でゾーン転送を制御できます。 次のサンプルスクリプトを使用すると、特定のサブネット上の任意のサーバーでゾーンを転送できます。  

```  
Add-DnsServerClientSubnet -Name "AllowedSubnet" -IPv4Subnet 172.21.33.0/24  
Add-DnsServerZoneTransferPolicy -Name "NorthAmericaPolicy" -Action IGNORE -ClientSubnet "ne,AllowedSubnet"  
```  

スクリプトの最初の行では、IP ブロック 172.21.33.0/24 を使用して、 *Allowedsubnet*という名前のサブネットオブジェクトを作成します。 2行目では、前に作成したサブネット上の任意の DNS サーバーへのゾーン転送を許可するゾーン転送ポリシーを作成します。  

### <a name="create-a-zone-level-zone-transfer-policy"></a>ゾーンレベルのゾーン転送ポリシーを作成する  
ゾーンレベルのゾーン転送ポリシーを作成することもできます。 次の例では、IP アドレスが10.0.0.33 のサーバーインターフェイスから受信した contoso.com のゾーン転送要求は無視されます。  

```  
Add-DnsServerZoneTransferPolicy -Name "InternalTransfers" -Action IGNORE -ServerInterfaceIP "eq,10.0.0.33" -PassThru -ZoneName "contoso.com"  
```  

## <a name="dns-policy-scenarios"></a>DNS ポリシーのシナリオ

特定のシナリオで DNS ポリシーを使用する方法については、このガイドの次のトピックを参照してください。

- [プライマリサーバーを使用した地理的な場所ベースのトラフィック管理に DNS ポリシーを使用する](primary-geo-location.md)  
- [プライマリとセカンダリのデプロイを使用した地理的な場所ベースのトラフィック管理に DNS ポリシーを使用する](primary-secondary-geo-location.md)  
- [1日の時間に基づくインテリジェント DNS 応答に DNS ポリシーを使用する](dns-tod-intelligent.md)
- [Azure Cloud App Server を使用した時間帯に基づく DNS 応答](dns-tod-azure-cloud-app-server.md)
- [スプリットブレイン DNS 展開に DNS ポリシーを使用する](split-brain-DNS-deployment.md)
- [Active Directory でのスプリットブレイン DNS に DNS ポリシーを使用する](dns-sb-with-ad.md)
- [Dns クエリにフィルターを適用するために DNS ポリシーを使用する](apply-filters-on-dns-queries.md)
- [アプリケーションの負荷分散に DNS ポリシーを使用する](app-lb.md)
- [Geo ロケーションを認識するアプリケーションの負荷分散に DNS ポリシーを使用する](app-lb-geo.md)

## <a name="using-dns-policy-on-read-only-domain-controllers"></a>読み取り専用ドメインコントローラーでの DNS ポリシーの使用

DNS ポリシーは、読み取り専用ドメインコントローラーと互換性があります。 新しい DNS ポリシーを読み取り専用ドメインコントローラーに読み込むには、DNS サーバーサービスを再起動する必要があることに注意してください。 書き込み可能なドメインコントローラーでは、これは必要ありません。
