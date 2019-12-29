---
title: ネットワーク上のレプリケーショントラフィックを調整するためのポリシーを構成する
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 82cb1aef-cdc3-4d0a-88d4-ef497ab79606
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 5b3afd594f56973007a2f0f4318de8a8c7a98209
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365114"
---
# <a name="configure-a-policy-to-throttle-the-replication-traffic-on-the-network"></a>ネットワーク上のレプリケーショントラフィックを調整するためのポリシーを構成する

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
*レプリケーションで使用できるネットワーク帯域幅の量に制限がない可能性があります。*  
  
## <a name="impact"></a>影響  
*ネットワーク帯域幅がレプリケーショントラフィックによって完全に左右され、他の重要なネットワークアクティビティに影響を与える可能性があります。これは、次のポートに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
*別の方法を使用してネットワークトラフィックを調整する場合は、これを無視してもかまいません。それ以外の場合は、グループポリシーエディターを使用して、レプリカサーバーの関連ポートへのネットワークトラフィックを制限するポリシーを構成します。*  
  
  


