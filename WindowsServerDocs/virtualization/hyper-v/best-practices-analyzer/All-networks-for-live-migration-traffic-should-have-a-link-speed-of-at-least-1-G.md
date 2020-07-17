---
title: ライブマイグレーショントラフィックのすべてのネットワークは、少なくとも 1 Gbps のリンク速度を持つ必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 89411b63-bec8-463d-b486-107548ed440e
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: adb16b1c4618e0874f48f4715440a9d903f5bc9f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857845"
---
# <a name="all-networks-for-live-migration-traffic-should-have-a-link-speed-of-at-least-1-gbps"></a>ライブマイグレーショントラフィックのすべてのネットワークは、少なくとも 1 Gbps のリンク速度を持つ必要があります。

>適用対象: Windows Server 2016


  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|［警告］|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*ライブマイグレーショントラフィックのネットワークには、少なくとも 1 Gbps のリンク速度がありません。*  
  
## <a name="impact"></a>影響  
*ライブマイグレーションが遅くなり、TCP 接続のタイムアウトによってネットワーク接続が中断される可能性があります。*  
  
## <a name="resolution"></a>解決方法  
*1 Gbps 以上の速度でライブマイグレーションネットワークを少なくとも1つ構成してください。*  
  
既存のネットワークアダプターが 1 Gbps 以上のリンク速度をサポートしているかどうかを確認するには、ネットワークハードウェアベンダーのドキュメントを参照してください。  
  


