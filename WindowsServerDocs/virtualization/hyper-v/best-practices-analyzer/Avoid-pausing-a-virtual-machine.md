---
title: 仮想マシンを一時停止しないように
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 930f927c-e414-4a36-9786-028941e886e4
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 4492ac385a289d075ebcd48b1c7c1c78c1af2f8c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814353"
---
# <a name="avoid-pausing-a-virtual-machine"></a>仮想マシンを一時停止しないように

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
  
*このサーバーは、1 つまたは複数の仮想マシンを一時停止状態にします。*  
  
## <a name="impact"></a>影響  
  
*使用可能なメモリの量、によっては、追加の仮想マシンを実行できない可能性があります。*  
  
一時停止中の仮想マシンは、割り当てられたメモリを解放しないので、そのメモリを使用できないその他の仮想マシンを起動します。  
  
## <a name="resolution"></a>解決方法  
  
*これが意図的な場合は、これ以上の操作は必要ありません。それ以外の場合、これらの仮想マシンを再開するか、シャット ダウンを検討してください。*  
  
#### <a name="use-hyper-v-manager-to-resume-the-virtual-machine"></a>HYPER-V マネージャーを使用して、仮想マシンを再開するには  
  
1.  Hyper-V マネージャーを開きます。 (から、**ツール**サーバー マネージャーのメニューのをクリックして **、HYPER-V Manager**)。  
  
2.  **仮想マシン**一覧で、仮想マシンの状態を見つける**Paused**します。  
  
    > [!IMPORTANT]  
    > 状態**Paused クリティカル**その仮想マシンに対する物理ストレージに残っているほとんどの空き領域があるときに発生します。 この状態で仮想マシンを再開する前に、物理記憶域の空き領域を解放します。  
  
3.  各仮想マシン名を右クリックし、をクリックして**再開**します。 実行中の状態に仮想マシンが返されます。 その後、仮想マシンをシャット ダウンする場合は、再び右クリックし、選択**シャット ダウン**します。  
  
#### <a name="use-windows-powershell-to-resume-the-virtual-machine"></a>Windows PowerShell を使用して、仮想マシンを再開するには  
  
これを行う 1 つのコマンドでフィルタ リングを使用しした後、パイプラインが、ホスト上のすべての仮想マシンを取得します。 タイプ:   
  
```  
get-vm | where state -eq 'paused' | resume-vm  
```  
  


