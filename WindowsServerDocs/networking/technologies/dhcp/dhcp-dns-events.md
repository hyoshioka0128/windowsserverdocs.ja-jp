---
title: DNS レコード登録の DHCP ログイベント
description: このトピックでは、Windows Server 2016 の DHCP サーバーログイベントについて説明します。
manager: brianlic
ms.topic: get-started-article
ms.assetid: beb8c188-6fcf-4520-8825-d17f8ee9fb04
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 6dd02ff590c3b616f60ed095d55d00b96c428aab
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942562"
---
# <a name="dhcp-logging-events-for-dns-registrations"></a>DNS 登録の DHCP ログイベント

>適用先:Windows Server (半期チャネル)、Windows Server 2016

DHCP サーバーのイベントログで、DNS 登録エラーに関する詳細情報が提供されるようになりました。

>[!NOTE]
>多くの場合、DNS 逆引き \- 参照ゾーンが正しく構成されていないか、構成されていないことが原因で、DHCP サーバーによる dns レコードの登録が失敗します。

次の新しい DHCP イベントを使用すると、dns 逆引き参照ゾーンが正しく構成されていないか見つからないために DNS 登録が失敗したことを簡単に特定でき \- ます。

|id|Event|値|
|-----|--------------------|--------------------------------------------------------|
|20317|DHCPv4 Recorddnsfailure|IPv4 アドレス %1 および FQDN %2 の前方レコード登録がエラー %3 で失敗しました。 このレコードの前方参照ゾーンが DNS サーバー上に存在しないことが原因である可能性があります。|
|20318|ForwardRecordDNSTimeout|IPv4 アドレス %1 および FQDN %2 の前方レコード登録がエラー %3 で失敗しました。|
|20319|PTRRecordDNSFailure|IPv4 アドレス %1 および FQDN %2 の PTR レコードの登録がエラー %3 で失敗しました。 このレコードの逆引き参照ゾーンが DNS サーバー上に存在しないことが原因である可能性があります。|
|20320|PTRRecordDNSTimeout|IPv4 アドレス %1 および FQDN %2 の PTR レコードの登録がエラー %3 で失敗しました。|
|20321|DHCPv6 ForwardRecordDNSFailure|IPv6 アドレス %1 および FQDN %2 の前方レコード登録がエラー %3 で失敗しました。 このレコードの前方参照ゾーンが DNS サーバー上に存在しないことが原因である可能性があります。|
|20322|ForwardRecordDNSTimeout|IPv6 アドレス %1 および FQDN %2 の前方レコード登録がエラー %3 で失敗しました。|
|20323|PTRRecordDNSFailure|IPv6 アドレス %1 および FQDN %2 の PTR レコードの登録がエラー %3 で失敗しました。 このレコードの逆引き参照ゾーンが DNS サーバー上に存在しないことが原因である可能性があります。|
|20324|PTRRecordDNSTimeout|IPv6 アドレス %1 および FQDN %2 の PTR レコードの登録がエラー %3 で失敗しました。|
|20325|ForwardRecordDNSError|IPv4 アドレス %1 および FQDN %2 の PTR レコードの登録に失敗しました。エラー %3 \( %4 \) 。|
|20326|ForwardRecordDNSError|IPv6 アドレス %1 および FQDN %2 の前方レコード登録が、エラー %3 %4 で失敗しました \(\)|
|20327|PTRRecordDNSError|IPv6 アドレス %1 および FQDN %2 の PTR レコードの登録に失敗しました。エラー %3 \( %4 \) 。|

