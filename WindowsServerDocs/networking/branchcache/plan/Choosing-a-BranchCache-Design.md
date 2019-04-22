---
title: BranchCache 設計の選択
description: このトピックは、BranchCache 展開ガイドの Windows Server 2016、ブランチ オフィスに WAN 帯域幅使用量を最適化するために分散され、ホスト型キャッシュ モードで BranchCache を展開する方法を示しますの一部
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 86c1ccad-2aa4-40fe-84c1-f77c49eb1216
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 330dcbee26f52ff69cd85ef8dc78d2e161b943d1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59811913"
---
# <a name="choosing-a-branchcache-design"></a>BranchCache 設計の選択

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

展開に最適なモードを選択して BranchCache のモードの詳細については、このトピックを使用できます。  
  
このガイドを使用して、次のモードおよびモードの組み合わせで BranchCache を展開することができます。  
  
-   すべてのブランチ オフィスは、分散キャッシュ モード用に構成されます。  
  
-   すべてのブランチ オフィスでは、ホスト型キャッシュ モードが構成され、サイトにホスト型キャッシュ サーバーがあります。  
  
-   一部のブランチ オフィス分散キャッシュ モードが構成され、いくつかのブランチ オフィス サイトにホスト型キャッシュ サーバーがあるし、ホスト型キャッシュ モード用に構成されます。  
  
次の図は、分散キャッシュ モード用に構成された 1 つのブランチ オフィスとホスト型キャッシュ モード用に構成された 1 つのブランチ オフィス、デュアル モードのインストールを示しています。  
  
![BranchCache 設計の選択](../../media/Choosing-a-BranchCache-Design/bc_new_modes.jpg)  
  
BranchCache を展開する前に、組織内で各ブランチ オフィスで望ましいとモードを選択します。  
  


