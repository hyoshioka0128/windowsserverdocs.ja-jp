---
title: 動的仮想ハードディスクまたは差分ディスク上の仮想ブロックと物理ディスクセクター間のアラインメントの不整合を回避する
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a17c8fd2-af81-485b-bfea-bd1ef3e43923
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: f77d80db1e2454eb460043cacef632e979fc16de
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366491"
---
# <a name="avoid-alignment-inconsistencies-between-virtual-blocks-and-physical-disk-sectors-on-dynamic-virtual-hard-disks-or-differencing-disks"></a>動的仮想ハードディスクまたは差分ディスク上の仮想ブロックと物理ディスクセクター間のアラインメントの不整合を回避する

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
*1つまたは複数のバーチャルハードディスクのアラインメントの不整合が検出されました。*  
  
### <a name="impact"></a>影響  
*If サイズが4K の物理ディスクにバーチャルハードディスクが格納されている場合、バーチャルハードディスクを使用するバーチャルマシンまたはアプリケーションでパフォーマンスの問題が発生する可能性があります。これは、次の仮想マシンに影響します:*  
  
@no__t-仮想マシンの > の一覧  
  
## <a name="resolution"></a>解決方法  
@no__t、仮想ハードディスクの作成ウィザードを使用して、新しい VHD 形式または VHDX 形式の仮想ハードディスクを作成し、既存の仮想ハードディスクをソースディスクとして指定します。新しい仮想ハードディスクが作成され、仮想ブロックと物理ディスクが配置されます。 *  
  


