---
title: DHCP DNS レコードの登録のイベントをログ記録
description: このトピックでは、Windows Server 2016 でのログ記録イベント DHCP サーバーに関する情報を提供します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: beb8c188-6fcf-4520-8825-d17f8ee9fb04
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7f4ce217b19cfd8a63bff1ae504362d4fc24fcd0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816903"
---
# <a name="dhcp-logging-events-for-dns-registrations"></a>DHCP DNS 登録のイベントをログ記録

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

DHCP サーバーのイベント ログは、DNS 登録エラーに関する詳細情報を提供します。

>[!NOTE]
>多くの場合、DHCP サーバーによって DNS レコードの登録エラーの理由は、DNS が反転\-参照ゾーンが正しく構成されていないか、まったく構成されていません。

次の新しい DHCP イベントでは、DNS 登録が間違っているため失敗するか DNS 逆引き不足しているときに簡単に識別するのに役立つ\-参照ゾーン。

|ID|event|値|
|-----|--------------------|--------------------------------------------------------|
|20317|DHCPv4.ForwardRecordDNSFailure|エラー %3 で IPv4 アドレス %1 と %2 の FQDN の転送レコードの登録が失敗しました。 これは、このレコードの前方参照ゾーンが DNS サーバーに存在しないためする可能性があります。|
|20318|DHCPv4.ForwardRecordDNSTimeout|エラー %3 で IPv4 アドレス %1 と %2 の FQDN の転送レコードの登録が失敗しました。|
|20319|DHCPv4.PTRRecordDNSFailure|エラー %3 で IPv4 アドレス %1 と %2 の FQDN の PTR レコードの登録が失敗しました。 これは、このレコードの逆引き参照ゾーンが DNS サーバーに存在しないためする可能性があります。|
|20320|DHCPv4.PTRRecordDNSTimeout|エラー %3 で IPv4 アドレス %1 と %2 の FQDN の PTR レコードの登録が失敗しました。|
|20321|DHCPv6.ForwardRecordDNSFailure|エラー %3 で IPv6 アドレス %1 と %2 の FQDN の転送レコードの登録が失敗しました。 これは、このレコードの前方参照ゾーンが DNS サーバーに存在しないためする可能性があります。|
|20322|DHCPv6.ForwardRecordDNSTimeout|エラー %3 で IPv6 アドレス %1 と %2 の FQDN の転送レコードの登録が失敗しました。|
|20323|DHCPv6.PTRRecordDNSFailure|エラー %3 で IPv6 アドレス %1 と %2 の FQDN の PTR レコードの登録が失敗しました。 これは、このレコードの逆引き参照ゾーンが DNS サーバーに存在しないためする可能性があります。|
|20324|DHCPv6.PTRRecordDNSTimeout|エラー %3 で IPv6 アドレス %1 と %2 の FQDN の PTR レコードの登録が失敗しました。|
|20325|DHCPv4.ForwardRecordDNSError|エラー %3 の %1 の IPv4 アドレスと FQDN %2 の PTR レコードの登録に失敗しました\(%4\)します。|
|20326|DHCPv6.ForwardRecordDNSError|エラー %3 で IPv6 アドレス %1 と %2 の FQDN の転送レコードの登録が失敗しました\(%4\)|
|20327|DHCPv6.PTRRecordDNSError|エラー %3 で IPv6 アドレス %1 と %2 の FQDN の PTR レコードの登録が失敗しました\(%4\)します。|

