---
title: query
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 675c5128-f3cf-4e8f-8a3f-b29ab2a8b6de
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8d89ae8c7c526bce396b2583abc1728456f7bcc3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836825"
---
# <a name="query"></a>query

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

プロセス、セッション、およびリモートデスクトップセッションホスト (RD セッションホスト) サーバーに関する情報を表示します。

> [!NOTE]
> Windows Server 2008 R2 では、ターミナル サービスはリモート デスクトップ サービスという名前に変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527)」を参照してください。

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
|[クエリプロセス](query-process.md)|Rd セッションホストサーバーで実行されているプロセスに関する情報を表示します。|
|[クエリセッション](query-session.md)|Rd セッションホストサーバー上のセッションに関する情報を表示します。|
|[クエリ termserver](query-termserver.md)|ネットワーク上のすべての rd セッションホストサーバーの一覧を表示します。|
|[ユーザーのクエリ](query-user.md)|Rd セッションホストサーバー上のユーザーセッションに関する情報を表示します。|

## <a name="additional-references"></a>その他の参照情報
- [コマンドライン構文のキー](command-line-syntax-key.md)
[リモートデスクトップサービス (ターミナルサービス) のコマンドリファレンス](remote-desktop-services-terminal-services-command-reference.md)
