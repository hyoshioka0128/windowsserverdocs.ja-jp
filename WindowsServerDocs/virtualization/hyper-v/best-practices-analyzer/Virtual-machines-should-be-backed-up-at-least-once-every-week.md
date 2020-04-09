---
title: 仮想マシンは、毎週少なくとも 1 回バックアップする必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 7dbd3dfc-c873-4a77-89f7-3166e18d9531
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 6cb425f92926aa1823ed89cd26afccc2d962603d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855035"
---
# <a name="virtual-machines-should-be-backed-up-at-least-once-every-week"></a>仮想マシンは、毎週少なくとも 1 回バックアップする必要があります。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|エラー|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*過去1週間に1つ以上の仮想マシンがバックアップされていません。*  
  
## <a name="impact"></a>影響  
*仮想マシンで問題が発生し、最新のバックアップが存在しない場合は、大量のデータが失われる可能性があります。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
*少なくとも1週間に1回実行するように仮想マシンのバックアップをスケジュールします。この仮想マシンがレプリカで、プライマリ仮想マシンがバックアップされている場合、またはプライマリ仮想マシンであり、そのレプリカがバックアップされている場合、この規則は無視できます。*  
  


