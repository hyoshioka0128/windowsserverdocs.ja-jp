---
title: BranchCache 設計の選択
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 86c1ccad-2aa4-40fe-84c1-f77c49eb1216
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2a1b4615dfda3989f0321725fd27da066fcb8a5e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406320"
---
# <a name="choosing-a-branchcache-design"></a>BranchCache 設計の選択

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、BranchCache モードについて学習し、展開に最適なモードを選択する方法について説明します。  
  
このガイドを使用して、次のモードとモードの組み合わせで BranchCache を展開できます。  
  
-   すべてのブランチオフィスは、分散キャッシュモード用に構成されています。  
  
-   すべてのブランチオフィスは、ホスト型キャッシュモード用に構成され、サイトにホスト型キャッシュサーバーがあります。  
  
-   一部のブランチオフィスは、分散キャッシュモード用に構成されています。一部のブランチオフィスには、サイトにホスト型キャッシュサーバーがあり、ホスト型キャッシュモード用に構成されています。  
  
次の図は、1つのブランチオフィスが分散キャッシュモード用に構成され、1つのブランチオフィスがホスト型キャッシュモード用に構成されている、デュアルモードインストールを示しています。  
  
![BranchCache 設計の選択](../../media/Choosing-a-BranchCache-Design/bc_new_modes.jpg)  
  
BranchCache を展開する前に、組織内の各ブランチオフィスに対して希望するモードを選択します。  
  


