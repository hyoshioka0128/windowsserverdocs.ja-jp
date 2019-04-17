---
title: DNS のポリシーを使用して Split-Brain Active Directory 内の DNS
description: このトピックを使用すると、トラフィックを活用する Active Directory でスプリット ブレイン展開用の DNS のポリシーの管理機能は、Windows Server 2016 での DNS ゾーンを統合します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: f9533204-ad7e-4e49-81c1-559324a16aeb
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d294fcad3b48c8698dffd93e94f6ef7ffc681ea2
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="use-dns-policy-for-split-brain-dns-in-active-directory"></a>DNS のポリシーを使用して Split-Brain Active Directory 内の DNS

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、Active Directory と split\ ブレイン展開に統合された DNS の DNS のポリシーのトラフィック管理機能を活用する Windows Server 2016 でのゾーンです。

Windows Server 2016 で、DNS のポリシーのサポートが拡張 Active Directory 統合 DNS ゾーンです。 Active Directory 統合 DNS サーバーにマルチ マスター高可用性機能を提供します。 

以前は、このシナリオは、DNS 管理者が異なる 2 つの DNS サーバー、各内部および外部のユーザーのセットごとにサービスを提供する管理が必要です。 この場合、専用で、ゾーン内のいくつかのレコードが split\ brained またはゾーン (内部および外部) の両方のインスタンスが同じ親ドメインに委任された、管理の難点ようになりました。

>[!NOTE]
> - DNS の展開は、1 つのゾーンの 2 つのバージョン、組織のイントラネット上の内部ユーザー用の 1 つのバージョンと外部ユーザー – は、通常、インターネット上のユーザーの 1 つのバージョンがある場合の split\ ブレインです。
> - トピック[DNS のポリシーを使用して Split-Brain DNS 展開](split-brain-DNS-deployment.md)DNS のポリシーとゾーンのスコープを使用して、単一の Windows Server 2016 の DNS サーバーに split\ ブレイン DNS システムを展開する方法について説明します。



##  <a name="example-split-brain-dns-in-active-directory"></a>Active Directory の Split\ ブレイン DNS の例

この例では、1 つ架空の会社で www.career.contoso.com 求人 Web サイトを保持する Contoso を使用します。

サイトでは、内部の求人が利用可能な内部ユーザー用の 1 つ、2 つのバージョンがあります。 この内部サイトでは、ローカル IP アドレス 10.0.0.39 で使用できます。 

2 番目のバージョンは、パブリック IP アドレス 65.55.39.10 利用可能な同じサイトのパブリック バージョンです。

DNS のポリシーがない場合、これら 2 つの個別の Windows Server DNS サーバーでゾーンをホストし、それらを個別に管理、管理者が必要です。 

DNS ポリシーを使用してこれらのゾーンできますでホストされるよう、同じ DNS サーバー。

contoso.com の DNS サーバーを統合すると、Active Directory、2 つのネットワーク インターフェイスでリッスンしている場合、Contoso の DNS 管理者は、split\ ブレイン展開を実現するために、このトピックの手順に従うことができます。

DNS 管理者は、次の IP アドレスを持つ DNS サーバーのインターフェイスを構成します。

- インターネット向けのネットワーク アダプターは、クエリは、外部 208.84.0.53 のパブリック IP アドレスで構成されます。
- イントラネット向けのネットワーク アダプターは、内部クエリが 10.0.0.56 のプライベート IP アドレスで構成されます。

次の図は、このシナリオを示しています。

![Split-BrainAD 統合 DNS の展開](../../media/DNS-SB-AD/DNS-SB-AD.jpg)

## <a name="how-dns-policy-for-split-brain-dns-in-active-directory-works"></a>DNS のポリシーを Active Directory で Split\ ブレイン DNS のしくみ

DNS サーバーが必要な DNS ポリシーで構成されると、各名前解決の要求は、DNS サーバー上のポリシーに対して評価されます。

サーバーのインターフェイスは、内部および外部のクライアントを区別するために、この例では、条件として使用されます。

クエリを受信する対象サーバーのインターフェイスには、任意のポリシーが一致すると、クエリに応答する、関連付けられているゾーンのスコープが使用されます。 

したがって、この例では、DNS クエリでプライベート IP (10.0.0.56 が受信 www.career.contoso.com)、内部の IP アドレスを含む DNS 応答を受信します。パブリック ネットワーク インターフェイスで受信 DNS クエリのゾーンの既定のスコープ (これは通常のクエリの解決策と同じ) のパブリック IP アドレスを含む DNS 応答を受信します。  

動的 DNS \(DDNS\) 更新プログラムと清掃のサポートは、既定のゾーンのスコープでのみサポートされます。 内部のクライアントは、既定のゾーン スコープによって処理され、ために、Contoso の DNS 管理者が (動的 DNS または静的) contoso.com でレコードを更新するのには、既存のメカニズムを使用してを続行することができます。既定以外のゾーンのスコープに対して \ (などの外部で、スコープこの example\)、DDNS か清掃サポートを利用できません。

### <a name="high-availability-of-policies"></a>ポリシーの高可用性

DNS のポリシーは、Active Directory 統合ではありません。 このため、DNS のポリシーは、同じ Active Directory 統合ゾーンをホストしている他の DNS サーバーにレプリケートされません。 

DNS のポリシーは、ローカル DNS サーバーに保存されます。 次の例の Windows PowerShell コマンドを使用して 1 台のサーバーから別に DNS ポリシーをエクスポートすることができます簡単にします。

    $policies = Get-DnsServerQueryResolutionPolicy -ZoneName "contoso.com" -ComputerName Server01
    
    $policies |  Add-DnsServerQueryResolutionPolicy -ZoneName "contoso.com" -ComputerName Server02

詳細については、次の Windows PowerShell リファレンスのトピックを参照してください。

- [Get-DnsServerQueryResolutionPolicy](https://technet.microsoft.com/itpro/powershell/windows/dns-server/get-dnsserverqueryresolutionpolicy)
- [Add-DnsServerQueryResolutionPolicy](https://technet.microsoft.com/itpro/powershell/windows/dns-server/add-dnsserverqueryresolutionpolicy)


## <a name="how-to-configure-dns-policy-for-split-brain-dns-in-active-directory"></a>Active Directory で Split\ ブレイン DNS の DNS ポリシーを構成する方法

DNS を構成する Split-Brain 展開用の DNS ポリシーを使用して、提供詳細な構成手順については、次のセクションを使用する必要があります。

### <a name="add-the-active-directory-integrated-zone"></a>Active Directory 統合ゾーンを追加します。

次のコマンド例を使用すると、DNS サーバーに Active Directory 統合 contoso.com ゾーンを追加します。

    Add-DnsServerPrimaryZone -Name "contoso.com" -ReplicationScope "Domain" -PassThru

詳細については、次を参照してください。[デモンストレーション](https://technet.microsoft.com/library/jj649876.aspx)します。

### <a name="create-the-scopes-of-the-zone"></a>ゾーンのスコープを作成します

このセクションを使用すると、ゾーン contoso.com、外部のゾーンのスコープを作成するのにパーティションを作成します。

ゾーンのスコープは、ゾーンの一意のインスタンスです。 DNS ゾーンには、複数のゾーンのスコープ、DNS レコードの独自セットが含まれている各ゾーンのスコープを持つことができます。 同じレコードは、別の IP アドレスを持つ複数のスコープまたは同じ IP アドレスに存在することができます。 

Active Directory 統合ゾーンでこの新しいゾーンのスコープを追加するため、ゾーンのスコープとその内部レコードは Active Directory を使ってドメイン内の他のレプリカ サーバーにレプリケートします。

既定では、ゾーンのスコープは、すべての DNS ゾーンに存在します。 このゾーンのスコープは、ゾーンと同じ名前を持つし、従来の DNS 操作は、このスコープで動作します。 この既定のゾーンのスコープでは、www.career.contoso.com の内部バージョンをホストします。

次のコマンド例を使用して、DNS サーバーでゾーンのスコープを作成することができます。

    Add-DnsServerZoneScope -ZoneName "contoso.com" -Name "external"

詳細については、次を参照してください。[追加 DnsServerZoneScope](https://technet.microsoft.com/library/mt126267.aspx)します。

### <a name="add-records-to-the-zone-scopes"></a>レコードをゾーンのスコープに追加します。

次の手順では、2 つに Web サーバーのホストを表すレコードをゾーンのスコープ外部と既定の追加を \(for internal clients\) します。 

内部のゾーンの既定のスコープでレコード www.career.contoso.com は 10.0.0.39、これは、プライベート IP アドレスの IP アドレスの追加します。され、外部のゾーンのスコープで同じレコード \(www.career.contoso.com\) が 65.55.39.10 のパブリック IP アドレスに追加されます。 

記録 \ (どちらも既定の内部ゾーン スコープと外部のゾーン scope\)、それぞれのゾーンのスコープを使用してドメイン間で自動的にレプリケートします。

次のコマンド例を使用して、レコードを DNS サーバーでゾーンのスコープに追加することができます。

    Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "65.55.39.10" -ZoneScope "external"
    
    Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "10.0.0.39”

>[!NOTE]
>**– ゾーン範囲ゾーン**パラメーターが含まれていない、レコードがゾーンの既定のスコープに追加されるとします。 この操作は、通常のゾーンにレコードを追加すると同じです。

詳細については、次を参照してください。[追加 DnsServerResourceRecord](https://technet.microsoft.com/library/jj649925.aspx)します。

### <a name="create-the-dns-policies"></a>DNS ポリシーを作成します。

外部ネットワークおよび内部ネットワーク用のサーバー インターフェイスを識別すると、ゾーンのスコープを作成した、内部および外部のゾーンのスコープを接続する DNS ポリシーを作成する必要があります。

>[!NOTE]
>この例は、サーバーのインターフェイスを使用して \ (例のコマンド below\ で - ServerInterface パラメーター)、内部および外部のクライアントを区別するために、条件とします。 内部および外部のクライアントを区別するために別の方法を条件としてクライアントのサブネットを使ってです。 内部のクライアントが属しているサブネットを特定できる場合は、クライアントのサブネットに基づいて区別するために DNS ポリシーを構成できます。 クライアントのサブネットの条件を使用したトラフィック管理を構成する方法については、次を参照してください。[地理的な場所ベースのトラフィック管理のプライマリ サーバーの DNS ポリシーを使用して](primary-geo-location.md)します。

DNS クエリがパブリック インターフェイスで受信したときに、ポリシーを構成した後は、外部のゾーンのスコープから、応答が返されます。 

>[!NOTE]
>ポリシーの既定の内部ゾーン スコープをマッピングするため必要はありません。 

    Add-DnsServerQueryResolutionPolicy -Name "SplitBrainZonePolicy" -Action ALLOW -ServerInterface "eq,208.84.0.53" -ZoneScope "external,1" -ZoneName contoso.com

>[!NOTE]
>208.84.0.53 は、パブリック ネットワーク インターフェイスで IP アドレスです。

詳細については、次を参照してください。[追加 DnsServerQueryResolutionPolicy](https://technet.microsoft.com/library/mt126273.aspx)します。

Active Directory でスプリット ブレイン ネーム サーバーに統合された DNS の必要な DNS ポリシーで、DNS サーバーが構成されているようになりましたゾーンです。

要件を作成できます何千もの DNS のポリシーに従って、トラフィックの管理、および DNS サーバーを再起動しなくても - 受信したクエリで、すべての新しいポリシーが動的 - 適用します。 
