---
title: 運用環境でサーバーワークロードを実行する仮想マシンで、VHD 形式の差分仮想ハードディスクを使用しない
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 272de33d-2708-4679-8564-ee28848a2839
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 7b6bee685a72f8f9af2e16ffe7ac5cc1e1f22a4f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366434"
---
# <a name="avoid-using-vhd-format-differencing-virtual-hard-disks-on-virtual-machines-that-run-server-workloads-in-a-production-environment"></a>運用環境でサーバーワークロードを実行する仮想マシンで、VHD 形式の差分仮想ハードディスクを使用しない

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
*1つまたは複数の仮想マシンで、VHD 形式の差分仮想ハードディスクを使用します。*  
  
## <a name="impact"></a>**よる**  
@no__t 0VHD 形式の差分仮想ハードディスクでは、電源障害が発生した場合に一貫性の問題が発生する可能性があります。一貫性の問題は、物理ディスクは、電源障害が発生したときに変更されている .vhd ファイルに不完全または不正確、セクターに更新プログラムを実行する場合に発生することができます。これは、次の仮想マシンに影響します: *  
  
@no__t-仮想マシンの > の一覧  
  
## <a name="resolution"></a>**解決方法**  
*Shut machine をシャットダウンし、VHD 形式の差分バーチャルハードディスクのチェーンを VHDX 形式に変換するか、またはチェーンを固定バーチャルハードディスクにマージします。(VHDX 形式には、電源障害によりディスクを破損から保護するのに役立つ信頼性機構があります)。ただし、変換しないバーチャル ハード ディスクにある時点で Windows の以前のリリースに接続する可能性が高い場合。Windows Server 2012 より前の windows リリースでは、VHDX 形式はサポートされていません。*  
  


