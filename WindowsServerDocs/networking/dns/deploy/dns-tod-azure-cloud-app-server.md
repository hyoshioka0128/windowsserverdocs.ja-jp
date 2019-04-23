---
title: Azure クラウド アプリケーション サーバーを使用した 1 日の時間に基づく DNS 応答
description: このトピックは、DNS ポリシー シナリオ ガイドの Windows Server 2016 の一部です。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 4846b548-8fbc-4a7f-af13-09e834acdec0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ed6ac2ebc8839d0e7ecee682d7644251f8a59381
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829073"
---
# <a name="dns-responses-based-on-time-of-day-with-an-azure-cloud-app-server"></a>Azure クラウド アプリケーション サーバーを使用した 1 日の時間に基づく DNS 応答

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用すると、1 日の時間に基づき、DNS のポリシーを使用して、アプリケーションの別の地理的に分散インスタンス間でアプリケーションのトラフィックを分散するのに方法について説明します。 

このシナリオでは、別のタイム ゾーンに配置されている、Microsoft Azure でホストされている Web サーバーなどの別のアプリケーション サーバーを 1 つのタイム ゾーンでトラフィックを転送する場合に便利です。 これにより、トラフィックを負荷分散アプリケーションのインスタンス間でのピーク時のトラフィックがプライマリ サーバーが、いつ過負荷の期間します。 

>[!NOTE]
>Azure を使用せず、インテリジェント DNS 応答に DNS のポリシーを使用する方法についてを参照してください。[インテリジェント DNS 応答に基づく 1 日の時間の DNS のポリシーを使用して](Scenario--Use-DNS-Policy-for-Intelligent-DNS-Responses-Based-on-the-Time-of-Day.md)します。 

## <a name="bkmk_azureexample"></a>Azure のクラウド アプリのサーバーの 1 日の時間に基づくインテリジェント DNS 応答の例

1 日の時間に基づくアプリケーションのトラフィックを分散する DNS ポリシーを使用する方法の例を次に示します。

この例は、1 つ架空の会社の Web サイトを通じて、世界各地でオンライン gifting ソリューションを提供する Contoso ギフト サービスを使用して contosogiftservices.com します。 

Contosogiftservices.com web サイトは、シアトル (パブリック ip アドレス 192.68.30.2) の単一のオンプレミス データ センターのみでホストされます。 

DNS サーバーは、オンプレミス データ センターにもあります。 

ビジネスで最近が急増したとき、contosogiftservices.com が訪問者の数を増やす、毎日とサービスの可用性に関する問題を報告した顧客の一部です。 

Contoso ギフト サービスは、サイト分析を実行し、毎晩、現地時間の午後 6 時と午後 9 時間が急増したとき、シアトルの Web サーバーへのトラフィックを検出します。 Web サーバーは、顧客サービス拒否攻撃にその結果、これらのピーク時に増加したトラフィックを処理するためにスケールことはできません。 

これらの時間帯、仮想マシンがによってレンタルはそれが Contoso ギフト サービス contosogiftservices.com 顧客が Web サイトから応答性の高いエクスペリエンスを取得するためには、決定\(VM\)でその Web サーバーのコピーをホストする Microsoft Azure.  

Contoso ギフト サービス Azure から VM (192.68.31.44) のパブリック IP アドレスを取得し、毎日 on Azure の間で 5-10 PM、1 時間のコンティンジェンシー期間のことができます、Web サーバーを展開するオートメーションを開発します。

>[!NOTE]
>Azure Vm の詳細については、次を参照してください[Virtual Machines のドキュメント。](https://azure.microsoft.com/documentation/services/virtual-machines/) 

DNS サーバーは、5 ~ 9 PM 毎日、間のクエリの 30% が Azure で実行されている Web サーバーのインスタンスに送信されるように、ゾーンのスコープおよび DNS のポリシーで構成されます。

次の図は、このシナリオを示しています。

![DNS のポリシーの 1 日の応答時間を](../../media/DNS-Policy-Tod2/dns_policy_tod2.jpg)  

## <a name="bkmk_azurehow"></a>アプリ サーバーが動作する Azure の 1 日の時間に基づくインテリジェント DNS 応答方法
 
この記事で 2 つの別のアプリケーション サーバーの IP アドレスの DNS クエリに応答する DNS サーバーを構成する 1 つの web サーバーは、シアトルおよび、Azure データ センターでは、その他の方法を示します。

DNS サーバーが、シアトルの Web サーバーの IP アドレスを格納しているクライアントへの DNS 応答の 70% とクライアントへの DNS 応答の 30% に送信、ピーク時間の午後 6 時の午後 9 時シアトルに基づいている新しい DNS ポリシーを構成した後nts、新しい Azure の Web サーバーにクライアント トラフィックを誘導とシアトルの Web サーバーが過負荷になることを防ぐための Azure の Web サーバーの IP アドレスを格納しています。 

他のすべての時間帯では、通常のクエリ処理を行うし、オンプレミス データ センター内の web サーバーのレコードを含む既定のゾーンのスコープから応答が送信されます。 

Azure のレコードに 10 分間の TTL は、VM が Azure から削除される前に、LDNS キャッシュからレコードが期限切れようにします。 このようなスケーリングの利点の 1 つは、DNS で、オンプレミス、データを保持することができ、維持にスケール アウトする Azure 需要に応じてことです。

## <a name="bkmk_azureconfigure"></a>アプリの Azure サーバーの時刻に基づくインテリジェント DNS 応答の DNS のポリシーを構成する方法
分散アプリケーションの負荷を 1 日の時間ベースのクエリの応答の DNS のポリシーを構成するには、次の手順を実行する必要があります。


- [ゾーンのスコープを作成します。](#bkmk_zscopes)
- [レコードをゾーンのスコープに追加します。](#bkmk_records)
- [DNS ポリシーを作成します。](#bkmk_policies)


>[!NOTE]
>構成する場合、ゾーンに対して権限のある DNS サーバーでは、これらの手順を実行する必要があります。 次の手順を実行するには、DnsAdmins、またはそれと同等のメンバーシップが必要です。 

次のセクションでは、詳細な構成手順を説明します。

>[!IMPORTANT]
>次のセクションでには、多くのパラメーターの値例にはが含まれている Windows PowerShell コマンド例にはが含まれます。 これらのコマンドで値の例は、これらのコマンドを実行する前に、展開に対応する値を置き換えることを確認します。 


### <a name="bkmk_zscopes"></a>ゾーンのスコープを作成します。
ゾーンのスコープは、ゾーンの一意のインスタンスです。 DNS ゾーンは、独自の DNS レコード セットを格納している各ゾーンのスコープを持つ、複数のゾーン スコープを持つことができます。 同じレコードは、別の IP アドレスを持つ、複数のスコープまたは同じ IP アドレスに存在することができます。 

>[!NOTE]
>既定では、ゾーンのスコープは、DNS ゾーンに存在します。 このゾーンのスコープでは、ゾーンと同じ名前と、従来の DNS の機能がこのスコープで動作します。 

次の例のコマンドを使用すると、Azure のレコードをホストするのにゾーン スコープを作成します。

```
Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "AzureZoneScope"
```

詳細については、次を参照してください [追加 DnsServerZoneScope。](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps)

### <a name="bkmk_records"></a>レコードをゾーンのスコープに追加します。
次の手順では、ゾーンのスコープに Web サーバーのホストを表すレコードを追加します。 

AzureZoneScope では、Azure パブリック クラウドにある 192.68.31.44、IP アドレスを持つレコード www.contosogiftservices.com が追加されます。 

同様に、ゾーンの既定のスコープで\(contosogiftservices.com\)、レコード\(www.contosogiftservices.com\)シアトル、オンプレミスで実行されている Web サーバーの IP アドレス 192.68.30.2 で追加されますデータ センターです。

次の 2 つ目コマンドレットで – ゾーン範囲ゾーン パラメーターは含まれません。 このため、レコードは、既定のゾーン範囲ゾーンに追加されます。 

さらであり、LDNS では、長い時間 - 負荷分散に支障をきたすキャッシュしないように、600s (10 分) ではこの Azure Vm のレコードの TTL が保持されます。 また、Azure Vm は 1 の余分な時間もクライアントにキャッシュされているレコードが解決することであることを確認する緊急時対応策として使用できます。

```
Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.68.31.44" -ZoneScope "AzureZoneScope" –TimeToLive 600

Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.68.30.2"
```

詳細については、次を参照してください。 [追加 DnsServerResourceRecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps)します。  

### <a name="bkmk_policies"></a>DNS ポリシーを作成します。 
ゾーンのスコープが作成された後は、次のようにできるように、これらのスコープの間で着信クエリを配布する DNS ポリシーを作成できます。

1. クライアントの午後 9 時 1 日、30% を午後 6 時からのクライアントの 70% が、シアトル、オンプレミスの Web サーバーの IP アドレスを受信中に、DNS 応答での Azure データ センターで Web サーバーの IP アドレスが表示されます。
2. 他のすべての時刻では、すべてのクライアントでは、シアトル、オンプレミスの Web サーバーの IP アドレスが表示されます。

1 日の時間は、DNS サーバーのローカル時刻で表現する必要があります。

次のコマンドの例を使用すると、DNS のポリシーを作成します。

```
Add-DnsServerQueryResolutionPolicy -Name "Contoso6To9Policy" -Action ALLOW -ZoneScope "contosogiftservices.com,7;AzureZoneScope,3" –TimeOfDay “EQ,18:00-21:00” -ZoneName "contosogiftservices.com" –ProcessingOrder 1
```

詳細については、次を参照してください。 [追加 DnsServerQueryResolutionPolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)します。  
  
これで、DNS サーバーは、1 日の時刻に基づく Azure の Web サーバーにトラフィックをリダイレクトする必要な DNS ポリシーで構成されます。 

式に注意してください。

`
 -ZoneScope "contosogiftservices.com,7;AzureZoneScope,3" –TimeOfDay “EQ,18:00-21:00” 
`

この式は、70% の時間を 30% の時間を Azure の Web サーバーの IP アドレスに送信中に、シアトルの Web サーバーの IP アドレスを送信する DNS サーバーに指示するゾーン範囲ゾーンと重みの組み合わせを使用して、DNS サーバーを構成します。

何千もの DNS のポリシーに合わせて作成できます、トラフィック管理の要件、DNS サーバーを再起動しなくても - 受信したクエリで、すべての新しいポリシーが動的 - 適用されます。
