---
title: このサーバーでの 1 つまたは複数の仮想マシンのレプリケーションが一時停止します。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: e1119a40-eda3-4058-8648-7df81cbc6c29
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 17d50f116c6cee488367c924bfbce3791a8d879f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393542"
---
# <a name="replication-is-paused-for-one-or-more-virtual-machines-on-this-server"></a>このサーバーでの 1 つまたは複数の仮想マシンのレプリケーションが一時停止します。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|Warning|  
|**カテゴリ**|運用|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*1つまたは複数の仮想マシンのレプリケーションが一時停止しています。プライマリ仮想マシンが一時停止されている間に発生したすべての変更が累積され、レプリケーションが再開されるとレプリカ仮想マシンに送信されます。*  
  
## <a name="impact"></a>影響  
*レプリケーションが一時停止されている限り、プライマリ仮想マシンで発生した累積された変更によって、プライマリサーバー上の使用可能なディスク領域が消費されます。レプリケーションが再開されると、レプリカサーバーへのネットワークトラフィックが大量に発生する可能性があります。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
*レプリケーションの一時停止が意図されていることを確認します。ディスク領域不足またはネットワーク接続に対処するためにレプリケーションが一時停止されている場合は、それらの問題が解決されるとすぐにレプリケーションを再開します。*  
  


