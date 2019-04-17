---
title: "Windows Server Essentials を新しいハードウェアに移行します。"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.openlocfilehash: 61106439a63a75143a9cca0989c70370adfedd38
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="migrate-windows-server-essentials-to-new-hardware"></a>Windows Server Essentials を新しいハードウェアに移行します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

このガイドでは、新しいハードウェア上の Windows Server Essentials を既存の Windows Server® 2012 Essentials ドメインを移行する方法について説明し、設定とデータを移行します。 このガイドでは、移行が完了したら、Windows Server Essentials ネットワークから既存のサーバーを削除する方法についても説明します。  
  
> [!NOTE]
>  移行中に問題が起きないように、移行を開始する前に、このドキュメントを読むことを Windows Server Essentials 製品開発チームは強く推奨します。  
  
> [!NOTE]

>  Windows Server Essentials の最新バージョンに、サーバー データを移行するを参照してください。[Windows Server Essentials への移行](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)します。  

  
## <a name="additional-resources"></a>その他のリソース  
 追加情報、ツール、および移行プロセスの実行を支援するコミュニティ リソースへのリンクを参照してください、[Windows Small Business Server の移行](https://go.microsoft.com/fwlink/?LinkId=217520)Web サイト。  
  
## <a name="terms-and-definitions"></a>用語と定義  
 **移行元サーバー:**設定とデータを移行する既存のサーバー。  
  
 **移行先サーバー:**設定とデータを移行する新しいサーバー。  
  
## <a name="migration-process-summary"></a>移行プロセスの概要  
 この移行ガイドには、次の手順が含まれています。  
  

1.  [Windows Server Essentials で移行元サーバーの移行準備](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md)します。  移行元サーバーとネットワーク移行の準備ができていることを確認する必要があります。 このセクションでは、を介して移行元サーバーのバックアップ、移行元サーバーのシステム正常性を評価する、最新の service pack と修正プログラム、インストール、およびネットワーク構成を検証する手順について説明します。  
  
2.  [Windows Server Essentials を移行モードでインストール](Install-Windows-Server-Essentials-in-migration-mode.md)します。  このセクションでは、Windows Server Essentials を移行モードで、移行先サーバーにインストールするために必要、手順について説明します。  
  
3.  [新しい Windows Server Essentials サーバーにコンピューターを参加させる](Join-computers-to-the-new-Windows-Server-Essentials-server.md)します。  このセクションでは、新しい Windows Server Essentials サーバー グループ ポリシー設定を更新するクライアント コンピューターを参加させについて説明します。  
  
4.  [Windows Server Essentials の移行先サーバーの移行に設定とデータを移動](Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)します。  このセクションでは、移行元サーバーから移行するデータと設定に関する情報を提供します。  
  
5.  [Windows Server Essentials の移行先サーバーでフォルダー リダイレクトを構成する](Configure-folder-redirection-on-the-Windows-Server-Essentials-Destination-Server.md)します。  移行元サーバーでフォルダー リダイレクトが有効である場合、移行先サーバーでフォルダー リダイレクトを有効にし、古いフォルダー リダイレクト グループ ポリシー設定を削除できます。  
  
6.  [降格して新しい Windows Server Essentials ネットワークから移行元サーバーを削除する](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md)します。  ネットワークから移行元サーバーを削除する前に、グループ ポリシーの更新を強制し、移行元サーバーを降格する必要があります。  
  
7.  [Windows Server Essentials 移行の移行後のタスクを実行](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md)します。  Windows Server Essentials へのすべての設定とデータの移行が完了したら、許可されているコンピューターをユーザー アカウントにマップする可能性があります。  
  
8.  [Windows Server Essentials ベスト プラクティス アナライザーを実行](Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)します。  設定の移行と Windows Server Essentials へのデータを完了したら、ダウンロードして、Windows Server Essentials BPA を実行する必要があります。  
  
 いくつかの移行の手順は、管理者としてコマンド プロンプト ウィンドウを開くことが必要です。  
  
#### <a name="to-open-a-command-prompt-window-as-an-administrator"></a>管理者としてコマンド プロンプト ウィンドウを開くには  
  
1.  **開始**] 画面で検索ボックスに、種類、**cmd**します。  
  
2.  右クリックし、結果の一覧で**cmd**、] をクリックし、**管理者として実行**します。
