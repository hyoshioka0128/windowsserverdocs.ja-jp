---
title: シリアル ポートが第 2 世代仮想マシンで構成します。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 87061193-dd3f-4398-aa5d-4cee83cadfa3
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 8a8c15076921efa0e1e791a18c6a45ea1bf27b0e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364728"
---
# <a name="serial-ports-should-not-be-configured-on-generation-2-virtual-machines"></a>シリアル ポートが第 2 世代仮想マシンで構成します。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|Warning|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*1つまたは複数の第2世代仮想マシンにシリアルポートが構成されています。*  
  
## <a name="impact"></a>**よる**  
*次の仮想マシンのパフォーマンスが影響を受ける可能性があります。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>**解決方法**  
*これが意図的なものである場合は、それ以上の操作は必要ありません。それ以外の場合は、Hyper-v マネージャーまたは Windows PowerShell を使用して、仮想マシンのシリアルポートから接続文字列を削除することを検討してください。*  
  


