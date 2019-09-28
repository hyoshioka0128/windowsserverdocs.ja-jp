---
title: DNS レコード登録の DHCP ログイベント
description: このトピックでは、Windows Server 2016 の DHCP サーバーログイベントについて説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: beb8c188-6fcf-4520-8825-d17f8ee9fb04
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ccd8024af30f1103afa8eac52926a6b42d32940a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355425"
---
# <a name="dhcp-logging-events-for-dns-registrations"></a>DNS 登録の DHCP ログイベント

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

DHCP サーバーのイベントログで、DNS 登録エラーに関する詳細情報が提供されるようになりました。

>[!NOTE]
>多くの場合、DHCP サーバーによる DNS レコードの登録に失敗する理由は、DNS 逆引き @ no__t-0Lookup ゾーンが正しく構成されていないか、構成されていないことです。

次の新しい DHCP イベントを使用すると、dns 逆引き @ no__t-0Lookup ゾーンが正しく構成されていないために DNS 登録が失敗したことを簡単に特定できます。

|ID|イベント|値|
|-----|--------------------|--------------------------------------------------------|
|20317|DHCPv4 Recorddnsfailure|IPv4 アドレス% 1 および FQDN% 2 の前方レコード登録がエラー% 3 で失敗しました。 このレコードの前方参照ゾーンが DNS サーバー上に存在しないことが原因である可能性があります。|
|20318|ForwardRecordDNSTimeout|IPv4 アドレス% 1 および FQDN% 2 の前方レコード登録がエラー% 3 で失敗しました。|
|20319|PTRRecordDNSFailure|IPv4 アドレス% 1 および FQDN% 2 の PTR レコードの登録がエラー% 3 で失敗しました。 このレコードの逆引き参照ゾーンが DNS サーバー上に存在しないことが原因である可能性があります。|
|20320|PTRRecordDNSTimeout|IPv4 アドレス% 1 および FQDN% 2 の PTR レコードの登録がエラー% 3 で失敗しました。|
|20321|DHCPv6 ForwardRecordDNSFailure|IPv6 アドレス% 1 および FQDN% 2 の前方レコード登録がエラー% 3 で失敗しました。 このレコードの前方参照ゾーンが DNS サーバー上に存在しないことが原因である可能性があります。|
|20322|ForwardRecordDNSTimeout|IPv6 アドレス% 1 および FQDN% 2 の前方レコード登録がエラー% 3 で失敗しました。|
|20323|PTRRecordDNSFailure|IPv6 アドレス% 1 および FQDN% 2 の PTR レコードの登録がエラー% 3 で失敗しました。 このレコードの逆引き参照ゾーンが DNS サーバー上に存在しないことが原因である可能性があります。|
|20324|PTRRecordDNSTimeout|IPv6 アドレス% 1 および FQDN% 2 の PTR レコードの登録がエラー% 3 で失敗しました。|
|20325|ForwardRecordDNSError|IPv4 アドレス% 1 と FQDN% 2 の PTR レコードの登録がエラー% 3 で失敗しました \(% 4 @ no__t。|
|20326|ForwardRecordDNSError|IPv6 アドレス% 1 および FQDN% 2 の前方レコード登録がエラー% 3 @no__t で失敗しました。-0% 4 @ no__t-1|
|20327|PTRRecordDNSError|IPv6 アドレス% 1 と FQDN% 2 の PTR レコードの登録がエラー% 3 で失敗しました \(% 4 @ no__t。|

