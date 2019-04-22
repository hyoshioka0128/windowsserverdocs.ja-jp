---
title: Windows Server 2008 Foundation から Windows Server Essentials への移行
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f22fc0a4-cb82-4e60-afe6-2d03145745e7
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 22721833d3ba97c7860c949764d565415bbc7cab
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813763"
---
# <a name="migrate-windows-server-2008-foundation-to-windows-server-essentials"></a>Windows Server 2008 Foundation から Windows Server Essentials への移行

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

既存の Windows Server 2008 Foundation ドメインを新しいハードウェアで Windows Server® 2012 Essentials に移行する方法を説明し、設定とデータを移行します。 このガイドでは、移行が完了したら、Windows Server Essentials ネットワークから既存のサーバーを削除する方法も説明します。  
  
> [!NOTE]
>  移行中に問題を回避するために、移行を開始する前に、このドキュメントを読むことを Windows Server Essentials 製品開発チームは強く推奨します。  
  
## <a name="additional-resources"></a>その他の資料  
 追加情報、ツール、および移行プロセスを支援するコミュニティ リソースへのリンクを参照してください。 [Windows Small Business Server の移行](https://go.microsoft.com/fwlink/?LinkId=217520)します。  
  
## <a name="terms-and-definitions"></a>用語と定義  
 **ソース サーバー:** 設定とデータを移行する元の既存のサーバー。  
  
 **移行先サーバー:** 設定とデータが移行される先の新しいサーバー。  
  
## <a name="migration-process-summary"></a>移行プロセスの概要  
 この移行ガイドには次の手順が含まれます。  
  

1.  [Windows Server Essentials でソース サーバーの移行に向けて準備](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md)します。  移行元サーバーおよびネットワークが、移行できる状態になっていることを確認する必要があります。 ここでは、移行元サーバーのバックアップ、移行元サーバーのシステム正常性の評価、最新のサービス パックと修正プログラムのインストール、およびネットワーク構成の確認について詳しく説明します。  
  
2.  [Windows Server Essentials を移行モードでインストール](Install-Windows-Server-Essentials-in-migration-mode.md)します。  このセクションでは、移行モードでの移行先サーバーで Windows Server Essentials をインストールする必要があります手順について説明します。  
  
3.  [新しい Windows Server Essentials ネットワークにコンピューターを参加させる](Join-computers-to-the-new-Windows-Server-Essentials-network.md)します。  このセクションでは、新しい Windows Server Essentials ネットワークとグループ ポリシー設定を更新するクライアント コンピューターの参加について説明します。  
  
4.  [移行先サーバーに Windows Server 2008 Foundation の設定とデータを移動する](Move-Windows-Server-2008-Foundation-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)します。  ここでは、移行元サーバーからのデータと設定の移行について説明します。  
  
5.  [降格して新しい Windows Server Essentials ネットワークから移行元サーバーを削除](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md)します。  移行元サーバーをネットワークから削除する前に、グループ ポリシーの更新を強制し、移行元サーバーを降格する必要があります。  
  
6.  [Windows Server Essentials への移行の移行後のタスクを実行](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md)します。  Windows Server Essentials へのすべての設定とデータの移行が完了したら、ユーザー アカウントに許可されているコンピューターにマップしたい場合があります。  
  
7.  [Windows Server Essentials ベスト プラクティス アナライザー実行](Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)します。  設定の移行と Windows Server Essentials へのデータを完了したら、Windows Server Essentials BPA を実行する必要があります。  

1.  [Windows Server Essentials でソース サーバーの移行に向けて準備](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md)します。  移行元サーバーおよびネットワークが、移行できる状態になっていることを確認する必要があります。 ここでは、移行元サーバーのバックアップ、移行元サーバーのシステム正常性の評価、最新のサービス パックと修正プログラムのインストール、およびネットワーク構成の確認について詳しく説明します。  
  
2.  [Windows Server Essentials を移行モードでインストール](../migrate/Install-Windows-Server-Essentials-in-migration-mode.md)します。  このセクションでは、移行モードでの移行先サーバーで Windows Server Essentials をインストールする必要があります手順について説明します。  
  
3.  [新しい Windows Server Essentials ネットワークにコンピューターを参加させる](../migrate/Join-computers-to-the-new-Windows-Server-Essentials-network.md)します。  このセクションでは、新しい Windows Server Essentials ネットワークとグループ ポリシー設定を更新するクライアント コンピューターの参加について説明します。  
  
4.  [移行先サーバーに Windows Server 2008 Foundation の設定とデータを移動する](../migrate/Move-Windows-Server-2008-Foundation-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)します。  ここでは、移行元サーバーからのデータと設定の移行について説明します。  
  
5.  [降格して新しい Windows Server Essentials ネットワークから移行元サーバーを削除](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md)します。  移行元サーバーをネットワークから削除する前に、グループ ポリシーの更新を強制し、移行元サーバーを降格する必要があります。  
  
6.  [Windows Server Essentials への移行の移行後のタスクを実行](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md)します。  Windows Server Essentials へのすべての設定とデータの移行が完了したら、ユーザー アカウントに許可されているコンピューターにマップしたい場合があります。  
  
7.  [Windows Server Essentials ベスト プラクティス アナライザー実行](../migrate/Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)します。  設定の移行と Windows Server Essentials へのデータを完了したら、Windows Server Essentials BPA を実行する必要があります。  

  
 いくつかの移行手順では、管理者としてコマンド プロンプト ウィンドウを開く必要があります。  
  
###  <a name="BKMK_OpenACommandPromptAsAdmin"></a> 移行元サーバーでコマンド プロンプト ウィンドウを管理者として開くには  
  
1.  **[開始]** をクリックします。  
  
2.  検索ボックスに「 **cmd**」と入力します。  
  
3.  結果一覧で **[cmd]** を右クリックし、 **[管理者として実行]** をクリックします。  
  
#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>移行先サーバーで管理者としてコマンド プロンプト ウィンドウを開くには  
  
1.  **[スタート]** 画面で、検索ボックスに「**cmd**」と入力します。  
  
2.  結果一覧で **[cmd]** を右クリックし、 **[管理者として実行]** をクリックします。
