---
title: BranchCache 機能をインストールする
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 4f31dc61-2dbe-4c7e-b3f9-85ae49a45049
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a895e65686a6ccfb1453bc7cc7ddfcab5720a206
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80319213"
---
# <a name="install-the-branchcache-feature"></a>BranchCache 機能をインストールする

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

この手順を使用するには、BranchCache 機能をインストールして Windows Server を実行するコンピューターで BranchCache サービスを開始する&reg; 2016、Windows Server 2012 R2、または Windows Server 2012 です。  
  
メンバーシップ **管理者** 等価は、この手順を実行するために必要な最小値またはです。  
  
この手順を実行する前に、インストールして、BITS ベースのアプリケーションまたは Web サーバーを構成することをお勧めします。  
  
> [!NOTE]  
> 管理者は、Windows PowerShell を実行する Windows PowerShell を使用して、この手順を実行するには、Windows PowerShell プロンプトで次のコマンドを入力し、ENTER キーを押します。  
>   
> `Install-WindowsFeature BranchCache`  
>   
> `Restart-Computer`  
  
### <a name="to-install-and-enable-the-branchcache-feature"></a>インストールして、BranchCache 機能を有効にします。  
  
1.  サーバー マネージャーで、 **[管理]** をクリックし、 **[役割と機能の追加]** をクリックします。 役割と機能の追加ウィザードが開きます。 **[次へ]** をクリックします。  
  
2.  **[インストールの種類の選択**] で、 **[役割ベースまたは機能ベースのインストール]** が選択されていることを確認し、 **[次へ]** をクリックします。  
  
3.  **対象サーバーの選択**, 、適切なサーバーが選択されていることを確認し、をクリックして **次**します。  
  
4.  **[サーバーの役割の選択]** で、 **[次へ]** をクリックします。  
  
5.  **機能の選択**, 、 をクリックして **BranchCache**, 、 をクリックし、 **次**します。  
  
6.  **[インストール オプションの確認]** で、 **[インストール]** をクリックします。 **インストールの進行状況**, 、BranchCache 機能のインストールを実行します。 インストールが完了したら、クリックして **閉じる**します。  
  
BranchCache 機能をインストールした後、PeerDistSvc - とも呼ばれます。-BranchCache サービスが有効になっているし、開始の種類が自動です。  
  


