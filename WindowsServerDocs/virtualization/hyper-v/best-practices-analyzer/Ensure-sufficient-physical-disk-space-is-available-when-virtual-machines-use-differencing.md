---
title: 差分仮想ハード_ディスクを使用して、仮想マシンと、十分な物理ディスクの空き領域があることを確認します。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 71f99aab-f994-4022-9da0-d661965b95ac
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 6d4d219402cdc321a75cc27d75ea7749eb6127e0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855573"
---
# <a name="ensure-sufficient-physical-disk-space-is-available-when-virtual-machines-use-differencing-virtual-hard-disks"></a>差分仮想ハード_ディスクを使用して、仮想マシンと、十分な物理ディスクの空き領域があることを確認します。

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
*1 つまたは複数の仮想マシンでは、差分仮想ハード_ディスクを使用しています。*  
  
## <a name="impact"></a>影響  
*差分仮想ハード_ディスクでは、仮想ハード ディスクへの書き込みが発生すると、領域を割り当てることができるようにホスト ボリュームの空き領域が必要です。使用可能な領域がなくなった場合は、物理記憶域に依存している任意の仮想マシンが影響を受ける可能性があります。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*仮想ハード ディスクの拡張に十分な空き領域があることを確認する使用可能なディスク領域を監視します。親の差分仮想ハード_ディスクをマージすることを検討してください。HYPER-V マネージャーでは、親バーチャル ハード_ディスクを決定する差分ディスクを検査します。その他の差分ディスクによって共有されている親ディスクに差分ディスクをマージする場合、そのアクションには、その他の差分ディスクと使用できないように、親ディスク間のリレーションシップが破損します。親バーチャル ハード_ディスクが共有されていないことを確認した後、差分ディスクを親バーチャル ハード_ディスクをマージするのにディスクの編集ウィザードを使用することができます。*  
  


