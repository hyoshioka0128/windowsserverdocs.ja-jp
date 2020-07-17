---
title: スプリット ブレイン DNS の展開に DNS ポリシーを使用する
description: このトピックは、Windows Server 2016 の DNS ポリシーシナリオガイドに含まれています。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: a255a4a5-c1a0-4edc-b41a-211bae397e3c
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 75da22fa4b1e59a7a666ee1a2c8f4e88cf7beeef
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80317732"
---
# <a name="use-dns-policy-for-split-brain-dns-deployment"></a>分割\-ブレイン DNS 展開に DNS ポリシーを使用する

>適用対象: Windows Server 2016

このトピックを使用して、Windows server DNS のポリシーを構成する方法について&reg; 2016 スプリット ブレイン DNS 展開では、1 つの 2 つのバージョンが存在するゾーンの組織のイントラネット上の内部ユーザーと外部のユーザーは、通常、インターネット上のユーザーに対して使用します。

>[!NOTE]
>Active Directory 統合 DNS ゾーン数を使用した split\-ブレイン DNS の展開に DNS ポリシーを使用する方法については、 [Active Directory でのスプリットブレイン dns の Dns ポリシーの使用](dns-sb-with-ad.md)に関する説明を参照してください。

以前は、このシナリオは、DNS 管理者の管理 2 台の DNS サーバー、各内部および外部のユーザーのセットごとにサービスを提供することが必要です。 ゾーン内の少数のレコードのみが brained\-分割された場合、またはゾーンの両方のインスタンス (内部および外部) が同じ親ドメインに委任された場合は、管理難問になります。 

スプリット ブレイン展開用の別の構成シナリオは、DNS 名前解決のための選択的の再帰コントロールです。 状況によっては、企業の DNS サーバーもする必要があります、外部ユーザーの権限を持つネーム サーバーとして機能し、再帰をブロック中に、内部ユーザー用のインターネット経由で再帰的な解決を行う必要があります。 

このトピックの内容は次のとおりです。

- [DNS スプリットブレイン展開の例](#bkmk_sbexample)
- [DNS の選択的な再帰制御の例](#bkmk_recursion)

## <a name="example-of-dns-split-brain-deployment"></a><a name="bkmk_sbexample"></a>DNS スプリットブレイン展開の例
DNS のポリシーを使用して、スプリット ブレイン DNS の既に説明したシナリオを実現する方法の例を次に示します。

このセクションのトピックは次のとおりです。

- [DNS スプリットブレイン展開のしくみ](#bkmk_sbhow)
- [DNS スプリットブレイン展開を構成する方法](#bkmk_sbconfigure)


この例では、1 つ架空の企業、 www.career.contoso.com で仕事紹介 Web サイトを保持する contoso 社で使用します。

サイトには、内部の求人が利用可能な内部ユーザー用、2 つのバージョンがあります。 この内部サイトは、ローカル IP アドレス 10.0.0.39 から入手できます。 

2 番目のバージョンは、パブリック IP アドレス 65.55.39.10 で利用可能な同じサイトのパブリック バージョンです。

DNS のポリシーがない場合を別の Windows Server DNS サーバーでこれら 2 つのゾーンをホストし、それらを個別に管理、管理者が必要です。 

DNS ポリシーを使用してこれらのゾーンできますでホストされるよう、同じ DNS サーバーです。  

次の図は、このシナリオを示しています。

![スプリット ブレイン DNS 展開](../../media/DNS-Split-Brain/Dns-Split-Brain-01.jpg)  


## <a name="how-dns-split-brain-deployment-works"></a><a name="bkmk_sbhow"></a>DNS スプリットブレイン展開のしくみ

必要な DNS ポリシーで、DNS サーバーを構成すると、各名前解決の要求は、DNS サーバー上のポリシーに対して評価されます。

サーバーのインターフェイスは、内部および外部のクライアントを区別するために、この例では、条件として使用されます。

クエリを受信するサーバーのインターフェイスには、任意のポリシーが一致すると、クエリに応答する、関連付けられているゾーンのスコープが使用されます。 

そのため、この例ではプライベート ip アドレス (10.0.0.56) で受信した www.career.contoso.com に関する DNS クエリ DNS 応答を受信する内部の IP アドレスを含むパブリック ネットワーク インターフェイスで受信 DNS クエリ応答を受信する DNS ゾーンの既定のスコープ (これは通常のクエリの解決策と同じ) のパブリック IP アドレスを含みます。  

## <a name="how-to-configure-dns-split-brain-deployment"></a><a name="bkmk_sbconfigure"></a>DNS スプリットブレイン展開を構成する方法
DNS のポリシーを使用して DNS Split-Brain 展開を構成するには、次の手順を使用する必要があります。

- [ゾーンのスコープを作成する](#bkmk_zscopes)  
- [ゾーンのスコープにレコードを追加する](#bkmk_records)  
- [DNS ポリシーを作成する](#bkmk_policies)

次のセクションでは、詳細な構成手順を説明します。

>[!IMPORTANT]
>以下のセクションには、多くのパラメーターの値の例を含む Windows PowerShell コマンドの例が含まれています。 これらのコマンドで値の例は、これらのコマンドを実行する前に、展開に対応する値を置き換えることを確認します。 

### <a name="create-the-zone-scopes"></a><a name="bkmk_zscopes"></a>ゾーンのスコープを作成する

ゾーンのスコープは、ゾーンの一意のインスタンスです。 DNS ゾーンは複数のゾーンスコープを持つことができ、各ゾーンスコープには独自の DNS レコードセットが含まれます。 同じレコードが複数のスコープに存在し、異なる IP アドレスまたは同じ IP アドレスを持つことができます。 

> [!NOTE]
> 既定では、ゾーンのスコープは、DNS ゾーンに存在します。 このゾーンのスコープでは、ゾーンと同じ名前と、従来の DNS の機能がこのスコープで動作します。 この既定のゾーンのスコープは、 www.career.contoso.com の外部のバージョンをホストします。

次のコマンド例は、内部ゾーン スコープを作成するのにゾーン スコープ contoso.com のパーティション分割に使用できます。 内部のゾーンのスコープは、 www.career.contoso.com の内部バージョンを保持するのには使用されます。

`Add-DnsServerZoneScope -ZoneName "contoso.com" -Name "internal"`

詳細については、次を参照してください [追加 DnsServerZoneScope。](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)

### <a name="add-records-to-the-zone-scopes"></a><a name="bkmk_records"></a>ゾーンのスコープにレコードを追加する

次の手順では、(外部クライアント向け)、2 つのゾーン スコープの内部に Web サーバーのホストと既定値を表すレコードを追加します。 

内部ゾーン スコープ内でレコード <strong>www.career.contoso.com</strong> 追加 10.0.0.39 で、プライベート IP アドレスは、IP アドレスを使用し、ゾーンの既定のスコープで同じレコードを <strong>www.career.contoso.com</strong>, 、65.55.39.10 の IP アドレスを追加します。

いいえ **– ゾーン範囲ゾーン** レコードがゾーンの既定のスコープに追加される場合に、次の例のコマンドにパラメーターが含まれています。 これは、バニラのゾーンにレコードを追加すると似ています。

`
Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "65.55.39.10"
`
`
Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "10.0.0.39” -ZoneScope "internal"
`

詳細については、次を参照してください。 [追加 DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)します。

### <a name="create-the-dns-policies"></a><a name="bkmk_policies"></a>DNS ポリシーを作成する

外部ネットワークおよび内部ネットワーク用のサーバー インターフェイスを識別する、ゾーンのスコープを作成した後は、内部および外部のゾーンのスコープを接続する DNS ポリシーを作成する必要があります。

>[!NOTE]
>この例では、条件として、サーバー インターフェイスを使用して、内部および外部のクライアントを区別します。 内部および外部のクライアントを区別するために別の方法では、クライアントのサブネットを使用して、条件として、です。 内部のクライアントが属するサブネットを特定する場合は、クライアントのサブネットに基づいて区別するために DNS のポリシーを構成できます。 クライアントのサブネットの条件を使用したトラフィック管理を構成する方法については、次を参照してください。 [のプライマリ サーバーの地理的な場所ベースのトラフィック管理用の DNS ポリシーを使用して](https://technet.microsoft.com/windows-server-docs/networking/dns/deploy/scenario--use-dns-policy-for-geo-location-based-traffic-management-with-primary-servers)します。

DNS サーバーは、プライベート インターフェイスでクエリを受信したときに、内部のゾーンのスコープから DNS クエリの応答が返されます。

>[!NOTE]
>ポリシーの既定のゾーンのスコープをマッピングするため必要はありません。 

前の図に示すように、次のコマンド例では、10.0.0.56 はプライベート ネットワーク インターフェイスの IP アドレスです。

`Add-DnsServerQueryResolutionPolicy -Name "SplitBrainZonePolicy" -Action ALLOW -ServerInterface "eq,10.0.0.56" -ZoneScope "internal,1" -ZoneName contoso.com`

詳細については、次を参照してください。 [追加 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)します。  


## <a name="example-of-dns-selective-recursion-control"></a><a name="bkmk_recursion"></a>DNS の選択的な再帰制御の例

DNS のポリシーを使用して、DNS 再帰のオプションを選択コントロールの既に説明したシナリオを実現する方法の例を次に示します。

このセクションのトピックは次のとおりです。

- [DNS の選択的再帰制御のしくみ](#bkmk_recursionhow)
- [DNS の選択的な再帰制御を構成する方法](#bkmk_recursionconfigure)

この例では、前の例では、Contoso, www.career.contoso.com で仕事紹介 Web サイトを保持すると、同じ架空の企業で使用します。

DNS スプリット ブレイン展開例では、同じ DNS サーバーは、内部および外部の両方のクライアントに応答し、さまざまな回答を提供します。 

一部の DNS 展開では、外部クライアントの権限を持つネーム サーバーとして機能するだけでなく、内部クライアントの再帰的名前解決を実行すると同じ DNS サーバーを必要があります。 このような状況は、DNS のオプションを選択再帰コントロールと呼ばれます。

Windows Server の以前のバージョンで再帰を有効にするものすべてのゾーンの DNS サーバーの全体で有効であることです。 外部クエリには、DNS サーバーがリッスンしても、いる再帰 DNS サーバーにオープンに競合回避モジュールを行う内部および外部のクライアントは有効です。 

オープンに競合回避モジュールは、リソースの枯渇を受ける可能性があり、リフレクション攻撃を作成する悪意のあるクライアントが悪用される可能性として構成されている DNS サーバー。 

このため、Contoso の DNS 管理者は外部クライアントの再帰的名前解決を実行する contoso.com の DNS サーバーをしません。 のみが必要な内部クライアントの再帰コントロールがある再帰コントロールは外部クライアントのブロックされたことができます。 

次の図は、このシナリオを示しています。

![選択的な再帰コントロール](../../media/DNS-Split-Brain/Dns-Split-Brain-02.jpg) 


### <a name="how-dns-selective-recursion-control-works"></a><a name="bkmk_recursionhow"></a>DNS の選択的再帰制御のしくみ

https://www.microsoft.comなど、Contoso の DNS サーバーに対して権限のないクエリを受信した場合、名前解決の要求は、DNS サーバーのポリシーに対して評価されます。 

ポリシー レベル、ゾーンのため、これらのクエリは、任意のゾーンにも属さない、 \(スプリット ブレインの例で定義されている\) は評価されません。 

DNS サーバーは、再帰ポリシーとプライベート インターフェイスの一致に受信したクエリを評価、 **SplitBrainRecursionPolicy**します。 このポリシーは、再帰が有効になっている再帰スコープを指しています。

次に、DNS サーバーは再帰を実行して、インターネットから https://www.microsoft.com の応答を取得し、応答をローカルにキャッシュします。 

外部インターフェイス、DNS のポリシーの一致なしと既定の再帰設定 - ここでは、クエリを受け取った場合 **無効になっている** -を適用します。

これにより、サーバーが内部クライアントのリゾルバーをキャッシュとして機能しています中に、外部のクライアントのオープンに競合回避モジュールとして機能します。 

### <a name="how-to-configure-dns-selective-recursion-control"></a><a name="bkmk_recursionconfigure"></a>DNS の選択的な再帰制御を構成する方法

コントロールを構成する DNS 選択的な再帰 DNS ポリシーを使用して、次の手順を使用する必要があります。

- [DNS 再帰スコープを作成する](#bkmk_recscopes)
- [DNS 再帰ポリシーを作成する](#bkmk_recpolicy)

#### <a name="create-dns-recursion-scopes"></a><a name="bkmk_recscopes"></a>DNS 再帰スコープを作成する

再帰のスコープは、DNS サーバーで再帰を制御する設定のグループの一意のインスタンスです。 再帰のスコープは、フォワーダの一覧が含まれていて、再帰が有効になっているかどうかを指定します。 DNS サーバーは、多くの再帰スコープを持つことができます。 

従来の再帰設定、フォワーダーの一覧は、既定の再帰範囲として呼ばれます。 追加または既定の名前のドットで識別される再帰スコープを削除できない \("です。"\)します。

この例では、再帰の既定の設定が無効に、再帰が有効になっている内部クライアントの新しい再帰スコープの作成中にします。

    
    Set-DnsServerRecursionScope -Name . -EnableRecursion $False
    Add-DnsServerRecursionScope -Name "InternalClients" -EnableRecursion $True 
    

詳細については、次を参照してください [追加 DnsServerRecursionScope。](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverrecursionscope?view=win10-ps)

#### <a name="create-dns-recursion-policies"></a><a name="bkmk_recpolicy"></a>DNS 再帰ポリシーを作成する

DNS サーバーに特定の条件に一致するクエリのセットに対して再帰適用範囲を選択するための再帰ポリシーを作成できます。 

DNS サーバーがいくつかのクエリの権限を持っていない場合は、DNS サーバーの再帰ポリシーで クエリを解決する方法を制御できます。 

この例では、再帰が有効になっている内部再帰スコープが、プライベートネットワークインターフェイスに関連付けられています。

次のコマンドの例を使用すると、DNS の再帰ポリシーを構成します。

    
    Add-DnsServerQueryResolutionPolicy -Name "SplitBrainRecursionPolicy" -Action ALLOW -ApplyOnRecursion -RecursionScope "InternalClients" -ServerInterfaceIP "EQ,10.0.0.39"
    

詳細については、次を参照してください。 [追加 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)します。

今すぐ選択的な再帰制御の内部クライアントの有効化と、スプリット ブレイン ネーム サーバーまたは DNS サーバーのいずれかの必要な DNS ポリシーで、DNS サーバーを構成します。

何千もの DNS のポリシーに合わせて作成できます、トラフィック管理の要件、DNS サーバーを再起動しなくても - 受信したクエリで、すべての新しいポリシーが動的 - 適用されます。 

詳細については、「 [DNS ポリシーシナリオガイド](DNS-Policy-Scenario-Guide.md)」を参照してください。
