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
ms.openlocfilehash: 1dcea0fa4ea91de56e81c51bf9fe87ec7e3a49fa
ms.sourcegitcommit: 4894649cc47dfa535306cc334871f81155198f76
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2020
ms.locfileid: "84254715"
---
# <a name="query"></a>query

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

プロセス、セッション、およびリモートデスクトップセッションホスト (RD セッションホスト) サーバーに関する情報を表示します。

> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Microsoft Docs Windows Server ライブラリの「 [Windows server のリモートデスクトップサービスの新機能](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn283323(v=ws.11))」を参照してください。

## <a name="syntax"></a>構文

```
query process
query session
query termserver
query user
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|-------|--------|
|[query process](query-process.md)|Rd セッションホストサーバーで実行されているプロセスに関する情報を表示します。|
|[query session](query-session.md)|Rd セッションホストサーバー上のセッションに関する情報を表示します。|
|[クエリ termserver](query-termserver.md)|ネットワーク上のすべての rd セッションホストサーバーの一覧を表示します。|
|[ユーザーのクエリ](query-user.md)|Rd セッションホストサーバー上のユーザーセッションに関する情報を表示します。|

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
- [リモート デスクトップ サービス (ターミナル サービス) のコマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
