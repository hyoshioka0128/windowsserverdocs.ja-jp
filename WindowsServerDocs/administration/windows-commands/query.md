---
title: クエリ (query)
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 675c5128-f3cf-4e8f-8a3f-b29ab2a8b6de
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ebe10bb78a6a901871a75e8533b3389c38060666
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863153"
---
# <a name="query"></a>クエリ (query)

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

プロセス、セッション、およびリモート デスクトップ セッション ホスト (RD セッション ホスト) サーバーについての情報を表示します。

> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 新機能については、最新バージョンについてを参照してください。 [Windows Server 2012 でのリモート デスクトップ サービスでどのような s の新しい](https://technet.microsoft.com/library/hh831527)、Windows Server TechNet ライブラリです。

## <a name="syntax"></a>構文
```
query process
query session
query termserver
query user
```

## <a name="parameters"></a>パラメーター
|パラメーター|説明|
|-------|--------|
|[query process](query-process.md)|Rd セッション ホスト サーバーで実行されているプロセスに関する情報が表示されます。|
|[query session](query-session.md)|Rd セッション ホスト サーバー上のセッションに関する情報を表示します。|
|[query termserver](query-termserver.md)|ネットワーク上のすべての rd セッション ホスト サーバーの一覧を表示します。|
|[query user](query-user.md)|Rd セッション ホスト サーバー上のユーザー セッションに関する情報を表示します。|

#### <a name="additional-references"></a>その他の参照
[コマンドライン構文キー](command-line-syntax-key.md)
[リモート デスクトップ サービスと #40 です。ターミナル サービスと #41 です。コマンドのリファレンス](remote-desktop-services-terminal-services-command-reference.md)
