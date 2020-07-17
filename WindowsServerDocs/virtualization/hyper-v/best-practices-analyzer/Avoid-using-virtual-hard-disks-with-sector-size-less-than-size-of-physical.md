---
title: バーチャルハードディスクファイルが保管されている物理記憶域のセクターサイズよりも小さいセクターサイズのバーチャルハードディスクは使用しないでください。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: b7cf994e-bf4b-4b1b-bad6-ecf7d46d105e
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: f7ea02ab83d3d896d2ad3681526133e23725b819
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857705"
---
# <a name="avoid-using-virtual-hard-disks-with-a-sector-size-less-than-the-sector-size-of-the-physical-storage-that-stores-the-virtual-hard-disk-file"></a>バーチャルハードディスクファイルが保管されている物理記憶域のセクターサイズよりも小さいセクターサイズのバーチャルハードディスクは使用しないでください。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング** <br />**System**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|［警告］|  
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
  


