---
title: auditpol get
description: Windows コマンド」のトピック**auditpol 取得**-システム ポリシー、ユーザーごとのポリシー、監査オプション、および監査セキュリティ記述子オブジェクトを取得します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 83aa1d9d193db977dfe3d375476106d7d6f81e85
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881543"
---
# <a name="auditpol-get"></a>auditpol get

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

システム ポリシー、ユーザーごとのポリシー、監査オプション、および監査セキュリティ記述子オブジェクトを取得します。

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
|パラメーター|説明|
|-------|--------|
|/user|ユーザーごとの監査ポリシーのクエリ対象のセキュリティ プリンシパルが表示されます。 /Category または/subcategory のいずれかのパラメーターを指定する必要があります。 ユーザーは、セキュリティ識別子 (SID) または名として指定できます。 ユーザー アカウントが指定されていない場合は、システム監査ポリシーが照会されます。|
|/category|グローバル一意識別子 (GUID) または名前で指定された 1 つ以上の監査カテゴリ。 すべての監査カテゴリを照会することを示すアスタリスク (*) を使用可能性があります。|
|/subcategory|GUID または名前で指定された 1 つ以上の監査サブカテゴリ。|
|/sd|監査ポリシーへのアクセスを委任するために使用するセキュリティ記述子を取得します。|
|/オプション|CrashOnAuditFail、バイパス、AuditBaseObjects または AuditBasedirectories オプションについては、既存のポリシーを取得します。|
|/r|レポートのコンマ区切り値 (CSV) 形式で出力が表示されます。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="remarks"></a>注釈
すべてのカテゴリとサブカテゴリは、GUID または引用符で囲まれた名前を指定できます。 ユーザーは、SID または名前で指定できます。
ユーザーごとのポリシーおよびシステム ポリシーのすべての get 操作では、セキュリティ記述子の設定、そのオブジェクトに対する権限を読み取りが必要です。 所有することによって、get 操作を実行することも、**監査とセキュリティ ログの管理**(SeSecurityPrivilege) ユーザー権利。 ただし、この権限は、取得操作を実行する必要はありません、追加のアクセスを許可します。
## <a name="BKMK_examples"></a>例
### <a name="examples-for-the-per-user-audit-policy"></a>ユーザーごとの監査ポリシーの例
Guest アカウントのユーザーごとの監査ポリシーを取得してシステムでは、出力を表示するには、追跡、詳細なし、オブジェクト アクセスのカテゴリを入力します。
```
auditpol /get /user:{S-1-5-21-1443922412-3030960370-963420232-51} /category:"System","detailed Tracking","Object Access"
```
> [!NOTE]
> このコマンドは、2 つのシナリオで役に立ちます。 不審なアクティビティの特定のユーザー アカウントを監視するには、/get/コマンドを使用して追加の監査を有効にする信頼ポリシーを使用して特定のカテゴリの結果を取得することができます。 または、除外ポリシーを使用してそのアカウントの無関係のイベントをフィルター処理する/get/コマンドを使用する場合は、アカウントの監査設定は、余分なイベントが、さまざまなログ記録は、ことができます。 すべてのカテゴリの一覧は、auditpol/list/category コマンドを使用します。
カテゴリとゲスト アカウントに対してシステム カテゴリの下には、そのサブカテゴリの包括的かつ排他的な設定をレポートするには、特定のサブカテゴリのユーザーごとの監査ポリシーを取得するには、次のように入力します。
```
auditpol /get /user:guest /category:"System" /subcategory:{0ccee921a-69ae-11d9-bed3-505054503030}
```
レポートの形式で出力を表示し、コンピューター名、ポリシーの対象、subcategory、subcategory GUID、包含設定、および除外の設定を含める、次のように入力します。
```
auditpol /get /user:guest /category:detailed Tracking" /r
```
### <a name="examples-for-the-system-audit-policy"></a>システム監査ポリシーの例
システム監査ポリシーのカテゴリとサブカテゴリのポリシー設定を報告するには、システムのカテゴリとサブカテゴリのポリシーを取得するには、次のように入力します。
```
auditpol /get /category:"System" /subcategory:{0ccee921a-69ae-11d9-bed3-505054503030}
```
詳細な追跡のカテゴリとサブカテゴリ レポート形式でのポリシーを取得し、コンピューター名、ポリシーの対象、subcategory、サブカテゴリの GUID、包含設定、および除外の設定の種類を含めます。
```
auditpol /get /category:"detailed Tracking" /r
```
Guid では、すべてのサブカテゴリのすべての監査ポリシーの設定をレポートとしては、カテゴリを持つ 2 つのカテゴリのポリシーを取得するには、2 つのカテゴリ、種類を指定します。
```
auditpol /get /category:{69979849-797a-11d9-bed3-505054503030},{69997984a-797a-11d9-bed3-505054503030} subcategory:{0ccee921a-69ae-11d9-bed3-505054503030}
```
### <a name="examples-for-auditing-options"></a>監査オプションの例
有効または無効になっている、AuditBaseObjects オプションのいずれかと、状態を取得するには、次のように入力します。
```
auditpol /get /option:AuditBaseObjects
```
> [!NOTE]
> 使用可能なオプションは AuditBaseObjects、AuditBaseOperations、およびバイパスされます。
有効になっている状態を取得するには、無効な場合、または CrashOnAuditFail オプションの 2 を入力します。
```
auditpol /get /option:CrashOnAuditFail /r
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文キー](command-line-syntax-key.md)
