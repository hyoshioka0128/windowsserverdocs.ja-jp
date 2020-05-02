---
title: bootcfg raw
description: Bootcfg raw コマンドのリファレンストピック。文字列として指定されたオペレーティングシステムの読み込みオプションを、Boot.ini ファイルのオペレーティングシステムセクションのオペレーティングシステムエントリに追加します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e3458749-b0a0-460f-a022-3ff199a71f27
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b9127b278a41bb8f1f36f7b45c544bf09f5c4ff7
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82708952"
---
# <a name="bootcfg-raw"></a>bootcfg raw

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Boot.ini ファイルの [オペレーティングシステム] セクションのオペレーティングシステムエントリに、文字列として指定されたオペレーティングシステムの読み込みオプションを追加します。 このコマンドは、既存のオペレーティングシステムのエントリオプションを上書きします。

## <a name="syntax"></a>構文

```
bootcfg /raw [/s <computer> [/u <domain>\<user> /p <password>]] <osloadoptionsstring> [/id <osentrylinenum>] [/a]
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| `/s <computer>` | リモートコンピューターの名前または IP アドレスを指定します (円記号は使用しないでください)。 既定はローカル コンピュータです。 |
| `/u <domain>\<user>`  | または`<user>` `<domain>\<user>`によって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行します。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。 |
| `/p <password>` | 指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。 |
| `<osloadoptionsstring>` | オペレーティングシステムエントリに追加するオペレーティングシステムの読み込みオプションを指定します。 これらの読み込みオプションは、オペレーティングシステムエントリに関連付けられている既存の読み込みオプションを置き換えます。 `<osloadoptions>`パラメーターに対する検証は行われません。
| `/id <osentrylinenum>` | オペレーティングシステムの読み込みオプションを追加する Boot.ini ファイルの [オペレーティングシステム] セクションのオペレーティングシステムエントリの行番号を指定します。 [オペレーティングシステム] セクションヘッダーの後の最初の行は1です。 |
| /a | 既存のオペレーティングシステムオプションに追加するオペレーティングシステムオプションを指定します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="examples"></a>例

このテキストに**は、有効**な OS 読み込みオプション ( **/debug**、 **/fastdetect**、 **/nodebug**、 **/crashdebug**、 **/sos**など) が含まれている必要があります。

最初のオペレーティングシステムエントリの末尾に **/debug/fastdetect**を追加するには、以前のオペレーティングシステムエントリのオプションを置き換えます。

```
bootcfg /raw /debug /fastdetect /id 1
```

**Bootcfg/raw**コマンドを使用するには、次のようにします。

```
bootcfg /raw /debug /sos /id 2
bootcfg /raw /s srvmain /u maindom\hiropln /p p@ssW23 /crashdebug  /id 2
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bootcfg コマンド](bootcfg.md)
