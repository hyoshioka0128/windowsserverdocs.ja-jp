---
title: クエリ (query)
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: d0aee400a3fae38cce73a34b55aa92f266082b19
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371839"
---
# <a name="query"></a>クエリ (query)

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

プロセス、セッション、およびリモートデスクトップセッションホスト (RD セッションホスト) サーバーに関する情報を表示します。

> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの[Windows Server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527) を参照してください。

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
|[query process](query-process.md)|Rd セッションホストサーバーで実行されているプロセスに関する情報を表示します。|
|[query session](query-session.md)|Rd セッションホストサーバー上のセッションに関する情報を表示します。|
|[query termserver](query-termserver.md)|ネットワーク上のすべての rd セッションホストサーバーの一覧を表示します。|
|[query user](query-user.md)|Rd セッションホストサーバー上のユーザーセッションに関する情報を表示します。|

#### <a name="additional-references"></a>その他の参照情報
[コマンドライン構文キー](command-line-syntax-key.md)
[リモート デスクトップ サービス(ターミナル サービス) のコマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
