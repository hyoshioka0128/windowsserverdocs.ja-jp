---
title: 仮想マシンは、毎週少なくとも 1 回バックアップする必要があります。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 7dbd3dfc-c873-4a77-89f7-3166e18d9531
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: e079e3cb225ec9c712233bbf3efc85bb6f09b218
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826753"
---
# <a name="virtual-machines-should-be-backed-up-at-least-once-every-week"></a>仮想マシンは、毎週少なくとも 1 回バックアップする必要があります。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|エラー|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*過去 1 週間に 1 つまたは複数の仮想マシンがバックアップされていません。*  
  
## <a name="impact"></a>影響  
*大量のデータ損失は、仮想マシンには、問題が発生した最新のバックアップが存在しない場合に発生する可能性があります。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*週 1 回以上実行するには、仮想マシンのバックアップをスケジュールします。これは、プライマリ仮想マシンとそのレプリカがバックアップされている場合、またはこの仮想マシンは、レプリカと、そのプライマリ仮想マシンのバックアップを場合、に、このルールを無視することができます。*  
  


