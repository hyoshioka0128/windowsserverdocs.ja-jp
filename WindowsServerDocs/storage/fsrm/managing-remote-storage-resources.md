---
title: リモートの記憶域リソースを管理する
description: この資料では、リモート コンピュータ上の記憶域リソースを管理する方法について説明します。
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 583c36f399848cf67c6f3a850e62015b224768d9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836633"
---
# <a name="managing-remote-storage-resources"></a>リモートの記憶域リソースを管理する

> 適用対象:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

リモート コンピューターの記憶域リソースを管理するには、2 とおりの方法があります。

-   ファイル サーバー リソース マネージャー Microsoft<sup>®</sup> 管理コンソール (MMC) スナップインからリモート コンピューターに接続します (接続後はこのスナップインを使用してリモート リソースを管理できます)。
-   ファイル サーバー リソース マネージャーと共にインストールされるコマンド ライン ツールを使用します。

どちらの方法でも、クォータの管理、ファイルのスクリーン処理、分類の管理、ファイル管理タスクのスケジューリング、およびこれらのリモート リソースについてのレポートを生成できます。

> [!Note]
> ファイル サーバー リソース マネージャーでは、ローカル コンピューターまたはリモート コンピューター上のリソースを管理できますが、両方を同時に管理することはできません。

たとえば、次のようなことができます。

-   ファイル サーバー リソース マネージャー MMC スナップインを使用して、ドメイン内の別のコンピューターに接続し、このリモート コンピューター上のボリュームやファイルの記憶域使用率を確認する。
-   ローカル サーバー上にクォータおよびファイル スクリーン テンプレートを作成し、コマンド ライン ツールを使用してこれらのテンプレートをブランチ オフィスのファイル サーバーにインポートする。

ここでは、次のトピックについて説明します。

-   [リモート コンピューターへの接続します。](connect-to-remote-computer.md)
-   [コマンドライン ツール](command-line-tools.md)
