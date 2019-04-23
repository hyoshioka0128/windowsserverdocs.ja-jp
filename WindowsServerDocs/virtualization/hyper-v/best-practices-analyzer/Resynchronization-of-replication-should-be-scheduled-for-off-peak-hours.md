---
title: オフピーク時間にレプリケーションの再同期をスケジュールする必要があります。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 093a7bb7-8e0a-486b-b42b-04edd8809710
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 2d6c18b7e37c5d17f56f41c7ff03ed8796457de0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840023"
---
# <a name="resynchronization-of-replication-should-be-scheduled-for-off-peak-hours"></a>オフピーク時間にレプリケーションの再同期をスケジュールする必要があります。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|操作|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*ピーク時に、プライマリ仮想マシンのレプリケーションの再同期は予定はありません。*  
  
## <a name="impact"></a>影響  
*期間が長いほど仮想マシンが再同期を必要とする状態が長いほどのレプリケーションのログ ファイルの拡張や、プライマリ仮想マシンで、レプリケート解除された変更が発生します。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*HYPER-V マネージャーを使用して、オフピーク時間中に自動的に再同期を実行する仮想マシンのレプリケーション設定を変更します。*  
  


