---
title: バーチャルハードディスクファイルが保管されている物理記憶域のセクターサイズよりも小さいセクターサイズのバーチャルハードディスクは使用しないでください。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: b7cf994e-bf4b-4b1b-bad6-ecf7d46d105e
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 944fdce68a2f0b8e9c122f5f9134f0e07de18bbd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366407"
---
# <a name="avoid-using-virtual-hard-disks-with-a-sector-size-less-than-the-sector-size-of-the-physical-storage-that-stores-the-virtual-hard-disk-file"></a>バーチャルハードディスクファイルが保管されている物理記憶域のセクターサイズよりも小さいセクターサイズのバーチャルハードディスクは使用しないでください。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング** <br />**システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|Warning|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*1つまたは複数のバーチャルハードディスクの物理セクターサイズが、バーチャルハードディスクファイルが配置されている記憶域の物理セクターサイズよりも小さくなっています。*  
  
## <a name="impact"></a>**よる**  
*バーチャルハードディスクを使用するバーチャルマシンまたはアプリケーションでパフォーマンスの問題が発生する可能性があります。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>**解決方法**  
*次のいずれかの操作を行います。*  
  
-   *記憶域の移行を実行して、仮想ハードディスクを新しい物理システムに移動する*  
  
-   *Windows PowerShell または WMI を使用して、VHDX 形式の仮想ハードディスクが特定のセクターサイズを報告できるようにする*  
  
-   *レジストリ設定を使用して、VHD 形式のバーチャルハードディスクが4k の物理セクターサイズを報告できるようにします。*  
  


