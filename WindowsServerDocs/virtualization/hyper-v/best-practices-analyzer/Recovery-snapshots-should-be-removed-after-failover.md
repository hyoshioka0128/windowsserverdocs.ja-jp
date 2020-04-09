---
title: フェールオーバー後に回復スナップショットを削除する必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 922115fa-e8dd-4055-aaf1-4a4437c5cf28
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: c995293ca67b4cad0837affa854fb4ac366856e1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861845"
---
# <a name="recovery-snapshots-should-be-removed-after-failover"></a>フェールオーバー後に回復スナップショットを削除する必要があります。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016| 
|**製品/機能**|Hyper-V|  
|**順**|［警告］|  
|**カテゴリ**|運用|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*フェールオーバーされた仮想マシンには、1つまたは複数の回復スナップショットがあります。*  
  
## <a name="impact"></a>**よる**  
*使用可能な領域は、スナップショットファイルが格納されている物理ディスク上で実行される可能性があります。これが発生した場合は、物理記憶域に対して追加のディスク操作を実行することはできません。物理記憶域に依存しているすべての仮想マシンが影響を受ける可能性があります。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>**解決方法**  
*フェールオーバーされた仮想マシンごとに、Windows PowerShell の Start-vmfailover コマンドレットを使用して、回復スナップショットを削除し、フェールオーバーの完了を示します。*  
  


