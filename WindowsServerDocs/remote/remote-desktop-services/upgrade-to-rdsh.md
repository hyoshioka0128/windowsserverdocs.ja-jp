---
title: リモート デスクトップ セッション ホストの Windows Server 2016 へのアップグレード
description: この記事では、既存のリモート デスクトップ サービスの展開を Windows Server 2016 にアップグレードする方法について説明します。
ms.prod: windows-server
ms.technology: remote-desktop-services
ms.author: spatnaik
ms.date: 08/01/2016
ms.topic: article
ms.assetid: 5c9b98b8-4eca-4a39-b10b-2bac729f7f44
author: spatnaik
manager: scottman
ms.openlocfilehash: e685c51a003a7121dab19c74d82796311ef0889a
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80857125"
---
# <a name="upgrading-your-remote-desktop-session-host-to-windows-server-2016"></a>リモート デスクトップ セッション ホストの Windows Server 2016 へのアップグレード

>適用先:Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016

> [!IMPORTANT]
> アップグレードのために発生する可能性のあるアプリの互換性の問題を回避するため、すべてのアプリケーションをアップグレード前にアンインストールし、アップグレード後に再インストールする必要があります。

## <a name="supported-os-upgrades-with-rds-role-installed"></a>RDS のロールがインストールされたサポート対象の OS のアップグレード
Windows Server 2016 へのアップグレードがサポートされるのは、Windows Server 2012 R2 および Windows Server 2016 TP5 からのみです。

## <a name="upgrading-a-rds-session-based-collection"></a>RDS セッション ベースのコレクションのアップグレード
ダウンタイムを最小限に抑えるために、RDS セッション ベース コレクションをアップグレードするときに次の手順に従うことをお勧めします。

1. アップグレードするサーバー、つまりコレクション内の半分のサーバーを識別します。
2. **[新しい接続の許可]** を false に設定して、これらのサーバーへの新しい接続を防止します。
3. これらのサーバー上のすべてのセッションをログオフします。 
4. これらのサーバーをコレクションから削除します。
5. サーバーを Windows Server 2016 にアップグレードします。
6. コレクション内の残りのサーバーで **[新しい接続の許可]** を "false" に設定します。
7. アップグレードしたサーバーを対応するコレクションに追加します。
8. アップグレードするサーバーの残りのセットをコレクションから削除します。
9. コレクション内のアップグレードしたサーバーで **[新しい接続の許可]** を "true" に設定します。
10. 次に上記の手順 3 から 9 に従って、展開内の残りのサーバーをアップグレードします。

## <a name="upgrading-a-standalone-rd-session-host-server"></a>スタンドアロンの RD セッション ホスト サーバーのアップグレード
スタンドアロンの RD セッション ホスト サーバーはいつでもアップグレードできます。