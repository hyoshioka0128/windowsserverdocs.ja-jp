---
title: msg
description: リモートデスクトップセッションホストサーバー上のユーザーにメッセージを送信する msg コマンドのリファレンス記事
ms.topic: article
ms.assetid: 9501cf3e-568e-4982-9987-8daecc6c17ff
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 044d6c7e6dbf7c92cb0c947fcb60eb79ab1db05b
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87886195"
---
# <a name="msg"></a>msg

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートデスクトップセッションホストサーバー上のユーザーにメッセージを送信します。

> [!NOTE]
> メッセージを送信するには、メッセージに特殊なアクセス許可が必要です。

## <a name="syntax"></a>構文

```
msg {<username> | <sessionname> | <sessionID>| @<filename> | *} [/server:<servername>] [/time:<seconds>] [/v] [/w] [<message>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<username>` | メッセージを受信するユーザーの名前を指定します。 ユーザーまたはセッションを指定しない場合は、このコマンドによってエラーメッセージが表示されます。 セッションを指定する場合は、アクティブなセッションである必要があります。 |
| `<sessionname>` | メッセージを受信するセッションの名前を指定します。 ユーザーまたはセッションを指定しない場合は、このコマンドによってエラーメッセージが表示されます。 セッションを指定する場合は、アクティブなセッションである必要があります。 |
| `<sessionID>` | メッセージを受信するユーザーのセッションの数値 ID を指定します。 |
| `@<filename>` | メッセージを受信するユーザー名、セッション名、セッション Id の一覧を含むファイルを識別します。 |
| * | システム上のすべてのユーザー名にメッセージを送信します。 |
| /server:`<servername>` | メッセージを受信するセッションまたはユーザーを含むリモートデスクトップセッションホストサーバーを指定します。 指定されていない場合、 **/server**は、現在ログオンしているサーバーを使用します。 |
| /時刻`<seconds>` | 送信したメッセージがユーザーの画面に表示される時間を指定します。 制限時間に達すると、メッセージは表示されなくなります。 時間制限が設定されていない場合は、ユーザーがメッセージを確認して **[OK]** をクリックするまで、メッセージはユーザーの画面に残ります。 |
| /v | 実行されているアクションに関する情報を表示します。 |
| /w | メッセージが受信されたことを示す受信確認を待機します。 ユーザーがすぐに応答しない場合は、を使用して、 `/time:<*seconds*>` 長い遅延が発生しないようにします。 このパラメーターを **/v**と共に使用することも役立ちます。 |
| `<message>` | 送信するメッセージのテキストを指定します。 メッセージが指定されていない場合は、メッセージを入力するように求められます。 ファイルに含まれているメッセージを送信するには、不等号 (<) 記号を入力し、その後にファイル名を入力します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

### <a name="examples"></a>例

次のようなメッセージを送信するには、 *1PM で* *User1*のすべてのセッションについて、次のように入力します。

```
msg User1 Let's meet at 1PM today
```

セッション*modeM02*に同じメッセージを送信するには、次のように入力します。

```
msg modem02 Let's meet at 1PM today
```

*Userlist*ファイルに含まれるすべてのセッションにメッセージを送信するには、次のように入力します。

```
msg @userlist Let's meet at 1PM today
```

ログオンしているすべてのユーザーにメッセージを送信するには、次のように入力します。

```
msg * Let's meet at 1PM today
```

受信確認のタイムアウト (10 秒など) を使用して、すべてのユーザーにメッセージを送信するには、次のように入力します。

```
msg * /time:10 Let's meet at 1PM today
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
