---
title: auditpol リスト
description: '**[Auditpol 一覧]** の Windows コマンドに関するトピックでは、監査ポリシーのカテゴリとサブカテゴリの一覧が表示されます。また、ユーザーごとの監査ポリシーが定義されているユーザーが一覧表示されます。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 45502abe-3d6e-4e13-94f0-8e6fcb6db860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9e0aff46e62ea4e4259360b78aae223dfcd66ef7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80851185"
---
# <a name="auditpol-list"></a>auditpol リスト

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

監査ポリシーのカテゴリまたはサブカテゴリの一覧を表示します。または、ユーザーごとの監査ポリシーが定義されているユーザーの一覧を表示します。

## <a name="syntax"></a>構文

```
auditpol /list
[/user|/category|subcategory[:<categoryname>|<{guid}>|*]]
[/v] [/r]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| ------- | -------- |
| /user | ユーザーごとの監査ポリシーが定義されているすべてのユーザーを取得します。 /V パラメーターと共に使用すると、ユーザーのセキュリティ識別子 (SID) も表示されます。 |
| /category | システムによって認識されるカテゴリの名前を表示します。 /V パラメーターと共に使用すると、カテゴリのグローバル一意識別子 (GUID) も表示されます。 |
| /subcategory | サブカテゴリの名前とそれに関連付けられている GUID が表示されます。 |
| /v | カテゴリまたはサブカテゴリの GUID を表示します。または、/user と共に使用すると、各ユーザーの SID が表示されます。 |
| /r | 出力をコンマ区切り値 (CSV) 形式でレポートとして表示します。 |
| /? | コマンド プロンプトでヘルプを表示します。 |

## <a name="remarks"></a>コメント

ユーザーごとのポリシーのすべてのリスト操作について、セキュリティ記述子で設定されたそのオブジェクトに対する読み取りアクセス許可を持っている必要があります。 また、"**監査とセキュリティログの管理**" (SeSecurityPrivilege) ユーザー権利を使用して、リスト操作を実行することもできます。 ただし、この権限により、リスト操作を実行するために必要な追加のアクセス権が許可されます。

## <a name="examples"></a><a name=BKMK_examples></a>例

監査ポリシーが定義されているすべてのユーザーを一覧表示するには、次のように入力します。

```
auditpol /list /user
```

定義済みの監査ポリシーとそれに関連付けられている SID を持つすべてのユーザーを一覧表示するには、次のように入力します。

```
auditpol /list /user /v
```

すべてのカテゴリとサブカテゴリをレポート形式で一覧表示するには、次のように入力します。

```
auditpol /list /subcategory:* /r
```

詳細な追跡カテゴリと DS アクセスカテゴリのサブカテゴリの一覧を表示するには、次のように入力します。

```
auditpol /list /subcategory:detailed Tracking,DS Access
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
