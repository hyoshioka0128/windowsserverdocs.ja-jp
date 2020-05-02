---
title: query session
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: abc0ace8-0b74-4b6e-a937-a78bb4b61a1f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a7a119cda5fad594638211bfcdbdc269fff13d20
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722724"
---
# <a name="query-session"></a>query session

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートデスクトップセッションホスト (rd セッションホスト) サーバー上のセッションに関する情報を表示します。
一覧には、アクティブなセッションだけでなく、サーバーが実行している他のセッションに関する情報も含まれています。

> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527)」を参照してください。
> ## <a name="syntax"></a>構文
> ```
> query session [<SessionName> | <UserName> | <SessionID>] [/server:<ServerName>] [/mode] [/flow] [/connect] [/counter]
> ```
> ### <a name="parameters"></a>パラメーター
> 
> |      パラメーター       |                                                      [説明]                                                      |
> |----------------------|-----------------------------------------------------------------------------------------------------------------------|
> |    <SessionName>     |                               クエリを実行するセッションの名前を指定します。                               |
> |      <UserName>      |                           クエリを実行するセッションを持つユーザーの名前を指定します。                            |
> |     <SessionID>      |                                クエリを実行するセッションの ID を指定します。                                |
> | /server:<ServerName> |                  照会する rd セッションホストサーバーを識別します。 既定値は現在のサーバーです。                   |
> |        /mode         |                                            現在の行の設定を表示します。                                            |
> |        フロー (& a)         |                                        現在のフロー制御の設定を表示します。                                        |
> |       /connect       |                                          現在の接続設定を表示します。                                           |
> |       /counter       | 作成、切断、再接続されたセッションの合計数など、現在のカウンター情報が表示されます。 |
> |          /?          |                                         コマンド プロンプトにヘルプを表示します。                                          |
> 
> ## <a name="remarks"></a>Remarks
> - ユーザーは、ユーザーが現在ログオンしているセッションに対していつでもクエリを実行できます。 他のセッションに対してクエリを実行するには、ユーザーがクエリ情報に特別なアクセス許可を持っている必要があります。
> - *<のセッション名>* 、<*ユーザー名*>、または <*SessionID*> を使用してセッションを指定しなかった場合、**クエリセッション**には、システム内のすべてのアクティブなセッションに関する情報が表示されます。
> - **クエリセッション**で情報が返されると、現在のセッションの前に、より大きい (>) 記号が表示されます。 **クエリセッション**のサンプル出力を次に示します。
>   ```
>   C:\>query session
>    SESSIONNAME    USERNAME       ID STATE  TYPE   DEVICE
>   console        Administrator1  0 active wdcon
>    rdp-tcp#1      User1           1 active wdtshare
>    rdp-tcp                        2 listen wdtshare
>                                   4 idle
>                                   5 idle
>   ```
>   不等号 (>) 記号は、現在のセッションを示します。 [セッション名は、セッションに割り当てられた名前を指定します。 USERNAME は、セッションに接続されているユーザーのユーザー名を示します。 STATE は、セッションの現在の状態に関する情報を提供します。 種類は、セッションの種類を示します。 コンソールまたはネットワークに接続されたセッションには存在しないデバイスは、セッションに割り当てられているデバイス名です。 セッション情報の後のコメントは、セッションプロファイルからのものです。 初期状態が無効として構成されているセッションは、有効になるまで、**クエリセッション**の一覧に表示されません。
>   ## <a name="examples"></a>例
> - サーバー SERver2 のすべてのアクティブなセッションに関する情報を表示するには、次のように入力します。
>   ```
>   query session /server:SERver2
>   ```
> - アクティブなセッションの modeM02 に関する情報を表示するには、次のように入力します。
>   ```
>   query session modeM02
>   ```
>   ## <a name="additional-references"></a>その他のリファレンス
>   - [コマンドライン構文キー](command-line-syntax-key.md)
>   [クエリ](query.md)
>   [リモートデスクトップサービス (ターミナルサービス) コマンドリファレンス](remote-desktop-services-terminal-services-command-reference.md)
