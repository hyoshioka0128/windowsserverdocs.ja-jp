---
title: msg
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 9501cf3e-568e-4982-9987-8daecc6c17ff
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91a85cd5d043b6c613f88e199670f55f6e0e72a7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839145"
---
# <a name="msg"></a>msg

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートデスクトップセッションホスト (rd セッションホスト) サーバー上のユーザーにメッセージを送信します。
このコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。
> [!NOTE]
> Windows Server 2008 R2 では、ターミナル サービスはリモート デスクトップ サービスという名前に変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527)」を参照してください。

## <a name="syntax"></a>構文
```
msg {<UserName> | <SessionName> | <SessionID>| @<FileName> | *} [/server:<ServerName>] [/time:<Seconds>] [/v] [/w] [<Message>]
```

### <a name="parameters"></a>パラメーター

|      パラメーター       |                                                                                                                               説明                                                                                                                               |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      <UserName>      |                                                                                                  メッセージを受信するユーザーの名前を指定します。                                                                                                   |
|    <SessionName>     |                                                                                                 メッセージを受信するセッションの名前を指定します。                                                                                                 |
|     <SessionID>      |                                                                                            メッセージを受信するユーザーのセッションの数値 ID を指定します。                                                                                            |
|     @<FileName>      |                                                                         メッセージを受信するユーザー名、セッション名、セッション Id の一覧を含むファイルを識別します。                                                                         |
|          \*          |                                                                                                           システム上のすべてのユーザー名にメッセージを送信します。                                                                                                            |
| /server:<ServerName> |                                              メッセージを受信するセッションまたはユーザーを含む rd セッションホストサーバーを指定します。 指定されていない場合、 **/server**は、現在ログオンしているサーバーを使用します。                                              |
|   /時刻:<Seconds>    | 送信したメッセージがユーザーの画面に表示される時間を指定します。 制限時間に達すると、メッセージは表示されなくなります。 時間制限が設定されていない場合は、ユーザーがメッセージを確認して **[OK]** をクリックするまで、メッセージはユーザーの画面に残ります。 |
|          /v          |                                                                                                         実行されているアクションに関する情報を表示します。                                                                                                         |
|          /w          |         メッセージが受信されたことを示す受信確認を待機します。 このパラメーターを **/時刻:** <*Seconds*> と共に使用すると、ユーザーがすぐに応答しない場合に長い遅延が発生しないようにすることができます。 このパラメーターを **/v**と共に使用することも役立ちます。          |
|      <Message>       |                  送信するメッセージのテキストを指定します。 メッセージが指定されていない場合は、メッセージを入力するように求められます。 ファイルに含まれているメッセージを送信するには、不等号 (<) 記号を入力し、その後にファイル名を入力します。                  |
|          /?          |                                                                                                                  コマンド プロンプトでヘルプを表示します。                                                                                                                   |

## <a name="remarks"></a>コメント
-   ユーザーまたはセッションを指定しない場合、 **msg**によってエラーメッセージが表示されます。 セッションを指定する場合は、アクティブなセッションである必要があります。
-   メッセージを送信するには、メッセージに特殊なアクセス許可が必要です。

## <a name="examples"></a><a name=BKMK_examples></a>例
-   1PM で、現在は User1 のすべてのセッションについて、次のようなメッセージを送信するには、次のように入力します。
    ```
    msg User1 Let's meet at 1PM today
    ```
-   セッション modeM02 に同じメッセージを送信するには、次のように入力します。
    ```
    msg modem02 Let's meet at 1PM today
    ```
-   セッション12にメッセージを送信するには、次のように入力します。
    ```
    msg 12 Let's meet at 1PM today
    ```
-   USERlist ファイルに含まれるすべてのセッションにメッセージを送信するには、次のように入力します。
    ```
    msg @userlist Let's meet at 1PM today
    ```
-   ログオンしているすべてのユーザーにメッセージを送信するには、次のように入力します。
    ```
    msg * Let's meet at 1PM today
    ```
-   受信確認のタイムアウト (10 秒など) を使用して、すべてのユーザーにメッセージを送信するには、次のように入力します。
    ```
    msg * /time:10 Let's meet at 1PM today
    ```

## <a name="additional-references"></a>その他の参照情報
-  - [コマンド ライン構文の記号](command-line-syntax-key.md)
-  [リモート デスクトップ サービス (ターミナル サービス) のコマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
