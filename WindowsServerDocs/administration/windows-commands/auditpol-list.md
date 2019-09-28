---
title: auditpol リスト
description: '**Auditpol リスト**の Windows コマンドのトピック-監査ポリシーのカテゴリまたはサブカテゴリを一覧表示します。または、ユーザーごとの監査ポリシーが定義されているユーザーの一覧を表示します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 45502abe-3d6e-4e13-94f0-8e6fcb6db860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 27a89ae18838989b4f2df27d777c1c35249b8991
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382458"
---
# <a name="auditpol-list"></a>auditpol リスト

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

監査ポリシーのカテゴリまたはサブカテゴリの一覧を表示します。または、ユーザーごとの監査ポリシーが定義されているユーザーの一覧を表示します。

## <a name="syntax"></a>構文
```
auditpol /list
[/user|/category|subcategory[:<categoryname>|<{guid}>|*]]
[/v] [/r]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/user|ユーザーごとの監査ポリシーが定義されているすべてのユーザーを取得します。 /V パラメーターと共に使用すると、ユーザーのセキュリティ識別子 (SID) も表示されます。|
|/category|システムによって認識されるカテゴリの名前を表示します。 /V パラメーターと共に使用すると、カテゴリのグローバル一意識別子 (GUID) も表示されます。|
|/subcategory|サブカテゴリの名前とそれに関連付けられている GUID が表示されます。|
|/v|カテゴリまたはサブカテゴリの GUID を表示します。または、/user と共に使用すると、各ユーザーの SID が表示されます。|
|/r|出力をコンマ区切り値 (CSV) 形式でレポートとして表示します。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="remarks"></a>コメント
ユーザーごとのポリシーのすべてのリスト操作について、セキュリティ記述子で設定されたそのオブジェクトに対する読み取りアクセス許可を持っている必要があります。 また、"**監査とセキュリティログの管理**" (SeSecurityPrivilege) ユーザー権利を使用して、リスト操作を実行することもできます。 ただし、この権限により、リスト操作を実行するために必要な追加のアクセス権が許可されます。
## <a name="BKMK_examples"></a>例
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
auditpol /list /subcategory:"detailed Tracking","DS Access"
```
#### <a name="additional-references"></a>その他の参照情報
[コマンド ライン構文の記号](command-line-syntax-key.md)
