---
title: bootcfg dbg1394
description: 指定されたオペレーティングシステムエントリに対して1394ポートのデバッグを構成する、bootcfg dbg1394 コマンドのリファレンストピック
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 35724697-90dd-4dbe-85b0-337fbd369dcc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 16230c52657fd5c9c14972726ed2465401995223
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82709705"
---
# <a name="bootcfg-dbg1394"></a>bootcfg dbg1394

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定されたオペレーティングシステムエントリに対して1394ポートデバッグを構成します。

## <a name="syntax"></a>構文

```
bootcfg /dbg1394 {on | off}[/s <computer> [/u <domain>\<user> /p <password>]] [/ch <channel>] /id <osentrylinenum>
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| `{on | off}` | 次のような1394ポートデバッグの値を指定します。<ul><li>**代わっ.** 指定さ`<osentrylinenum>`れたに/dbg1394 オプションを追加することにより、リモートデバッグのサポートを有効にします。</li><li>**オート.** 指定さ<osentrylinenum>れたから/dbg1394 オプションを削除することで、リモートデバッグのサポートを無効にします。</li></ul> |
| `/s <computer>` | リモートコンピューターの名前または IP アドレスを指定します (円記号は使用しないでください)。 既定はローカル コンピュータです。 |
| `/u <domain>\<user>`  | または`<user>` `<domain>\<user>`によって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行します。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。 |
| `/p <password>` | 指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。 |
| `/ch <channel>` | デバッグに使用するチャネルを指定します。 有効な値は、1 ~ 64 の整数です。 1394ポートデバッグが無効になっている場合は、このパラメーターを使用しないでください。 |
| `/id <osentrylinenum>` | オペレーティングシステムの読み込みオプションを追加する Boot.ini ファイルの [オペレーティングシステム] セクションのオペレーティングシステムエントリの行番号を指定します。 [オペレーティングシステム] セクションヘッダーの後の最初の行は1です。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="examples"></a>例

**Bootcfg/dbg1394**コマンドを使用するには、次のようにします。

```
bootcfg /dbg1394 /id 2
bootcfg /dbg1394 on /ch 1 /id 3
bootcfg /dbg1394 edit /ch 8 /id 2
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /dbg1394 off /id 2
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bootcfg コマンド](bootcfg.md)
