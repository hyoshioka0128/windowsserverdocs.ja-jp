---
title: 仮想マシンが動的に拡張されるバーチャル ハード_ディスクを使用するとき、十分な物理ディスクの空き領域があることを確認します。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 9e3e3e64-4b3a-4b9d-acf1-e4df61a04f1e
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 09e481b99594ac543dadab2b60bf9b3f4c29e54b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883293"
---
# <a name="ensure-sufficient-physical-disk-space-is-available-when-virtual-machines-use-dynamically-expanding-virtual-hard-disks"></a>仮想マシンが動的に拡張されるバーチャル ハード_ディスクを使用するとき、十分な物理ディスクの空き領域があることを確認します。

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
*1 つまたは複数の仮想マシンでは、可変の拡張バーチャル ハード_ディスクを使用しています。*  
  
## <a name="impact"></a>影響  
*可変の仮想ハード_ディスクでは、仮想ハード ディスクへの書き込みが発生すると、領域を割り当てることができるようにホスト ボリュームの空き領域が必要です。使用可能な領域がなくなった場合は、物理記憶域に依存している任意の仮想マシンが影響を受ける可能性があります。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*モニターの使用可能なディスク領域を十分な領域を確認しますが、拡張に使用できます。仮想マシンをシャット ダウンを検討してくださいし、HYPER-V マネージャーでディスクの編集ウィザードを使用して各は、この仮想マシンの容量可変の拡張バーチャル ハード ディスクを固定サイズ バーチャル ハード ディスクに変換します。*  
  


