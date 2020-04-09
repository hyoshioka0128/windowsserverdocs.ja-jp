---
title: 仮想スイッチ上 PVLAN 構成は、一貫性のあるである必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 4db63bcc-7a54-4f19-98a6-c274c3956d51
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 7e42c874e883157b3f85f523511b950e2863b155
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861855"
---
# <a name="pvlan-configuration-on-a-virtual-switch-must-be-consistent"></a>仮想スイッチ上 PVLAN 構成は、一貫性のあるである必要があります。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016| 
|**製品/機能**|Hyper-V|  
|**順**|エラー|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。
  
## <a name="issue"></a>**問題**  
*1つまたは複数の仮想ネットワークアダプターで、プライベート仮想ローカルエリアネットワーク (PVLAN) が正しく構成されていません。*  
  
## <a name="impact"></a>**よる**  
*PVLAN は、仮想マシン間のネットワークトラフィックを正しく分離できない可能性があります。*  
  
## <a name="resolution"></a>**解決方法**  
*Windows PowerShell コマンドレット Set-vmnetworkadaptervlan を使用して、PVLAN を正しく構成します。*  
  


