---
title: 手順 1 - WSUS サーバーの役割のインストール
description: -Windows Server Update Service (WSUS) のトピックでは、サーバー マネージャーを使用して、サーバーの役割をインストールする方法を説明します。
ms.prod: windows-server-threshold
ms.reviewer: na
ms.technology: manage-wsus
ms.topic: article
ms.assetid: fabc8619-350e-403b-96f8-116424931300
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4027f7656c17b2ba46fdf44e3af4de42bb056a6f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814003"
---
# <a name="step-1-install-the-wsus-server-role"></a>手順 1:WSUS サーバーの役割をインストールします。

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

WSUS サーバーの展開では、次に、WSUS サーバーの役割をインストールします。 次の手順では、サーバー マネージャーを使用して WSUS サーバーの役割をインストールする方法について説明します。

> [!IMPORTANT]
> このインストール手順では、Windows Internal Database (WID) を使用して WSUS をインストールする方法のみを説明します。 Microsoft SQL Server を使用して WSUS をインストールする方法については、 [こちらの記事](https://social.technet.microsoft.com/wiki/contents/articles/10020.installing-wsus-server-role-on-windows-server-2012-with-microsoft-sql-database.aspx)をご覧ください。

### <a name="to-install-the-wsus-server-role"></a>WSUS サーバーの役割をインストールするには

1.  WSUS サーバーの役割をインストールするサーバーに、ローカルの Administrators グループのメンバーのアカウントを使用してログオンします。

2.  **サーバー マネージャー**、 をクリックして**管理**、 をクリックし、**役割と機能の追加**します。

3.  **[開始する前に]** ページで、 **[次へ]** をクリックします。

4.  **インストールの種類を選択します。** ことを確認します ページで、**役割ベースまたは機能ベースのインストール**オプションが選択されていると、 をクリック**次**。

5.  **対象サーバーの選択** ページで、サーバーがある場所 (サーバー プールまたは仮想ハード_ディスクを使用して) を選択します。 場所を選択したら、WSUS サーバーの役割をインストールするサーバーを選択し、 **[次へ]** をクリックします。

6.  **サーバーの役割の選択**] ページで、[ **Windows Server Update Services**します。  **[Windows Server Update Services に必要な機能の追加]** が表示されます。 **[機能の追加]** をクリックし、 **[次へ]** をクリックします。

7.  **機能の選択**ページ。 クリックして、既定の選択を保持**次**します。

    > [!IMPORTANT]
    > WSUS で必要になるのは、既定の Web サーバーの役割の構成のみです。 WSUS のセットアップ中に追加の Web サーバーの役割の構成を求められた場合は、既定値をそのまま使用しても問題ありません。WSUS のセットアップを続行してください。

8.  **[Windows Server Update Services]** ページで、 **[次へ]** をクリックします。

9. **[役割サービスの選択]** ページで、既定の設定をそのまま使用し、 **[次へ]** をクリックします。

    > [!TIP]
    > 1 つのデータベース種類を選択する必要があります。 データベース オプションがすべてオフになっている (選択されていない) 場合、インストール後のタスクは失敗します。

10. **[コンテンツの場所の選択]** ページで、更新プログラムを保存する有効な場所を入力します。 たとえば、この目的のためだけにドライブ K のルートに WSUS_database という名前のフォルダーを作成し、有効な場所として「 **k:\WSUS_database** 」と入力できます。

11. **[次へ]** をクリックします。 **[Web サーバーの役割 (IIS)]** ページが開きます。 情報を確認して、**[次へ]** をクリックします。 **Web サーバー (IIS) をインストールする役割サービスの選択**、既定値を保持し、クリックして**次**します。

12. **[インストール オプションの確認]** ページで、選択したオプションを確認し、**[インストール]** をクリックします。 WSUS インストール ウィザードが実行します。 この処理は数分かかる場合があります。

13. WSUS のインストールが完了した後、概要ウィンドウの **[インストールの進行状況]** ページで、**[インストール後のタスクを起動する]** をクリックします。 テキスト変更を要求する:**サーバーが構成までお待ちください**します。 タスクが完了したら、テキストに変更します。**構成が正常に完了した**します。 **[閉じる]** をクリックします。

14. **サーバー マネージャー**で、再起動が必要であることを知らせる通知が表示されるかどうかを確認します。 これは、インストールしたサーバーの役割によって異なる場合があります。 再起動が必要な場合は、必ずサーバーを再起動して、インストールを完了します。

> [!IMPORTANT]
> この時点で、インストール プロセスが完了したら、ただしを続行する必要が機能するために WSUS の[手順 2。WSUS 構成](2-configure-wsus.md)します。

