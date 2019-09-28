---
title: 新しいファイル サーバーをコンテンツ サーバーとしてインストールする
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 1f49fc3c-28a6-4d3d-b787-1be9e61e792f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 489006c50ccbfa1f452d56b1a18217692d45cb1f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406454"
---
# <a name="install-a-new-file-server-as-a-content-server"></a>新しいファイル サーバーをコンテンツ サーバーとしてインストールする

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

この手順を使用して、Windows Server 2016 を実行しているコンピューターにファイルサービスサーバーの役割と**ネットワークファイルの BranchCache**の役割サービスをインストールできます。  
  
メンバーシップ **管理者**, 、または同等がこの手順を実行するために必要な最小値。  
  
> [!NOTE]  
> 管理者は、Windows PowerShell を実行する Windows PowerShell を使用して、この手順を実行するには、Windows PowerShell プロンプトで次のコマンドを入力し、ENTER キーを押します。  
>   
> `Install-WindowsFeature FS-BranchCache -IncludeManagementTools`  
>   
> `Restart-Computer`  
>   
> データ重複除去の役割サービスをインストールするには、次のコマンドを入力して、enter キーを押します。  
>   
> `Install-WindowsFeature FS-Data-Deduplication -IncludeManagementTools`  
  
### <a name="to-install-file-services-and-the-branchcache-for-network-files-role-service"></a>ファイルサービスおよびネットワークファイル用 BranchCache 役割サービスをインストールするには  
  
1.  サーバー マネージャーで、 **[管理]** をクリックし、 **[役割と機能の追加]** をクリックします。 役割と機能の追加ウィザードが起動されます。 **[開始する前に]** で **[次へ]** をクリックします。  
  
2.  **[インストールの種類の選択**] で、 **[役割ベースまたは機能ベースのインストール]** が選択されていることを確認し、 **[次へ]** をクリックします。  
  
3.  **対象サーバーの選択**, 、適切なサーバーが選択されていることを確認し、をクリックして **次**します。  
  
4.  **[サーバーの役割の選択**] の **[役割]** で、**ファイルサービスおよび記憶域サービス**の役割が既にインストールされていることに注意してください。役割名の左側にある矢印をクリックして役割サービスを選択し、 **[ファイルサービスおよび ISCSI サービス]** の左側にある矢印をクリックします。  
  
5.  **ネットワークファイルの** **ファイルサーバー**と BranchCache のチェックボックスをオンにします。  
  
    > [!TIP]  
    > また、 **[データ重複除去]** のチェックボックスもオンにすることをお勧めします。
  
    **[次へ]** をクリックします。  
  
6.  **機能の選択**, をクリックして **次**します。  
  
7.  **[インストールオプションの確認]** で、選択内容を確認し、 **[インストール]** をクリックします。 インストール中に **[インストールの進行状況]** ウィンドウが表示されます。 インストールが完了したら、クリックして **閉じる**します。
