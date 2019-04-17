---
title: BranchCache ファイル サーバー組織単位を作成します。
description: このトピックの「BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法示しますの一部である
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 2cda192f-6b45-4e6c-88d9-70ca179ddb94
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a92cb3110e4aecb1ef09a45ed14173305722c655
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="create-the-branchcache-file-servers-organizational-unit"></a>BranchCache ファイル サーバー組織単位を作成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

Active Directory ドメイン サービス (AD DS) の BranchCache ファイル サーバーで、組織単位 (OU) を作成するのにこの手順を使用することができます。  
  
メンバーシップ**Domain Admins**、またはそれと同等がこの手順を実行するために必要な最小値。  
  
### <a name="to-create-the-branchcache-file-servers-organizational-unit"></a>BranchCache ファイル サーバー組織単位を作成するには  
  
1.  AD DS がインストールされている、サーバー マネージャーで、コンピューター上] をクリックして**ツール**、] をクリックし、**Active Directory ユーザーとコンピューター**します。 Active Directory ユーザーとコンピューター コンソールが開きます。  
  
2.  Active Directory ユーザーとコンピューター コンソールで、OU を追加するドメインを右クリックします。 たとえば、ドメインが example.com をという名前の場合を右クリックして**example.com**します。をポイント**新規**、] をクリックし、**組織単位**します。 **新しいオブジェクト - 組織単位**] ダイアログ ボックスが開きます。  
  
3.  **新しいオブジェクト - 組織単位**] ダイアログ ボックスで、**名**、新しい OU の名前を入力します。 たとえば、OU の BranchCache ファイル サーバーの名前を付ける場合は、入力**BranchCache ファイル サーバー**、] をクリックし、**OK**します。  
  


