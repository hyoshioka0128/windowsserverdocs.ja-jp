---
title: すべての仮想ネットワークアダプターを有効にする必要があります
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: b17d647d-a34a-44de-ada6-01a2bf5eeb48
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: fce564fdb47d0677b36078f3d8446579bc06816c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366594"
---
# <a name="all-virtual-network-adapters-should-be-enabled"></a>すべての仮想ネットワークアダプターを有効にする必要があります

>適用先:Windows Server 2016


  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*物理ネットワークアダプターに関連付けられている1つまたは複数の仮想ネットワークアダプターが、管理オペレーティングシステムで無効になっています。*  
  
## <a name="impact"></a>影響  
  
*このサーバーの構成は最適ではありません。*  
  
管理オペレーティングシステムは、無効な仮想ネットワークアダプターに関連付けられているため、このコンピューターの物理ネットワークアダプターのいずれかを使用して物理 (外部) ネットワークに接続することはできません。  
  
## <a name="resolution"></a>解決方法  
  
*Use & のインターネット設定を使用して、仮想ネットワークアダプターを有効にします。または、仮想スイッチマネージャーを使用して外部仮想スイッチを再構成し、管理オペレーティングシステムと共有しないようにしてください。*  
  


