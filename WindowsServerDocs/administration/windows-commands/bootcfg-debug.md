---
title: bootcfg debug
description: 指定されたオペレーティングシステムエントリのデバッグ設定を追加または変更する、bootcfg debug コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 28afa5fb-a236-46e2-b1a4-a3c43a49c437
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c8059aaefd1b23b3e74f4c27ba96e322c44b5cb6
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82709717"
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

| パラメーター | [説明] |
| --------- | ----------- |
| `{on | off | edit}` | 次のようなポートデバッグの値を指定します。<ul><li>**代わっ.** 指定さ`<osentrylinenum>`れたに/debug オプションを追加することにより、リモートデバッグのサポートを有効にします。</li><li>**オート.** 指定さ<osentrylinenum>れたから/debug オプションを削除することにより、リモートデバッグのサポートを無効にします。</li><li>**編集.** 指定さ<osentrylinenum>れたの/debug オプションに関連付けられている値を変更することにより、ポートとボーレートの設定を変更できます。</li></ul> |
| `/s <computer>` | リモートコンピューターの名前または IP アドレスを指定します (円記号は使用しないでください)。 既定はローカル コンピュータです。 |
| `/u <domain>\<user>`  | または`<user>` `<domain>\<user>`によって指定されたユーザーのアカウントアクセス許可を使用してコマンドを実行します。 既定値は、コマンドを実行しているコンピューターの現在のログオンユーザーのアクセス許可です。 |
| `/p <password>` | 指定されているユーザー アカウントのパスワードを指定します、 **/u** パラメーター。 |
| `/port {COM1 | COM2 | COM3 | COM4}` |  デバッグに使用する COM ポートを指定します。 デバッグが無効になっている場合は、このパラメーターを使用しないでください。 |
| `/baud {9600 | 19200 | 38400 | 57600 | 115200}` | デバッグに使用するボーレートを指定します。 デバッグが無効になっている場合は、このパラメーターを使用しないでください。 |
| `/id <osentrylinenum>` | オペレーティングシステムの読み込みオプションを追加する Boot.ini ファイルの [オペレーティングシステム] セクションのオペレーティングシステムエントリの行番号を指定します。 [オペレーティングシステム] セクションヘッダーの後の最初の行は1です。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="examples"></a>例

**Bootcfg/debug**コマンドを使用するには、次のようにします。

```
bootcfg /debug on /port com1 /id 2
bootcfg /debug edit /port com2 /baud 19200 /id 2
bootcfg /s srvmain /u maindom\hiropln /p p@ssW23 /debug off /id 2
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [bootcfg コマンド](bootcfg.md)
