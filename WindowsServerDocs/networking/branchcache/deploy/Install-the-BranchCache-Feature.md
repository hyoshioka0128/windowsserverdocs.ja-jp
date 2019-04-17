---
title: BranchCache 機能をインストールします。
description: このトピックの「BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法示しますの一部である
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 4f31dc61-2dbe-4c7e-b3f9-85ae49a45049
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a69848536b56521da9b5ef07689aba7f8690e888
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="install-the-branchcache-feature"></a>BranchCache 機能をインストールします。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

この手順を使用するには、BranchCache 機能をインストールし、Windows Server を実行するコンピューターで BranchCache サービスの開始を&reg;2016、Windows Server 2012 R2、または Windows Server 2012 です。  
  
メンバーシップ**管理者**またはそれと同等がこの手順を実行するために必要な最小値。  
  
この手順を実行する前に、インストールして、BITS ベースのアプリケーションや Web サーバーを構成することをお勧めします。  
  
> [!NOTE]  
> 管理者は、Windows PowerShell を実行する Windows PowerShell を使用してこの手順を実行するには、Windows PowerShell プロンプトで次のコマンドを入力し、し、ENTER キーを押します。  
>   
> `Install-WindowsFeature BranchCache`  
>   
> `Restart-Computer`  
  
### <a name="to-install-and-enable-the-branchcache-feature"></a>インストールして、BranchCache 機能を有効にするには  
  
1.  サーバー マネージャーで、クリックして**管理**、] をクリックし、**追加の役割と機能**します。 追加の役割と機能のウィザードが開きます。 をクリックして**次**します。  
  
2.  **インストールの種類を選択**、いることを確認**役割ベースまたは機能ベースのインストール**をクリックして選択して**次**します。  
  
3.  **対象サーバーの選択**、] をクリックし、適切なサーバーが選択されていることを確認**次**します。  
  
4.  **サーバーの役割の選択**、] をクリックして**次**します。  
  
5.  **機能の選択**、] をクリックして**BranchCache**、] をクリックし、**次**します。  
  
6.  **インストール オプションの確認**、] をクリックして**インストール**します。 **インストールの進行状況**、BranchCache 機能のインストールを実行します。 インストールが完了したら、クリックして**閉じる**します。  
  
BranchCache 機能をインストールした後、PeerDistSvc - とも呼ばれます。-BranchCache サービスを有効にすると、し、開始の種類が自動します。  
  


