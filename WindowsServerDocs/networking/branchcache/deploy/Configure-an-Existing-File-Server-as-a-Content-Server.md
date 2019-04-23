---
title: 既存のファイル サーバーをコンテンツ サーバーとして構成する
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: bdac7d2a-25b4-4f61-bed1-b290700c18f3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d031e8aa853849c322692552ca9107838cebb5e5
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866913"
---
# <a name="configure-an-existing-file-server-as-a-content-server"></a>既存のファイル サーバーをコンテンツ サーバーとして構成する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

インストールするこの手順を使用することができます、**ネットワーク ファイル用 BranchCache** Windows Server 2016 を実行するコンピューターにファイル サービス サーバー役割の役割サービスです。  
  
> [!IMPORTANT]  
> ファイル サービス サーバーの役割がインストールされていない場合は、この手順を実行しません。 代わりを参照してください[コンテンツ サーバーとして新しいファイル サーバーをインストール](../../branchcache/deploy/Install-a-New-File-Server-as-a-Content-Server.md)します。  
  
メンバーシップ **管理者**, 、または同等がこの手順を実行するために必要な最小値。  
  
> [!NOTE]  
> 管理者は、Windows PowerShell を実行する Windows PowerShell を使用して、この手順を実行するには、Windows PowerShell プロンプトで次のコマンドを入力し、ENTER キーを押します。  
>   
> `Install-WindowsFeature FS-BranchCache -IncludeManagementTools`  
>   
> データ重複除去の役割サービスをインストールするには、次のコマンドを入力し、し、ENTER キーを押します。  
>   
> `Install-WindowsFeature FS-Data-Deduplication -IncludeManagementTools`  
  
### <a name="to-install-the-branchcache-for-network-files-role-service"></a>役割サービスのネットワーク ファイル用 BranchCache をインストールするには  
  
1.  サーバー マネージャーで、**[管理]** をクリックし、**[役割と機能の追加]** をクリックします。 追加の役割と機能のウィザードが開きます。 **[次へ]** をクリックします。  
  
2.  **インストールの種類を選択します。**、いることを確認**役割ベースまたは機能ベースのインストール**が選択されていると、[] をクリックし、 **[次へ]** します。  
  
3.  **対象サーバーの選択**, 、適切なサーバーが選択されていることを確認し、をクリックして **次**します。  
  
4.  **サーバーの役割の選択**の**ロール**、なお、**ファイルおよび記憶域サービス**ロールが既にインストールされている; を展開するロール名の左側にある矢印をクリックして、役割サービスの選択範囲の左側にある矢印をクリックして**ファイルおよび iSCSI サービス**します。  
  
5.  チェック ボックスをオン**ネットワーク ファイル用 BranchCache**します。  
  
    > [!TIP]  
    > されていない場合は、チェック ボックスを選択することをお勧め**データ重複除去**します。  
  
    **[次へ]** をクリックします。  
  
6.  **機能の選択**, をクリックして **次**します。  
  
7.  **インストール オプションの確認**選択内容を確認し、クリックして**インストール**します。 **インストールの進行状況**インストール中にウィンドウが表示されます。 インストールが完了したら、クリックして **閉じる**します。  
  


