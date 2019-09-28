---
title: auditpol の取得
description: '**Auditpol get**の Windows コマンドトピックでは、システムポリシー、ユーザーごとのポリシー、監査オプション、および監査セキュリティ記述子オブジェクトを取得します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fe13de4e-836c-4207-b47c-64b6272d6c41
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 296fc5afb540411d76b563faca42fc045b8df3b3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382489"
---
# <a name="auditpol-get"></a>auditpol の取得

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

システムポリシー、ユーザーごとのポリシー、監査オプション、および監査セキュリティ記述子オブジェクトを取得します。

## <a name="syntax"></a>構文
```
auditpol /get 
[/user[:<username>|<{sid}>]]
[/category:*|<name>|<{guid}>[,:<name|<{guid}> ]]
[/subcategory:*|<name>|<{guid}>[,:<name|<{guid}> ]]
[/option:<option name>]
[/sd]
[/r]
```
## <a name="parameters"></a>パラメーター

|  パラメーター   |                                                                                                                                         説明                                                                                                                                          |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /user     | ユーザーごとの監査ポリシーを照会する対象のセキュリティプリンシパルを表示します。 /Category パラメーターまたは/サブカテゴリパラメーターのどちらかを指定する必要があります。 ユーザーは、セキュリティ識別子 (SID) または名前として指定できます。 ユーザーアカウントが指定されていない場合は、システム監査ポリシーが照会されます。 |
|  /category   |                                                          グローバル一意識別子 (GUID) または名前によって指定された1つ以上の監査カテゴリ。 アスタリスク (\*) を使用して、すべての監査カテゴリを照会する必要があることを示すことができます。                                                          |
| /subcategory |                                                                                                                  GUID または名前で指定された1つ以上の監査サブカテゴリ。                                                                                                                  |
|     /sd      |                                                                                                        監査ポリシーへのアクセスを委任するために使用されるセキュリティ記述子を取得します。                                                                                                        |
|   /option    |                                                                              CrashOnAuditFail、FullprivilegeAuditing、AuditBaseObjects、または Auditbaseobjects オプションの既存のポリシーを取得します。                                                                               |
|      /r      |                                                                                                              出力をレポート形式で、コンマ区切り値 (CSV) で表示します。                                                                                                              |
|      /?      |                                                                                                                             コマンド プロンプトにヘルプを表示します。                                                                                                                             |

## <a name="remarks"></a>コメント
すべてのカテゴリおよびサブカテゴリは、引用符で囲まれた GUID または名前で指定できます。 ユーザーは SID または名前で指定できます。
ユーザーごとのポリシーとシステムポリシーのすべての取得操作について、セキュリティ記述子で設定されたそのオブジェクトに対する読み取りアクセス許可が必要です。 また、"**監査とセキュリティログの管理**" (SeSecurityPrivilege) ユーザー権利を所有して、get 操作を実行することもできます。 ただし、この権限により、取得操作を実行するために必要な追加のアクセス権が許可されます。
## <a name="BKMK_examples"></a>例
### <a name="examples-for-the-per-user-audit-policy"></a>ユーザーごとの監査ポリシーの例
Guest アカウントのユーザーごとの監査ポリシーを取得し、システムの出力、詳細な追跡、およびオブジェクトアクセスのカテゴリを表示するには、次のように入力します。
```
auditpol /get /user:{S-1-5-21-1443922412-3030960370-963420232-51} /category:"System","detailed Tracking","Object Access"
```
> [!NOTE]
> このコマンドは、2つのシナリオで役立ちます。 特定のユーザーアカウントで不審なアクティビティが発生していないかを監視する場合、追加の監査を有効にする包含ポリシーを使用して、/get コマンドを使用して特定のカテゴリの結果を取得できます。 また、アカウントの監査設定によって大量のイベントが大量にログに記録されている場合は、/get コマンドを使用して、除外ポリシーによってそのアカウントの不要なイベントをフィルターで除外できます。 すべてのカテゴリの一覧を表示するには、auditpol/list/category コマンドを使用します。
> カテゴリおよび特定のサブカテゴリについて、ユーザーごとの監査ポリシーを取得するには、次のように入力します。これにより、そのサブカテゴリの包括的設定と排他設定が Guest アカウントの [システム] カテゴリに表示されます。
> ```
> auditpol /get /user:guest /category:"System" /subcategory:{0ccee921a-69ae-11d9-bed3-505054503030}
> ```
> 出力をレポート形式で表示し、コンピューター名、ポリシーターゲット、サブカテゴリ、サブカテゴリ GUID、包含設定、および除外設定を含めるには、次のように入力します。
> ```
> auditpol /get /user:guest /category:detailed Tracking" /r
> ```
> ### <a name="examples-for-the-system-audit-policy"></a>システム監査ポリシーの例
> システム監査ポリシーのカテゴリおよびサブカテゴリポリシー設定を報告するシステムカテゴリおよびサブカテゴリのポリシーを取得するには、次のように入力します。
> ```
> auditpol /get /category:"System" /subcategory:{0ccee921a-69ae-11d9-bed3-505054503030}
> ```
> 詳細な追跡カテゴリおよびレポート形式のサブカテゴリのポリシーを取得し、コンピューター名、ポリシーターゲット、サブカテゴリ、サブカテゴリ GUID、包含設定、および除外設定を含めるには、次のように入力します。
> ```
> auditpol /get /category:"detailed Tracking" /r
> ```
> Guid として指定されたカテゴリを持つ2つのカテゴリのポリシーを取得し、2つのカテゴリの下にあるすべてのサブカテゴリのすべての監査ポリシー設定を報告するには、次のように入力します。
> ```
> auditpol /get /category:{69979849-797a-11d9-bed3-505054503030},{69997984a-797a-11d9-bed3-505054503030} subcategory:{0ccee921a-69ae-11d9-bed3-505054503030}
> ```
> ### <a name="examples-for-auditing-options"></a>監査オプションの例
> AuditBaseObjects オプションの状態 (有効または無効) を取得するには、次のように入力します。
> ```
> auditpol /get /option:AuditBaseObjects
> ```
> [!NOTE]
> 使用可能なオプションは、AuditBaseObjects、Auditbaseobjects、および FullprivilegeAuditing です。
> CrashOnAuditFail オプションの有効、無効、または2の状態を取得するには、次のように入力します。
> ```
> auditpol /get /option:CrashOnAuditFail /r
> ```
> #### <a name="additional-references"></a>その他の参照情報
> [コマンド ライン構文の記号](command-line-syntax-key.md)
