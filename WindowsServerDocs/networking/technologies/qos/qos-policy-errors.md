---
title: QoS ポリシーのエラーとイベントメッセージ
description: このトピックでは、Windows Server 2016 のサービス品質 (QoS) ポリシーのエラーメッセージとイベントメッセージの一覧を示します。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 76974e10-6a57-4533-83be-cfd5a0d364a3
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d0eb137716795c324afcf1a708fff00c2f7266d6
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315561"
---
# <a name="qos-policy-error-and-event-messages"></a>QoS ポリシーのエラーとイベントメッセージ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

次に、QoS ポリシーに関連付けられているエラーメッセージとイベントメッセージを示します。  
  
## <a name="informational-messages"></a>情報メッセージ  

QoS ポリシーの情報メッセージの一覧を次に示します。

|||  
|-|-|  
|**Id**|16500|  
|**順**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_NO_CHANGE|  
|**言語**|日本語|  
|**メッセージ**|コンピューターの QoS ポリシーが正常に更新されました。 変更は検出されませんでした。|  
  
|||  
|-|-|  
|**Id**|16501|  
|**順**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_WITH_CHANGE|  
|**言語**|日本語|  
|**メッセージ**|コンピューターの QoS ポリシーが正常に更新されました。 ポリシーの変更が検出されました。|  
  
|||  
|-|-|  
|**Id**|16502|  
|**順**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_NO_CHANGE|  
|**言語**|日本語|  
|**メッセージ**|ユーザー QoS ポリシーが正常に更新されました。 変更は検出されませんでした。|  
  
|||  
|-|-|  
|**Id**|16503|  
|**順**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_WITH_CHANGE|  
|**言語**|日本語|  
|**メッセージ**|ユーザー QoS ポリシーが正常に更新されました。 ポリシーの変更が検出されました。|  
  
|||  
|-|-|  
|**Id**|16504|  
|**順**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NOT_CONFIGURED|  
|**言語**|日本語|  
|**メッセージ**|受信 TCP スループットレベルの QoS の詳細設定が正常に更新されました。 設定値が QoS ポリシーで指定されていません。 ローカルコンピューターの既定値が適用されます。|  
  
|||  
|-|-|  
|**Id**|16505|  
|**順**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_OFF|  
|**言語**|日本語|  
|**メッセージ**|受信 TCP スループットレベルの QoS の詳細設定が正常に更新されました。 設定値はレベル 0 (最小スループット) です。|  
  
|||  
|-|-|  
|**Id**|16506|  
|**順**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_HIGHLY_RESTRICTED|  
|**言語**|日本語|  
|**メッセージ**|受信 TCP スループットレベルの QoS の詳細設定が正常に更新されました。 設定値は Level 1 です。|  
  
|||  
|-|-|  
|**Id**|16507|  
|**順**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_RESTRICTED|  
|**言語**|日本語|  
|**メッセージ**|受信 TCP スループットレベルの QoS の詳細設定が正常に更新されました。 設定値は Level 2 です。|  
  
|||  
|-|-|  
|**Id**|16508|  
|**順**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NORMAL|  
|**言語**|日本語|  
|**メッセージ**|受信 TCP スループットレベルの QoS の詳細設定が正常に更新されました。 設定値は Level 3 (最大スループット) です。|  
  
|||  
|-|-|  
|**Id**|16509|  
|**順**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_NOT_CONFIGURED|  
|**言語**|日本語|  
|**メッセージ**|DSCP マーキングオーバーライドの高度な QoS 設定が正常に更新されました。 設定値が指定されていません。 アプリケーションでは、QoS ポリシーとは独立して DSCP 値を設定できます。|  
  
|||  
|-|-|  
|**Id**|16510|  
|**順**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_IGNORED|  
|**言語**|日本語|  
|**メッセージ**|DSCP マーキングオーバーライドの高度な QoS 設定が正常に更新されました。 アプリケーションの DSCP マーキング要求は無視されます。 DSCP 値を設定できるのは QoS ポリシーのみです。|  
  
|||  
|-|-|  
|**Id**|16511|  
|**順**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_ALLOWED|  
|**言語**|日本語|  
|**メッセージ**|DSCP マーキングオーバーライドの高度な QoS 設定が正常に更新されました。 アプリケーションでは、QoS ポリシーとは独立して DSCP 値を設定できます。|  
  
|||  
|-|-|  
|**Id**|16512|  
|**順**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_LOCAL_SETTING_DONT_USE_NLA|  
|**言語**|日本語|  
|**メッセージ**|ドメインネットワークカテゴリに基づく QoS ポリシーの選択的適用が無効になっています。 QoS ポリシーは、すべてのネットワークインターフェイスに適用されます。|  
  
## <a name="warning-messages"></a>警告メッセージ

次に、QoS ポリシーの警告メッセージの一覧を示します。

|||  
|-|-|  
|**Id**|16600|  
|**順**|［警告］|  
|**SymbolicName**|EVENT_EQOS_WARNING_TEST_1|  
|**言語**|日本語|  
|**メッセージ**|EQOS: * * * テスト\*\*\*[,、1つの文字列] "%2"。|  
  
|||  
|-|-|  
|**Id**|16601|  
|**順**|［警告］|  
|**SymbolicName**|EVENT_EQOS_WARNING_TEST_2|  
|**言語**|日本語|  
|**メッセージ**|EQOS: * * * テスト\*\*\*[、2つの文字列、string1 は] "%2" [、string2 は] "%3" です。|  
  
|||  
|-|-|  
|**Id**|16602|  
|**順**|［警告］|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_VERSION|  
|**言語**|日本語|  
|**メッセージ**|コンピューターの QoS ポリシー "%2" のバージョン番号が無効です。 このポリシーは適用されません。|  
  
|||  
|-|-|  
|**Id**|16603|  
|**順**|［警告］|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_VERSION|  
|**言語**|日本語|  
|**メッセージ**|ユーザー QoS ポリシー "%2" に無効なバージョン番号が含まれています。 このポリシーは適用されません。|  
  
|||  
|-|-|  
|**Id**|16604|  
|**順**|［警告］|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_PROFILE_NOT_SPECIFIED|  
|**言語**|日本語|  
|**メッセージ**|コンピューターの QoS ポリシー "%2" で、DSCP 値またはスロットル率が指定されていません。 このポリシーは適用されません。|  
  
|||  
|-|-|  
|**Id**|16605|  
|**順**|［警告］|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_PROFILE_NOT_SPECIFIED|  
|**言語**|日本語|  
|**メッセージ**|ユーザー QoS ポリシー "%2" では、DSCP 値またはスロットル率が指定されていません。 このポリシーは適用されません。|  
  
|||  
|-|-|  
|**Id**|16606|  
|**順**|［警告］|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_QUOTA_EXCEEDED|  
|**言語**|日本語|  
|**メッセージ**|コンピューターの QoS ポリシーの最大数を超えました。 QoS ポリシー "%2" とそれ以降のコンピューター QoS ポリシーは適用されません。|  
  
|||  
|-|-|  
|**Id**|16607|  
|**順**|［警告］|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_QUOTA_EXCEEDED|  
|**言語**|日本語|  
|**メッセージ**|ユーザー QoS ポリシーの最大数を超えました。 QoS ポリシー "%2" とそれ以降のユーザー QoS ポリシーは適用されません。|  
  
|||  
|-|-|  
|**Id**|16608|  
|**順**|［警告］|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_CONFLICT|  
|**言語**|日本語|  
|**メッセージ**|コンピューターの QoS ポリシー "%2" は、他の QoS ポリシーと競合する可能性があります。 適用されるポリシーに関する規則については、ドキュメントを参照してください。|  
  
|||  
|-|-|  
|**Id**|16609|  
|**順**|［警告］|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_CONFLICT|  
|**言語**|日本語|  
|**メッセージ**|ユーザーの QoS ポリシー "%2" は、他の QoS ポリシーと競合する可能性があります。 適用されるポリシーに関する規則については、ドキュメントを参照してください。|  
  
|||  
|-|-|  
|**Id**|16610|  
|**順**|［警告］|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_NO_FULLPATH_APPNAME|  
|**言語**|日本語|  
|**メッセージ**|アプリケーションパスを処理できないため、コンピューターの QoS ポリシー "%2" は無視されました。 アプリケーションパスが無効であるか、無効なドライブ文字を含んでいるか、ネットワークにマップされたドライブが含まれている可能性があります。|  
  
|||  
|-|-|  
|**Id**|16611|  
|**順**|［警告］|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_NO_FULLPATH_APPNAME|  
|**言語**|日本語|  
|**メッセージ**|アプリケーションパスを処理できないため、ユーザー QoS ポリシー "%2" は無視されました。 アプリケーションパスが無効であるか、無効なドライブ文字を含んでいるか、ネットワークにマップされたドライブが含まれている可能性があります。|  
  
## <a name="error-messages"></a>エラー メッセージ  

QoS ポリシーのエラーメッセージの一覧を次に示します。

|||  
|-|-|  
|**Id**|16700|  
|**順**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_REFERESH|  
|**言語**|日本語|  
|**メッセージ**|コンピューターの QoS ポリシーを更新できませんでした。 エラーコード: "%2"。|  
  
|||  
|-|-|  
|**Id**|16701|  
|**順**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_REFERESH|  
|**言語**|日本語|  
|**メッセージ**|ユーザー QoS ポリシーを更新できませんでした。 エラーコード: "%2"。|  
  
|||  
|-|-|  
|**Id**|16702|  
|**順**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_ROOT_KEY|  
|**言語**|日本語|  
|**メッセージ**|Qos ポリシーのコンピューターレベルのルートキーを開くことができませんでした。 エラーコード: "%2"。|  
  
|||  
|-|-|  
|**Id**|16703|  
|**順**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_ROOT_KEY|  
|**言語**|日本語|  
|**メッセージ**|Qos ポリシーのユーザーレベルのルートキーを開くことができませんでした。 エラーコード: "%2"。|  
  
|||  
|-|-|  
|**Id**|16704|  
|**順**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_TOO_LONG|  
|**言語**|日本語|  
|**メッセージ**|コンピューターの QoS ポリシーが、許可されている名前の最大長を超えています。 問題のあるポリシーが、インデックス "%2" のコンピューターレベルの QoS ポリシールートキーの下に一覧表示されます。|  
  
|||  
|-|-|  
|**Id**|16705|  
|**順**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_TOO_LONG|  
|**言語**|日本語|  
|**メッセージ**|ユーザーの QoS ポリシーが、許可されている最大名の長さを超えています。 問題のあるポリシーが、インデックス "%2" と共に、ユーザーレベルの QoS ポリシールートキーの下に一覧表示されます。|  
  
|||  
|-|-|  
|**Id**|16706|  
|**順**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_SIZE_ZERO|  
|**言語**|日本語|  
|**メッセージ**|コンピューターの QoS ポリシーの長さはゼロです。 問題のあるポリシーが、インデックス "%2" のコンピューターレベルの QoS ポリシールートキーの下に一覧表示されます。|  
  
|||  
|-|-|  
|**Id**|16707|  
|**順**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_SIZE_ZERO|  
|**言語**|日本語|  
|**メッセージ**|ユーザー QoS ポリシーの長さはゼロです。 問題のあるポリシーが、インデックス "%2" と共に、ユーザーレベルの QoS ポリシールートキーの下に一覧表示されます。|  
  
|||  
|-|-|  
|**Id**|16708|  
|**順**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_SUBKEY|  
|**言語**|日本語|  
|**メッセージ**|QoS は、コンピュータの QoS ポリシーのレジストリサブキーを開くことができませんでした。 ポリシーがコンピューターレベルの QoS ポリシールートキーの下にインデックス "%2" と共に一覧表示されます。|  
  
|||  
|-|-|  
|**Id**|16709|  
|**順**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_SUBKEY|  
|**言語**|日本語|  
|**メッセージ**|QoS は、ユーザー QoS ポリシーのレジストリサブキーを開くことができませんでした。 ポリシーは、インデックス "%2" を使用して、ユーザーレベルの QoS ポリシールートキーの下に一覧表示されます。|  
  
|||  
|-|-|  
|**Id**|16710|  
|**順**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_PROCESSING_MACHINE_POLICY_FIELD|  
|**言語**|日本語|  
|**メッセージ**|QoS は、コンピュータの QoS ポリシー "%3" の "%2" フィールドの読み取りまたは検証に失敗しました。|  
  
|||  
|-|-|  
|**Id**|16711|  
|**順**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_PROCESSING_USER_POLICY_FIELD|  
|**言語**|日本語|  
|**メッセージ**|QoS は、ユーザーの QoS ポリシー "%3" の "%2" フィールドの読み取りまたは検証に失敗しました。|  
  
|||  
|-|-|  
|**Id**|16712|  
|**順**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_SETTING_TCP_AUTOTUNING|  
|**言語**|日本語|  
|**メッセージ**|QoS が受信 TCP スループットレベルを読み取りまたは設定できませんでした。エラーコード: "%2"。|  
  
|||  
|-|-|  
|**Id**|16713|  
|**順**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_SETTING_APP_MARKING|  
|**言語**|日本語|  
|**メッセージ**|QoS が DSCP マーキングオーバーライド設定の読み取りまたは設定に失敗しました。エラーコード: "%2"。|  

このガイドの次のトピックについては、「QoS ポリシーに関して[よく寄せられる質問](qos-policy-faq.md)」を参照してください。

このガイドの最初のトピックについては、「[サービスの品質 (QoS) ポリシー](qos-policy-top.md)」を参照してください。
