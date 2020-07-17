---
title: ライブマイグレーショントラフィック用の少なくとも1つのネットワークで、少なくとも 1 Gbps のリンク速度が必要です
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 5714df3f-f810-4618-8c93-e24881651100
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 04ce4ea86e39e8bd98216ae4e6b12899c9366421
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857825"
---
# <a name="at-least-one-network-for-live-migration-traffic-should-have-a-link-speed-of-at-least-1-gbps"></a>ライブマイグレーショントラフィック用の少なくとも1つのネットワークで、少なくとも 1 Gbps のリンク速度が必要です

>適用対象: Windows Server 2016


  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|エラー|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*ライブマイグレーショントラフィックのネットワークには、少なくとも 1 Gbps のリンク速度がありません。*  
  
## <a name="impact"></a>影響  
*ライブマイグレーションが遅くなり、TCP 接続のタイムアウトによってネットワーク接続が中断される可能性があります。*  
  
## <a name="resolution"></a>解決方法  
*1 Gbps 以上の速度でライブマイグレーションネットワークを少なくとも1つ構成してください。*  
  
既存のネットワークアダプターが 1 Gbps 以上のリンク速度をサポートしているかどうかを確認するには、ネットワークハードウェアベンダーのドキュメントを参照してください。  
  


