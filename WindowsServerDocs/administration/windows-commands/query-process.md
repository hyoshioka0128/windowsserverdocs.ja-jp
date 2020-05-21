---
title: query process
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 36ce3ffc-0092-4eb1-a374-28e6616ca946
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9ac3e5a458d88d945e857cd1922783e5b0ff5cf0
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436287"
---
# <a name="query-process"></a>query process

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモートデスクトップセッションホスト (rd セッションホスト) サーバーで実行されているプロセスに関する情報を表示します。
このコマンドを使用すると、特定のユーザーが実行しているプログラム、および特定のプログラムを実行しているユーザーを調べることができます。

> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527)」を参照してください。
> ## <a name="syntax"></a>構文
> ```
> query process [* | <ProcessID> | <UserName> | <SessionName> | /id:<nn> | <ProgramName>] [/server:<ServerName>]
> ```
> ### <a name="parameters"></a>パラメーター
>
> |      パラメーター       |                                                                 説明                                                                  |
> |----------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
> |          \*          |                                                    すべてのセッションのプロセスを一覧表示します。                                                     |
> |     <ProcessID>      |                                   クエリするプロセスを識別する数値 ID を指定します。                                   |
> |      <UserName>      |                                       プロセスを一覧表示するユーザーの名前を指定します。                                       |
> |    <SessionName>     |                                     プロセスを一覧表示するセッションの名前を指定します。                                      |
> |       /id<nn>       |                                      一覧表示するプロセスを含むセッションの ID を指定します。                                       |
> |    <ProgramName>     |                     クエリするプロセスのプログラムの名前を指定します。 .Exe 拡張子が必要です。                     |
> | /server:<ServerName> | 一覧表示するプロセスを含む rd セッションホストサーバーを指定します。 指定しない場合は、現在ログオンしているサーバーが使用されます。 |
> |          /?          |                                                     コマンド プロンプトにヘルプを表示します。                                                     |
>
>#### <a name="remarks"></a>解説
> - 管理者は、すべての**クエリ処理**機能にフルアクセスできます。
> - <*UserName*>、<の*セッション*名>、 **/id:** < *nn*>、<*ProgramName*>、または * パラメーターを指定しない場合 **\\** 、**クエリプロセス**では、現在のユーザーに属するプロセスのみが表示されます。
> - セッションが指定されている場合は、アクティブなセッションを識別する必要があります。
> - **クエリプロセス**では、次の情報が返されます。
>   -   プロセスを所有しているユーザー
>   -   プロセスを所有するセッション
>   -   セッションの ID
>   -   プロセスの名前
>   -   プロセスの ID
> - **クエリ処理**で情報が返されると、現在のセッションに属する各プロセスの前に、より大きい (>) 記号が表示されます。
>   ## <a name="examples"></a>例
> - すべてのセッションで使用されているプロセスに関する情報を表示するには、次のように入力します。
>   ```
>   query process *
>   ```
> - セッション ID 2 によって使用されているプロセスに関する情報を表示するには、次のように入力します。
>   ```
>   query process /ID:2
>   ```
>   ## <a name="additional-references"></a>その他のリファレンス
>   - [コマンドライン構文のキー](command-line-syntax-key.md) 
>   [クエリ](query.md) 
>   [リモートデスクトップサービス (ターミナルサービス) のコマンドリファレンス](remote-desktop-services-terminal-services-command-reference.md)
