---
title: リモート デスクトップ サービス (ターミナル サービス) のコマンド リファレンス
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2f371848-5c48-470c-908c-afbc95d3a805
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b7524973c50b597b8fd8798c5268746dd1d991d7
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441835"
---
# <a name="remote-desktop-services-terminal-services-command-reference"></a>リモート デスクトップ サービス (ターミナル サービス) のコマンド リファレンス

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

リモート デスクトップ サービスのコマンド ライン ツールの一覧を次に示します。
> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 新機能については、最新バージョンについてを参照してください。 [Windows Server 2012 でのリモート デスクトップ サービスでどのような s の新しい](https://technet.microsoft.com/library/hh831527)、Windows Server TechNet ライブラリです。
> 
> |                 コマンド                 |                                                      説明                                                       |
> |-----------------------------------------|------------------------------------------------------------------------------------------------------------------------|
> |           [change](change.md)           | ログオン、COM ポートのマッピング、およびインストール モードのリモート デスクトップ セッション ホスト (rd セッション ホスト) サーバーの設定を変更します。 |
> |     [change logon](change-logon.md)     |    有効または、rd セッション ホスト サーバー上のクライアント セッションからのログオンを無効にします。 または現在のログオン状態を表示します。     |
> |      [change port](change-port.md)      |                   リストまたは MS-DOS アプリケーションと互換性がある COM ポートのマッピングを変更します。                    |
> |      [change user](change-user.md)      |                                rd セッション ホスト サーバーのインストール モードを変更します。                                |
> |         [chglogon](chglogon.md)         |    有効または、rd セッション ホスト サーバー上のクライアント セッションからのログオンを無効にします。 または現在のログオン状態を表示します。     |
> |          [chgport](chgport.md)          |                   リストまたは MS-DOS アプリケーションと互換性がある COM ポートのマッピングを変更します。                    |
> |           [chgusr](chgusr.md)           |                                rd セッション ホスト サーバーのインストール モードを変更します。                                |
> |         [flattemp](flattemp.md)         |                                      有効または、フラットな一時フォルダーを無効にします。                                       |
> |           [logoff](logoff.md)           |          Rd セッション ホスト サーバー上のセッションからユーザーをログオフし、サーバーからセッションを削除します。          |
> |              [msg](msg.md)              |                                Rd セッション ホスト サーバー上のユーザーにメッセージを送信します。                                 |
> |            [mstsc](mstsc.md)            |                       rd セッション ホスト サーバーまたは他のリモート コンピューターへの接続を作成します。                        |
> |          [qappsrv](qappsrv.md)          |                             ネットワーク上のすべての rd セッション ホスト サーバーの一覧を表示します。                             |
> |         [qprocess](qprocess.md)         |                  Rd セッション ホスト サーバーで実行されているプロセスに関する情報が表示されます。                   |
> |            [query](query.md)            |                      プロセス、セッション、および rd セッション ホスト サーバーに関する情報が表示されます。                      |
> |    [query process](query-process.md)    |                  Rd セッション ホスト サーバーで実行されているプロセスに関する情報が表示されます。                   |
> |    [query session](query-session.md)    |                           Rd セッション ホスト サーバー上のセッションに関する情報を表示します。                            |
> | [query termserver](query-termserver.md) |                             ネットワーク上のすべての rd セッション ホスト サーバーの一覧を表示します。                             |
> |       [query user](query-user.md)       |                         Rd セッション ホスト サーバー上のユーザー セッションに関する情報を表示します。                         |
> |            [quser](quser.md)            |                         Rd セッション ホスト サーバー上のユーザー セッションに関する情報を表示します。                         |
> |          [qwinsta](qwinsta.md)          |                           Rd セッション ホスト サーバー上のセッションに関する情報を表示します。                            |
> |          [rdpsign](rdpsign.md)          |                          リモート デスクトップ プロトコル (.rdp) ファイルにデジタル署名することできます。                          |
> |    [reset session](reset-session.md)    |                         Rd セッション ホスト サーバー上のセッションのリセット (削除) できます。                          |
> |          [rwinsta](rwinsta.md)          |                         Rd セッション ホスト サーバー上のセッションのリセット (削除) できます。                          |
> |           [shadow](shadow.md)           |            Rd セッション ホスト サーバー上の別のユーザーのアクティブなセッションをリモートで制御できます。             |
> |            [tscon](tscon.md)            |                               Rd セッション ホスト サーバー上の別のセッションに接続します。                                |
> |         [tsdiscon](tsdiscon.md)         |                                 Rd セッション ホスト サーバーからセッションを切断します。                                  |
> |           [tskill](tskill.md)           |                           Rd セッション ホスト サーバー上のセッションで実行中のプロセスを終了します。                            |
> |           [tsprof](tsprof.md)           |              1 人のユーザーから別のリモート デスクトップ サービス ユーザーの構成情報をコピーします。               |
