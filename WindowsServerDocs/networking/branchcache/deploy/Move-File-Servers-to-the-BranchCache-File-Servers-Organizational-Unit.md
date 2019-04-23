---
title: ファイル サーバーを BranchCache ファイル サーバー組織単位に移動する
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 56c915ec-edb1-43b0-8ad2-c93841bb566f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 037b354bb6725ac7f91fc323b81bbdf15d03ac15
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885903"
---
# <a name="move-file-servers-to-the-branchcache-file-servers-organizational-unit"></a>ファイル サーバーを BranchCache ファイル サーバー組織単位に移動する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

Active Directory Domain Services (AD DS) で BranchCache ファイル サーバーを組織単位 (OU) に追加するのにこの手順を使用することができます。  
  
この手順を実行するには、**Domain Admins** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。  
  
> [!NOTE]  
> この手順を OU にコンピューター アカウントを追加する前に、Active Directory ユーザーとコンピューター コンソールで BranchCache ファイル サーバーの OU を作成する必要があります。 詳細については、次を参照してください。 [BranchCache ファイル サーバー組織単位を作成](../../branchcache/deploy/Create-the-BranchCache-File-Servers-Organizational-Unit.md)です。  
  
### <a name="to-move-file-servers-to-the-branchcache-file-servers-organizational-unit"></a>ファイル サーバー、BranchCache をファイル サーバー組織単位を移動するには  
  
1.  AD DS がインストールされている、サーバー マネージャーで、コンピューターで次のようにクリックします。**ツール**、 をクリックし、 **Active Directory ユーザーとコンピューター**します。 Active Directory ユーザーとコンピューター コンソールが開きます。  
  
2.  Active Directory ユーザーとコンピューター コンソールでは、アカウントを選択してドラッグし、以前に作成した OU の BranchCache ファイル サーバー上のコンピューター アカウントを削除するには、左クリックして、BranchCache ファイル サーバー用のコンピューター アカウントを見つけます。 たとえば、という名前の OU を以前に作成した場合**BranchCache ファイル サーバー**にドラッグ アンド ドロップのコンピューター アカウント、 **BranchCache ファイル サーバー** OU。  
  
3.  OU に移動したいドメイン内の BranchCache ファイル サーバーごとに、前の手順を繰り返します。  
  


