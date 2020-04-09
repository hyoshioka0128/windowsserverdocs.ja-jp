---
title: 初期レプリケーションが完了後は、テスト フェールオーバーを実行しようとする必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: cea7eeaa-c1a7-4f87-89be-d4e1208c546f
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 41d96b33c686631f57cd35e76b64ee3dde206655
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858945"
---
# <a name="test-failover-should-be-attempted-after-initial-replication-is-complete"></a>初期レプリケーションが完了後は、テスト フェールオーバーを実行しようとする必要があります。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|［警告］|  
|**カテゴリ**|運用|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="problem"></a>Problem  
*少なくとも1か月にテストフェールオーバーが発生していません。*  
  
## <a name="impact"></a>影響  
*計画済みまたは計画外のフェールオーバーが成功するか、フェールオーバー後にワークロード操作が正常に続行されるかを確認するメッセージは表示されません。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
*Hyper-v マネージャーを使用して、テストフェールオーバーを実行します。*  
  


