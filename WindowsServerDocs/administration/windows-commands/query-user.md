---
title: query user
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: a670fb78-c055-464a-b61d-3a85632c52c5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e8c095226a5445e976e47e461044ec002dc007fe
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722691"
---
# <a name="query-user"></a>query user

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートデスクトップセッションホスト (rd セッションホスト) サーバー上のユーザーセッションに関する情報を表示します。

> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527)」を参照してください。
> ## <a name="syntax"></a>構文
> ```
> query user [<UserName> | <SessionName> | <SessionID>] [/server:<ServerName>]
> ```
> ### <a name="parameters"></a>パラメーター
> 
> |      パラメーター       |                                                     [説明]                                                     |
> |----------------------|---------------------------------------------------------------------------------------------------------------------|
> |      <UserName>      |                            クエリを実行するユーザーのログオン名を指定します。                             |
> |    <SessionName>     |                              クエリを実行するセッションの名前を指定します。                              |
> |     <SessionID>      |                               クエリを実行するセッションの ID を指定します。                               |
> | /server:<ServerName> | 照会する rd セッションホストサーバーを指定します。 それ以外の場合は、現在の rd セッションホストサーバーが使用されます。 |
> |          /?          |                                        コマンド プロンプトにヘルプを表示します。                                         |
> 
> ## <a name="remarks"></a>Remarks
> - このコマンドを使用すると、特定のユーザーが特定の rd セッションホストサーバーにログオンしているかどうかを確認できます。 **query user**は、次の情報を返します。
>   -   ユーザーの名前
>   -   Rd セッションホストサーバー上のセッションの名前
>   -   セッション ID
>   -   (アクティブまたは切断) セッションの状態
>   -   アイドル時間 (セッションで最後にキーストロークやマウスの動きを以降の分単位の数)
>   -   ユーザーがログオンした日付と時刻
> - **クエリユーザー**を使用するには、フルコントロールアクセス許可またはクエリ情報の特別なアクセス許可を持っている必要があります。
> - <*UserName*> *、<の*SessionID>、または <*SessionID*> を指定せずに**クエリユーザー**を使用すると、サーバーにログオンしているすべてのユーザーの一覧が返されます。 またはも使用できます **クエリ セッション** 、サーバー上のすべてのセッションの一覧を表示します。
> - **クエリ ユーザー** 情報、不等号 (>) を返しますが、現在のセッションの前に表示されます。
> - **/Server** パラメーターは、使用する場合にのみ必要 **クエリ ユーザー** リモート サーバーからです。
>   ## <a name="examples"></a>例
> - システムにログオンしているすべてのユーザーに関する情報を表示するには、次のように入力します。
>   ```
>   query user
>   ```
> - サーバー SERver1 のユーザー USER1 に関する情報を表示するには、次のように入力します。
>   ```
>   query user USER1 /server:SERver1
>   ```
>   ## <a name="additional-references"></a>その他のリファレンス
>   - [コマンドライン構文キー](command-line-syntax-key.md)
>   [クエリ](query.md)
>   [リモートデスクトップサービス (ターミナルサービス) コマンドリファレンス](remote-desktop-services-terminal-services-command-reference.md)
