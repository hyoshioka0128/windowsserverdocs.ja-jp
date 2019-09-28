---
title: オフピーク時間にレプリケーションの再同期をスケジュールする必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 093a7bb7-8e0a-486b-b42b-04edd8809710
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 379f8c8cd6744fe5db176efb55a84f231ce45857
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393511"
---
# <a name="resynchronization-of-replication-should-be-scheduled-for-off-peak-hours"></a>オフピーク時間にレプリケーションの再同期をスケジュールする必要があります。

>適用先:Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|警告|  
|**カテゴリ**|操作|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*プライマリ仮想マシンのレプリケーションの再同期は、ピーク時以外にはスケジュールされません。*  
  
## <a name="impact"></a>影響  
*The machine が再同期が必要な状態になっているほど、レプリケーションログファイルが大きくなり、プライマリ仮想マシンでレプリケートされていない変更が発生する時間が長くなります。これは、次の仮想マシンに影響します:*  
  
@no__t-仮想マシンの > の一覧  
  
## <a name="resolution"></a>解決方法  
*Hyper-v マネージャーを使用して、仮想マシンのレプリケーション設定を変更し、オフピーク時間中に自動的に再同期を実行します。*  
  


