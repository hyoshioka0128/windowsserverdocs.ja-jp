---
title: 新しいファイル サーバーをコンテンツ サーバーとしてインストールする
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 1f49fc3c-28a6-4d3d-b787-1be9e61e792f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e3a4dbe5339685b385b0157756379e9e545f1964
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812023"
---
# <a name="install-a-new-file-server-as-a-content-server"></a>新しいファイル サーバーをコンテンツ サーバーとしてインストールする

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

この手順を使用するには、ファイル サービス サーバーの役割をインストールして、**ネットワーク ファイル用 BranchCache** Windows Server 2016 を実行しているコンピューター上のロール サービス。  
  
メンバーシップ **管理者**, 、または同等がこの手順を実行するために必要な最小値。  
  
> [!NOTE]  
> 管理者は、Windows PowerShell を実行する Windows PowerShell を使用して、この手順を実行するには、Windows PowerShell プロンプトで次のコマンドを入力し、ENTER キーを押します。  
>   
> `Install-WindowsFeature FS-BranchCache -IncludeManagementTools`  
>   
> `Restart-Computer`  
>   
> データ重複除去の役割サービスをインストールするには、次のコマンドを入力し、し、ENTER キーを押します。  
>   
> `Install-WindowsFeature FS-Data-Deduplication -IncludeManagementTools`  
  
### <a name="to-install-file-services-and-the-branchcache-for-network-files-role-service"></a>ファイル サービスと、BranchCache のネットワーク ファイルの役割サービスをインストールするには  
  
1.  サーバー マネージャーで、**[管理]** をクリックし、**[役割と機能の追加]** をクリックします。 役割と機能の追加ウィザードが起動されます。 **[開始する前に]** で **[次へ]** をクリックします。  
  
2.  **インストールの種類を選択します。**、いることを確認**役割ベースまたは機能ベースのインストール**が選択されていると、[] をクリックし、 **[次へ]** します。  
  
3.  **対象サーバーの選択**, 、適切なサーバーが選択されていることを確認し、をクリックして **次**します。  
  
4.  **サーバーの役割の選択**の**ロール**、なお、**ファイルおよび記憶域サービス**ロールが既にインストールされている; を展開するロール名の左側にある矢印をクリックして、役割サービスの選択範囲の左側にある矢印をクリックして**ファイルおよび iSCSI サービス**します。  
  
5.  チェック ボックスをオン**ファイル サーバー**と**ネットワーク ファイル用 BranchCache**します。  
  
    > [!TIP]  
    > チェック ボックスを選択することをお勧め**データ重複除去**します。
  
    **[次へ]** をクリックします。  
  
6.  **機能の選択**, をクリックして **次**します。  
  
7.  **インストール オプションの確認**選択内容を確認し、クリックして**インストール**します。 **インストールの進行状況**インストール中にウィンドウが表示されます。 インストールが完了したら、クリックして **閉じる**します。
