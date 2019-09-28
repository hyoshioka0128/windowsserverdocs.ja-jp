---
title: 仮想マシンが容量可変の拡張バーチャルハードディスクを使用する場合に、十分な物理ディスク領域が使用可能であることを確認します。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 9e3e3e64-4b3a-4b9d-acf1-e4df61a04f1e
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: c38d7c11a05eef9d29097e625fec2830000cf550
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393639"
---
# <a name="ensure-sufficient-physical-disk-space-is-available-when-virtual-machines-use-dynamically-expanding-virtual-hard-disks"></a>仮想マシンが容量可変の拡張バーチャルハードディスクを使用する場合に、十分な物理ディスク領域が使用可能であることを確認します。

>適用先:Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*1つ以上の仮想マシンで、動的に拡張される仮想ハードディスクが使用されています。*  
  
## <a name="impact"></a>影響  
容量可変の拡張バーチャルハードディスクを @no__t には、バーチャルハードディスクへの書き込みが発生したときに領域を割り当てることができるように、ホストボリュームに使用可能な領域が必要です。使用可能な領域が不足している場合は、物理記憶域に依存しているすべての仮想マシンが影響を受ける可能性があります。これは、次の仮想マシンに影響します: *  
  
@no__t-仮想マシンの > の一覧  
  
## <a name="resolution"></a>解決方法  
@no__t は、使用可能なディスク領域を監視して、十分な領域を拡張できることを確認します。バーチャルマシンをシャットダウンし、Hyper-v マネージャーのディスクの編集ウィザードを使用して、このバーチャルマシン用に容量可変の拡張バーチャルハードディスクを固定サイズのバーチャルハードディスクに変換することを検討してください。 *  
  


