---
title: Active Directory でスプリット ブレイン DNS に DNS ポリシーを使用する
description: このトピックを使用して、トラフィックを活用することができますスプリット ブレイン展開を Active Directory と DNS のポリシーの管理機能は、Windows Server 2016 での DNS ゾーンを統合します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: f9533204-ad7e-4e49-81c1-559324a16aeb
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7a5761cafff0a4bf148958a7f14aeaf311075b2e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839783"
---
# <a name="use-dns-policy-for-split-brain-dns-in-active-directory"></a>Active Directory でスプリット ブレイン DNS に DNS ポリシーを使用する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用して、分割 DNS のポリシーのトラフィック管理機能を活用することができます\-ブレイン展開と Active Directory は、Windows Server 2016 での DNS ゾーンを統合します。

DNS のポリシーのサポートの拡張 Active Directory に Windows Server 2016 で DNS ゾーンを統合します。 Active Directory 統合は、マルチ\-マスターの DNS サーバーに高可用性機能。 

以前は、このシナリオは、DNS 管理者の管理 2 台の DNS サーバー、各内部および外部のユーザーのセットごとにサービスを提供することが必要です。 ゾーン内のいくつかのレコードが分割された場合のみ\-brained またはゾーン (内部および外部) の両方のインスタンスが委任された同じ親ドメインになり、管理の難点です。

>[!NOTE]
> - DNS 展開を分割\-脳の 1 つのゾーンの 2 つのバージョン、組織のイントラネット上の内部ユーザー用の 1 つのバージョンとは、通常、インターネット上のユーザー – 外部ユーザー向けの 1 つのバージョンがある場合。
> - トピック[Split-Brain DNS の展開の DNS のポリシーを使用して](split-brain-DNS-deployment.md)DNS のポリシーとゾーンのスコープを使用して、デプロイを分割する方法について説明します。\-脳は単一の Windows Server 2016 の DNS サーバー上の DNS システム。



##  <a name="example-split-brain-dns-in-active-directory"></a>例の分割\-脳 Active Directory での DNS

この例では、1 つ架空の企業、www.career.contoso.com で仕事紹介 Web サイトを保持する contoso 社で使用します。

サイトには、内部の求人が利用可能な内部ユーザー用、2 つのバージョンがあります。 この内部サイトは、ローカル IP アドレス 10.0.0.39 から入手できます。 

2 番目のバージョンは、パブリック IP アドレス 65.55.39.10 で利用可能な同じサイトのパブリック バージョンです。

DNS のポリシーがない場合を別の Windows Server DNS サーバーでこれら 2 つのゾーンをホストし、それらを個別に管理、管理者が必要です。 

DNS ポリシーを使用してこれらのゾーンできますでホストされるよう、同じ DNS サーバーです。

Contoso.com の DNS サーバーが Active Directory 統合が 2 つのネットワーク インターフェイスでリッスンしている場合は、Contoso の DNS 管理者は、分割を実現するために、このトピックの手順に\-ブレイン展開します。

DNS 管理者は、次の IP アドレスで DNS サーバーのインターフェイスを構成します。

- インターネットに接続するネットワーク アダプターは、外部クエリ 208.84.0.53 のパブリック IP アドレスで構成されます。
- イントラネットに接続するネットワーク アダプターは、内部クエリ 10.0.0.56 のプライベート IP アドレスで構成されます。

次の図は、このシナリオを示しています。

![AD スプリット ブレイン DNS 展開を統合します。](../../media/DNS-SB-AD/DNS-SB-AD.jpg)

## <a name="how-dns-policy-for-split-brain-dns-in-active-directory-works"></a>DNS のポリシーの分割\-ブレインの DNS の Active Directory の機能

必要な DNS ポリシーで、DNS サーバーを構成すると、各名前解決の要求は、DNS サーバー上のポリシーに対して評価されます。

サーバーのインターフェイスは、内部および外部のクライアントを区別するために、この例では、条件として使用されます。

クエリを受信するサーバーのインターフェイスには、任意のポリシーが一致すると、クエリに応答する、関連付けられているゾーンのスコープが使用されます。 

そのため、この例ではプライベート ip アドレス (10.0.0.56) で受信した www.career.contoso.com に関する DNS クエリ DNS 応答を受信する内部の IP アドレスを含むパブリック ネットワーク インターフェイスで受信 DNS クエリ応答を受信する DNS ゾーンの既定のスコープ (これは通常のクエリの解決策と同じ) のパブリック IP アドレスを含みます。  

動的 DNS のサポート\(DDNS\)更新プログラムと清掃がゾーンの既定のスコープでのみサポートされます。 ゾーンの既定のスコープでは、内部のクライアントが処理される、ために、Contoso の DNS 管理者が (動的 DNS または静的) contoso.com 内のレコードを更新する既存のメカニズムを使用してを続行することができます。 非\-ゾーンのスコープを既定\(など、この例では、外部スコープ\)、DDNS または清掃のサポートは使用できません。

### <a name="high-availability-of-policies"></a>ポリシーの高可用性

DNS のポリシーは、Active Directory 統合ではありません。 このため、DNS のポリシーは、同じ Active Directory 統合ゾーンをホストしている他の DNS サーバーはレプリケートされません。 

DNS のポリシーは、ローカルの DNS サーバーに格納されます。 次の例の Windows PowerShell コマンドを使用して 1 つのサーバーから別に DNS ポリシーをエクスポートすることができます簡単にします。

    $policies = Get-DnsServerQueryResolutionPolicy -ZoneName "contoso.com" -ComputerName Server01
    
    $policies |  Add-DnsServerQueryResolutionPolicy -ZoneName "contoso.com" -ComputerName Server02

詳細については、次の Windows PowerShell のリファレンス トピックを参照してください。

- [Get-DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/get-dnsserverqueryresolutionpolicy?view=win10-ps)
- [Add-DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)


## <a name="how-to-configure-dns-policy-for-split-brain-dns-in-active-directory"></a>分割 DNS のポリシーを構成する方法\-脳 Active Directory での DNS

DNS のポリシーを使用して DNS Split-Brain 展開を構成するには、詳細な構成の指示を提供する次のセクションを使用する必要があります。

### <a name="add-the-active-directory-integrated-zone"></a>Active Directory 統合ゾーンを追加します。

次の例のコマンドを使用すると、DNS サーバーに Active Directory 統合 contoso.com ゾーンを追加します。

    Add-DnsServerPrimaryZone -Name "contoso.com" -ReplicationScope "Domain" -PassThru

詳細については、次を参照してください。[デモンストレーション](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverprimaryzone?view=win10-ps)します。

### <a name="create-the-scopes-of-the-zone"></a>ゾーンのスコープを作成します。

このセクションを使用するには、外部のゾーンのスコープを作成するのに、ゾーン contoso.com をパーティション分割します。

ゾーンのスコープは、ゾーンの一意のインスタンスです。 DNS ゾーンは、独自の DNS レコード セットを格納している各ゾーンのスコープを持つ、複数のゾーン スコープを持つことができます。 同じレコードは、別の IP アドレスを持つ、複数のスコープまたは同じ IP アドレスに存在することができます。 

Active Directory 統合ゾーンでこの新しいゾーンのスコープを追加するため、ゾーンのスコープとその中のレコードは Active Directory を使用してドメイン内の他のレプリカ サーバーにレプリケートします。

既定では、ゾーンのスコープは、すべての DNS ゾーンに存在します。 このゾーンのスコープでは、ゾーンと同じ名前と、従来の DNS の機能がこのスコープで動作します。 この既定のゾーンのスコープは、www.career.contoso.com の内部バージョンをホストします。

次のコマンドの例を使用して、DNS サーバーでゾーンのスコープを作成することができます。

    Add-DnsServerZoneScope -ZoneName "contoso.com" -Name "external"

詳細については、次を参照してください。 [追加 DnsServerZoneScope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)します。

### <a name="add-records-to-the-zone-scopes"></a>レコードをゾーンのスコープに追加します。

次の手順では、2 つに、web サーバーのホストを表すレコードがゾーンのスコープ外部と既定の追加を\(内部クライアントの\)します。 

これはプライベート IP アドレスは IP アドレス 10.0.0.39、内部のゾーンの既定のスコープでレコード www.career.contoso.com が追加されます。同じレコードの外部のゾーン スコープで\(www.career.contoso.com\)パブリック IP アドレス 65.55.39.10 で追加されます。 

レコード\(の両方で、既定の内部ゾーンのスコープと外部のゾーン スコープ\)それぞれのゾーンのスコープを使用してドメイン間で自動的にレプリケートされます。

次のコマンドの例を使用して、レコードを DNS サーバーでゾーンのスコープに追加することができます。

    Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "65.55.39.10" -ZoneScope "external"
    
    Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "10.0.0.39”

>[!NOTE]
>**– ゾーン範囲ゾーン**パラメーターは、レコードがゾーンの既定のスコープに追加されたときに含まれません。 このアクションは、標準のゾーンにレコードを追加することと同じです。

詳細については、次を参照してください。 [追加 DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)します。

### <a name="create-the-dns-policies"></a>DNS のポリシーを作成します。

外部ネットワークおよび内部ネットワーク用のサーバー インターフェイスを識別する、ゾーンのスコープを作成した後は、内部および外部のゾーンのスコープを接続する DNS ポリシーを作成する必要があります。

>[!NOTE]
>この例は、サーバーのインターフェイスを使用して\(次の例のコマンドで - ServerInterface パラメーター\)内部および外部のクライアントを区別する検索条件として。 内部および外部のクライアントを区別するために別の方法では、クライアントのサブネットを使用して、条件として、です。 内部のクライアントが属するサブネットを特定する場合は、クライアントのサブネットに基づいて区別するために DNS のポリシーを構成できます。 クライアントのサブネットの条件を使用したトラフィック管理を構成する方法については、次を参照してください。 [のプライマリ サーバーの地理的な場所ベースのトラフィック管理用の DNS ポリシーを使用して](primary-geo-location.md)します。

DNS クエリがパブリック インターフェイスで受信したときに、ポリシーを構成した後は、ゾーンの外部スコープから、応答が返されます。 

>[!NOTE]
>ポリシーの既定の内部ゾーン スコープをマッピングするため必要はありません。 

    Add-DnsServerQueryResolutionPolicy -Name "SplitBrainZonePolicy" -Action ALLOW -ServerInterface "eq,208.84.0.53" -ZoneScope "external,1" -ZoneName contoso.com

>[!NOTE]
>208.84.0.53 は、パブリック ネットワーク インターフェイスの IP アドレスです。

詳細については、次を参照してください。 [追加 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)します。

Active Directory とスプリット ブレイン ネーム サーバーが DNS を統合するために必要な DNS ポリシーで、DNS サーバーが構成されているようになりましたゾーン。

何千もの DNS のポリシーに合わせて作成できます、トラフィック管理の要件、DNS サーバーを再起動しなくても - 受信したクエリで、すべての新しいポリシーが動的 - 適用されます。 
