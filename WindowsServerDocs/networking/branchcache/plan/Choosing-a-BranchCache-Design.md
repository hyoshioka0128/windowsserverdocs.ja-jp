---
title: BranchCache 設計の選択
description: このトピックの「BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法示しますの一部である
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 86c1ccad-2aa4-40fe-84c1-f77c49eb1216
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4fe40b3d9ece771a46af8ecc70297b8713d65875
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="choosing-a-branchcache-design"></a>BranchCache 設計の選択

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用するには、BranchCache のモードについて説明し、展開に最適なモードを選択します。  
  
このガイドを使用すると、次のモードとモードの組み合わせで BranchCache を展開します。  
  
-   すべてのブランチ オフィスは分散キャッシュ モード用に構成されます。  
  
-   すべてのブランチ オフィスでは、ホスト型キャッシュ モード用に構成され、サイトにホスト型キャッシュ サーバーがあります。  
  
-   いくつかのブランチ オフィスは分散キャッシュ モードの構成され、いくつかのブランチ オフィス サイトでホスト型キャッシュ サーバーがあるし、ホスト型キャッシュ モード用に構成されました。  
  
次の図は、分散キャッシュ モード用に構成された 1 つのブランチ オフィスとホスト型キャッシュ モード用に構成された 1 つのブランチ オフィス、デュアル モード インストールを示しています。  
  
![BranchCache 設計の選択](../../media/Choosing-a-BranchCache-Design/bc_new_modes.jpg)  
  
BranchCache を展開する前に、組織内の各ブランチ オフィスの必要に応じて、モードを選択します。  
  


