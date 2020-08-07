---
title: auditpol get
description: Auditpol get コマンドの参照記事。システムポリシー、ユーザーごとのポリシー、監査オプション、および監査セキュリティ記述子オブジェクトを取得します。
ms.topic: article
ms.assetid: fe13de4e-836c-4207-b47c-64b6272d6c41
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: edb6619ed551de481b77009c320240951cdca06e
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895434"
---
# <a name="auditpol-get"></a>auditpol get

> 適用対象: Windows Server (半期チャネル)、Windows Server、2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

システムポリシー、ユーザーごとのポリシー、監査オプション、および監査セキュリティ記述子オブジェクトを取得します。

*ユーザーごと*のポリシーと*システム*ポリシーに対して*get*操作を実行するには、セキュリティ記述子でそのオブジェクトの**読み取り**アクセス許可を持っている必要があります。 "**監査とセキュリティログの管理**" (SeSecurityPrivilege) ユーザー権利を持っている場合は、 *get*操作を実行することもできます。 ただし、この権限は、全体的な*get*操作を実行するために必要ではない追加のアクセスを許可します。

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

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| /user | ユーザーごとの監査ポリシーを照会する対象のセキュリティプリンシパルを表示します。 /Category パラメーターまたは/サブカテゴリパラメーターのどちらかを指定する必要があります。 ユーザーは、セキュリティ識別子 (SID) または名前として指定できます。 ユーザーアカウントが指定されていない場合は、システム監査ポリシーが照会されます。 |
| /category | グローバル一意識別子 (GUID) または名前によって指定された1つ以上の監査カテゴリ。 アスタリスク (*) を使用して、すべての監査カテゴリを照会する必要があることを示すことができます。 |
| /subcategory | GUID または名前で指定された1つ以上の監査サブカテゴリ。 |
| /sd | 監査ポリシーへのアクセスを委任するために使用されるセキュリティ記述子を取得します。 |
| /option | CrashOnAuditFail、FullprivilegeAuditing、AuditBaseObjects、または Auditbaseobjects オプションの既存のポリシーを取得します。 |
| /r | 出力をレポート形式で、コンマ区切り値 (CSV) で表示します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

### <a name="remarks"></a>Remarks

すべてのカテゴリおよびサブカテゴリは、引用符 (") で囲まれた GUID または名前で指定できます。 ユーザーは SID または名前で指定できます。

## <a name="examples"></a>例

Guest アカウントのユーザーごとの監査ポリシーを取得し、システムの出力、詳細な追跡、およびオブジェクトアクセスのカテゴリを表示するには、次のように入力します。

```
auditpol /get /user:{S-1-5-21-1443922412-3030960370-963420232-51} /category:System,detailed Tracking,Object Access
```

> [!NOTE]
> このコマンドは、2つのシナリオで役立ちます。 1) 特定のユーザーアカウントで疑わしいアクティビティを監視する場合は、コマンドを使用して、 `/get` 追加の監査を有効にする包含ポリシーを使用して、特定のカテゴリの結果を取得できます。 2) アカウントの監査設定によって多数の余分なイベントがログに記録される場合は、コマンドを使用して、除外ポリシーを使用して `/get` そのアカウントの不要なイベントを除外できます。 すべてのカテゴリの一覧を表示するには、コマンドを使用し `auditpol /list /category` ます。

カテゴリおよび特定のサブカテゴリについて、ユーザーごとの監査ポリシーを取得するには、次のように入力します。これにより、そのサブカテゴリの包括的設定と排他設定が Guest アカウントの [システム] カテゴリに表示されます。

```
auditpol /get /user:guest /category:System /subcategory:{0ccee921a-69ae-11d9-bed3-505054503030}
```

出力をレポート形式で表示し、コンピューター名、ポリシーターゲット、サブカテゴリ、サブカテゴリ GUID、包含設定、および除外設定を含めるには、次のように入力します。

```
auditpol /get /user:guest /category:detailed Tracking /r
```

システム監査ポリシーのカテゴリおよびサブカテゴリポリシー設定を報告するシステムカテゴリおよびサブカテゴリのポリシーを取得するには、次のように入力します。

```
auditpol /get /category:System /subcategory:{0ccee921a-69ae-11d9-bed3-505054503030}
```

詳細な追跡カテゴリおよびレポート形式のサブカテゴリのポリシーを取得し、コンピューター名、ポリシーターゲット、サブカテゴリ、サブカテゴリ GUID、包含設定、および除外設定を含めるには、次のように入力します。

```
auditpol /get /category:detailed Tracking /r
```

Guid として指定されたカテゴリを持つ2つのカテゴリのポリシーを取得し、2つのカテゴリの下にあるすべてのサブカテゴリのすべての監査ポリシー設定を報告するには、次のように入力します。

```
auditpol /get /category:{69979849-797a-11d9-bed3-505054503030},{69997984a-797a-11d9-bed3-505054503030} subcategory:{0ccee921a-69ae-11d9-bed3-505054503030}
```

AuditBaseObjects オプションの状態 (有効または無効) を取得するには、次のように入力します。

```
auditpol /get /option:AuditBaseObjects
```

使用可能なオプションは、AuditBaseObjects、Auditbaseobjects、および FullprivilegeAuditing です。 CrashOnAuditFail オプションの有効、無効、または2の状態を取得するには、次のように入力します。

```
auditpol /get /option:CrashOnAuditFail /r
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [auditpol コマンド](auditpol.md)
