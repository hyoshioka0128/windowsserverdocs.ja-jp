---
title: auditpol セット
description: Windows コマンド」のトピック**auditpol セット**- ユーザーごとの監査ポリシー、システムの監査ポリシーを設定または監査オプション。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f4947486-87bd-48cb-ba81-7230c8e70895
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c9c0fb17620147d2de5b991c1a9a0fb95e782677
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826993"
---
# <a name="auditpol-set"></a>auditpol セット

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

監査ポリシーの設定ユーザー、システム監査ポリシー、または監査オプション。

## <a name="syntax"></a>構文
```
auditpol /set
[/user[:<username>|<{sid}>][/include][/exclude]]
[/category:<name>|<{guid}>[,:<name|<{guid}> ]]
[/success:<enable>|<disable>][/failure:<enable>|<disable>]
[/subcategory:<name>|<{guid}>[,:<name|<{guid}> ]]
[/success:<enable>|<disable>][/failure:<enable>|<disable>]
[/option:<option name> /value: <enable>|<disable>]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/user|ユーザーごとのカテゴリまたはサブカテゴリで指定されたポリシーの監査対象のセキュリティ プリンシパルが設定されています。 セキュリティ識別子 (SID) または名として、カテゴリまたはサブカテゴリのいずれかのオプションを指定する必要があります。|
|/include|/User; で指定されました。ユーザーのユーザーごとのポリシーはシステム監査ポリシーで指定されていない場合でも生成される監査が発生することを示します。 この設定は既定値であり、どちらの場合は自動的に適用、/が含まれても、/exclude パラメーターを明示的に指定します。|
|/exclude|/User; で指定されました。ユーザーのユーザーごとのポリシーによって、システム監査ポリシーに関係なく抑制する監査が発生することを示します。 この設定では、ローカルの Administrators グループのメンバーであるユーザーは無視されます。|
|/category|グローバル一意識別子 (GUID) または名前で指定された 1 つ以上の監査カテゴリ。 ユーザーが指定されていない場合は、システム ポリシーが設定されます。|
|/subcategory|GUID または名前で指定された 1 つ以上の監査サブカテゴリ。 ユーザーが指定されていない場合は、システム ポリシーが設定されます。|
|/success|成功の監査を指定します。 この設定は既定値であり、/success も/failure パラメーターが明示的に指定されている場合は自動的に適用します。 この設定は、有効または、設定を無効にするかどうかを示すパラメーターを使用する必要があります。|
|/failure|失敗の監査を指定します。 この設定は、有効または、設定を無効にするかどうかを示すパラメーターを使用する必要があります。|
|/オプション|CrashOnAuditFail、バイパス、AuditBaseObjects または AuditBasedirectories オプションについては、監査ポリシーを設定します。|
|/sd|監査ポリシーへのアクセスを委任するために使用するセキュリティ記述子を設定します。 セキュリティ記述子定義言語 (SDDL) を使用してセキュリティ記述子を指定する必要があります。 セキュリティ記述子には、随意アクセス制御リスト (DACL) が必要です。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="remarks"></a>注釈
ユーザーごとのポリシーおよびシステム ポリシーのすべての設定操作では、記述する必要がありますがまたはセキュリティ記述子でそのオブジェクトに対するフル コントロール アクセス許可を設定します。 所有することによって、セットの操作を実行することも、**監査とセキュリティ ログの管理**(SeSecurityPrivilege) ユーザー権利。 ただし、この権限は、設定操作を実行する必要はありません、追加のアクセスを許可します。
## <a name="BKMK_examples"></a>例
### <a name="examples-for-the-per-user-audit-policy"></a>ユーザーごとの監査ポリシーの例
設定を監査するユーザーの試行が成功した場合は、すべての型をユーザーごとのユーザー mikedan の詳細な追跡カテゴリの下のすべてのサブカテゴリのポリシーを監査します。
```
auditpol /set /user:mikedan /category:"detailed Tracking" /include /success:enable
```
名前と GUID、および監査の成功または失敗した試行を非表示には GUID で指定されたサブカテゴリで指定されたカテゴリのユーザーごとの監査ポリシーを設定するには、次のように入力します。
```
auditpol /set /user:mikedan /exclude /category:"Object Access","System",{6997984b-797a-11d9-bed3-505054503030} 
/subcategory:{0ccee9210-69ae-11d9-bed3-505054503030},:{0ccee9211-69ae-11d9-bed3-505054503030}, /success:enable /failure:enable
```
すべてのカテゴリを除くすべての試行の成功の監査の抑制に関する指定されたユーザーのユーザーごとの監査ポリシーを設定するには、次のように入力します。
```
auditpol /set /user:mikedan /exclude /category:* /success:enable
```
### <a name="examples-for-the-system-audit-policy"></a>システム監査ポリシーの例
すべてのサブカテゴリに成功した試行の監査を含める詳細な追跡カテゴリの下の システム監査ポリシーを設定するには、次のように入力します。
```
auditpol /set /category:"detailed Tracking" /success:enable
```
> [!NOTE]
> エラーの設定は変更されません。
(これは暗黙のサブカテゴリがリストされているため)、オブジェクトへのアクセスとシステム カテゴリとサブカテゴリが失敗した試行の抑制と成功した試行の監査の Guid で指定されたシステム監査ポリシーを設定するには、次のように入力します。
```
auditpol /set /subcategory:{0ccee9210-69ae-11d9-bed3-505054503030},{0ccee9211-69ae-11d9-bed3-505054503030}, /failure:disable /success:enable
```
### <a name="example-for-auditing-options"></a>監査オプションの例
監査オプションを CrashOnAuditFail オプションが有効な状態を設定するには、次のように入力します。
```
auditpol /set /option:CrashOnAuditFail /value:enable
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文キー](command-line-syntax-key.md)
