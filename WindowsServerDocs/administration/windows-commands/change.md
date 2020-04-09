---
title: 変更
description: Windows コマンドの変更に関するトピック。ログオン、COM ポートのマッピング、およびインストールモードのリモートデスクトップセッションホストサーバーの設定を変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 90012116-0fb3-4f34-a819-cf4d4b4f8981
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d5d91f8d0941fc96e776c761b9c7037e58588df8
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847955"
---
# <a name="change"></a>変更

> 適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ログオン、COM ポートのマッピング、およびインストールモードのリモートデスクトップセッションホストサーバーの設定を変更します。

> [!NOTE]
> Windows Server 2008 R2 では、ターミナル サービスはリモート デスクトップ サービスという名前に変更されました。 最新バージョンの新機能については、Windows Server TechNet ライブラリの「 [Windows server 2012 のリモートデスクトップサービスの新機能](https://technet.microsoft.com/library/hh831527)」を参照してください。

## <a name="syntax"></a>構文

 ```
 change logon
 change port
 change user
 ```
 
 ### <a name="parameters"></a>パラメーター
 
 |            パラメーター            |                                                   説明                                                   |
 |---------------------------------|-----------------------------------------------------------------------------------------------------------------|
 | [change logon](change-logon.md) | Rd セッションホストサーバー上のクライアントセッションからのログオンを有効または無効にします。または、現在のログオン状態を表示します。 |
 |  [change port](change-port.md)  |                MS-DOS アプリケーションと互換性があるように、COM ポートのマッピングを一覧表示または変更します。                |
 |  [change user](change-user.md)  |                            rd セッションホストサーバーのインストールモードを変更します。                             |
 
 ## <a name="additional-references"></a>その他の参照情報
 - [コマンドライン構文のキー](command-line-syntax-key.md)
 [リモートデスクトップサービス (ターミナルサービス) のコマンドリファレンス](remote-desktop-services-terminal-services-command-reference.md)
