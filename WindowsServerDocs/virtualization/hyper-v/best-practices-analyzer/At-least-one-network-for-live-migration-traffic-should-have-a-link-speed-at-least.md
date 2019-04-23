---
title: ライブ マイグレーション トラフィックの少なくとも 1 つのネットワークに少なくとも 1 Gbps のリンク速度である必要があります。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 5714df3f-f810-4618-8c93-e24881651100
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: ef75f73bd934b863b146e93f4cdc7323e5d4c6fb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837733"
---
# <a name="at-least-one-network-for-live-migration-traffic-should-have-a-link-speed-of-at-least-1-gbps"></a>ライブ マイグレーション トラフィックの少なくとも 1 つのネットワークに少なくとも 1 Gbps のリンク速度である必要があります。

>適用先:Windows Server 2016


  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|エラー|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*なしのライブ マイグレーション トラフィック用のネットワークがある少なくとも 1 Gbps のリンク速度。*  
  
## <a name="impact"></a>影響  
*ライブ マイグレーションが発生する時間がかかり、TCP 接続のタイムアウトのためにネットワーク接続が中断される可能性があります。*  
  
## <a name="resolution"></a>解決方法  
*1 Gbps 以上の速度で少なくとも 1 つのライブ マイグレーション ネットワークを構成します。*  
  
かどうかは、少なくとも 1 Gbps のリンク速度をサポート、既存のネットワーク アダプターのいずれかを確認する、ネットワーク ハードウェアの製造元からドキュメントを参照してください。  
  


