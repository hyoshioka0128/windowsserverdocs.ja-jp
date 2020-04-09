---
title: バーチャルマシンで差分バーチャルハードディスクを使用する場合は、十分な物理ディスク領域が使用可能であることを確認します。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 71f99aab-f994-4022-9da0-d661965b95ac
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 52e09cfb8695389d2c37def2c39ff43b4091fb76
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861955"
---
# <a name="ensure-sufficient-physical-disk-space-is-available-when-virtual-machines-use-differencing-virtual-hard-disks"></a>バーチャルマシンで差分バーチャルハードディスクを使用する場合は、十分な物理ディスク領域が使用可能であることを確認します。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|［警告］|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*1つ以上のバーチャルマシンで差分バーチャルハードディスクが使用されています。*  
  
## <a name="impact"></a>影響  
*差分仮想ハードディスクでは、仮想ハードディスクへの書き込みが発生したときに領域を割り当てることができるように、ホストボリュームに使用可能な領域が必要です。使用可能な領域が不足している場合は、物理記憶域に依存しているすべての仮想マシンが影響を受ける可能性があります。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
*使用可能なディスク領域を監視して、仮想ハードディスクの拡張に十分な領域があることを確認します。差分仮想ハードディスクをその親にマージすることを検討してください。Hyper-v マネージャーで、差分ディスクを調べて親バーチャルハードディスクを特定します。差分ディスクを他の差分ディスクで共有されている親ディスクにマージすると、その操作によって、他の差分ディスクと親ディスクとの間の関係が破損し、使用できなくなります。親バーチャルハードディスクが共有されていないことを確認したら、ディスクの編集ウィザードを使用して、差分ディスクを親バーチャルハードディスクにマージできます。*  
  


