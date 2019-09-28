---
title: ユーザーのクエリ
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 65bf42281e6e1956331c061167aea23d1cd61a1d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384873"
---
# <a name="query-user"></a>ユーザーのクエリ

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートデスクトップセッションホスト (rd セッションホスト) サーバー上のユーザーセッションに関する情報を表示します。
このコマンドの使用方法の例については、「[例](#BKMK_examples)」を参照してください。
> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの[Windows Server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527) を参照してください。
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
> | /server:<ServerName> | 照会する rd セッションホストサーバーを指定します。 それ以外の場合は、現在の rd セッションホストサーバーが使用されます。 |
> |          /?          |                                        コマンド プロンプトにヘルプを表示します。                                         |
> 
> ## <a name="remarks"></a>コメント
> - このコマンドを使用すると、特定のユーザーが特定の rd セッションホストサーバーにログオンしているかどうかを確認できます。 **query user**は、次の情報を返します。
>   -   ユーザーの名前
>   -   Rd セッションホストサーバー上のセッションの名前
>   -   セッション ID
>   -   (アクティブまたは切断) セッションの状態
>   -   アイドル時間 (セッションで最後にキーストロークやマウスの動きを以降の分単位の数)
>   -   ユーザーがログオンした日付と時刻
> - **クエリユーザー**を使用するには、フルコントロールアクセス許可またはクエリ情報の特別なアクセス許可を持っている必要があります。
> - <*UserName*> *、< の*SessionID >、または <*SessionID*> を指定せずに**クエリユーザー**を使用すると、サーバーにログオンしているすべてのユーザーの一覧が返されます。 またはも使用できます **クエリ セッション** 、サーバー上のすべてのセッションの一覧を表示します。
> - **クエリ ユーザー** 情報、不等号 (>) を返しますが、現在のセッションの前に表示されます。
> - **/Server** パラメーターは、使用する場合にのみ必要 **クエリ ユーザー** リモート サーバーからです。
>   ## <a name="BKMK_examples"></a>例
> - システムにログオンしているすべてのユーザーに関する情報を表示するには、次のように入力します。
>   ```
>   query user
>   ```
> - サーバー SERver1 のユーザー USER1 に関する情報を表示するには、次のように入力します。
>   ```
>   query user USER1 /server:SERver1
>   ```
>   #### <a name="additional-references"></a>その他の参照情報
>   [コマンドライン構文のキー](command-line-syntax-key.md)
>   [クエリ](query.md)
>   [リモートデスクトップサービス&#40;ターミナルサービス&#41;のコマンドリファレンス](remote-desktop-services-terminal-services-command-reference.md)
