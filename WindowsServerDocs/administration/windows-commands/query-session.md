---
title: クエリのセッション
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: abc0ace8-0b74-4b6e-a937-a78bb4b61a1f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 25e2457d792b463ca861f0cba29f1c290684e7b0
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442047"
---
# <a name="query-session"></a>クエリのセッション

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート デスクトップ セッション ホスト (rd セッション ホスト) サーバー上のセッションに関する情報を表示します。
一覧には、アクティブなセッションに関するだけでなく、サーバーが実行されているその他のセッションに関する情報が含まれます。
このコマンドを使用する方法の例については、次を参照してください。[例](#BKMK_examples)します。
> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 新機能については、最新バージョンについてを参照してください。 [Windows Server 2012 でのリモート デスクトップ サービスでどのような s の新しい](https://technet.microsoft.com/library/hh831527)、Windows Server TechNet ライブラリです。
> ## <a name="syntax"></a>構文
> ```
> query session [<SessionName> | <UserName> | <SessionID>] [/server:<ServerName>] [/mode] [/flow] [/connect] [/counter]
> ```
> ## <a name="parameters"></a>パラメーター
> 
> |      パラメーター       |                                                      説明                                                      |
> |----------------------|-----------------------------------------------------------------------------------------------------------------------|
> |    <SessionName>     |                               クエリを実行するセッションの名前を指定します。                               |
> |      <UserName>      |                           ユーザー クエリを実行するセッションの名前を指定します。                            |
> |     <SessionID>      |                                クエリを実行するセッションの ID を指定します。                                |
> | /server:<ServerName> |                  クエリに、rd セッション ホスト サーバーを識別します。 既定では、現在のサーバーです。                   |
> |        /mode         |                                            現在の行の設定を表示します。                                            |
> |        /flow         |                                        現在のフロー制御の設定を表示します。                                        |
> |       接続/       |                                          現在の表示では、設定を接続します。                                           |
> |       /counter       | 現在カウンター情報を表示、作成されると、セッションの合計数を含む、切断されているし、再接続します。 |
> |          /?          |                                         コマンド プロンプトにヘルプを表示します。                                          |
> 
> ## <a name="remarks"></a>注釈
> - ユーザーは、ユーザーは、現在ログオンして、セッションを照会して常にします。 他のセッションを照会するには、クエリについては特別なアクセス許可がユーザーに必要です。
> - 使用して、セッションを指定しない場合は、<*SessionName*>、<*UserName*>、または <*SessionID*>、**クエリ セッション**システムのすべてのアクティブなセッションに関する情報を表示します。
> - ときに**クエリ セッション**情報、不等号 (>) を返しますが、現在のセッションの前に表示されます。 次のサンプル出力は、**クエリ セッション**:
>   ```
>   C:\>query session
>    SESSIONNAME    USERNAME       ID STATE  TYPE   DEVICE
>   console        Administrator1  0 active wdcon
>    rdp-tcp#1      User1           1 active wdtshare
>    rdp-tcp                        2 listen wdtshare
>                                   4 idle
>                                   5 idle
>   ```
>   大なり (>) 記号では、現在のセッションを示します。 セッション名には、セッションに割り当てられた名前を指定します。 ユーザー名では、セッションに接続しているユーザーのユーザー名を示します。 状態は、セッションの現在の状態に関する情報を提供します。 型では、セッションの種類を示します。 コンソールまたはネットワーク接続のセッションに存在しない、デバイスは、セッションに割り当てられているデバイスの名前です。 セッション情報を次のコメントは、セッションのプロファイルです。 初期状態が無効になっているとして構成されているすべてのセッションを表示しない、**クエリ セッション**有効にするまで一覧表示します。
>   ## <a name="BKMK_examples"></a>例
> - サーバーは、SERver2 ですべてのアクティブなセッションに関する情報を表示するには、次のように入力します。
>   ```
>   query session /server:SERver2
>   ```
> - アクティブなセッション modeM02 に関する情報を表示するには、次のように入力します。
>   ```
>   query session modeM02
>   ```
>   #### <a name="additional-references"></a>その他の参照
>   [コマンドライン構文のポイント](command-line-syntax-key.md)
>   [クエリ](query.md)
>   [Remote Desktop Services&#40;ターミナル サービス&#41;コマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
