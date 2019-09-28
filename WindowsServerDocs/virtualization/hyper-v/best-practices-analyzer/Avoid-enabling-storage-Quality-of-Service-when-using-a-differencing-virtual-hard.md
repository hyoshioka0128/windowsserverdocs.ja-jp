---
title: 親と子のバーチャルハードディスクが異なるボリュームにある場合に差分バーチャルハードディスクを使用すると、記憶域のサービスの品質を有効にしない
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: aa9ed408-65cf-40dc-aad2-118b54c70179
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 716a32de2f9327e5eca38c470fa1b7c44150e9cb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366441"
---
# <a name="avoid-enabling-storage-quality-of-service-when-using-a-differencing-virtual-hard-disk-when-the-parent-and-child-virtual-hard-disks-are-on-different-volumes"></a>親と子のバーチャルハードディスクが異なるボリュームにある場合に差分バーチャルハードディスクを使用すると、記憶域のサービスの品質を有効にしない

>適用先:Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。
  
## <a name="issue"></a>**問題**  
*異なるボリューム上の親および子のバーチャルハードディスクを持つ差分バーチャルハードディスクで、記憶域のサービスの品質が有効になっています。*  
  
## <a name="impact"></a>**よる**  
@no__t この構成では、差分仮想ハードディスクと、親ボリュームおよび子ボリュームの他の仮想ハードディスクに、予期しない記憶域のサービス品質の動作が発生する可能性があります。これは、次のバーチャルハードディスクに影響します: *  
  
@no__t-仮想ハードディスクの一覧 >  
  
## <a name="resolution"></a>**解決方法**  
*参照されるバーチャルハードディスク上の記憶域のサービス品質を無効にするか、記憶域の移行を実行して親と子の仮想ハードディスクを同じボリュームに移動してください。*  
  


