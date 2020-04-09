---
title: VHD 形式の動的な仮想ハード ディスクは、運用環境でサーバーのワークロードを実行する仮想マシンには推奨されません。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 324a60a0-1d15-4ef2-9f17-23cbd2eb42ce
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 195bc4c85d380c8f0b15b27d042b30491f635d5d
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854175"
---
# <a name="vhd-format-dynamic-virtual-hard-disks-are-not-recommended-for-virtual-machines-that-run-server-workloads-in-a-production-environment"></a>VHD 形式の動的な仮想ハード ディスクは、運用環境でサーバーのワークロードを実行する仮想マシンには推奨されません。

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
*1つまたは複数の仮想マシンで、VHD 形式の動的な拡張バーチャルハードディスクを使用します。*  
  
## <a name="impact"></a>**よる**  
*VHD 形式の動的な仮想ハードディスクでは、電源障害が発生した場合に一貫性の問題が発生する可能性があります。整合性の問題は、物理ディスクが、電源障害が発生したときに変更されている .vhd ファイル内のセクターに対して不完全または不適切な更新を実行すると発生する可能性があります。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>**解決方法**  
*仮想マシンをシャットダウンし、VHD 形式の動的仮想ハードディスクを VHDX 形式の仮想ハードディスクまたは容量固定の仮想ハードディスクに変換します。(VHDX 形式には、システム電源障害によりディスクを破損から保護するのに役立つ信頼性機構があります)。ただし、仮想ハードディスクが、ある時点で以前のリリースの Windows に接続されている可能性がある場合は、変換しないでください。Windows Server 2012 より前の windows リリースでは、VHDX 形式はサポートされていません。*  
  


