---
title: Windows Server 2016 へのリモート デスクトップ セッション ホストのアップグレード
description: この記事では、既存のリモート デスクトップ サービスのデプロイを Windows Server 2016 にアップグレードする方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: spatnaik
ms.date: 08/01/2016
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5c9b98b8-4eca-4a39-b10b-2bac729f7f44
author: spatnaik
manager: scottman
ms.openlocfilehash: 0cf5af29d610ba64d045e10241fd39b01d3f7024
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856063"
---
# <a name="upgrading-your-remote-desktop-session-host-to-windows-server-2016"></a>Windows Server 2016 へのリモート デスクトップ セッション ホストのアップグレード

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

> [!IMPORTANT]
> すべてのアプリケーションをアップグレードする前にアンインストールし、アップグレードのために上昇がアプリの互換性に関する問題を回避するために、アップグレード後に再インストールする必要があります。

## <a name="supported-os-upgrades-with-rds-role-installed"></a>RDS 役割がインストールされた OS のアップグレードをサポート
Windows Server 2016 へのアップグレードは、Windows Server 2012 R2 および Windows Server 2016 TP5 からのみサポートされます。

## <a name="upgrading-a-rds-session-based-collection"></a>RDS セッション ベースのコレクションをアップグレードします。
ダウン時間を最小限に抑えるためには、RDS セッション ベースのコレクションをアップグレードするときに次の手順に従うことをお勧めします。

1. アップグレードするサーバーを識別、半分、サーバーの集合です。
2. 設定してこれらのサーバーへの新しい接続を禁止**新しい接続を許可する**を false にします。
3. これらのサーバー上のすべてのセッションをログオフします。 
4. これらのサーバーをコレクションから削除します。
5. サーバーを Windows Server 2016 にアップグレードします。
6. 設定**新しい接続を許可する**コレクション内の残りのサーバーで"false"にします。
7. アップグレードされたサーバーを対応するコレクションに追加します。
8. コレクションからアップグレードするサーバーの残りのセットを削除します。
9. 設定**新しい接続を許可する**コレクションのアップグレード済みのサーバーには、"true"にします。
10. これで、手順 3 から 9 の上記展開内の残りのサーバーをアップグレードします。

## <a name="upgrading-a-standalone-rd-session-host-server"></a>スタンドアロンの RD セッション ホスト サーバーをアップグレードします。
スタンドアロンの RD セッション ホスト サーバーは、いつでもアップグレードできます。