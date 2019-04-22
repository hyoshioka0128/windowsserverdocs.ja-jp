---
title: QoS ポリシーのエラー メッセージおよびイベント メッセージ
description: このトピックでは、Windows Server 2016 でのサービスの品質 (QoS) ポリシーのエラーとイベント メッセージの一覧を示します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 76974e10-6a57-4533-83be-cfd5a0d364a3
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 774d9473beed1da861c6827357710133aeaca15e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824053"
---
# <a name="qos-policy-error-and-event-messages"></a>QoS ポリシーのエラー メッセージおよびイベント メッセージ

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

QoS ポリシーに関連付けられているエラーおよびイベント メッセージを次に示します。  
  
## <a name="informational-messages"></a>情報メッセージ  

QoS ポリシーの情報メッセージの一覧を次に示します。

|||  
|-|-|  
|**メッセージ Id**|16500|  
|**重要度**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_NO_CHANGE|  
|**言語**|日本語|  
|**メッセージ**|コンピューターの QoS ポリシーが正常に更新します。 変更は検出されません。|  
  
|||  
|-|-|  
|**メッセージ Id**|16501|  
|**重要度**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_WITH_CHANGE|  
|**言語**|日本語|  
|**メッセージ**|コンピューターの QoS ポリシーが正常に更新します。 ポリシーの変更が検出されました。|  
  
|||  
|-|-|  
|**メッセージ Id**|16502|  
|**重要度**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_NO_CHANGE|  
|**言語**|日本語|  
|**メッセージ**|ユーザーの QoS ポリシーが正常に更新します。 変更は検出されません。|  
  
|||  
|-|-|  
|**メッセージ Id**|16503|  
|**重要度**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_WITH_CHANGE|  
|**言語**|日本語|  
|**メッセージ**|ユーザーの QoS ポリシーが正常に更新します。 ポリシーの変更が検出されました。|  
  
|||  
|-|-|  
|**メッセージ Id**|16504|  
|**重要度**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NOT_CONFIGURED|  
|**言語**|日本語|  
|**メッセージ**|受信 TCP スループット レベルの高度な QoS 設定が正常に更新されます。 値の設定は、QoS ポリシーによって指定されていません。 ローカル コンピューターの既定値が適用されます。|  
  
|||  
|-|-|  
|**メッセージ Id**|16505|  
|**重要度**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_OFF|  
|**言語**|日本語|  
|**メッセージ**|受信 TCP スループット レベルの高度な QoS 設定が正常に更新されます。 レベル 0 (最小スループット) は、値を設定します。|  
  
|||  
|-|-|  
|**メッセージ Id**|16506|  
|**重要度**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_HIGHLY_RESTRICTED|  
|**言語**|日本語|  
|**メッセージ**|受信 TCP スループット レベルの高度な QoS 設定が正常に更新されます。 レベル 1 は、値を設定します。|  
  
|||  
|-|-|  
|**メッセージ Id**|16507|  
|**重要度**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_RESTRICTED|  
|**言語**|日本語|  
|**メッセージ**|受信 TCP スループット レベルの高度な QoS 設定が正常に更新されます。 値の設定は、レベル 2 です。|  
  
|||  
|-|-|  
|**メッセージ Id**|16508|  
|**重要度**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NORMAL|  
|**言語**|日本語|  
|**メッセージ**|受信 TCP スループット レベルの高度な QoS 設定が正常に更新されます。 レベル 3 (最大のスループット) は、値を設定します。|  
  
|||  
|-|-|  
|**メッセージ Id**|16509|  
|**重要度**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_NOT_CONFIGURED|  
|**言語**|日本語|  
|**メッセージ**|DSCP マーキングの高度な QoS 設定をオーバーライドが正常に更新します。 値を設定することが指定されていません。 アプリケーションでは、QoS ポリシーとは無関係に DSCP 値を設定できます。|  
  
|||  
|-|-|  
|**メッセージ Id**|16510|  
|**重要度**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_IGNORED|  
|**言語**|日本語|  
|**メッセージ**|DSCP マーキングの高度な QoS 設定をオーバーライドが正常に更新します。 アプリケーションの DSCP マーキング要求は無視されます。 QoS ポリシーだけでは、DSCP 値を設定できます。|  
  
|||  
|-|-|  
|**メッセージ Id**|16511|  
|**重要度**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_ALLOWED|  
|**言語**|日本語|  
|**メッセージ**|DSCP マーキングの高度な QoS 設定をオーバーライドが正常に更新します。 アプリケーションでは、QoS ポリシーとは無関係に DSCP 値を設定できます。|  
  
|||  
|-|-|  
|**メッセージ Id**|16512|  
|**重要度**|情報|  
|**SymbolicName**|EVENT_EQOS_INFO_LOCAL_SETTING_DONT_USE_NLA|  
|**言語**|日本語|  
|**メッセージ**|ドメイン ネットワーク カテゴリに基づいた QoS ポリシーの選択的にアプリケーションが無効になりました。 QoS ポリシーは、すべてのネットワーク インターフェイスに適用されます。|  
  
## <a name="warning-messages"></a>警告メッセージ

QoS ポリシーの警告メッセージの一覧を次に示します。

|||  
|-|-|  
|**メッセージ Id**|16600|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_TEST_1|  
|**言語**|日本語|  
|**メッセージ**|EQOS: ***Testing\*\*\*[, with one string] "%2".|  
  
|||  
|-|-|  
|**メッセージ Id**|16601|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_TEST_2|  
|**言語**|日本語|  
|**メッセージ**|EQOS: ***Testing\*\*\*[, with two strings, string1 is] "%2"[, string2 is] "%3".|  
  
|||  
|-|-|  
|**メッセージ Id**|16602|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_VERSION|  
|**言語**|日本語|  
|**メッセージ**|コンピューターの QoS ポリシー"%2"には、無効なバージョン番号があります。 このポリシーは適用されません。|  
  
|||  
|-|-|  
|**メッセージ Id**|16603|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_VERSION|  
|**言語**|日本語|  
|**メッセージ**|ユーザーの QoS ポリシー"%2"では、無効なバージョン番号を持っています。 このポリシーは適用されません。|  
  
|||  
|-|-|  
|**メッセージ Id**|16604|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_PROFILE_NOT_SPECIFIED|  
|**言語**|日本語|  
|**メッセージ**|コンピューターの QoS ポリシー"%2"では、DSCP 値またはスロットル率は指定しません。 このポリシーは適用されません。|  
  
|||  
|-|-|  
|**メッセージ Id**|16605|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_PROFILE_NOT_SPECIFIED|  
|**言語**|日本語|  
|**メッセージ**|ユーザーの QoS ポリシー"%2"では、DSCP 値またはスロットル率は指定しません。 このポリシーは適用されません。|  
  
|||  
|-|-|  
|**メッセージ Id**|16606|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_QUOTA_EXCEEDED|  
|**言語**|日本語|  
|**メッセージ**|コンピューターの QoS ポリシーの最大数を超えています。 QoS ポリシー"%2"と以降のコンピューターの QoS ポリシーは適用されません。|  
  
|||  
|-|-|  
|**メッセージ Id**|16607|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_QUOTA_EXCEEDED|  
|**言語**|日本語|  
|**メッセージ**|QoS ポリシーのユーザーの最大数を超えています。 QoS ポリシー"%2"とその後のユーザーの QoS ポリシーは適用されません。|  
  
|||  
|-|-|  
|**メッセージ Id**|16608|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_CONFLICT|  
|**言語**|日本語|  
|**メッセージ**|コンピューターの QoS ポリシー"%2"は、可能性のあるその他の QoS ポリシーと競合します。 ポリシーの適用に関するルールのドキュメントを参照してください。|  
  
|||  
|-|-|  
|**メッセージ Id**|16609|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_CONFLICT|  
|**言語**|日本語|  
|**メッセージ**|QoS ポリシー"%2"のユーザーは、可能性のあるその他の QoS ポリシーと競合します。 ポリシーの適用に関するルールのドキュメントを参照してください。|  
  
|||  
|-|-|  
|**メッセージ Id**|16610|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_NO_FULLPATH_APPNAME|  
|**言語**|日本語|  
|**メッセージ**|アプリケーションのパスを処理できないために、コンピューターの QoS ポリシー"%2"は無視されました。 アプリケーション パスでは、無効である、無効なドライブ文字を含める、またはマップされたネットワーク ドライブが含まれて可能性があります。|  
  
|||  
|-|-|  
|**メッセージ Id**|16611|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_NO_FULLPATH_APPNAME|  
|**言語**|日本語|  
|**メッセージ**|アプリケーションのパスを処理できないために、ユーザーの QoS ポリシー"%2"は無視されました。 アプリケーション パスでは、無効である、無効なドライブ文字を含める、またはマップされたネットワーク ドライブが含まれて可能性があります。|  
  
## <a name="error-messages"></a>エラー メッセージ  

QoS ポリシーのエラー メッセージの一覧を次に示します。

|||  
|-|-|  
|**メッセージ Id**|16700|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_REFERESH|  
|**言語**|日本語|  
|**メッセージ**|コンピューターの QoS ポリシーを更新できませんでした。 エラー コード:"%2"です。|  
  
|||  
|-|-|  
|**メッセージ Id**|16701|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_REFERESH|  
|**言語**|日本語|  
|**メッセージ**|ユーザーの QoS ポリシーを更新できませんでした。 エラー コード:"%2"です。|  
  
|||  
|-|-|  
|**メッセージ Id**|16702|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_ROOT_KEY|  
|**言語**|日本語|  
|**メッセージ**|QoS は、QoS ポリシーのコンピューター レベルのルート キーを開けませんでした。 エラー コード:"%2"です。|  
  
|||  
|-|-|  
|**メッセージ Id**|16703|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_ROOT_KEY|  
|**言語**|日本語|  
|**メッセージ**|QoS は、QoS ポリシーのユーザー レベルのルート キーを開けませんでした。 エラー コード:"%2"です。|  
  
|||  
|-|-|  
|**メッセージ Id**|16704|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_TOO_LONG|  
|**言語**|日本語|  
|**メッセージ**|コンピューターの QoS ポリシーは、許可されている名前の最大長を超えています。 問題が発生したポリシーは、コンピューター レベル QoS ポリシー ルート キーのインデックス"%2"の下に表示されます。|  
  
|||  
|-|-|  
|**メッセージ Id**|16705|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_TOO_LONG|  
|**言語**|日本語|  
|**メッセージ**|ユーザーの QoS ポリシーは、許可されている名前の最大長を超えています。 問題が発生したポリシーは、ユーザー レベルの QoS ポリシー ルート キーのインデックス"%2"の下に表示されます。|  
  
|||  
|-|-|  
|**メッセージ Id**|16706|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_SIZE_ZERO|  
|**言語**|日本語|  
|**メッセージ**|コンピューター QoS ポリシーが、長さゼロの名。 問題が発生したポリシーは、コンピューター レベル QoS ポリシー ルート キーのインデックス"%2"の下に表示されます。|  
  
|||  
|-|-|  
|**メッセージ Id**|16707|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_SIZE_ZERO|  
|**言語**|日本語|  
|**メッセージ**|ユーザーの QoS ポリシーは、長さ 0 の名前を持ちます。 問題が発生したポリシーは、ユーザー レベルの QoS ポリシー ルート キーのインデックス"%2"の下に表示されます。|  
  
|||  
|-|-|  
|**メッセージ Id**|16708|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_SUBKEY|  
|**言語**|日本語|  
|**メッセージ**|QoS は、QoS ポリシーのコンピューターのレジストリ サブキーを開けませんでした。 ポリシーは、コンピューター レベル QoS ポリシー ルート キーのインデックス"%2"の下に表示されます。|  
  
|||  
|-|-|  
|**メッセージ Id**|16709|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_SUBKEY|  
|**言語**|日本語|  
|**メッセージ**|QoS は、ユーザーの QoS ポリシーのレジストリ サブキーを開けませんでした。 ポリシーは、ユーザー レベルの QoS ポリシー ルート キーのインデックス"%2"の下に表示されます。|  
  
|||  
|-|-|  
|**メッセージ Id**|16710|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_PROCESSING_MACHINE_POLICY_FIELD|  
|**言語**|日本語|  
|**メッセージ**|QoS は、読み取りまたはコンピューターの QoS ポリシー"%3"を"%2"のフィールドの検証に失敗しました。|  
  
|||  
|-|-|  
|**メッセージ Id**|16711|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_PROCESSING_USER_POLICY_FIELD|  
|**言語**|日本語|  
|**メッセージ**|QoS は、読み取りまたはユーザーの QoS ポリシー"%3"を"%2"のフィールドの検証に失敗しました。|  
  
|||  
|-|-|  
|**メッセージ Id**|16712|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_SETTING_TCP_AUTOTUNING|  
|**言語**|日本語|  
|**メッセージ**|QoS の読み取りまたは受信 TCP スループット レベル、エラー コードを設定できませんでした:"%2"です。|  
  
|||  
|-|-|  
|**メッセージ Id**|16713|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_SETTING_APP_MARKING|  
|**言語**|日本語|  
|**メッセージ**|エラー コードを設定します。 無効に QoS を読み取りまたは DSCP マーキングを設定できませんでした:"% 2"です。|  

次のトピックでは、このガイドでは、次を参照してください。 [QoS ポリシーよく寄せられる質問](qos-policy-faq.md)します。

このガイドの最初のトピックを参照してください。[サービスの品質 (QoS) ポリシー](qos-policy-top.md)します。
