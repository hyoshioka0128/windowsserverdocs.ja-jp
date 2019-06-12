---
title: Windows Server Essentials の新しいハードウェアへの移行
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f695ae90-3160-407b-bebf-9e460f22c86d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f59e84877606f65d3f8eb6fd9dc39fe701af8a5a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432931"
---
# <a name="migrate-windows-server-essentials-to-new-hardware"></a>Windows Server Essentials の新しいハードウェアへの移行

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

このガイドで新しいハードウェアは、既存の Windows Server® 2012 Essentials ドメインを Windows Server Essentials に移行する方法を説明し、設定とデータを移行します。 このガイドでは、移行が完了したら、Windows Server Essentials ネットワークから既存のサーバーを削除する方法も説明します。  
  
> [!NOTE]
>  移行中に問題を回避するために、移行を開始する前に、このドキュメントを読むことを Windows Server Essentials 製品開発チームは強く推奨します。  
> 
> [!NOTE]
> 
>  サーバー データを Windows Server Essentials の最新バージョンに移行する、次を参照してください。 [Windows Server Essentials への移行](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)します。  

  
## <a name="additional-resources"></a>その他の資料  
 追加情報、ツール、および移行プロセスを支援するコミュニティ リソースへのリンクを参照してください、 [Windows Small Business Server の移行](https://go.microsoft.com/fwlink/?LinkId=217520)web サイト。  
  
## <a name="terms-and-definitions"></a>用語と定義  
 **ソース サーバー:** 設定とデータを移行する元の既存のサーバー。  
  
 **移行先サーバー:** 設定とデータが移行される先の新しいサーバー。  
  
## <a name="migration-process-summary"></a>移行プロセスの概要  
 この移行ガイドには次の手順が含まれます。  
  

1. [Windows Server Essentials でソース サーバーの移行に向けて準備](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md)します。  移行元サーバーおよびネットワークが、移行できる状態になっていることを確認する必要があります。 ここでは、移行元サーバーのバックアップ、移行元サーバーのシステム正常性の評価、最新のサービス パックと修正プログラムのインストール、およびネットワーク構成の確認について詳しく説明します。  
  
2. [Windows Server Essentials を移行モードでインストール](Install-Windows-Server-Essentials-in-migration-mode.md)します。  このセクションでは、移行モードでの移行先サーバーで Windows Server Essentials をインストールする必要があります手順について説明します。  
  
3. [新しい Windows Server Essentials サーバーにコンピューターを参加させる](Join-computers-to-the-new-Windows-Server-Essentials-server.md)します。  このセクションでは、新しい Windows Server Essentials サーバーとグループ ポリシー設定を更新するクライアント コンピューターの参加について説明します。  
  
4. [Windows Server Essentials の移行先サーバーへの移行の設定とデータの移動](Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)します。  ここでは、移行元サーバーからのデータと設定の移行について説明します。  
  
5. [Windows Server Essentials の移行先サーバーでフォルダー リダイレクトを構成](Configure-folder-redirection-on-the-Windows-Server-Essentials-Destination-Server.md)します。  移行元サーバーでフォルダー リダイレクトが有効になっている場合は、移行先サーバーでフォルダー リダイレクトを有効にしてから、以前のフォルダー リダイレクト グループ ポリシー設定を削除できます。  
  
6. [降格して新しい Windows Server Essentials ネットワークから移行元サーバーを削除](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md)します。  移行元サーバーをネットワークから削除する前に、グループ ポリシーの更新を強制し、移行元サーバーを降格する必要があります。  
  
7. [Windows Server Essentials への移行の移行後のタスクを実行](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md)します。  Windows Server Essentials へのすべての設定とデータの移行が完了したら、ユーザー アカウントに許可されているコンピューターにマップしたい場合があります。  
  
8. [Windows Server Essentials ベスト プラクティス アナライザー実行](Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)します。  設定の移行と Windows Server Essentials へのデータを完了したら、ダウンロードして、Windows Server Essentials BPA を実行する必要があります。  
  
   いくつかの移行手順では、管理者としてコマンド プロンプト ウィンドウを開く必要があります。  
  
#### <a name="to-open-a-command-prompt-window-as-an-administrator"></a>[コマンド プロンプト] ウィンドウを管理者として開くには  
  
1.  **[スタート]** 画面で、検索ボックスに「**cmd**」と入力します。  
  
2.  結果一覧で **[cmd]** を右クリックし、 **[管理者として実行]** をクリックします。
