---
title: "以前のバージョンから Windows Server Essentials または Windows Server Essentials エクスペリエンスに移行します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/20116
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2974fb3a-5150-43fd-a73f-3e5074eb5d03
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 213ee4304d9d4ebdb7580f7f78fdaca78aa454c9
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="migrate-from-previous-versions-to-windows-server-essentials-or-windows-server-essentials-experience"></a>以前のバージョンから Windows Server Essentials または Windows Server Essentials エクスペリエンスに移行します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

このガイドでは、インストールされている Windows Server Essentials エクスペリエンスの役割を持つ Windows Server Essentials または Windows Server 2012 R2 を以前のバージョンの Windows Small Business Server と Windows Server Essentials が (Windows Server Essentials、Windows Small Business Server 2011 Standard、Windows Small Business Server 2011 Essentials、Windows Small Business Server 2008、および Windows Small Business Server 2003 を含む) から移行する方法について説明します。  
  
 **環境で最大 25 ユーザーおよび 50 デバイス**、以前のバージョンの Windows SBS から Windows Server Essentials に移行するには、このガイドの手順に従うことができます。  
  
 **最大 100 人のユーザーと 200 台のデバイス環境で**、Windows Server Essentials エクスペリエンス役割がインストールされた Windows Server 2012 R2 Standard または Datacenter エディションに移行する同じガイダンスに従うことができます。  
  
> [!NOTE]
>  移行中に問題が起きないように、移行を開始する前に、このドキュメントを読むことを Windows Server Essentials 製品開発チームは強く推奨します。  
  
## <a name="terms-and-definitions"></a>用語と定義  
 **ソース サーバー**設定とデータを移行する既存のサーバー。  
  
 **移行先サーバー**設定とデータを移行する新しいサーバー。  
  
## <a name="migration-process-summary"></a>移行プロセスの概要  
 この移行ガイドには、次の手順が含まれています。  
  
1.  [手順 1: Windows Server Essentials で移行元サーバーの移行の準備](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md)します。  移行元サーバーとネットワーク移行の準備ができていることを確認する必要があります。 このセクションでは、を介して移行元サーバーのバックアップ、移行元サーバーのシステム正常性を評価する、最新の service pack と修正プログラム、インストール、およびネットワーク構成を検証する手順について説明します。  
  
2.  [手順 2: インストールの Windows Server Essentials を新しいレプリカ ドメイン コントローラーとして](Step-2--Install-Windows-Server-Essentials-as-a-new-replica-domain-controller.md)します。 このセクションでは、ドメイン コントローラーとして (Windows Server Essentials エクスペリエンス役割を有効になっている) と Windows Server Essentials、または Windows Server 2012 R2 Standard をインストールする方法について説明します。  
  
3.  [手順 3: 新しい Windows Server Essentials サーバーにコンピューターを参加させる](Step-3--Join-computers-to-the-new-Windows-Server-Essentials-server.md)します。  このセクションでは、Windows Server Essentials を実行しているグループ ポリシー設定を更新、新しいサーバーにクライアント コンピューターを参加させる方法について説明します。  
  
4.  [手順 4: Destination Server for Windows Server Essentials 移行の設定とデータの移動](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)します。  このセクションでは、移行元サーバーから移行するデータと設定に関する情報を提供します。  
  
5.  [手順 5: Windows Server Essentials の移行先サーバーの移行でフォルダー リダイレクトを有効にする](Step-5--Enable-folder-redirection-on-the-Destination-Server-for-Windows-Server-Essentials-migration.md)します。  移行元サーバーでフォルダー リダイレクトが有効である場合、移行先サーバーでフォルダー リダイレクトを有効にし、古いフォルダー リダイレクト グループ ポリシー設定を削除できます。  
  
6.  [手順 6: を降格して新しい Windows Server Essentials ネットワークから移行元サーバーを削除する](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md)します。  ネットワークから移行元サーバーを削除する前に、グループ ポリシーの更新を強制し、移行元サーバーを降格する必要があります。  
  
7.  [手順 7: Windows Server Essentials 移行の移行後のタスクを実行する](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md)します。  Windows Server Essentials へのすべての設定とデータの移行が完了したら、許可されているコンピューターをユーザー アカウントにマップする可能性があります。  
  
8.  [手順 8: Windows Server Essentials ベスト プラクティス アナライザーを実行する](Step-8--Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)します。  設定の移行と Windows Server Essentials へのデータを完了したら、Windows Server Essentials ベスト プラクティス アナライザー (BPA) を実行する必要があります。  
  
 いくつかの移行の手順は、管理者としてコマンド プロンプト ウィンドウを開くことが必要です。 次の手順では、これを行う方法を説明します。  
  
###  <a name="BKMK_OpenACommandPromptAsAdmin"></a>移行元サーバーでコマンド プロンプト ウィンドウを管理者として開くには  
  
1.  をクリックして**開始**します。  
  
2.  検索ボックスに次のように入力します。**cmd**します。  
  
3.  右クリックし、結果の一覧で**cmd**、] をクリックし、**管理者として実行**します。  
  
#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>管理者として移行先サーバーでコマンド プロンプト ウィンドウを開くには  
  
1.  **開始**] 画面で検索ボックスに、種類、**cmd**します。  
  
2.  右クリックし、結果の一覧で**cmd**、] をクリックし、**管理者として実行**します。  
  
## <a name="see-also"></a>参照してください。  
  
-   [Windows Server Essentials へのサーバー データを移行します。](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [Windows Server Essentials へのサーバー データを移行します。](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

