---
title: auditpol 一覧
description: Windows コマンド」のトピック**auditpol 一覧**- リスト監査ポリシー カテゴリやサブカテゴリ、またはユーザーごとの監査ポリシーを対象のユーザーがリストを定義します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 08f524ef0aacd731f709ce7a2e17b3d831da1e5b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858583"
---
# <a name="auditpol-list"></a>auditpol 一覧

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リストの監査ポリシー カテゴリやサブカテゴリ、または一覧のユーザーがユーザーごとの監査ポリシーが定義されます。

## <a name="syntax"></a>構文
```
auditpol /list
[/user|/category|subcategory[:<categoryname>|<{guid}>|*]]
[/v] [/r]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|/user|ユーザーごとの監査ポリシーが定義されたすべてのユーザーを取得します。 /V パラメーターを併用する場合も、ユーザーのセキュリティ識別子 (SID) が表示されます。|
|/category|システムで認識されるカテゴリの名前が表示されます。 /V パラメーターを併用する場合も、カテゴリのグローバル一意識別子 (GUID) が表示されます。|
|/subcategory|サブカテゴリと、関連付けられている GUID の名前が表示されます。|
|/v|カテゴリまたはサブカテゴリを GUID を表示または/user を併用すると、各ユーザーの SID を表示します。|
|/r|コンマ区切り値 (CSV) 形式でレポートをレポートとして出力が表示されます。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="remarks"></a>注釈
ユーザーごとのポリシーのすべての一覧操作では、セキュリティ記述子の設定、そのオブジェクトに対する権限を読み取りが必要です。 所有することによって、リスト操作を実行することも、**監査とセキュリティ ログの管理**(SeSecurityPrivilege) ユーザー権利。 ただし、この権限は、リスト操作を実行する必要はありません、追加のアクセスを許可します。
## <a name="BKMK_examples"></a>例
定義された監査ポリシーが適用されているすべてのユーザーを一覧表示するには、次のように入力します。
```
auditpol /list /user
```
定義された監査ポリシーと関連付けられている SID を持つすべてのユーザーを一覧表示するには、次のように入力します。
```
auditpol /list /user /v
```
すべてのカテゴリとサブカテゴリ レポート形式で一覧表示、次のように入力します。
```
auditpol /list /subcategory:* /r
```
詳細な追跡および DS アクセスのカテゴリのサブカテゴリの一覧を表示、次のように入力します。
```
auditpol /list /subcategory:"detailed Tracking","DS Access"
```
#### <a name="additional-references"></a>その他の参照
[コマンドライン構文キー](command-line-syntax-key.md)
