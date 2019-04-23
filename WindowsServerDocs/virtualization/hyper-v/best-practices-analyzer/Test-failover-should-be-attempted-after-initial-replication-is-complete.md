---
title: 初期レプリケーションが完了後は、テスト フェールオーバーを実行しようとする必要があります。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: cea7eeaa-c1a7-4f87-89be-d4e1208c546f
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 347b089330548e5fb2631e43ca66c96bb6bc4e9d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880413"
---
# <a name="test-failover-should-be-attempted-after-initial-replication-is-complete"></a>初期レプリケーションが完了後は、テスト フェールオーバーを実行しようとする必要があります。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|操作|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="problem"></a>問題  
*なかったテスト フェールオーバーには少なくとも 1 か月間で。*  
  
## <a name="impact"></a>影響  
*計画または計画外のフェールオーバーが成功またはワークロードの操作は、フェールオーバー後に正しく続行を確認することはありません。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*HYPER-V マネージャーを使用して、テスト フェールオーバーを実行します。*  
  


