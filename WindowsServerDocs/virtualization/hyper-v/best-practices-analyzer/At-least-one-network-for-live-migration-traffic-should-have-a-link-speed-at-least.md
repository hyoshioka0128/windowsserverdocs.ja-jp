---
title: ライブマイグレーショントラフィック用の少なくとも1つのネットワークで、少なくとも 1 Gbps のリンク速度が必要です
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 5714df3f-f810-4618-8c93-e24881651100
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 95066cc111fb91ac1d6745dfb93527735de92a69
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365289"
---
# <a name="at-least-one-network-for-live-migration-traffic-should-have-a-link-speed-of-at-least-1-gbps"></a>ライブマイグレーショントラフィック用の少なくとも1つのネットワークで、少なくとも 1 Gbps のリンク速度が必要です

>適用先:Windows Server 2016


  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|Error|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*ライブマイグレーショントラフィックのネットワークには、少なくとも 1 Gbps のリンク速度がありません。*  
  
## <a name="impact"></a>影響  
*ライブマイグレーションが遅くなり、TCP 接続のタイムアウトによってネットワーク接続が中断される可能性があります。*  
  
## <a name="resolution"></a>解決方法  
*1 Gbps 以上の速度でライブマイグレーションネットワークを少なくとも1つ構成してください。*  
  
既存のネットワークアダプターが 1 Gbps 以上のリンク速度をサポートしているかどうかを確認するには、ネットワークハードウェアベンダーのドキュメントを参照してください。  
  


