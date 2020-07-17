---
title: bootcfg debug
description: 指定されたオペレーティングシステムエントリのデバッグ設定を追加または変更する、bootcfg debug コマンドの参照記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 28afa5fb-a236-46e2-b1a4-a3c43a49c437
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: da4179d85d4e84918e75fb4c8490e229230412eb
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85926315"
---
# <a name="bootcfg-debug"></a>bootcfg debug

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

指定したオペレーティングシステムエントリのデバッグ設定を追加または変更します。

>[!NOTE]
> ポート1394をデバッグする場合は、代わりに[bootcfg dbg1394](bootcfg-dbg1394.md)コマンドを使用します。

## <a name="syntax"></a>構文

```
bootcfg /debug {on | off | edit}[/s <computer> [/u <domain>\<user> /p <password>]] [/port {COM1 | COM2 | COM3 | COM4}] [/baud {9600 | 19200 | 38400 | 57600 | 115200}] [/id <osentrylinenum>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `{on | off | edit}` | 次のようなポートデバッグの値を指定します。<ul><li>**代わっ.** 指定されたに/debug オプションを追加することにより、リモートデバッグのサポートを有効にし `<osentrylinenum>` ます。</li><li>**オート.** 指定されたから/debug オプションを削除することにより、リモートデバッグのサポートを無効にし <osentrylinenum> ます。</li><li>**編集.** 指定されたの/debug オプションに関連付けられている値を変更することにより、ポートとボーレートの設定を変更でき <osentrylinenum> ます。</li></ul> |
| `/s <computer>` | リモートコンピューターの名前または IP アドレスを指定します (円記号は使用しないでください)。 既定値はローカル コンピューターです。 |
| `/u <domain>\<user>`  | またはによって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行し `<user>` `<domain>\<user>` ます。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。 |
| `/p <password>` | 指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。 |
| `/port {COM1 | COM2 | COM3 | COM4}` |  デバッグに使用する COM ポートを指定します。 デバッグが無効になっている場合は、このパラメーターを使用しないでください。 |
| `/baud {9600 | 19200 | 38400 | 57600 | 115200}` | デバッグに使用するボーレートを指定します。 デバッグが無効になっている場合は、このパラメーターを使用しないでください。 |
| `/id <osentrylinenum>` | オペレーティングシステムの読み込みオプションが追加される Boot.ini ファイルの [オペレーティングシステム] セクションのオペレーティングシステムエントリの行番号を指定します。 [オペレーティングシステム] セクションヘッダーの後の最初の行は1です。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="examples"></a>例

**Bootcfg/debug**コマンドを使用するには、次のようにします。

```
bootcfg /debug on /port com1 /id 2
bootcfg /debug edit /port com2 /baud 19200 /id 2
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /debug off /id 2
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bootcfg コマンド](bootcfg.md)
