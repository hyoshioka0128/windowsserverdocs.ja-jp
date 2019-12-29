---
title: 仮想スイッチ上 PVLAN 構成は、一貫性のあるである必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 4db63bcc-7a54-4f19-98a6-c274c3956d51
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 36616a5c4d8e57ae929cdab846db65dcdda57b85
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364752"
---
# <a name="pvlan-configuration-on-a-virtual-switch-must-be-consistent"></a>仮想スイッチ上 PVLAN 構成は、一貫性のあるである必要があります。

>適用先:Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016| 
|**製品/機能**|Hyper-V|  
|**順**|Error|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。
  
## <a name="issue"></a>**問題**  
*1つまたは複数の仮想ネットワークアダプターで、プライベート仮想ローカルエリアネットワーク (PVLAN) が正しく構成されていません。*  
  
## <a name="impact"></a>**よる**  
*PVLAN は、仮想マシン間のネットワークトラフィックを正しく分離できない可能性があります。*  
  
## <a name="resolution"></a>**解決方法**  
*Windows PowerShell コマンドレット Set-vmnetworkadaptervlan を使用して、PVLAN を正しく構成します。*  
  


