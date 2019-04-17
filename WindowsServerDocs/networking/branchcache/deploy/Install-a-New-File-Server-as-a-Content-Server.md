---
title: 新しいファイル サーバーをコンテンツ サーバーとしてインストールします。
description: このトピックの「BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法示しますの一部である
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 1f49fc3c-28a6-4d3d-b787-1be9e61e792f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 53937cfc139efc6df5facfa872e63609229a548c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="install-a-new-file-server-as-a-content-server"></a>新しいファイル サーバーをコンテンツ サーバーとしてインストールします。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

この手順を使用するには、ファイル サービス サーバーの役割をインストールして、**ネットワーク ファイル用 BranchCache** Windows Server 2016 を実行しているコンピューター上の役割サービスです。  
  
メンバーシップ**管理者**、またはそれと同等がこの手順を実行するために必要な最小値。  
  
> [!NOTE]  
> 管理者は、Windows PowerShell を実行する Windows PowerShell を使用してこの手順を実行するには、Windows PowerShell プロンプトで次のコマンドを入力し、し、ENTER キーを押します。  
>   
> `Install-WindowsFeature FS-BranchCache -IncludeManagementTools`  
>   
> `Restart-Computer`  
>   
> データ重複除去役割サービスをインストールするに次のコマンドを入力し、し、ENTER キーを押します。  
>   
> `Install-WindowsFeature FS-Data-Deduplication -IncludeManagementTools`  
  
### <a name="to-install-file-services-and-the-branchcache-for-network-files-role-service"></a>ファイル サービスと、ファイル用 BranchCache ネットワークの役割サービスをインストールするには  
  
1.  サーバー マネージャーで、クリックして**管理**、] をクリックし、**追加の役割と機能**します。 追加の役割と機能のウィザードが開きます。 **開始する前に**、] をクリックして**次**します。  
  
2.  **インストールの種類を選択**、いることを確認**役割ベースまたは機能ベースのインストール**をクリックして選択して**次**します。  
  
3.  **対象サーバーの選択**、] をクリックし、適切なサーバーが選択されていることを確認**次**します。  
  
4.  **サーバーの役割の選択**で、**役割**、ことに注意してください、**ファイルおよび記憶域のサービス**ロールが既にインストールされています。役割サービスの選択項目を展開する役割名の左側の矢印をクリックしの左側の矢印をクリックして**ファイル サービスおよび iSCSI サービス**します。  
  
5.  チェック ボックスをオンに**ファイル サーバー**と**ネットワーク ファイル用 BranchCache**します。  
  
    > [!TIP]  
    > チェック ボックスを選択することをお勧め**データ重複除去**します。
  
    をクリックして**次**します。  
  
6.  **機能の選択**、] をクリックして**次**します。  
  
7.  **インストール オプションの確認**、選択内容を確認し、[クリックして**インストール**します。 **インストールの進行状況**インストール中にウィンドウが表示されます。 インストールが完了したら、クリックして**閉じる**します。
