---
title: クエリの処理
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 36ce3ffc-0092-4eb1-a374-28e6616ca946
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3248c2b1f476a1a9843f7e930b05a3dca812d694
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442125"
---
# <a name="query-process"></a>クエリの処理

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート デスクトップ セッション ホスト (rd セッション ホスト) サーバーで実行されているプロセスに関する情報が表示されます。
このコマンドを使用するには、特定のユーザーが実行されているプログラムを確認して、ユーザーが特定のプログラムを実行しても。
このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。
> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 新機能については、最新バージョンについてを参照してください。 [Windows Server 2012 でのリモート デスクトップ サービスでどのような s の新しい](https://technet.microsoft.com/library/hh831527)、Windows Server TechNet ライブラリです。
> ## <a name="syntax"></a>構文
> ```
> query process [* | <ProcessID> | <UserName> | <SessionName> | /id:<nn> | <ProgramName>] [/server:<ServerName>]
> ```
> ## <a name="parameters"></a>パラメーター
> 
> |      パラメーター       |                                                                 説明                                                                  |
> |----------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
> |          \*          |                                                    すべてのセッションのプロセスを一覧表示します。                                                     |
> |     <ProcessID>      |                                   クエリを実行するプロセスを識別する数値 ID を指定します。                                   |
> |      <UserName>      |                                       ユーザーの一覧を取得するプロセスの名前を指定します。                                       |
> |    <SessionName>     |                                     一覧を取得するプロセスのセッションの名前を指定します。                                      |
> |       /id:<nn>       |                                      一覧を取得するプロセスのセッションの ID を指定します。                                       |
> |    <ProgramName>     |                     プロセスを照会するプログラムの名前を指定します。 拡張子 .exe が必要です。                     |
> | /server:<ServerName> | Rd セッション ホスト サーバーを一覧表示するプロセスを指定します。 指定しない場合、現在ログオンしているサーバーが使用されます。 |
> |          /?          |                                                     コマンド プロンプトにヘルプを表示します。                                                     |
> 
> ## <a name="remarks"></a>注釈
> - 管理者は、すべてにフル アクセス権を持つ**クエリ プロセス**関数。
> - 指定しない場合、<*UserName*>、<*SessionName*>、 **/id:** <*nn*>、<*ProgramName*>、または **\\** * パラメーター、**クエリ プロセス**現在のユーザーに属しているプロセスのみが表示されます。
> - セッションが指定されている場合にアクティブなセッション、識別する必要があります。
> - **クエリ プロセス**次の情報を返します。
>   -   プロセスを所有するユーザー
>   -   プロセスを所有しているセッション
>   -   セッションの ID
>   -   プロセスの名前
>   -   プロセスの ID
> - ときに**クエリ プロセス**情報、不等号 (>) を返しますが、現在のセッションに属している各プロセスの前に表示されます。
>   ## <a name="BKMK_examples"></a>例
> - すべてのセッションで使用されているプロセスに関する情報を表示するには、次のように入力します。
>   ```
>   query process *
>   ```
> - セッション ID が 2 で使用されているプロセスに関する情報を表示するには、次のように入力します。
>   ```
>   query process /ID:2
>   ```
>   #### <a name="additional-references"></a>その他の参照
>   [コマンドライン構文のポイント](command-line-syntax-key.md)
>   [クエリ](query.md)
>   [Remote Desktop Services&#40;ターミナル サービス&#41;コマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
