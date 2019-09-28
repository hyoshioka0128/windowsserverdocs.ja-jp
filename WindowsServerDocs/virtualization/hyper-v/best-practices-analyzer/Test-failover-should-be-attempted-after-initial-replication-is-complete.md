---
title: 初期レプリケーションが完了後は、テスト フェールオーバーを実行しようとする必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: cea7eeaa-c1a7-4f87-89be-d4e1208c546f
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: ec3ad3994227eb14d1d2e53842c755af76ac538d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364703"
---
# <a name="test-failover-should-be-attempted-after-initial-replication-is-complete"></a>初期レプリケーションが完了後は、テスト フェールオーバーを実行しようとする必要があります。

>適用先:Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|警告|  
|**カテゴリ**|操作|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="problem"></a>問題  
*少なくとも1か月にテストフェールオーバーが発生していません。*  
  
## <a name="impact"></a>影響  
@no__t、計画済みまたは計画外のフェールオーバーが成功するか、フェールオーバー後にワークロード操作が正常に続行されるかを確認するメッセージが表示されません。これは、次の仮想マシンに影響します: *  
  
@no__t-仮想マシンの > の一覧  
  
## <a name="resolution"></a>解決方法  
*Hyper-v マネージャーを使用して、テストフェールオーバーを実行します。*  
  


