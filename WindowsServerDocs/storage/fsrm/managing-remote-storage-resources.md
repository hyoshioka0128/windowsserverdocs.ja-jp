---
title: リモートの記憶域リソースを管理する
description: この資料では、リモート コンピュータ上の記憶域リソースを管理する方法について説明します。
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 5c6dc9c931e130e36e01655de05fbd209f50f3dc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394075"
---
# <a name="managing-remote-storage-resources"></a>リモートの記憶域リソースを管理する

> 適用対象:Windows Server 2019、Windows Server 2016、Windows Server (半期チャネル)、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2

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

-   [リモート コンピューターに接続する](connect-to-remote-computer.md)
-   [コマンドライン ツール](command-line-tools.md)
