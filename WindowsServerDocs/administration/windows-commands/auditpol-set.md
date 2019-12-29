---
title: auditpol セット
description: '**Auditpol セット**の Windows コマンドのトピック-ユーザーごとの監査ポリシー、システム監査ポリシー、または監査オプションを設定します。'
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: f3c9ec2fab4cad408e0bb845fe157cfdf94f8e09
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382398"
---
# <a name="auditpol-set"></a>auditpol セット

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ユーザーごとの監査ポリシー、システム監査ポリシー、または監査オプションを設定します。

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

|  パラメーター   |                                                                                                                                          説明                                                                                                                                           |
|--------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    /user     |                                        カテゴリまたはサブカテゴリによって指定されたユーザーごとの監査ポリシーが設定されているセキュリティプリンシパル。 カテゴリまたはサブカテゴリオプションは、セキュリティ識別子 (SID) または名前として指定する必要があります。                                         |
|   /include   | /User で指定します。システム監査ポリシーによって指定されていない場合でも、ユーザーごとのポリシーによって監査が生成されることを示します。 この設定は既定値であり、/include と/exclude の両方のパラメーターが明示的に指定されていない場合に自動的に適用されます。 |
|   /exclude   |                                /User で指定します。ユーザーごとのポリシーによって、システム監査ポリシーに関係なく監査が抑制されることを示します。 ローカルの Administrators グループのメンバーであるユーザーの場合、この設定は無視されます。                                |
|  /category   |                                                                            グローバル一意識別子 (GUID) または名前によって指定された1つ以上の監査カテゴリ。 ユーザーが指定されていない場合は、システムポリシーが設定されます。                                                                             |
| /subcategory |                                                                                         GUID または名前で指定された1つ以上の監査サブカテゴリ。 ユーザーが指定されていない場合は、システムポリシーが設定されます。                                                                                          |
|   /success   |                 成功の監査を指定します。 この設定は既定の設定であり、/成功と失敗の両方のパラメーターが明示的に指定されていない場合に自動的に適用されます。 この設定は、設定を有効にするか無効にするかを示すパラメーターと共に使用する必要があります。                 |
|   /failure   |                                                                                  失敗の監査を指定します。 この設定は、設定を有効にするか無効にするかを示すパラメーターと共に使用する必要があります。                                                                                   |
|   /option    |                                                                                   CrashOnAuditFail、FullprivilegeAuditing、AuditBaseObjects、または Auditbaseobjects オプションの監査ポリシーを設定します。                                                                                    |
|     /sd      |                 監査ポリシーへのアクセスを委任するために使用されるセキュリティ記述子を設定します。 セキュリティ記述子は、セキュリティ記述子定義言語 (SDDL) を使用して指定する必要があります。 セキュリティ記述子には随意アクセス制御リスト (DACL) が必要です。                 |
|      /?      |                                                                                                                              コマンド プロンプトにヘルプを表示します。                                                                                                                              |

## <a name="remarks"></a>コメント
ユーザーごとのポリシーとシステムポリシーのすべての設定操作について、セキュリティ記述子で設定されたオブジェクトに対する書き込みまたはフルコントロールのアクセス許可を持っている必要があります。 **監査とセキュリティログの管理**(SeSecurityPrivilege) ユーザー権利を使用して、設定操作を実行することもできます。 ただし、この権限では、設定操作を実行するために必要な追加のアクセス権が許可されます。
## <a name="BKMK_examples"></a>例
### <a name="examples-for-the-per-user-audit-policy"></a>ユーザーごとの監査ポリシーの例
すべてのユーザーの成功した試行が監査されるように、ユーザーの詳細な追跡カテゴリの下にあるすべてのサブカテゴリについて、ユーザーごとの監査ポリシーを設定するには、次のように入力します。
```
auditpol /set /user:mikedan /category:"detailed Tracking" /include /success:enable
```
名前と GUID で指定されたカテゴリに対してユーザーごとの監査ポリシーを設定し、GUID によって指定されたサブカテゴリに対して、成功または失敗した試行の監査を抑制するには、次のように入力します。
```
auditpol /set /user:mikedan /exclude /category:"Object Access","System",{6997984b-797a-11d9-bed3-505054503030} 
/subcategory:{0ccee9210-69ae-11d9-bed3-505054503030},:{0ccee9211-69ae-11d9-bed3-505054503030}, /success:enable /failure:enable
```
すべてのカテゴリについて、指定したユーザーについて、すべての監査ポリシーを設定するには、次のように入力します。
```
auditpol /set /user:mikedan /exclude /category:* /success:enable
```
### <a name="examples-for-the-system-audit-policy"></a>システム監査ポリシーの例
[詳細な追跡] カテゴリのすべてのサブカテゴリについて、成功した試行のみの監査を含めるようにシステム監査ポリシーを設定するには、次のように入力します。
```
auditpol /set /category:"detailed Tracking" /success:enable
```
> [!NOTE]
> エラーの設定は変更されません。
> オブジェクトアクセスおよびシステムカテゴリ (サブカテゴリが一覧表示されているために暗黙的に使用される) と、失敗した試行を監査するために Guid によって指定されたサブカテゴリのシステム監査ポリシーを設定するには、次のように入力します。
> ```
> auditpol /set /subcategory:{0ccee9210-69ae-11d9-bed3-505054503030},{0ccee9211-69ae-11d9-bed3-505054503030}, /failure:disable /success:enable
> ```
> ### <a name="example-for-auditing-options"></a>監査オプションの例
> 監査オプションを [CrashOnAuditFail] オプションの [有効] 状態に設定するには、次のように入力します。
> ```
> auditpol /set /option:CrashOnAuditFail /value:enable
> ```
> #### <a name="additional-references"></a>その他の参照情報
> [コマンド ライン構文の記号](command-line-syntax-key.md)
