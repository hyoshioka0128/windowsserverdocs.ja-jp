---
title: 運用環境でサーバーワークロードを実行する仮想マシンで、VHD 形式の差分仮想ハードディスクを使用しない
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 272de33d-2708-4679-8564-ee28848a2839
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: a11959266db4c9f3da73123c41a211198f27b9a5
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857725"
---
# <a name="avoid-using-vhd-format-differencing-virtual-hard-disks-on-virtual-machines-that-run-server-workloads-in-a-production-environment"></a>運用環境でサーバーワークロードを実行する仮想マシンで、VHD 形式の差分仮想ハードディスクを使用しない

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
*1つまたは複数の仮想マシンで、VHD 形式の差分仮想ハードディスクを使用します。*  
  
## <a name="impact"></a>**よる**  
*VHD 形式の差分仮想ハードディスクでは、電源障害が発生した場合に一貫性の問題が発生する可能性があります。整合性の問題は、物理ディスクが、電源障害が発生したときに変更されている .vhd ファイル内のセクターに対して不完全または不適切な更新を実行すると発生する可能性があります。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>**解決方法**  
*バーチャルマシンをシャットダウンし、VHD 形式の差分バーチャルハードディスクのチェーンを VHDX 形式に変換するか、固定バーチャルハードディスクにチェーンを結合します。(VHDX 形式には、電源障害によりディスクを破損から保護するのに役立つ信頼性機構があります)。ただし、仮想ハードディスクが、ある時点で以前のリリースの Windows に接続されている可能性がある場合は、変換しないでください。Windows Server 2012 より前の windows リリースでは、VHDX 形式はサポートされていません。*  
  


