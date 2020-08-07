---
title: bootcfg copy
description: 既存のブートエントリのコピーを作成する、bootcfg copy コマンドの参照記事。コマンドラインオプションを追加できます。
ms.topic: article
ms.assetid: 2a236c2a-8675-444d-b695-9cbc9aff643b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5082f5d7e0cd585039b0ceb198052d528f1170cc
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87880719"
---
# <a name="bootcfg-copy"></a>bootcfg copy

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

既存のブートエントリのコピーを作成します。これには、コマンドラインオプションを追加できます。

## <a name="syntax"></a>構文

```
bootcfg /copy [/s <computer> [/u <domain>\<user> /p <password>]] [/d <description>] [/id <osentrylinenum>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `/s <computer>` | リモートコンピューターの名前または IP アドレスを指定します (円記号は使用しないでください)。 既定値はローカル コンピューターです。 |
| `/u <domain>\<user>`  | またはによって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行し `<user>` `<domain>\<user>` ます。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。 |
| `/p <password>` | 指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。 |
| `/d <description>` | 新しいオペレーティングシステムエントリの説明を指定します。 |
| `/id <osentrylinenum>` | オペレーティングシステムの読み込みオプションが追加される Boot.ini ファイルの [オペレーティングシステム] セクションのオペレーティングシステムエントリの行番号を指定します。 [オペレーティングシステム] セクションヘッダーの後の最初の行は1です。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="examples"></a>例

ブートエントリ1をコピーし、「」と入力します。

```
bootcfg /copy /d \ABC Server\ /id 1
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bootcfg コマンド](bootcfg.md)
