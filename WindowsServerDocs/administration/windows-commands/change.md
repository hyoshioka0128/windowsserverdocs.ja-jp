---
title: change (変更)
description: 変更コマンドの参照記事。ログオン、COM ポートのマッピング、およびインストールモードのリモートデスクトップセッションホストサーバーの設定を変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90012116-0fb3-4f34-a819-cf4d4b4f8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4b1350b39633580dd60bbc0eb07e567029447d5f
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85922451"
---
# <a name="change"></a>change (変更)

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ログオン、COM ポートのマッピング、およびインストールモードのリモートデスクトップセッションホストサーバーの設定を変更します。

> [!NOTE]
> Windows Server 2008 R2 で、「ターミナル サービス」は「リモート デスクトップ サービス」に名前変更されました。 最新バージョンの新機能については、「 [Windows Server でのリモートデスクトップサービスの新](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn283323(v=ws.11))機能」を参照してください。

## <a name="syntax"></a>構文

 ```
 change logon
 change port
 change user
 ```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| [ログオンコマンドの変更](change-logon.md) | リモートデスクトップセッションホストサーバー上のクライアントセッションからのログオンを有効または無効にします。または、現在のログオン状態を表示します。 |
| [ポートの変更コマンド](change-port.md) | 一覧表示したり、MS-DOS アプリケーションと互換性がある COM ポートのマッピングを変更します。 |
| [ユーザーの変更コマンド](change-user.md) | リモートデスクトップセッションホストサーバーのインストールモードを変更します。 |

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [リモート デスクトップ サービス (ターミナル サービス) のコマンド リファレンス](remote-desktop-services-terminal-services-command-reference.md)
