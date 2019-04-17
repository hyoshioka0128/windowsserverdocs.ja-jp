---
title: DNS のポリシーを使用して Split-Brain DNS の展開
description: このトピックでは、DNS ポリシー シナリオ ガイドの Windows Server 2016 の一部
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: a255a4a5-c1a0-4edc-b41a-211bae397e3c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0b25ac752ea347f4d184628eb26bc7e297443306
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-split-brain-dns-deployment"></a>Split\ ブレイン DNS 展開用の DNS ポリシーを使用します。

>Windows Server 2016 の適用対象:

このトピックを使用すると、Windows server DNS のポリシーを構成する方法について&reg;2016 スプリット ブレイン DNS 展開で、1 つの 2 つのバージョンが存在するゾーンの組織のイントラネット上のユーザーに内部のいずれかと、外部ユーザーは、通常、インターネット上のユーザーの 1 つです。

>[!NOTE]
>Split\ ブレイン DNS の展開を Active Directory 統合 DNS ゾーンの DNS のポリシーを使用する方法については、次を参照してください。[DNS のポリシーを使用して Split-Brain Active Directory 内の DNS](dns-sb-with-ad.md)します。

以前は、このシナリオは、DNS 管理者が異なる 2 つの DNS サーバー、各内部および外部のユーザーのセットごとにサービスを提供する管理が必要です。 この場合、専用で、ゾーン内のいくつかのレコードが split\ brained またはゾーン (内部および外部) の両方のインスタンスが同じ親ドメインに委任された、管理の難点ようになりました。 

スプリット ブレイン展開用の別の構成シナリオでは、選択的の再帰コントロールは DNS 名前解決用です。 状況によっては、企業の DNS サーバーもする必要があります、外部のユーザーの権限を持つネーム サーバーとして機能し、再帰をブロック中に、内部ユーザー用のインターネット経由で再帰的な解決を実行する必要があります。 

このトピックには、次のセクションが含まれています。

- [例の DNS Split-Brain 展開](#bkmk_sbexample)
- [DNS オプションを選択再帰コントロールの例](#bkmk_recursion)

##<a name="bkmk_sbexample"></a>例の DNS Split-Brain 展開
スプリット ブレイン DNS の既に説明したシナリオを実現する DNS ポリシーを使用する方法の例を次に示します。

このセクションには、次のトピックが含まれています。

- [どの DNS Split-Brain 展開の仕組み](#bkmk_sbhow)
- [DNS を構成する方法 Split-Brain 展開](#bkmk_sbconfigure)


この例では、1 つ架空の会社で www.career.contoso.com 求人 Web サイトを保持する Contoso を使用します。

サイトでは、内部の求人が利用可能な内部ユーザー用の 1 つ、2 つのバージョンがあります。 この内部サイトでは、ローカル IP アドレス 10.0.0.39 で使用できます。 

2 番目のバージョンは、パブリック IP アドレス 65.55.39.10 利用可能な同じサイトのパブリック バージョンです。

DNS のポリシーがない場合、これら 2 つの個別の Windows Server DNS サーバーでゾーンをホストし、それらを個別に管理、管理者が必要です。 

DNS ポリシーを使用してこれらのゾーンできますでホストされるよう、同じ DNS サーバー。  

次の図は、このシナリオを示しています。

![Split-BrainDNS の展開](../../media/DNS-Split-Brain/Dns-Split-Brain-01.jpg)  


##<a name="bkmk_sbhow"></a>どの DNS Split-Brain 展開の仕組み

DNS サーバーが必要な DNS ポリシーで構成されると、各名前解決の要求は、DNS サーバー上のポリシーに対して評価されます。

サーバーのインターフェイスは、内部および外部のクライアントを区別するために、この例では、条件として使用されます。

クエリを受信する対象サーバーのインターフェイスには、任意のポリシーが一致すると、クエリに応答する、関連付けられているゾーンのスコープが使用されます。 

したがって、この例では、DNS クエリでプライベート IP (10.0.0.56 が受信 www.career.contoso.com)、内部の IP アドレスを含む DNS 応答を受信します。パブリック ネットワーク インターフェイスで受信 DNS クエリのゾーンの既定のスコープ (これは通常のクエリの解決策と同じ) のパブリック IP アドレスを含む DNS 応答を受信します。  

##<a name="bkmk_sbconfigure"></a>DNS を構成する方法 Split-Brain 展開
DNS を構成する Split-Brain 展開用の DNS ポリシーを使用すると、次の手順を使用する必要があります。

- [ゾーンのスコープを作成します。](#bkmk_zscopes)  
- [レコードをゾーンのスコープに追加します。](#bkmk_records)  
- [DNS ポリシーを作成します。](#bkmk_policies)

次のセクションでは、詳細な構成手順を提供します。

>[!IMPORTANT]
>次のセクションでには、多くのパラメーターの値例にはが含まれている Windows PowerShell コマンド例にはが含まれます。 これらのコマンドを実行する前に、展開に適切な値を持つこれらのコマンドで値の例を置き換えることを確認します。 

###<a name="bkmk_zscopes"></a>ゾーンのスコープを作成します。

ゾーンのスコープは、ゾーンの一意のインスタンスです。 DNS ゾーンには、複数のゾーンのスコープ、DNS レコードの独自セットが含まれている各ゾーンのスコープを持つことができます。 同じレコードは、別の IP アドレスを持つ複数のスコープまたは同じ IP アドレスに存在することができます。 

>[!NOTE]
>既定では、ゾーンのスコープは、DNS ゾーンに存在します。 このゾーンのスコープは、ゾーンと同じ名前を持つし、従来の DNS 操作は、このスコープで動作します。 この既定のゾーンのスコープでは、www.career.contoso.com の外部のバージョンをホストします。

次のコマンド例を使用すると、ゾーンのスコープ contoso.com、内部ゾーン スコープを作成するのにパーティションを作成します。 www.career.contoso.com の内部バージョンを保持する、内部ゾーン スコープが使用されます。

`Add-DnsServerZoneScope -ZoneName "contoso.com" -Name "internal"`

詳細については、次を参照してください[追加 DnsServerZoneScope。](https://technet.microsoft.com/library/mt126267.aspx)

###<a name="bkmk_records"></a>レコードをゾーンのスコープに追加します。

次の手順では、(外部クライアント向け)、2 つのゾーン スコープの内部に Web サーバーのホストと既定値を表すレコードを追加します。 

内部のゾーンのスコープ、レコード**www.career.contoso.com**プライベート IP アドレスは、IP アドレス、10.0.0.39 の追加既定のゾーン スコープで同じレコードを**www.career.contoso.com**、65.55.39.10 IP アドレスを追加します。

いいえ**– ゾーン範囲ゾーン**レコードがゾーンの既定のスコープに追加されるときに、次の例のコマンドにパラメーターが含まれています。 これは、バニラのゾーンにレコードを追加すると同様です。

`
Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "65.55.39.10"
`
`
Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "10.0.0.39” -ZoneScope "internal"
`

詳細については、次を参照してください。[追加 DnsServerResourceRecord](https://technet.microsoft.com/library/jj649925.aspx)します。

###<a name="bkmk_policies"></a>DNS ポリシーを作成します。

外部ネットワークおよび内部ネットワーク用のサーバー インターフェイスを識別すると、ゾーンのスコープを作成した、内部および外部のゾーンのスコープを接続する DNS ポリシーを作成する必要があります。

>[!NOTE]
>この例では、条件として、サーバー インターフェイスを使用して、内部および外部のクライアントを区別します。 内部および外部のクライアントを区別するために別の方法を条件としてクライアントのサブネットを使ってです。 内部のクライアントが属しているサブネットを特定できる場合は、クライアントのサブネットに基づいて区別するために DNS ポリシーを構成できます。 クライアントのサブネットの条件を使用したトラフィック管理を構成する方法については、次を参照してください。[地理的な場所ベースのトラフィック管理のプライマリ サーバーの DNS ポリシーを使用して](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/scenario--use-dns-policy-for-geo-location-based-traffic-management-with-primary-servers)します。

DNS サーバーは、プライベート インターフェイスでクエリを受け取った場合は、内部ゾーン スコープから DNS クエリの応答が返されます。

>[!NOTE]
>ポリシーの既定のゾーンのスコープをマッピングするため必要はありません。 

前の図に示すように、次のコマンド例では、10.0.0.56 はプライベート ネットワーク インターフェイスで、IP アドレスです。

`Add-DnsServerQueryResolutionPolicy -Name "SplitBrainZonePolicy" -Action ALLOW -ServerInterface "eq,10.0.0.56" -ZoneScope "internal,1" -ZoneName contoso.com`

詳細については、次を参照してください。[追加 DnsServerQueryResolutionPolicy](https://technet.microsoft.com/library/mt126273.aspx)します。  


## <a name="bkmk_recursion"></a>DNS オプションを選択再帰コントロールの例

DNS オプションを選択再帰コントロールの既に説明したシナリオを実現する DNS ポリシーを使用する方法の例を次に示します。

このセクションには、次のトピックが含まれています。

- [どの DNS 選択的な再帰制御のしくみ](#bkmk_recursionhow)
- [DNS オプションを選択再帰コントロールを構成する方法](#bkmk_recursionconfigure)

この例では、同じ架空の企業で www.career.contoso.com で求人 Web サイトを保持する Contoso、前の例に示すようを使用します。

DNS スプリット ブレイン展開例では、同じ DNS サーバーは、外部および内部の両方のクライアントに応答し、さまざまな回答を提供します。 

一部の DNS 展開では、外部クライアントの権限を持つネーム サーバーとして機能するだけでなく、内部クライアントの再帰的名前解決を実行すると同じ DNS サーバーを必要があります。 このような状況は、DNS のオプションを選択再帰コントロールと呼ばれます。

Windows Server の以前のバージョンで再帰を有効にするものでは DNS サーバーは、すべてのゾーンの全体でそれが有効になっています。 外部クエリには、DNS サーバーがリッスンしても、いる再帰 DNS サーバーにオープンに競合回避モジュールを行う内部および外部の両方のクライアント、有効です。 

オープンに競合回避モジュールは、リソースの枯渇を受ける可能性があります、リフレクション攻撃を作成する悪意のあるクライアントが悪用される可能性として構成されている DNS サーバー。 

このため、Contoso の DNS 管理者は外部クライアントの再帰的名前解決を実行する contoso.com の DNS サーバーを必要はありません。 のみ必要がある内部クライアントの再帰コントロールの中に、外部クライアントの再帰コントロールをブロックすることができます。 

次の図は、このシナリオを示しています。

![オプションを選択再帰コントロール](../../media/DNS-Split-Brain/Dns-Split-Brain-02.jpg) 


### <a name="bkmk_recursionhow"></a>どの DNS 選択的な再帰制御のしくみ

Contoso の DNS サーバーの権限のないクエリが受信した場合、し、www.microsoft.com は、名前解決の要求は、DNS サーバー上のポリシーに対して評価などです。 

ポリシー レベル、ゾーンのため、これらのクエリは、任意のゾーンにも属さない、\ (で定義されているスプリット ブレイン example\) は評価されません。 

DNS サーバーは、再帰ポリシーとプライベート インターフェイスの一致に受信したクエリを評価、**SplitBrainRecursionPolicy**します。 このポリシーは、再帰が有効になっている再帰スコープを指しています。

DNS サーバーは、インターネットから www.microsoft.com の回答を取得する再帰を実行し、ローカルで応答をキャッシュします。 

外部インターフェイス、ない DNS のポリシーの一致、および既定の再帰設定 - ここでは、クエリを受け取った場合**無効になっている**-を適用します。

これにより、サーバーが内部クライアントのリゾルバーをキャッシュとして機能しています中に、外部のクライアントのオープンに競合回避モジュールとして動作しています。 

### <a name="bkmk_recursionconfigure"></a>DNS オプションを選択再帰コントロールを構成する方法

コントロールを構成する DNS 選択的な再帰 DNS ポリシーを使用して、次の手順を使用する必要があります。

- [DNS の再帰スコープを作成します](#bkmk_recscopes)
- [DNS の再帰ポリシーを作成します。](#bkmk_recpolicy)

#### <a name="bkmk_recscopes"></a>DNS の再帰スコープを作成します

再帰のスコープは、DNS サーバーで再帰を制御する設定のグループの一意のインスタンスです。 再帰スコープは、フォワーダの一覧が含まれていて、再帰が有効になっているかどうかを指定します。 DNS サーバーは、多くの再帰スコープを持つことができます。 

従来の再帰設定、フォワーダーの一覧は、既定の再帰範囲として呼ばれます。 追加または既定の名前のドットで識別される再帰スコープを削除することはできません \("."\).

この例では、既定の再帰設定が無効に、再帰が有効になっている内部クライアントの新しい再帰スコープを作成します。

    
    Set-DnsServerRecursionScope -Name . -EnableRecursion $False
    Add-DnsServerRecursionScope -Name "InternalClients" -EnableRecursion $True 
    

詳細については、次を参照してください[追加 DnsServerRecursionScope。](https://technet.microsoft.com/library/mt126268.aspx)

#### <a name="bkmk_recpolicy"></a>DNS の再帰ポリシーを作成します。

DNS サーバーを特定の条件に一致するクエリのセットに対して再帰スコープを選択再帰ポリシーを作成できます。 

DNS サーバーがいくつかのクエリの権限を持っていない場合は、DNS サーバーの再帰ポリシーで [クエリを解決する方法を制御できます。 

この例では、再帰が有効になっている内部再帰スコープは、プライベート ネットワーク インターフェイスに関連付けられました。

次のコマンド例を使用して、DNS の再帰ポリシーを構成することができます。

    
    Add-DnsServerQueryResolutionPolicy -Name "SplitBrainRecursionPolicy" -Action ALLOW -ApplyOnRecursion -RecursionScope "InternalClients" -ServerInterfaceIP  "EQ,10.0.0.39"
    

詳細については、次を参照してください。[追加 DnsServerQueryResolutionPolicy](https://technet.microsoft.com/library/mt126273.aspx)します。

今すぐ、DNS サーバーは、内部クライアントに対して有効にするオプションを選択再帰コントロールとスプリット ブレイン ネーム サーバーまたは DNS サーバーのいずれかの必要な DNS ポリシーで構成されます。

要件を作成できます何千もの DNS のポリシーに従って、トラフィックの管理、および DNS サーバーを再起動しなくても - 受信したクエリで、すべての新しいポリシーが動的 - 適用します。 

詳細については、次を参照してください。[DNS ポリシー シナリオ ガイド](DNS-Policy-Scenario-Guide.md)します。
