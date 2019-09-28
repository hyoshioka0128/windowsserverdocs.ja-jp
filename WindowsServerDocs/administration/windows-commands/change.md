---
title: change
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 90012116-0fb3-4f34-a819-cf4d4b4f8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eee52bbb24824ea01f9c55a4bfe6e3e60ad2ab58
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379547"
---
# <a name="change"></a>change

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ログオン、COM ポートのマッピング、およびインストールモードのリモートデスクトップセッションホスト (rd セッションホスト) サーバーの設定を変更します。
> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの[Windows Server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527) を参照してください。
> ## <a name="syntax"></a>構文
> ```
> change logon
> change port
> change user
> ```
> ## <a name="parameters"></a>パラメーター
> 
> |            パラメーター            |                                                   説明                                                   |
> |---------------------------------|-----------------------------------------------------------------------------------------------------------------|
> | [change logon](change-logon.md) | Rd セッションホストサーバー上のクライアントセッションからのログオンを有効または無効にします。または、現在のログオン状態を表示します。 |
> |  [change port](change-port.md)  |                MS-DOS アプリケーションと互換性があるように、COM ポートのマッピングを一覧表示または変更します。                |
> |  [change user](change-user.md)  |                            rd セッションホストサーバーのインストールモードを変更します。                             |
> 
> #### <a name="additional-references"></a>その他の参照情報
> [コマンドライン構文キー](command-line-syntax-key.md)
> [リモート デスクトップ サービス(ターミナル サービス) のコマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
