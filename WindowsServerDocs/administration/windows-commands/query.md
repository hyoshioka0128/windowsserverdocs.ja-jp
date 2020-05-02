---
title: query
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 675c5128-f3cf-4e8f-8a3f-b29ab2a8b6de
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 90ef2cc14ef0131978956de8df029eaf04baabd3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722684"
---
# <a name="query"></a>query

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

プロセス、セッション、およびリモートデスクトップセッションホスト (RD セッションホスト) サーバーに関する情報を表示します。

> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527)」を参照してください。

## <a name="syntax"></a>構文
```
query process
query session
query termserver
query user
```

### <a name="parameters"></a>パラメーター
|パラメーター|[説明]|
|-------|--------|
|[query process](query-process.md)|Rd セッションホストサーバーで実行されているプロセスに関する情報を表示します。|
|[query session](query-session.md)|Rd セッションホストサーバー上のセッションに関する情報を表示します。|
|[クエリ termserver](query-termserver.md)|ネットワーク上のすべての rd セッションホストサーバーの一覧を表示します。|
|[ユーザーのクエリ](query-user.md)|Rd セッションホストサーバー上のユーザーセッションに関する情報を表示します。|

## <a name="additional-references"></a>その他のリファレンス
- [コマンドライン構文のキー](command-line-syntax-key.md)
[リモートデスクトップサービス (ターミナルサービス) のコマンドリファレンス](remote-desktop-services-terminal-services-command-reference.md)
