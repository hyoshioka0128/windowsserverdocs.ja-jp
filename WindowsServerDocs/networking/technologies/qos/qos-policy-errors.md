---
title: QoS ポリシーのエラーおよびイベント メッセージ
description: このトピックでは、Windows Server 2016 でのサービスの品質 (QoS) ポリシーのエラーとイベント メッセージの一覧を示します。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 76974e10-6a57-4533-83be-cfd5a0d364a3
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e2e890a7947d4f7de09159d7de606c0542f45045
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="qos-policy-error-and-event-messages"></a>QoS ポリシーのエラーおよびイベント メッセージ

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

QoS ポリシーに関連付けられているエラーとイベント メッセージを次に示します。  
  
## <a name="informational-messages"></a>情報メッセージ  

QoS ポリシーの情報メッセージの一覧を次に示します。

|||  
|-|-|  
|**メッセージ Id**|16500|  
|**重要度**|情報提供|  
|**SymbolicName**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_NO_CHANGE|  
|**言語**|英語|  
|**メッセージ**|コンピューターの QoS ポリシーの更新が完了します。 変更は検出されません。|  
  
|||  
|-|-|  
|**メッセージ Id**|16501|  
|**重要度**|情報提供|  
|**SymbolicName**|EVENT_EQOS_INFO_MACHINE_POLICY_REFRESH_WITH_CHANGE|  
|**言語**|英語|  
|**メッセージ**|コンピューターの QoS ポリシーの更新が完了します。 ポリシーの変更が検出されました。|  
  
|||  
|-|-|  
|**メッセージ Id**|16502|  
|**重要度**|情報提供|  
|**SymbolicName**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_NO_CHANGE|  
|**言語**|英語|  
|**メッセージ**|ユーザーの QoS ポリシーの更新が完了します。 変更は検出されません。|  
  
|||  
|-|-|  
|**メッセージ Id**|16503|  
|**重要度**|情報提供|  
|**SymbolicName**|EVENT_EQOS_INFO_USER_POLICY_REFRESH_WITH_CHANGE|  
|**言語**|英語|  
|**メッセージ**|ユーザーの QoS ポリシーの更新が完了します。 ポリシーの変更が検出されました。|  
  
|||  
|-|-|  
|**メッセージ Id**|16504|  
|**重要度**|情報提供|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NOT_CONFIGURED|  
|**言語**|英語|  
|**メッセージ**|受信 TCP スループット レベルの QoS の高度な設定が正常に更新されます。 値に設定するすべての QoS ポリシーでは指定されません。 ローカル コンピューターの既定値が適用されます。|  
  
|||  
|-|-|  
|**メッセージ Id**|16505|  
|**重要度**|情報提供|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_OFF|  
|**言語**|英語|  
|**メッセージ**|受信 TCP スループット レベルの QoS の高度な設定が正常に更新されます。 レベル 0 (最低限のスループット) は、値を設定します。|  
  
|||  
|-|-|  
|**メッセージ Id**|16506|  
|**重要度**|情報提供|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_HIGHLY_RESTRICTED|  
|**言語**|英語|  
|**メッセージ**|受信 TCP スループット レベルの QoS の高度な設定が正常に更新されます。 レベル 1 は、値を設定します。|  
  
|||  
|-|-|  
|**メッセージ Id**|16507|  
|**重要度**|情報提供|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_RESTRICTED|  
|**言語**|英語|  
|**メッセージ**|受信 TCP スループット レベルの QoS の高度な設定が正常に更新されます。 第 2 レベルは、値を設定します。|  
  
|||  
|-|-|  
|**メッセージ Id**|16508|  
|**重要度**|情報提供|  
|**SymbolicName**|EVENT_EQOS_INFO_TCP_AUTOTUNING_NORMAL|  
|**言語**|英語|  
|**メッセージ**|受信 TCP スループット レベルの QoS の高度な設定が正常に更新されます。 レベル 3 (最大スループット) は、値を設定します。|  
  
|||  
|-|-|  
|**メッセージ Id**|16509|  
|**重要度**|情報提供|  
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_NOT_CONFIGURED|  
|**言語**|英語|  
|**メッセージ**|DSCP マーキングの QoS の高度な設定は上書きが正常に更新します。 値を設定することは指定されません。 アプリケーションは、QoS ポリシーとは別の DSCP 値を設定できます。|  
  
|||  
|-|-|  
|**メッセージ Id**|16510|  
|**重要度**|情報提供|  
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_IGNORED|  
|**言語**|英語|  
|**メッセージ**|DSCP マーキングの QoS の高度な設定は上書きが正常に更新します。 アプリケーションの DSCP マーキング要求は無視されます。 QoS ポリシーだけでは、DSCP 値を設定できます。|  
  
|||  
|-|-|  
|**メッセージ Id**|16511|  
|**重要度**|情報提供|  
|**SymbolicName**|EVENT_EQOS_INFO_APP_MARKING_ALLOWED|  
|**言語**|英語|  
|**メッセージ**|DSCP マーキングの QoS の高度な設定は上書きが正常に更新します。 アプリケーションは、QoS ポリシーとは別の DSCP 値を設定できます。|  
  
|||  
|-|-|  
|**メッセージ Id**|16512|  
|**重要度**|情報提供|  
|**SymbolicName**|EVENT_EQOS_INFO_LOCAL_SETTING_DONT_USE_NLA|  
|**言語**|英語|  
|**メッセージ**|選択したアプリケーションがドメイン ネットワーク カテゴリに基づいて QoS ポリシーが無効にします。 QoS ポリシーは、すべてのネットワーク インターフェイスに適用されます。|  
  
## <a name="warning-messages"></a>警告メッセージ

QoS ポリシーの警告メッセージの一覧を次に示します。

|||  
|-|-|  
|**メッセージ Id**|16600|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_TEST_1|  
|**言語**|英語|  
|**メッセージ**|EQOS: * * * Testing\ * \ * \ * [、1 つの文字列]"%2"です。|  
  
|||  
|-|-|  
|**メッセージ Id**|16601|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_TEST_2|  
|**言語**|英語|  
|**メッセージ**|EQOS: * * * Testing\ * \ * \ * [、string1 は、2 つの文字列と]"%2"[、文字列 2]"%3"です。|  
  
|||  
|-|-|  
|**メッセージ Id**|16602|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_VERSION|  
|**言語**|英語|  
|**メッセージ**|コンピューターの QoS ポリシー"%2"には、無効なバージョン番号があります。 このポリシーは適用されません。|  
  
|||  
|-|-|  
|**メッセージ Id**|16603|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_VERSION|  
|**言語**|英語|  
|**メッセージ**|ユーザーの QoS ポリシー"%2"には、無効なバージョン番号があります。 このポリシーは適用されません。|  
  
|||  
|-|-|  
|**メッセージ Id**|16604|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_PROFILE_NOT_SPECIFIED|  
|**言語**|英語|  
|**メッセージ**|コンピューターの QoS ポリシー"%2"では、DSCP 値またはスロットル率は指定されません。 このポリシーは適用されません。|  
  
|||  
|-|-|  
|**メッセージ Id**|16605|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_PROFILE_NOT_SPECIFIED|  
|**言語**|英語|  
|**メッセージ**|ユーザーの QoS ポリシー"%2"は、DSCP 値またはスロットル率を指定しません。 このポリシーは適用されません。|  
  
|||  
|-|-|  
|**メッセージ Id**|16606|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_QUOTA_EXCEEDED|  
|**言語**|英語|  
|**メッセージ**|コンピューターの QoS ポリシーの最大数を超えています。 QoS ポリシー"%2"とそれ以降のコンピューターの QoS ポリシーは適用されません。|  
  
|||  
|-|-|  
|**メッセージ Id**|16607|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_QUOTA_EXCEEDED|  
|**言語**|英語|  
|**メッセージ**|ユーザーの QoS ポリシーの最大数を超えています。 QoS ポリシー"%2"とその後のユーザーの QoS ポリシーは適用されません。|  
  
|||  
|-|-|  
|**メッセージ Id**|16608|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_CONFLICT|  
|**言語**|英語|  
|**メッセージ**|コンピューターの QoS ポリシー"%2"は、可能性のあるその他の QoS ポリシーと競合します。 ポリシーの適用に関する規則のドキュメントを参照してください。|  
  
|||  
|-|-|  
|**メッセージ Id**|16609|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_CONFLICT|  
|**言語**|英語|  
|**メッセージ**|ユーザーの QoS ポリシー"%2"は、可能性のあるその他の QoS ポリシーと競合します。 ポリシーの適用に関する規則のドキュメントを参照してください。|  
  
|||  
|-|-|  
|**メッセージ Id**|16610|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_MACHINE_POLICY_NO_FULLPATH_APPNAME|  
|**言語**|英語|  
|**メッセージ**|アプリケーション パスを処理できないために、コンピューターの QoS ポリシー"%2"が無視されました。 アプリケーション パスでは、無効である、無効なドライブ文字が含まれている、またはネットワークにマップされたドライブが含まれている可能性があります。|  
  
|||  
|-|-|  
|**メッセージ Id**|16611|  
|**重要度**|警告|  
|**SymbolicName**|EVENT_EQOS_WARNING_USER_POLICY_NO_FULLPATH_APPNAME|  
|**言語**|英語|  
|**メッセージ**|アプリケーション パスを処理できないために、ユーザーの QoS ポリシー"%2"が無視されました。 アプリケーション パスでは、無効である、無効なドライブ文字が含まれている、またはネットワークにマップされたドライブが含まれている可能性があります。|  
  
## <a name="error-messages"></a>エラー メッセージ  

QoS ポリシーのエラー メッセージの一覧を次に示します。

|||  
|-|-|  
|**メッセージ Id**|16700|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_REFERESH|  
|**言語**|英語|  
|**メッセージ**|コンピューターの QoS ポリシーを更新できませんでした。 エラー コード:"%2"です。|  
  
|||  
|-|-|  
|**メッセージ Id**|16701|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_REFERESH|  
|**言語**|英語|  
|**メッセージ**|ユーザーの QoS ポリシーを更新できませんでした。 エラー コード:"%2"です。|  
  
|||  
|-|-|  
|**メッセージ Id**|16702|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_ROOT_KEY|  
|**言語**|英語|  
|**メッセージ**|QoS は、QoS ポリシーをコンピューター レベルのルート キーを開けませんでした。 エラー コード:"%2"です。|  
  
|||  
|-|-|  
|**メッセージ Id**|16703|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_ROOT_KEY|  
|**言語**|英語|  
|**メッセージ**|QoS は、QoS ポリシーのユーザー レベルのルート キーを開けませんでした。 エラー コード:"%2"です。|  
  
|||  
|-|-|  
|**メッセージ Id**|16704|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_TOO_LONG|  
|**言語**|英語|  
|**メッセージ**|コンピューターの QoS ポリシーは、許可された名前の最大長を超えています。 問題のあるポリシーがコンピューター レベルの QoS ポリシー ルート キーの下、インデックス"%2"と表示されます。|  
  
|||  
|-|-|  
|**メッセージ Id**|16705|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_TOO_LONG|  
|**言語**|英語|  
|**メッセージ**|ユーザーの QoS ポリシーは、許可された名前の最大長を超えています。 問題のあるポリシーは、ユーザー レベルの QoS ポリシー ルート キーの下、インデックス"%2"と表示されます。|  
  
|||  
|-|-|  
|**メッセージ Id**|16706|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_MACHINE_POLICY_KEYNAME_SIZE_ZERO|  
|**言語**|英語|  
|**メッセージ**|コンピューターの QoS ポリシーは、長さゼロ名を持ちます。 問題のあるポリシーがコンピューター レベルの QoS ポリシー ルート キーの下、インデックス"%2"と表示されます。|  
  
|||  
|-|-|  
|**メッセージ Id**|16707|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_USER_POLICY_KEYNAME_SIZE_ZERO|  
|**言語**|英語|  
|**メッセージ**|ユーザーの QoS ポリシーは、長さゼロの名前を持ちます。 問題のあるポリシーは、ユーザー レベルの QoS ポリシー ルート キーの下、インデックス"%2"と表示されます。|  
  
|||  
|-|-|  
|**メッセージ Id**|16708|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_MACHINE_POLICY_SUBKEY|  
|**言語**|英語|  
|**メッセージ**|QoS は、QoS ポリシーのコンピューターのレジストリ サブキーを開けませんでした。 ポリシーがコンピューター レベルの QoS ポリシー ルート キーの下、インデックス"%2"と表示されます。|  
  
|||  
|-|-|  
|**メッセージ Id**|16709|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_OPENING_USER_POLICY_SUBKEY|  
|**言語**|英語|  
|**メッセージ**|QoS は、ユーザーの QoS ポリシーのレジストリ サブキーを開けませんでした。 ポリシーは、ユーザー レベルの QoS ポリシー ルート キーの下、インデックス"%2"と表示されます。|  
  
|||  
|-|-|  
|**メッセージ Id**|16710|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_PROCESSING_MACHINE_POLICY_FIELD|  
|**言語**|英語|  
|**メッセージ**|QoS は、読み取りまたはコンピューターの QoS ポリシー"%3"の"%2"フィールドの検証に失敗しました。|  
  
|||  
|-|-|  
|**メッセージ Id**|16711|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_PROCESSING_USER_POLICY_FIELD|  
|**言語**|英語|  
|**メッセージ**|QoS は、読み取りまたはユーザーの QoS ポリシー"%3"の"%2"フィールドの検証に失敗しました。|  
  
|||  
|-|-|  
|**メッセージ Id**|16712|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_SETTING_TCP_AUTOTUNING|  
|**言語**|英語|  
|**メッセージ**|QoS の読み取りや受信 TCP スループット レベル、エラー コードを設定できませんでした。"% 2"です。|  
  
|||  
|-|-|  
|**メッセージ Id**|16713|  
|**重要度**|エラー|  
|**SymbolicName**|EVENT_EQOS_ERROR_SETTING_APP_MARKING|  
|**言語**|英語|  
|**メッセージ**|QoS の読み取りや DSCP マーキングを設定できませんでした上書き設定で、エラー コード:"%2"です。|  

このガイドの次のトピックを参照してください。[QoS ポリシーに関してよく寄せられる質問](qos-policy-faq.md)します。

このガイドで最初のトピックを参照してください。[サービスの品質 (QoS) ポリシー](qos-policy-top.md)します。
