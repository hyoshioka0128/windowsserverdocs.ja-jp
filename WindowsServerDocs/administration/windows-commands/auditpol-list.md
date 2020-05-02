---
title: auditpol リスト
description: '[Auditpol リスト] コマンドのリファレンストピック。監査ポリシーのカテゴリとサブカテゴリを一覧表示したり、ユーザーごとの監査ポリシーが定義されているユーザーの一覧を表示したりします。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 45502abe-3d6e-4e13-94f0-8e6fcb6db860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 96ee4388c716c066a2e9b55b57dd2e70b4b4f69c
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82719096"
---
# <a name="auditpol-list"></a>auditpol リスト

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

監査ポリシーのカテゴリとサブカテゴリを一覧表示します。または、ユーザーごとの監査ポリシーが定義されているユーザーの一覧を表示します。

*ユーザーごと*のポリシーに対して*リスト*操作を実行するには、セキュリティ記述子でそのオブジェクトの**読み取り**アクセス許可を持っている必要があります。 また、"**監査とセキュリティログの管理**" (SeSecurityPrivilege) ユーザー権利を持っている場合は、*リスト*操作を実行することもできます。 ただし、この権限を使用すると、*リスト*操作全体を実行するために必要な追加のアクセス権が許可されます。

## <a name="syntax"></a>構文

```
auditpol /list
[/user|/category|subcategory[:<categoryname>|<{guid}>|*]]
[/v] [/r]
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| ------- | -------- |
| /user | ユーザーごとの監査ポリシーが定義されているすべてのユーザーを取得します。 /V パラメーターと共に使用すると、ユーザーのセキュリティ識別子 (SID) も表示されます。 |
| /category | システムによって認識されるカテゴリの名前を表示します。 /V パラメーターと共に使用すると、カテゴリのグローバル一意識別子 (GUID) も表示されます。 |
| /subcategory | サブカテゴリの名前とそれに関連付けられている GUID が表示されます。 |
| /v | カテゴリまたはサブカテゴリの GUID を表示します。または、/user と共に使用すると、各ユーザーの SID が表示されます。 |
| /r | 出力をコンマ区切り値 (CSV) 形式でレポートとして表示します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="examples"></a>例

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

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [auditpol コマンド](auditpol.md)
