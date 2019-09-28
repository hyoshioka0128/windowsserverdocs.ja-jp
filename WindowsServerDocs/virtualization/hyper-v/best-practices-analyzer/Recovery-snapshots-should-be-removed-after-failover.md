---
title: フェールオーバー後に回復スナップショットを削除する必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 922115fa-e8dd-4055-aaf1-4a4437c5cf28
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 4b8574956fb1b46ca0cf9678187fffcd68c2d261
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393532"
---
# <a name="recovery-snapshots-should-be-removed-after-failover"></a>フェールオーバー後に回復スナップショットを削除する必要があります。

>適用先:Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016| 
|**製品/機能**|Hyper-V|  
|**順**|警告|  
|**カテゴリ**|操作|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*フェールオーバーされた仮想マシンには、1つまたは複数の回復スナップショットがあります。*  
  
## <a name="impact"></a>**よる**  
スナップショットファイルが格納されている物理ディスクでは、使用可能な空き領域が @no__t ます。このような場合、物理記憶域に対して追加のディスク操作を実行できるはされません。物理ストレージに依存する任意の仮想マシンを受ける可能性があります。これは、次の仮想マシンに影響します: *  
  
@no__t-仮想マシンの > の一覧  
  
## <a name="resolution"></a>**解決方法**  
*フェールオーバーされた仮想マシンごとに、Windows PowerShell の Start-vmfailover コマンドレットを使用して、回復スナップショットを削除し、フェールオーバーの完了を示します。*  
  


