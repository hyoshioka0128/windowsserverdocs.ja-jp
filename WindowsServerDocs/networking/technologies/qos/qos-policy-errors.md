---
title: QoS ポリシーのエラーとイベントメッセージ
description: このトピックでは、Windows Server 2016 のサービス品質 (QoS) ポリシーのエラーメッセージとイベントメッセージの一覧を示します。
ms.topic: article
ms.assetid: 76974e10-6a57-4533-83be-cfd5a0d364a3
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: dc100c7ae8ff4ab65dc8cacdde9d46ade8d2b20e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87940023"
---
# <a name="qos-policy-error-and-event-messages"></a>QoS ポリシーのエラーとイベントメッセージ

>適用先:Windows Server (半期チャネル)、Windows Server 2016

次に、QoS ポリシーに関連付けられているエラーメッセージとイベントメッセージを示します。

## <a name="informational-messages"></a>情報メッセージ

QoS ポリシーの情報メッセージの一覧を次に示します。

|||
|-|-|
|**MessageId**|16500|
|**重大度**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_NO_CHANGE|
|**Language**|英語|
|**Message**|コンピューターの QoS ポリシーが正常に更新されました。 変更は検出されませんでした。|

|||
|-|-|
|**MessageId**|16501|
|**重大度**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_WITH_CHANGE|
|**Language**|英語|
|**Message**|コンピューターの QoS ポリシーが正常に更新されました。 ポリシーの変更が検出されました。|

|||
|-|-|
|**MessageId**|16502|
|**重大度**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_NO_CHANGE|
|**Language**|英語|
|**Message**|ユーザー QoS ポリシーが正常に更新されました。 変更は検出されませんでした。|

|||
|-|-|
|**MessageId**|16503|
|**重大度**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_WITH_CHANGE|
|**Language**|英語|
|**Message**|ユーザー QoS ポリシーが正常に更新されました。 ポリシーの変更が検出されました。|

|||
|-|-|
|**MessageId**|16504|
|**重大度**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NOT_CONFIGURED|
|**Language**|英語|
|**Message**|受信 TCP スループットレベルの QoS の詳細設定が正常に更新されました。 設定値が QoS ポリシーで指定されていません。 ローカルコンピューターの既定値が適用されます。|

|||
|-|-|
|**MessageId**|16505|
|**重大度**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_OFF|
|**Language**|英語|
|**Message**|受信 TCP スループットレベルの QoS の詳細設定が正常に更新されました。 設定値はレベル 0 (最小スループット) です。|

|||
|-|-|
|**MessageId**|16506|
|**重大度**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_HIGHLY_RESTRICTED|
|**Language**|英語|
|**Message**|受信 TCP スループットレベルの QoS の詳細設定が正常に更新されました。 設定値は Level 1 です。|

|||
|-|-|
|**MessageId**|16507|
|**重大度**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_RESTRICTED|
|**Language**|英語|
|**Message**|受信 TCP スループットレベルの QoS の詳細設定が正常に更新されました。 設定値は Level 2 です。|

|||
|-|-|
|**MessageId**|16508|
|**重大度**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NORMAL|
|**Language**|英語|
|**Message**|受信 TCP スループットレベルの QoS の詳細設定が正常に更新されました。 設定値は Level 3 (最大スループット) です。|

|||
|-|-|
|**MessageId**|16509|
|**重大度**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_NOT_CONFIGURED|
|**Language**|英語|
|**Message**|DSCP マーキングオーバーライドの高度な QoS 設定が正常に更新されました。 設定値が指定されていません。 アプリケーションでは、QoS ポリシーとは独立して DSCP 値を設定できます。|

|||
|-|-|
|**MessageId**|16510|
|**重大度**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_IGNORED|
|**Language**|英語|
|**Message**|DSCP マーキングオーバーライドの高度な QoS 設定が正常に更新されました。 アプリケーションの DSCP マーキング要求は無視されます。 DSCP 値を設定できるのは QoS ポリシーのみです。|

|||
|-|-|
|**MessageId**|16511|
|**重大度**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_ALLOWED|
|**Language**|英語|
|**Message**|DSCP マーキングオーバーライドの高度な QoS 設定が正常に更新されました。 アプリケーションでは、QoS ポリシーとは独立して DSCP 値を設定できます。|

|||
|-|-|
|**MessageId**|16512|
|**重大度**|Informational|
|**SymbolicName**|EVENT_EQOS_INFO_LOCAL_SETTING_DONT_USE_NLA|
|**Language**|英語|
|**Message**|ドメインネットワークカテゴリに基づく QoS ポリシーの選択的適用が無効になっています。 QoS ポリシーは、すべてのネットワークインターフェイスに適用されます。|

## <a name="warning-messages"></a>警告メッセージ

次に、QoS ポリシーの警告メッセージの一覧を示します。

|||
|-|-|
|**MessageId**|16600|
|**重大度**|警告|
|**SymbolicName**|EVENT_EQOS_WARNING_TEST_1|
|**Language**|英語|
|**Message**|EQOS: * * * テスト \* \* \* [,、1つの文字列] "%2"。|

|||
|-|-|
|**MessageId**|16601|
|**重大度**|警告|
|**SymbolicName**|EVENT_EQOS_WARNING_TEST_2|
|**Language**|英語|
|**Message**|EQOS: * * * テスト \* \* \* [、2つの文字列、string1 は] "%2" [、string2 は] "%3"。|

|||
|-|-|
|**MessageId**|16602|
|**重大度**|警告|
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_VERSION|
|**Language**|英語|
|**Message**|コンピューターの QoS ポリシー "%2" のバージョン番号が無効です。 このポリシーは適用されません。|

|||
|-|-|
|**MessageId**|16603|
|**重大度**|警告|
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_VERSION|
|**Language**|英語|
|**Message**|ユーザー QoS ポリシー "%2" に無効なバージョン番号が含まれています。 このポリシーは適用されません。|

|||
|-|-|
|**MessageId**|16604|
|**重大度**|警告|
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_PROFILE_NOT_SPECIFIED|
|**Language**|英語|
|**Message**|コンピューターの QoS ポリシー "%2" で、DSCP 値またはスロットル率が指定されていません。 このポリシーは適用されません。|

|||
|-|-|
|**MessageId**|16605|
|**重大度**|警告|
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_PROFILE_NOT_SPECIFIED|
|**Language**|英語|
|**Message**|ユーザー QoS ポリシー "%2" では、DSCP 値またはスロットル率が指定されていません。 このポリシーは適用されません。|

|||
|-|-|
|**MessageId**|16606|
|**重大度**|警告|
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_QUOTA_EXCEEDED|
|**Language**|英語|
|**Message**|コンピューターの QoS ポリシーの最大数を超えました。 QoS ポリシー "%2" とそれ以降のコンピューター QoS ポリシーは適用されません。|

|||
|-|-|
|**MessageId**|16607|
|**重大度**|警告|
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_QUOTA_EXCEEDED|
|**Language**|英語|
|**Message**|ユーザー QoS ポリシーの最大数を超えました。 QoS ポリシー "%2" とそれ以降のユーザー QoS ポリシーは適用されません。|

|||
|-|-|
|**MessageId**|16608|
|**重大度**|警告|
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_CONFLICT|
|**Language**|英語|
|**Message**|コンピューターの QoS ポリシー "%2" は、他の QoS ポリシーと競合する可能性があります。 適用されるポリシーに関する規則については、ドキュメントを参照してください。|

|||
|-|-|
|**MessageId**|16609|
|**重大度**|警告|
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_CONFLICT|
|**Language**|英語|
|**Message**|ユーザーの QoS ポリシー "%2" は、他の QoS ポリシーと競合する可能性があります。 適用されるポリシーに関する規則については、ドキュメントを参照してください。|

|||
|-|-|
|**MessageId**|16610|
|**重大度**|警告|
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_NO_FULLPATH_APPNAME|
|**Language**|英語|
|**Message**|アプリケーションパスを処理できないため、コンピューターの QoS ポリシー "%2" は無視されました。 アプリケーションパスが無効であるか、無効なドライブ文字を含んでいるか、ネットワークにマップされたドライブが含まれている可能性があります。|

|||
|-|-|
|**MessageId**|16611|
|**重大度**|警告|
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_NO_FULLPATH_APPNAME|
|**Language**|英語|
|**Message**|アプリケーションパスを処理できないため、ユーザー QoS ポリシー "%2" は無視されました。 アプリケーションパスが無効であるか、無効なドライブ文字を含んでいるか、ネットワークにマップされたドライブが含まれている可能性があります。|

## <a name="error-messages"></a>エラー メッセージ

QoS ポリシーのエラーメッセージの一覧を次に示します。

|||
|-|-|
|**MessageId**|16700|
|**重大度**|エラー|
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_REFERESH|
|**Language**|英語|
|**Message**|コンピューターの QoS ポリシーを更新できませんでした。 エラーコード: "%2"。|

|||
|-|-|
|**MessageId**|16701|
|**重大度**|エラー|
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_REFERESH|
|**Language**|英語|
|**Message**|ユーザー QoS ポリシーを更新できませんでした。 エラーコード: "%2"。|

|||
|-|-|
|**MessageId**|16702|
|**重大度**|エラー|
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_ROOT_KEY|
|**Language**|英語|
|**Message**|Qos ポリシーのコンピューターレベルのルートキーを開くことができませんでした。 エラーコード: "%2"。|

|||
|-|-|
|**MessageId**|16703|
|**重大度**|エラー|
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_ROOT_KEY|
|**Language**|英語|
|**Message**|Qos ポリシーのユーザーレベルのルートキーを開くことができませんでした。 エラーコード: "%2"。|

|||
|-|-|
|**MessageId**|16704|
|**重大度**|エラー|
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_TOO_LONG|
|**Language**|英語|
|**Message**|コンピューターの QoS ポリシーが、許可されている名前の最大長を超えています。 問題のあるポリシーが、インデックス "%2" のコンピューターレベルの QoS ポリシールートキーの下に一覧表示されます。|

|||
|-|-|
|**MessageId**|16705|
|**重大度**|エラー|
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_TOO_LONG|
|**Language**|英語|
|**Message**|ユーザーの QoS ポリシーが、許可されている最大名の長さを超えています。 問題のあるポリシーが、インデックス "%2" と共に、ユーザーレベルの QoS ポリシールートキーの下に一覧表示されます。|

|||
|-|-|
|**MessageId**|16706|
|**重大度**|エラー|
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_SIZE_ZERO|
|**Language**|英語|
|**Message**|コンピューターの QoS ポリシーの長さはゼロです。 問題のあるポリシーが、インデックス "%2" のコンピューターレベルの QoS ポリシールートキーの下に一覧表示されます。|

|||
|-|-|
|**MessageId**|16707|
|**重大度**|エラー|
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_SIZE_ZERO|
|**Language**|英語|
|**Message**|ユーザー QoS ポリシーの長さはゼロです。 問題のあるポリシーが、インデックス "%2" と共に、ユーザーレベルの QoS ポリシールートキーの下に一覧表示されます。|

|||
|-|-|
|**MessageId**|16708|
|**重大度**|エラー|
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_SUBKEY|
|**Language**|英語|
|**Message**|QoS は、コンピュータの QoS ポリシーのレジストリサブキーを開くことができませんでした。 ポリシーがコンピューターレベルの QoS ポリシールートキーの下にインデックス "%2" と共に一覧表示されます。|

|||
|-|-|
|**MessageId**|16709|
|**重大度**|エラー|
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_SUBKEY|
|**Language**|英語|
|**Message**|QoS は、ユーザー QoS ポリシーのレジストリサブキーを開くことができませんでした。 ポリシーは、インデックス "%2" を使用して、ユーザーレベルの QoS ポリシールートキーの下に一覧表示されます。|

|||
|-|-|
|**MessageId**|16710|
|**重大度**|エラー|
|**SymbolicName**|EVENT_EQOS_ERROR_PROCESSING_MACHINE_POLICY_FIELD|
|**Language**|英語|
|**Message**|QoS は、コンピュータの QoS ポリシー "%3" の "%2" フィールドの読み取りまたは検証に失敗しました。|

|||
|-|-|
|**MessageId**|16711|
|**重大度**|エラー|
|**SymbolicName**|EVENT_EQOS_ERROR_PROCESSING_USER_POLICY_FIELD|
|**Language**|英語|
|**Message**|QoS は、ユーザーの QoS ポリシー "%3" の "%2" フィールドの読み取りまたは検証に失敗しました。|

|||
|-|-|
|**MessageId**|16712|
|**重大度**|エラー|
|**SymbolicName**|EVENT_EQOS_ERROR_SETTING_TCP_AUTOTUNING|
|**Language**|英語|
|**Message**|QoS が受信 TCP スループットレベルを読み取りまたは設定できませんでした。エラーコード: "%2"。|

|||
|-|-|
|**MessageId**|16713|
|**重大度**|エラー|
|**SymbolicName**|EVENT_EQOS_ERROR_SETTING_APP_MARKING|
|**Language**|英語|
|**Message**|QoS が DSCP マーキングオーバーライド設定の読み取りまたは設定に失敗しました。エラーコード: "%2"。|

このガイドの次のトピックについては、「QoS ポリシーに関して[よく寄せられる質問](qos-policy-faq.md)」を参照してください。

このガイドの最初のトピックについては、「[サービスの品質 (QoS) ポリシー](qos-policy-top.md)」を参照してください。
