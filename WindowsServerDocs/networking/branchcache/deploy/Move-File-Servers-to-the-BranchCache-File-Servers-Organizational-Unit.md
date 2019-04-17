---
title: ファイル サーバーを BranchCache ファイル サーバー組織単位に移動します。
description: このトピックの「BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法示しますの一部である
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 56c915ec-edb1-43b0-8ad2-c93841bb566f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 09afb4936545cb1f5bb14573261008ff18badd4d
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="move-file-servers-to-the-branchcache-file-servers-organizational-unit"></a>ファイル サーバーを BranchCache ファイル サーバー組織単位に移動します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

Active Directory ドメイン サービス (AD DS) で、組織単位 (OU) に BranchCache ファイル サーバーを追加するのにこの手順を使用することができます。  
  
メンバーシップ**Domain Admins**、またはそれと同等がこの手順を実行するために必要な最小値。  
  
> [!NOTE]  
> この手順を OU にコンピューター アカウントを追加する前に、Active Directory ユーザーとコンピューター コンソールで BranchCache ファイル サーバーの OU を作成する必要があります。 詳細については、次を参照してください。[BranchCache ファイル サーバー組織単位を作成する](../../branchcache/deploy/Create-the-BranchCache-File-Servers-Organizational-Unit.md)します。  
  
### <a name="to-move-file-servers-to-the-branchcache-file-servers-organizational-unit"></a>ファイル サーバーを BranchCache ファイル サーバー組織単位を移動するには  
  
1.  AD DS がインストールされている、サーバー マネージャーで、コンピューター上] をクリックして**ツール**、] をクリックし、**Active Directory ユーザーとコンピューター**します。 Active Directory ユーザーとコンピューター コンソールが開きます。  
  
2.  Active Directory ユーザーとコンピューター コンソールで、アカウントを選択し、ドラッグ アンド ドロップ BranchCache ファイル サーバー以前に作成した OU にコンピューター アカウントを左クリック BranchCache ファイル サーバーのコンピューター アカウントを探します。 たとえば、以前にという名前の OU を作成した場合**BranchCache ファイル サーバー**にドラッグ アンド ドロップ、コンピューター アカウント、**BranchCache ファイル サーバー** OU です。  
  
3.  OU に移動するドメイン内の各 BranchCache ファイル サーバーを前の手順を繰り返します。  
  


