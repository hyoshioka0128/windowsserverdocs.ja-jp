---
title: 親と子のバーチャルハードディスクが異なるボリュームにある場合に差分バーチャルハードディスクを使用すると、記憶域のサービスの品質を有効にしない
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: aa9ed408-65cf-40dc-aad2-118b54c70179
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 4190b164b473e54c7fcecd68ddf8f746cebcfdc9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857785"
---
# <a name="avoid-enabling-storage-quality-of-service-when-using-a-differencing-virtual-hard-disk-when-the-parent-and-child-virtual-hard-disks-are-on-different-volumes"></a>親と子のバーチャルハードディスクが異なるボリュームにある場合に差分バーチャルハードディスクを使用すると、記憶域のサービスの品質を有効にしない

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|［警告］|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。
  
## <a name="issue"></a>**問題**  
*異なるボリューム上の親および子のバーチャルハードディスクを持つ差分バーチャルハードディスクで、記憶域のサービスの品質が有効になっています。*  
  
## <a name="impact"></a>**よる**  
*この構成では、差分仮想ハードディスクと、親ボリュームおよび子ボリューム上のその他の仮想ハードディスクに、予期しない記憶域のサービス品質の動作が発生する可能性があります。これは、次の仮想ハードディスクに影響します。*  
  
バーチャルハードディスクの一覧を \<>  
  
## <a name="resolution"></a>**解決方法**  
*参照されるバーチャルハードディスク上の記憶域のサービス品質を無効にするか、記憶域の移行を実行して親と子の仮想ハードディスクを同じボリュームに移動してください。*  
  


