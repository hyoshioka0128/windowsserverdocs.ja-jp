---
title: DHCP DNS レコードの登録のイベントをログ記録
description: このトピックでは、Windows Server 2016 でログ イベントの DHCP サーバーに関する情報を提供します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: beb8c188-6fcf-4520-8825-d17f8ee9fb04
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 61a5099cd5e1ef1d4687baa8c20411c96ea8f519
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="dhcp-logging-events-for-dns-registrations"></a>DHCP DNS 登録のイベントをログ記録

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

DHCP サーバーのイベント ログは、DNS 登録の失敗に関する詳細情報を提供するようになりました。

>[!NOTE]
>多くの場合、DHCP サーバーによって DNS レコードの登録が失敗の理由は、DNS Reverse\ 参照ゾーンが正しく構成されていない、またはまったく構成されていません。

次の新しい DHCP イベントでは、DNS 登録を正しく構成されていないため失敗または DNS Reverse\ 参照ゾーンが見つからないときに簡単に識別するのに役立ちます。

|ID|イベント|値|
|-----|--------------------|--------------------------------------------------------|
|20317|DHCPv4.ForwardRecordDNSFailure|エラー %3 が IPv4 アドレス %1 および %2 の FQDN の転送レコードの登録が失敗しました。 これは、DNS サーバーでこのレコードの前方参照ゾーンが存在しないためにある可能性があります。|
|20318|DHCPv4.ForwardRecordDNSTimeout|エラー %3 が IPv4 アドレス %1 および %2 の FQDN の転送レコードの登録が失敗しました。|
|20319|DHCPv4.PTRRecordDNSFailure|エラー %3 が IPv4 アドレス %1 および %2 の FQDN の PTR レコードの登録が失敗しました。 これは、DNS サーバーでこのレコードの逆引き参照ゾーンが存在しないためにある可能性があります。|
|20320|DHCPv4.PTRRecordDNSTimeout|エラー %3 が IPv4 アドレス %1 および %2 の FQDN の PTR レコードの登録が失敗しました。|
|20321|DHCPv6.ForwardRecordDNSFailure|エラー %3 が IPv6 アドレス %1 および %2 の FQDN の転送レコードの登録が失敗しました。 これは、DNS サーバーでこのレコードの前方参照ゾーンが存在しないためにある可能性があります。|
|20322|DHCPv6.ForwardRecordDNSTimeout|エラー %3 が IPv6 アドレス %1 および %2 の FQDN の転送レコードの登録が失敗しました。|
|20323|DHCPv6.PTRRecordDNSFailure|エラー %3 が IPv6 アドレス %1 および %2 の FQDN の PTR レコードの登録が失敗しました。 これは、DNS サーバーでこのレコードの逆引き参照ゾーンが存在しないためにある可能性があります。|
|20324|DHCPv6.PTRRecordDNSTimeout|エラー %3 が IPv6 アドレス %1 および %2 の FQDN の PTR レコードの登録が失敗しました。|
|20325|DHCPv4.ForwardRecordDNSError|エラー %3 \(%4\) と FQDN %2 の %1 の IPv4 アドレスの PTR レコードの登録に失敗しました。|
|20326|DHCPv6.ForwardRecordDNSError|エラー %3 \(%4\) で IPv6 アドレス %1 および %2 の FQDN の転送レコードの登録が失敗しました|
|20327|DHCPv6.PTRRecordDNSError|エラー %3 \(%4\) と FQDN %2 の %1 の IPv6 アドレスの PTR レコードの登録に失敗しました。|

