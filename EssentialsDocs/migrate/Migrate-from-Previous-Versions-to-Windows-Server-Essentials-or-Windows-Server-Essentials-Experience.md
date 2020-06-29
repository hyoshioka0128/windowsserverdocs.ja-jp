---
title: 以前のバージョンから Windows Server Essentials または Windows Server Essentials エクスペリエンスに移行する
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 2974fb3a-5150-43fd-a73f-3e5074eb5d03
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 559de1602ca2ebf397d47e5418d323fa20c68f5e
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85470287"
---
# <a name="migrate-from-previous-versions-to-windows-server-essentials-or-windows-server-essentials-experience"></a>以前のバージョンから Windows Server Essentials または Windows Server Essentials エクスペリエンスに移行する

>適用対象: Windows Server 2012 R2 Essentials

このガイドで2012は、以前のバージョンの Windows Small Business Server と Windows Server Essentials (Windows Server essentials、Windows Small Business Server 2011 Standard、Windows Small Business Server 2011 Essentials、windows small business Server 2008、および Windows Small business server 2003 を含む) から、windows server essentials エクスペリエンスの役割がインストールされた windows server Essentials に移行する方法について説明します。

 **25 人のユーザーと50デバイスまでの環境**では、このガイドの手順に従って、以前のバージョンの windows SBS から Windows Server Essentials に移行することができます。

 **最大100人のユーザーと200台のデバイスがある環境**では、同じガイダンスに従って windows Server 2012 R2 の Standard edition または Datacenter Edition に Windows Server Essentials Experience 役割がインストールされた状態で移行することができます。

> [!NOTE]
>  移行中に問題が起きないように、Windows Server Essentials 製品開発チームでは、このドキュメントを読んでから移行を開始することを強くお勧めします。

## <a name="terms-and-definitions"></a>用語と定義
 **移行元サーバー** : 設定とデータを移行する元の既存のサーバー。

 **移行先サーバー** : 設定とデータが移行される先の新しいサーバー。

## <a name="migration-process-summary"></a>移行プロセスの概要
 この移行ガイドには次の手順が含まれます。

1. [手順 1: Windows Server Essentials への移行のために移行元サーバーを準備する](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md)  移行元サーバーおよびネットワークが、移行できる状態になっていることを確認する必要があります。 ここでは、移行元サーバーのバックアップ、移行元サーバーのシステム正常性の評価、最新のサービス パックと修正プログラムのインストール、およびネットワーク構成の確認について詳しく説明します。

2. [手順 2: Windows Server Essentials を新しいレプリカドメインコントローラーとしてインストール](Step-2--Install-Windows-Server-Essentials-as-a-new-replica-domain-controller.md)します。 このセクションでは、windows Server Essentials または windows server 2012 R2 Standard (Windows Server Essentials Experience 役割が有効になっている) をドメインコントローラーとしてインストールする方法について説明します。

3. [手順 3: 新しい Windows Server Essentials サーバーにコンピューターを参加](Step-3--Join-computers-to-the-new-Windows-Server-Essentials-server.md)させます。  このセクションでは、Windows Server Essentials を実行している新しいサーバーにクライアントコンピューターを参加させ、グループポリシーの設定を更新する方法について説明します。

4. [手順 4: Windows Server Essentials への移行のために設定とデータを移行先サーバーに移動する](Step-4--Move-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md)  ここでは、移行元サーバーからのデータと設定の移行について説明します。

5. [手順 5: Windows Server Essentials への移行のために移行先サーバーでフォルダーリダイレクトを有効に](Step-5--Enable-folder-redirection-on-the-Destination-Server-for-Windows-Server-Essentials-migration.md)します。  移行元サーバーでフォルダー リダイレクトが有効になっている場合は、移行先サーバーでフォルダー リダイレクトを有効にしてから、以前のフォルダー リダイレクト グループ ポリシー設定を削除できます。

6. [手順 6: 新しい Windows Server Essentials ネットワークから移行元サーバーを降格し、削除](Step-6--Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md)します。  移行元サーバーをネットワークから削除する前に、グループ ポリシーの更新を強制し、移行元サーバーを降格する必要があります。

7. [手順 7: Windows Server Essentials の移行に関する移行後のタスクを実行](Step-7--Perform-post-migration-tasks-for-the-Windows-Server-Essentials-migration.md)します。  すべての設定とデータを Windows Server Essentials に移行したら、許可されたコンピューターをユーザーアカウントにマップすることができます。

8. [手順 8: Windows Server Essentials ベストプラクティスアナライザーを実行](Step-8--Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md)します。  Windows Server Essentials への設定とデータの移行が完了したら、Windows Server Essentials ベストプラクティスアナライザー (BPA) を実行する必要があります。

   いくつかの移行手順では、管理者としてコマンド プロンプト ウィンドウを開く必要があります。 次の手順でこの方法について説明します。

###  <a name="to-open-a-command-prompt-window-on-the-source-server-as-an-administrator"></a><a name="BKMK_OpenACommandPromptAsAdmin"></a>移行元サーバーで管理者としてコマンドプロンプトウィンドウを開くには

1.  **[開始]** をクリックします。

2.  検索ボックスに「**cmd**」と入力します。

3.  結果一覧で **[cmd]** を右クリックし、**[管理者として実行]** をクリックします。

#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>移行先サーバーで管理者としてコマンド プロンプト ウィンドウを開くには

1.  [**スタート**] 画面で、検索ボックスに「**cmd**」と入力します。

2.  結果一覧で **[cmd]** を右クリックし、**[管理者として実行]** をクリックします。

## <a name="additional-references"></a>その他のリファレンス

-   [サーバー データの Windows Server Essentials への移行](Migrate-Server-Data-to-Windows-Server-Essentials.md)

