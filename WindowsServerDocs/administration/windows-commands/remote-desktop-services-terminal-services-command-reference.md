---
title: リモート デスクトップ サービス (ターミナル サービス) のコマンド リファレンス
description: 参照記事 * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2f371848-5c48-470c-908c-afbc95d3a805
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: dd054e59c7245eddfb66725bd5d95333f602b2c6
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86956304"
---
# <a name="remote-desktop-services-terminal-services-command-reference"></a>リモート デスクトップ サービス (ターミナル サービス) のコマンド リファレンス

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート デスクトップ サービスのコマンド ライン ツールの一覧を次に示します。
> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](/previous-versions/orphan-topics/ws.11/hh831527(v=ws.11))」を参照してください。
>
> |                 コマンド                 |                                                      説明                                                       |
> |-----------------------------------------|------------------------------------------------------------------------------------------------------------------------|
> |           [change](change.md)           | ログオン、COM ポートのマッピング、およびインストールモードのリモートデスクトップセッションホスト (rd セッションホスト) サーバーの設定を変更します。 |
> |     [change logon](change-logon.md)     |    Rd セッションホストサーバー上のクライアントセッションからのログオンを有効または無効にします。または、現在のログオン状態を表示します。     |
> |      [change port](change-port.md)      |                   MS-DOS アプリケーションと互換性があるように、COM ポートのマッピングを一覧表示または変更します。                    |
> |      [change user](change-user.md)      |                                rd セッションホストサーバーのインストールモードを変更します。                                |
> |         [chglogon](chglogon.md)         |    Rd セッションホストサーバー上のクライアントセッションからのログオンを有効または無効にします。または、現在のログオン状態を表示します。     |
> |          [chgport](chgport.md)          |                   MS-DOS アプリケーションと互換性があるように、COM ポートのマッピングを一覧表示または変更します。                    |
> |           [chgusr](chgusr.md)           |                                rd セッションホストサーバーのインストールモードを変更します。                                |
> |         [flattemp](flattemp.md)         |                                      有効または、フラットな一時フォルダーを無効にします。                                       |
> |           [logoff](logoff.md)           |          Rd セッションホストサーバー上のセッションからユーザーをログオフし、そのセッションをサーバーから削除します。          |
> |              [msg](msg.md)              |                                Rd セッションホストサーバー上のユーザーにメッセージを送信します。                                 |
> |            [mstsc](mstsc.md)            |                       rd セッションホストサーバーまたはその他のリモートコンピューターへの接続を作成します。                        |
> |          [qappsrv](qappsrv.md)          |                             ネットワーク上のすべての rd セッションホストサーバーの一覧を表示します。                             |
> |         [qprocess](qprocess.md)         |                  Rd セッションホストサーバーで実行されているプロセスに関する情報を表示します。                   |
> |            [query](query.md)            |                      プロセス、セッション、および rd セッションホストサーバーに関する情報を表示します。                      |
> |    [query process](query-process.md)    |                  Rd セッションホストサーバーで実行されているプロセスに関する情報を表示します。                   |
> |    [query session](query-session.md)    |                           Rd セッションホストサーバー上のセッションに関する情報を表示します。                            |
> | [query termserver](query-termserver.md) |                             ネットワーク上のすべての rd セッションホストサーバーの一覧を表示します。                             |
> |       [query user](query-user.md)       |                         Rd セッションホストサーバー上のユーザーセッションに関する情報を表示します。                         |
> |            [quser](quser.md)            |                         Rd セッションホストサーバー上のユーザーセッションに関する情報を表示します。                         |
> |          [qwinsta](qwinsta.md)          |                           Rd セッションホストサーバー上のセッションに関する情報を表示します。                            |
> |          [rdpsign](rdpsign.md)          |                          リモート デスクトップ プロトコル (.rdp) ファイルにデジタル署名することできます。                          |
> |    [reset session](reset-session.md)    |                         Rd セッションホストサーバー上のセッションをリセット (削除) できます。                          |
> |          [rwinsta](rwinsta.md)          |                         Rd セッションホストサーバー上のセッションをリセット (削除) できます。                          |
> |           [shadow](shadow.md)           |            Rd セッションホストサーバー上の別のユーザーのアクティブなセッションをリモートで制御できます。             |
> |            [tscon](tscon.md)            |                               Rd セッションホストサーバー上の別のセッションに接続します。                                |
> |         [tsdiscon](tsdiscon.md)         |                                 Rd セッションホストサーバーからセッションを切断します。                                  |
> |           [tskill](tskill.md)           |                           Rd セッションホストサーバー上のセッションで実行されているプロセスを終了します。                            |
> |           [tsprof](tsprof.md)           |              1 人のユーザーから別のリモート デスクトップ サービス ユーザーの構成情報をコピーします。               |
