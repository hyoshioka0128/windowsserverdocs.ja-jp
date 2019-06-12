---
title: msg
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9501cf3e-568e-4982-9987-8daecc6c17ff
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 68a393b57a255915b93759b4b26286ce4d838019
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437225"
---
# <a name="msg"></a>msg

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート デスクトップ セッション ホスト (rd セッション ホスト) サーバー上のユーザーにメッセージを送信します。
このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。
> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 新機能については、最新バージョンについてを参照してください。 [Windows Server 2012 でのリモート デスクトップ サービスでどのような s の新しい](https://technet.microsoft.com/library/hh831527)、Windows Server TechNet ライブラリです。

## <a name="syntax"></a>構文
```
msg {<UserName> | <SessionName> | <SessionID>| @<FileName> | *} [/server:<ServerName>] [/time:<Seconds>] [/v] [/w] [<Message>]
```

## <a name="parameters"></a>パラメーター

|      パラメーター       |                                                                                                                               説明                                                                                                                               |
|----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      <UserName>      |                                                                                                  メッセージを受信するユーザーの名前を指定します。                                                                                                   |
|    <SessionName>     |                                                                                                 メッセージを受信するセッションの名前を指定します。                                                                                                 |
|     <SessionID>      |                                                                                            メッセージを受信するユーザーのセッションの数値 ID を指定します。                                                                                            |
|     @<FileName>      |                                                                         ユーザー名、セッション名、およびメッセージを受信するセッション Id の一覧を含むファイルを識別します。                                                                         |
|          \*          |                                                                                                           システム上のすべてのユーザー名をメッセージを送信します。                                                                                                            |
| /server:<ServerName> |                                              セッションまたはメッセージを受信するユーザーは、rd セッション ホスト サーバーを指定します。 指定しない場合、 **/server**を現在ログオンしているサーバーを使用します。                                              |
|   /time:<Seconds>    | 送信したメッセージがユーザーの画面に表示される時間数を指定します。 時間制限に達すると、メッセージは表示されなくなります。 ユーザーがこのメッセージが表示しをクリックするまでに、メッセージがユーザーの画面に残ります時間制限が設定されていない場合**OK**します。 |
|          /v          |                                                                                                         実行する操作についての情報を表示します。                                                                                                         |
|          /w          |         メッセージを受け取ったユーザーからの受信確認を待機します。 このパラメーターを **/時刻:** <*秒*> ユーザーがすぐに応答しない場合は、可能な長時間の遅延を回避するためにします。 このパラメーターを使用して **/v**も便利です。          |
|      <Message>       |                  送信するメッセージのテキストを指定します。 メッセージが指定されていない場合は、メッセージを入力する促されます。 ファイルに含まれるメッセージを送信するには、小なり (<) 記号の後に、ファイル名を入力します。                  |
|          /?          |                                                                                                                  コマンド プロンプトにヘルプを表示します。                                                                                                                   |

## <a name="remarks"></a>注釈
-   ユーザーを指定しない場合、またはセッション、 **msg**エラー メッセージが表示されます。 セッションを指定するときに、作業中の 1 つがあります。
-   メッセージを送信するメッセージの特殊アクセス許可が必要です。

## <a name="BKMK_examples"></a>例
-   メッセージの「会いましょう本日午後 1 時に」すべてのセッションに User1 の対象を送信するには、次のように入力します。
    ```
    msg User1 Let's meet at 1PM today
    ```
-   にセッション modeM02 を、同じメッセージを送信するには、次のように入力します。
    ```
    msg modem02 Let's meet at 1PM today
    ```
-   12 のセッションに、メッセージを送信するには、次のように入力します。
    ```
    msg 12 Let's meet at 1PM today
    ```
-   USERlist ファイルに含まれるすべてのセッションに、メッセージを送信するには、次のように入力します。
    ```
    msg @userlist Let's meet at 1PM today
    ```
-   ログオンしているすべてのユーザーに、メッセージを送信するには、次のように入力します。
    ```
    msg * Let's meet at 1PM today
    ```
-   応答のタイムアウト (たとえば、10 秒) のすべてのユーザーにメッセージを送信するには、次のように入力します。
    ```
    msg * /time:10 Let's meet at 1PM today
    ```

#### <a name="additional-references"></a>その他の参照
-  [コマンド ライン構文の記号](command-line-syntax-key.md)
-  [リモート デスクトップ サービス&#40;ターミナル サービス&#41;コマンドのリファレンス](remote-desktop-services-terminal-services-command-reference.md)
