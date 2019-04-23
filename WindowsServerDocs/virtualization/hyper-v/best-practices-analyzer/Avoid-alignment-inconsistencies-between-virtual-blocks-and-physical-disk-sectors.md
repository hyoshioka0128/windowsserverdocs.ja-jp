---
title: 仮想のブロックと動的な仮想ハード_ディスクまたは差分ディスク上の物理ディスクのセクターの間での配置の不整合を回避します。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a17c8fd2-af81-485b-bfea-bd1ef3e43923
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 4973c199a5507d00e15da8f621a09f0c602a29fa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833863"
---
# <a name="avoid-alignment-inconsistencies-between-virtual-blocks-and-physical-disk-sectors-on-dynamic-virtual-hard-disks-or-differencing-disks"></a>仮想のブロックと動的な仮想ハード_ディスクまたは差分ディスク上の物理ディスクのセクターの間での配置の不整合を回避します。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*1 つまたは複数の仮想ハード_ディスクの配置の不整合が検出されました。*  
  
### <a name="impact"></a>影響  
*仮想ハード_ディスクが格納されている場合、セクター サイズが 4 K、仮想マシンまたはバーチャル ハード_ディスクを使用するアプリケーションの物理ディスク パフォーマンスの問題が発生する可能性があります。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*仮想ハード_ディスクの作成ウィザードを使用して、新しい VHD 形式または VHDX 形式の仮想ハード_ディスクを作成し、ソース ディスクと既存のバーチャル ハード_ディスクを指定します。新しい仮想ハード_ディスクが仮想のブロックと物理ディスクの配置で作成されます。*  
  


