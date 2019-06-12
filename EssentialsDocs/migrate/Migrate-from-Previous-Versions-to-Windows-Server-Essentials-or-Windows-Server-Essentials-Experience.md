---
title: 以前のバージョンから Windows Server Essentials または Windows Server Essentials エクスペリエンスに移行する
description: Windows Server Essentials を使用する方法について説明します
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
ms.openlocfilehash: 107a20cae83072ee0066ba0a335eb5078341e59b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432849"
---
# <a name="migrate-from-previous-versions-to-windows-server-essentials-or-windows-server-essentials-experience"></a>以前のバージョンから Windows Server Essentials または Windows Server Essentials エクスペリエンスに移行する

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

このガイドは、以前のバージョンの Windows Small Business Server と (Windows Server Essentials、Windows Small Business Server 2011 Standard、Windows Small Business Server 2011 Essentials、Windows を含む Windows Server Essentials から移行する方法を説明します。Small Business Server 2008、および Windows Small Business Server 2003) Windows Server Essentials または Windows Server 2012 R2、Windows Server Essentials エクスペリエンス役割をインストールします。  
  
 **最大 25 ユーザーおよび 50 台のデバイスを使用した環境**、以前のバージョンの Windows SBS から Windows Server Essentials に移行するには、このガイドの手順を行うことができます。  
  
 **最大 100 人のユーザーと 200 台のデバイス環境で**、Windows Server Essentials エクスペリエンス役割がインストールされた Windows Server 2012 R2 の Standard または Datacenter エディションに移行するのと同じガイダンスに従うことができます。  
  
> [!NOTE]
>  移行中に問題が起きないように、Windows Server Essentials 製品開発チームでは、このドキュメントを読んでから移行を開始することを強くお勧めします。  
  
## <a name="terms-and-definitions"></a>用語と定義  
 **移行元サーバー** : 設定とデータを移行する元の既存のサーバー。  
  
 **移行先サーバー** : 設定とデータが移行される先の新しいサーバー。  
  
## <a name="migration-process-summary"></a>移行プロセスの概要  
 この移行ガイドには次の手順が含まれます。  
  
1. [ステップ 1: Windows Server Essentials でソース サーバーの移行に向けて準備](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md)します。  移行元サーバーおよびネットワークが、移行できる状態になっていることを確認する必要があります。 ここでは、移行元サーバーのバックアップ、移行元サーバーのシステム正常性の評価、最新のサービス パックと修正プログラムのインストール、およびネットワーク構成の確認について詳しく説明します。  
  
2. [手順 2:Windows Server Essentials を新しいレプリカ ドメイン コント ローラーとしてインストール](Step-2--Install-Windows-Server-Essentials-as-a-new-replica-domain-controller.md)します。 このセクションでは、ドメイン コント ローラーとして (Windows Server Essentials エクスペリエンス役割を有効になっている) で Windows Server Essentials、または Windows Server 2012 R2 Standard をインストールする方法について説明します。  
  
3. [手順 3:新しい Windows Server Essentials サーバーにコンピューターを参加させる](Step-3--Join-computers-to-the-new-Windows-Server-Essentials-server.md)します。  このセクションでは、Windows Server Essentials を実行していると、グループ ポリシー設定を更新して、新しいサーバーにクライアント コンピューターを参加させる方法について説明します。  
  
4. [手順 4:Windows Server Essentials の移行先サーバーへの移行の設定とデータの移動](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)します。  ここでは、移行元サーバーからのデータと設定の移行について説明します。  
  
5. [手順 5:Windows Server Essentials の移行先サーバーの移行でフォルダー リダイレクトを有効にする](Step-5--Enable-folder-redirection-on-the-Destination-Server-for-Windows-Server-Essentials-migration.md)します。  移行元サーバーでフォルダー リダイレクトが有効になっている場合は、移行先サーバーでフォルダー リダイレクトを有効にしてから、以前のフォルダー リダイレクト グループ ポリシー設定を削除できます。  
  
6. [手順 6:降格して新しい Windows Server Essentials ネットワークから移行元サーバーを削除](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md)します。  移行元サーバーをネットワークから削除する前に、グループ ポリシーの更新を強制し、移行元サーバーを降格する必要があります。  
  
7. [手順 7:Windows Server Essentials の移行の移行後のタスクを実行](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md)します。  Windows Server Essentials へのすべての設定とデータの移行が完了したら、ユーザー アカウントに許可されているコンピューターにマップしたい場合があります。  
  
8. [手順 8:Windows Server Essentials ベスト プラクティス アナライザー実行](Step-8--Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)します。  設定の移行と Windows Server Essentials へのデータを完了したら、Windows Server Essentials ベスト プラクティス アナライザー (BPA) を実行する必要があります。  
  
   いくつかの移行手順では、管理者としてコマンド プロンプト ウィンドウを開く必要があります。 次の手順でこの方法について説明します。  
  
###  <a name="BKMK_OpenACommandPromptAsAdmin"></a> 移行元サーバーでコマンド プロンプト ウィンドウを管理者として開くには  
  
1.  **[開始]** をクリックします。  
  
2.  検索ボックスに「 **cmd**」と入力します。  
  
3.  結果一覧で **[cmd]** を右クリックし、 **[管理者として実行]** をクリックします。  
  
#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>移行先サーバーで管理者としてコマンド プロンプト ウィンドウを開くには  
  
1.  **[スタート]** 画面で、検索ボックスに「**cmd**」と入力します。  
  
2.  結果一覧で **[cmd]** を右クリックし、 **[管理者として実行]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
  
-   [サーバー データの Windows Server Essentials への移行](Migrate-Server-Data-to-Windows-Server-Essentials.md)

-   [サーバー データの Windows Server Essentials への移行](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)

