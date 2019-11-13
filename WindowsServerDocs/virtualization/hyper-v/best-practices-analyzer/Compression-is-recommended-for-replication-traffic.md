---
title: レプリケーショントラフィックには圧縮を使用することをお勧めします
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: cf8be6e9-2909-4e4a-bb63-d1e1ebbc6930
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 77a314e816c36f626ea3edb10b80f65e3897e7c5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365102"
---
# <a name="compression-is-recommended-for-replication-traffic"></a>レプリケーショントラフィックには圧縮を使用することをお勧めします

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|Warning|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*ネットワーク経由でプライマリサーバーからレプリカサーバーに送信されるレプリケーショントラフィックは圧縮されていません。*  
  
## <a name="impact"></a>影響  
*レプリケーショントラフィックでは、必要以上の帯域幅が使用されます。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
*Hyper-v マネージャーで、仮想マシンの設定でネットワーク経由で転送されるデータを圧縮するように Hyper-v レプリカを構成します。また、Hyper-v の外部でツールを使用して圧縮を行うこともできます。*  
  


