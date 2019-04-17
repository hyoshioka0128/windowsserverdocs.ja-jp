---
title: DNS クエリにフィルターを適用するために DNS ポリシーを使用します。
description: このトピックでは、DNS ポリシー シナリオ ガイドの Windows Server 2016 の一部
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: b86beeac-b0bb-4373-b462-ad6fa6cbedfa
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ff10af5f88a03f806a5e5b5fa698c7c3637816bd
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-applying-filters-on-dns-queries"></a>DNS クエリにフィルターを適用するために DNS ポリシーを使用します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、Windows server DNS のポリシーを構成する方法について&reg;2016 指定した条件に基づいてクエリ フィルターを作成します。 

DNS ポリシーでクエリ フィルターを使用すると、DNS クエリと、DNS クエリを送信する DNS クライアントに基づくカスタムの方法で応答する DNS サーバーを構成できます。

たとえば、フィルターを使用してクエリ禁止リストをブロックする既知の悪意のあるドメインからの DNS クエリ DNS がこれらのドメインからのクエリに応答するを防ぎます DNS のポリシーを構成できます。 DNS サーバーから応答が送信されるないので、悪意のあるドメイン メンバーの DNS クエリがタイムアウトします。

別の例では、クエリ フィルターにより、特定の名前を解決するのにはクライアントの特定のセットのみ許可リストを作成します。

## <a name="bkmk_criteria"></a>クエリのフィルター条件
次の条件の論理任意の組み合わせでクエリ フィルター (やかどうか) を作成できます。

|名|説明|
|-----------------|---------------------|
|クライアントのサブネット|定義済みのクライアントのサブネットの名前です。 クエリの送信元となるサブネットを確認するために使用します。|
|トランスポート プロトコル|トランスポート プロトコルのクエリで使用します。 指定可能な値は、UDP および TCP です。|
|インターネット プロトコル|クエリで使用されるネットワーク プロトコルです。 指定可能な値は、IPv4 および IPv6 です。|
|サーバーのインターフェイスの IP アドレス|DNS 要求を受信した DNS サーバーのネットワーク インターフェイスの IP アドレス|
|FQDN|完全修飾ドメイン名、クエリ内のレコードのワイルドカードを使用する可能性です。|
|クエリの種類|照会しているレコードの種類 \ (A、SRV、TXT など \)。|
|1 日の時間|クエリを受信した時刻。|

次の例では、ブロックを作成する DNS のポリシーのフィルターをいずれかまたは DNS 名前解決クエリを許可する方法を示しています。

>[!NOTE]
>このトピックの「例のコマンドは、Windows PowerShell コマンドを使用して**追加 DnsServerQueryResolutionPolicy**します。 詳細については、次を参照してください。[追加 DnsServerQueryResolutionPolicy](https://technet.microsoft.com/library/mt126273.aspx)します。 

##<a name="bkmk_block1"></a>ドメインからのクエリのブロック

状況によっては、悪意のあるとしてユーザーが識別されるドメインまたは組織のガイドラインに準拠していないドメインの DNS 名前解決をブロックする可能性があります。 DNS ポリシーを使用してドメインのブロックの照会を行うことができます。

この例で構成するポリシーは、特定のゾーンに作成されません – 代わりに、DNS サーバーに構成されているすべてのゾーンに適用される、サーバー レベルでポリシーを作成します。 サーバー レベルのポリシーが最初に評価およびしたがって最初とき、クエリに一致するが受信した DNS サーバーが。

次のコマンド例は、ドメインとすべてのクエリをブロックするためのサーバー レベル ポリシーを構成**サフィックス contosomalicious.com**します。

`
Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicy" -Action IGNORE -FQDN "EQ,*.contosomalicious.com" -PassThru 
`

>[!NOTE]
>構成するときに、**アクション**パラメーターに値**無視**、DNS サーバーがまったく応答のないクエリを削除するように構成します。 これにより、DNS クライアントがタイムアウト悪意のあるドメイン。

##<a name="bkmk_block2"></a>サブネットからブロック クエリ
この例では、一部のマルウェアに感染することがわかったし、DNS サーバーを使用して、悪意のあるサイトに接続しようとしている場合はサブネットからのクエリをブロックできます。 

' Add-DnsServerClientSubnet-名前"MaliciousSubnet06"-IPv4Subnet 172.0.33.0/24-passthru

Add-DnsServerQueryResolutionPolicy-名前"BlockListPolicyMalicious06"-アクション無視 ClientSubnet"EQ、MaliciousSubnet06"-passthru '

次の例では、感染したサブネットから特定の悪意のあるドメインに対するクエリをブロックする FQDN 基準との組み合わせでサブネットの条件を使用する方法について説明します。

`
Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicyMalicious06" -Action IGNORE -ClientSubnet  "EQ,MaliciousSubnet06" –FQDN “EQ,*.contosomalicious.com” -PassThru
`

##<a name="bkmk_block3"></a>クエリの種類をブロックします。
クエリ サーバー上の特定の種類の名前解決をブロックする必要があります。 たとえば、増幅攻撃を作成する悪用される可能性が '、' クエリをブロックすることができます。

`
Add-DnsServerQueryResolutionPolicy -Name "BlockListPolicyQType" -Action IGNORE -QType "EQ,ANY" -PassThru
`

##<a name="bkmk_allow1"></a>クエリをドメインからのみを許可します。
ブロックのクエリに DNS ポリシーを使用することはできませんのみ、それらを使用して、特定のドメインまたはサブネットからのクエリを自動的に承認することができます。 許可一覧を構成するときに、DNS サーバーは他のドメインから他のすべてのクエリをブロックしているときに許可するドメインからのクエリをのみ処理します。

次のコマンド例によりのみのコンピューターとデバイス contoso.com と子はドメインに DNS サーバーを照会できます。

`
Add-DnsServerQueryResolutionPolicy -Name "AllowListPolicyDomain" -Action IGNORE -FQDN "NE,*.contoso.com" -PassThru 
`

##<a name="bkmk_allow2"></a>サブネットのみからのクエリを許可します。
作成することも許可一覧の IP サブネット、できるように、これらのサブネットから送信されたいないすべてのクエリは無視されます。

`
Add-DnsServerClientSubnet -Name "AllowedSubnet06" -IPv4Subnet 172.0.33.0/24 -PassThru
`
`
Add-DnsServerQueryResolutionPolicy -Name "AllowListPolicySubnet” -Action IGNORE -ClientSubnet  "NE, AllowedSubnet06" -PassThru
`

##<a name="bkmk_allow3"></a>特定の QTypes のみを許可します。
許可一覧は、QTYPEs に適用できます。 

たとえば、164.8.1.1 DNS サーバー インターフェイスをクエリする外部の顧客がある場合は場合、は、特定 QTYPEs のみが照会する SRV、TXT レコードまたは監視の目的で名前解決のために、内部サーバーで使用するように、その他の QTYPEs 中に許可されます。

`
Add-DnsServerQueryResolutionPolicy -Name "AllowListQType" -Action IGNORE -QType "NE,A,AAAA,MX,NS,SOA" –ServerInterface “EQ,164.8.1.1” -PassThru
`

要件を作成できます何千もの DNS のポリシーに従って、トラフィックの管理、および DNS サーバーを再起動しなくても - 受信したクエリで、すべての新しいポリシーが動的 - 適用します。 
