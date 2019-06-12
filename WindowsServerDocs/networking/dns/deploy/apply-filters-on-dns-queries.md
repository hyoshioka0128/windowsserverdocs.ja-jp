---
title: DNS クエリへのフィルターの適用に DNS ポリシーを使用する
description: このトピックは、DNS ポリシー シナリオ ガイドの Windows Server 2016 の一部です。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: b86beeac-b0bb-4373-b462-ad6fa6cbedfa
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e9322da3142c584c7b9d0a28396a1d1fd62ce6ee
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446404"
---
# <a name="use-dns-policy-for-applying-filters-on-dns-queries"></a>DNS クエリへのフィルターの適用に DNS ポリシーを使用する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用するには、Windows server DNS のポリシーを構成する方法について&reg;2016 に指定した基準に基づくクエリ フィルターを作成します。 

DNS のポリシーでのクエリ フィルターを使用すると、カスタムの DNS クエリを送信する DNS クライアントと DNS クエリに基づく方法で応答する DNS サーバーを構成できます。

たとえば、フィルターを使用してクエリのブロック一覧既知の悪意のあるドメインからの DNS クエリをブロックする DNS がこれらのドメインからのクエリに応答することを防止する DNS ポリシーを構成できます。 DNS サーバーから応答が送信しないため、悪意のあるドメイン メンバーの DNS クエリがタイムアウトします。

別の例では、クエリ フィルターにより、特定の名前を解決するのにはクライアントの特定のセットのみを許可リストを作成します。

## <a name="bkmk_criteria"></a> クエリのフィルター条件
次の条件の論理の任意の組み合わせをクエリ フィルター (AND/OR/NOT) を作成できます。

|名前|説明|
|-----------------|---------------------|
|クライアントのサブネット|定義済みのクライアントのサブネットの名前です。 クエリの送信元となるサブネットを確認するために使用します。|
|トランスポート プロトコル|トランスポート プロトコル クエリで使用をします。 指定できる値は、UDP と TCP には。|
|インターネット プロトコル|クエリで使用されるネットワーク プロトコルです。 IPv4 と IPv6 の有効値は。|
|サーバーのインターフェイスの IP アドレス|DNS 要求を受信した DNS サーバーのネットワーク インターフェイスの IP アドレス。|
|FQDN|完全修飾ドメイン名のレコードのクエリでワイルドカードを使用する可能性があります。|
|クエリの種類|クエリ対象のレコードの種類\(A、SRV、TXT など\)します。|
|1 日の時間|クエリが受信した時刻。|

次の例では、フィルターを作成の DNS のポリシーをいずれかのブロックまたは DNS 名前解決クエリを許可するための方法を示します。

>[!NOTE]
>コマンドの例では、このトピックでは、Windows PowerShell コマンドを使って**追加 DnsServerQueryResolutionPolicy**します。 詳細については、次を参照してください。 [追加 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)します。 

## <a name="bkmk_block1"></a>ドメインからクエリがブロック

状況によっては、悪意のあるとして指定したドメインまたは組織の使用方法のガイドラインに準拠していないドメインの DNS 名前解決をブロックする可能性があります。 DNS ポリシーを使用してドメインのブロックの照会を行うことができます。

この例で構成したポリシーは、特定のゾーンに作成されません – 代わりに、DNS サーバーで構成されているすべてのゾーンに適用されるサーバー レベルのポリシーを作成します。 サーバー レベルのポリシーが評価される最初されため最初とクエリに一致するが、DNS サーバーから。

次のコマンド例は、ドメインとすべてのクエリをブロックするためのサーバー レベル ポリシーを構成します。**サフィックス contosomalicious.com**します。

`
Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicy" -Action IGNORE -FQDN "EQ,*.contosomalicious.com" -PassThru 
`

>[!NOTE]
>構成するとき、**アクション**パラメーター値を持つ**無視**、すべての応答のないクエリを削除する DNS サーバーが構成されています。 これにより、DNS クライアントがタイムアウトする悪意のあるドメイン。

## <a name="bkmk_block2"></a>サブネットからのブロックのクエリ
この例では、一部のマルウェアに感染することが判明し、DNS サーバーを使用して悪意のあるサイトにアクセスしようした場合、サブネットからのクエリをブロックできます。 

` Add-DnsServerClientSubnet -Name "MaliciousSubnet06" -IPv4Subnet 172.0.33.0/24 -PassThru

Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicyMalicious06" -Action IGNORE -ClientSubnet  "EQ,MaliciousSubnet06" -PassThru `

次の例では、ウイルスに感染したサブネットから特定の悪意のあるドメインに対するクエリをブロックする FQDN 条件と組み合わせてサブネットの条件を使用する方法を示します。

`
Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicyMalicious06" -Action IGNORE -ClientSubnet  "EQ,MaliciousSubnet06" –FQDN “EQ,*.contosomalicious.com” -PassThru
`

## <a name="bkmk_block3"></a>クエリの種類をブロックします。
特定の種類、サーバーに対するクエリの名前解決をブロックする必要があります。 たとえば、作成増幅攻撃に悪用される可能性が"ANY"クエリをブロックできます。

`
Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicyQType" -Action IGNORE -QType "EQ,ANY" -PassThru
`

## <a name="bkmk_allow1"></a>ドメインからのみクエリを許可します。
クエリがブロックに DNS ポリシーを使用することができましていないのみ、それらを使用して、特定のドメインまたはサブネットからのクエリを自動的に承認することができます。 許可一覧を構成するときに、DNS サーバーはのみ、他のドメインから他のすべてのクエリのブロックから許可されるドメインは、クエリを処理します。

次のコマンドの例には、コンピューターと、DNS サーバーを照会するドメイン contoso.com と子ドメイン内のデバイスのみができます。

`
Add-DnsServerQueryResolutionPolicy -Name "AllowListPolicyDomain" -Action IGNORE -FQDN "NE,*.contoso.com" -PassThru 
`

## <a name="bkmk_allow2"></a>サブネットからのみクエリを許可します。
作成することも許可一覧の IP サブネット、これらのサブネットから発信されていないすべてのクエリが無視されるようにします。

`
Add-DnsServerClientSubnet -Name "AllowedSubnet06" -IPv4Subnet 172.0.33.0/24 -PassThru
`
`
Add-DnsServerQueryResolutionPolicy -Name "AllowListPolicySubnet” -Action IGNORE -ClientSubnet  "NE, AllowedSubnet06" -PassThru
`

## <a name="bkmk_allow3"></a>特定の QTypes のみを許可します。
許可一覧は、QTYPEs に適用できます。 

たとえば、DNS サーバー インターフェイス 164.8.1.1 のクエリを実行する外部の顧客がある場合は場合、は、特定 QTYPEs のみは SRV や TXT のレコードの名前解決または監視目的で内部サーバーで使用されるように、その他の QTYPEs がありますが、照会する許可されます。

`
Add-DnsServerQueryResolutionPolicy -Name "AllowListQType" -Action IGNORE -QType "NE,A,AAAA,MX,NS,SOA" –ServerInterface “EQ,164.8.1.1” -PassThru
`

何千もの DNS のポリシーに合わせて作成できます、トラフィック管理の要件、DNS サーバーを再起動しなくても - 受信したクエリで、すべての新しいポリシーが動的 - 適用されます。 
