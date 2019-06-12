---
title: クエリ ユーザー
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a670fb78-c055-464a-b61d-3a85632c52c5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c6e0d936e03e14e134c7bfd450a878fda1a796c4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442000"
---
# <a name="query-user"></a>クエリ ユーザー

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート デスクトップ セッション ホスト (rd セッション ホスト) サーバー上のユーザー セッションに関する情報を表示します。
このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。
> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 新機能については、最新バージョンについてを参照してください。 [Windows Server 2012 でのリモート デスクトップ サービスでどのような s の新しい](https://technet.microsoft.com/library/hh831527)、Windows Server TechNet ライブラリです。
> ## <a name="syntax"></a>構文
> ```
> query user [<UserName> | <SessionName> | <SessionID>] [/server:<ServerName>]
> ```
> ## <a name="parameters"></a>パラメーター
> 
> |      パラメーター       |                                                     説明                                                     |
> |----------------------|---------------------------------------------------------------------------------------------------------------------|
> |      <UserName>      |                            クエリを実行するユーザーのログオン名を指定します。                             |
> |    <SessionName>     |                              クエリを実行するセッションの名前を指定します。                              |
> |     <SessionID>      |                               クエリを実行するセッションの ID を指定します。                               |
> | /server:<ServerName> | クエリを実行する rd セッション ホスト サーバーを指定します。 それ以外の場合、現在の rd セッション ホスト サーバーが使用されます。 |
> |          /?          |                                        コマンド プロンプトにヘルプを表示します。                                         |
> 
> ## <a name="remarks"></a>注釈
> - このコマンドを使用すると、特定のユーザーが特定の rd セッション ホスト サーバーにログオンしているかどうかを確認します。 **クエリ ユーザー**次の情報を返します。
>   -   ユーザーの名前
>   -   Rd セッション ホスト サーバー上のセッションの名前
>   -   セッション ID
>   -   (アクティブまたは切断) セッションの状態
>   -   アイドル時間 (セッションで最後にキーストロークやマウスの動きを以降の分単位の数)
>   -   ユーザーがログオンした日付と時刻
> - 使用する**クエリ ユーザー**、フル コントロール権限を持っているまたは特別なアクセス許可の情報をクエリする必要があります。
> - 使用する場合**クエリ ユーザー**を指定せず <*UserName*>、<*SessionName*>、または <*SessionID*>、すべての一覧サーバーにログオンしているユーザーが返されます。 またはも使用できます **クエリ セッション** 、サーバー上のすべてのセッションの一覧を表示します。
> - **クエリ ユーザー** 情報、不等号 (>) を返しますが、現在のセッションの前に表示されます。
> - **/Server** パラメーターは、使用する場合にのみ必要 **クエリ ユーザー** リモート サーバーからです。
>   ## <a name="BKMK_examples"></a>例
> - システムにログオンしているすべてのユーザーに関する情報を表示するには、次のように入力します。
>   ```
>   query user
>   ```
> - サーバー SERver1 上 USER1 のユーザーに関する情報を表示するには、次のように入力します。
>   ```
>   query user USER1 /server:SERver1
>   ```
>   #### <a name="additional-references"></a>その他の参照
>   [コマンドライン構文のポイント](command-line-syntax-key.md)
>   [クエリ](query.md)
>   [Remote Desktop Services&#40;ターミナル サービス&#41;コマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
