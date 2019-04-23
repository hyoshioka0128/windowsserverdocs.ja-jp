---
title: logoff
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 939f09cc-de8c-436c-a05d-aca5f2a06371
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 75dd5fa5860101f80179d9c602b1d919e7caacbc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831523"
---
# <a name="logoff"></a>logoff

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート デスクトップ セッション ホスト (rd セッション ホスト) サーバー上のセッションからユーザーをログオフし、サーバーからセッションを削除します。
このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。

> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 新機能については、最新バージョンについてを参照してください。 [Windows Server 2012 でのリモート デスクトップ サービスでどのような s の新しい](https://technet.microsoft.com/library/hh831527)、Windows Server TechNet ライブラリです。

## <a name="syntax"></a>構文
```
logoff [<SessionName> | <SessionID>] [/server:<ServerName>] [/v]
```
## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|<SessionName>|セッションの名前を指定します。|
|<SessionID>|サーバーにセッションを識別する数値 ID を指定します。|
|/server:<ServerName>|ログオフするユーザーのセッションを含む、rd セッション ホスト サーバーを指定します。 指定しない場合は、現在アクティブになっているサーバーが使用されます。|
|/v|実行する操作についての情報を表示します。|
|/?|コマンド プロンプトにヘルプを表示します。|
## <a name="remarks"></a>注釈
-   現在ログオンするセッションからログオフすることが常にします。 ただし、他のセッションからユーザーをログオフするフル コントロール アクセス許可がある必要があります。
-   警告なしのセッションからユーザーをログオフすると、ユーザーのセッションでのデータが失われる可能性です。 使用して、ユーザーにメッセージを送信する必要があります、 **msg**コマンドをこの操作を実行する前にユーザーに警告します。
-   場合 <*SessionID*> または <*SessionName*> が指定されていない**ログオフ**現在のセッションからユーザーをログオフします。 指定した場合 <*SessionName*>、アクティブな必要があります。
-   ユーザーをログオフするときは、すべてのプロセスが終了し、セッションがサーバーから削除されます。
-   コンソール セッションからユーザーをログオフすることはできません。
## <a name="BKMK_examples"></a>例
-   現在のセッションからユーザーをログオフするには、次のように入力します。
    ```
    logoff
    ```
-   たとえばセッション 12 のセッションの ID を使用してセッションからユーザーをログオフするには、次のように入力します。
    ```
    logoff 12
    ```
-   セッションを使用して、セッションとサーバーの名前など TERM04 Server1 上のセッションからユーザーをログオフするには、次のように入力します。
    ```
    logoff TERM04 /server:Server1
    ```
    
#### <a name="additional-references"></a>その他の参照
-   [コマンドライン構文キー](command-line-syntax-key.md)
-   [リモート デスクトップ サービス&#40;ターミナル サービス&#41;コマンドのリファレンス](remote-desktop-services-terminal-services-command-reference.md)
