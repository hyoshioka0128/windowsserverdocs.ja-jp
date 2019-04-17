---
title: 既存のファイル サーバーをコンテンツ サーバーとして構成します。
description: このトピックの「BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法示しますの一部である
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: bdac7d2a-25b4-4f61-bed1-b290700c18f3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: da4c38b6209dc10704aee8c79344ee2da98da272
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="configure-an-existing-file-server-as-a-content-server"></a>既存のファイル サーバーをコンテンツ サーバーとして構成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

この手順を使用してをインストールすることができます、**ネットワーク ファイル用 BranchCache** Windows Server 2016 を実行するコンピューターで、ファイル サービス サーバーの役割の役割サービスです。  
  
> [!IMPORTANT]  
> ファイル サービス サーバーの役割がインストールされていない場合は、この手順を実行しないでください。 代わりを参照してください。[新しいファイル サーバーをコンテンツ サーバーとしてインストール](../../branchcache/deploy/Install-a-New-File-Server-as-a-Content-Server.md)します。  
  
メンバーシップ**管理者**、またはそれと同等がこの手順を実行するために必要な最小値。  
  
> [!NOTE]  
> 管理者は、Windows PowerShell を実行する Windows PowerShell を使用してこの手順を実行するには、Windows PowerShell プロンプトで次のコマンドを入力し、し、ENTER キーを押します。  
>   
> `Install-WindowsFeature FS-BranchCache -IncludeManagementTools`  
>   
> データ重複除去役割サービスをインストールするに次のコマンドを入力し、し、ENTER キーを押します。  
>   
> `Install-WindowsFeature FS-Data-Deduplication -IncludeManagementTools`  
  
### <a name="to-install-the-branchcache-for-network-files-role-service"></a>役割サービスのネットワーク ファイル用 BranchCache をインストールするには  
  
1.  サーバー マネージャーで、クリックして**管理**、] をクリックし、**追加の役割と機能**します。 追加の役割と機能のウィザードが開きます。 をクリックして**次**します。  
  
2.  **インストールの種類を選択**、いることを確認**役割ベースまたは機能ベースのインストール**をクリックして選択して**次**します。  
  
3.  **対象サーバーの選択**、] をクリックし、適切なサーバーが選択されていることを確認**次**します。  
  
4.  **サーバーの役割の選択**で、**役割**、ことに注意してください、**ファイルおよび記憶域のサービス**ロールが既にインストールされています。役割サービスの選択項目を展開する役割名の左側の矢印をクリックしの左側の矢印をクリックして**ファイル サービスおよび iSCSI サービス**します。  
  
5.  チェック ボックスをオン**ネットワーク ファイル用 BranchCache**します。  
  
    > [!TIP]  
    > されていない場合は、チェック ボックスを選択することをお勧め**データ重複除去**します。  
  
    をクリックして**次**します。  
  
6.  **機能の選択**、] をクリックして**次**します。  
  
7.  **インストール オプションの確認**、選択内容を確認し、[クリックして**インストール**します。 **インストールの進行状況**インストール中にウィンドウが表示されます。 インストールが完了したら、クリックして**閉じる**します。  
  


