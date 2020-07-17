---
title: 動的仮想ハードディスクまたは差分ディスク上の仮想ブロックと物理ディスクセクター間のアラインメントの不整合を回避する
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a17c8fd2-af81-485b-bfea-bd1ef3e43923
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 3f090f015f2179ba372e56d580477ef8d72d977f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857805"
---
# <a name="avoid-alignment-inconsistencies-between-virtual-blocks-and-physical-disk-sectors-on-dynamic-virtual-hard-disks-or-differencing-disks"></a>動的仮想ハードディスクまたは差分ディスク上の仮想ブロックと物理ディスクセクター間のアラインメントの不整合を回避する

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
*1つまたは複数のバーチャルハードディスクのアラインメントの不整合が検出されました。*  
  
### <a name="impact"></a>影響  
*バーチャルハードディスクがセクターサイズ4K の物理ディスクに格納されている場合、バーチャルハードディスクを使用するバーチャルマシンまたはアプリケーションでパフォーマンスの問題が発生する可能性があります。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
*バーチャルハードディスクの作成ウィザードを使用して、新しい VHD 形式または VHDX 形式のバーチャルハードディスクを作成し、既存のバーチャルハードディスクをソースディスクとして指定します。新しい仮想ハードディスクは、仮想ブロックと物理ディスクの間に配置されます。*  
  


