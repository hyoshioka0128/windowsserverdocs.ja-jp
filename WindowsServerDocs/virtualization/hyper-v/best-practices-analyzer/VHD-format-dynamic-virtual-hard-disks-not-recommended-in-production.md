---
title: VHD 形式の動的な仮想ハード ディスクは、運用環境でサーバーのワークロードを実行する仮想マシンには推奨されません。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 324a60a0-1d15-4ef2-9f17-23cbd2eb42ce
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: bf5464208fc145a31571f01822bb5ba54efe89c4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364590"
---
# <a name="vhd-format-dynamic-virtual-hard-disks-are-not-recommended-for-virtual-machines-that-run-server-workloads-in-a-production-environment"></a>VHD 形式の動的な仮想ハード ディスクは、運用環境でサーバーのワークロードを実行する仮想マシンには推奨されません。

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
*1つまたは複数の仮想マシンで、VHD 形式の動的な拡張バーチャルハードディスクを使用します。*  
  
## <a name="impact"></a>**よる**  
*VHD 形式の動的な仮想ハードディスクは、電源障害が発生した場合に一貫性の問題が発生する可能性があります。一貫性の問題は、物理ディスクは、電源障害が発生したときに変更されている .vhd ファイルに不完全または不正確、セクターに更新プログラムを実行する場合に発生することができます。これは、次の仮想マシンに影響します:*  
  
@no__t-仮想マシンの > の一覧  
  
## <a name="resolution"></a>**解決方法**  
*Shut machine をシャットダウンし、VHD 形式の動的バーチャルハードディスクを VHDX 形式のバーチャルハードディスクまたは容量固定のバーチャルハードディスクに変換します。(VHDX 形式とは、システム電源障害による破損からディスクを保護するための信頼性メカニズムのことです)。ただし、変換しないバーチャル ハード ディスクにある時点で Windows の以前のリリースに接続する可能性が高い場合。Windows Server 2012 より前の windows リリースでは、VHDX 形式はサポートされていません。*  
  


