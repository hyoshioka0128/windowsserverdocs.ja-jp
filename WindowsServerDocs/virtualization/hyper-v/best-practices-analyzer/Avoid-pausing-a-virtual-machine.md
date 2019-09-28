---
title: 仮想マシンの一時停止を避ける
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 930f927c-e414-4a36-9786-028941e886e4
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 406b24edd4a7e87e32058006590ac7cd37206568
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366450"
---
# <a name="avoid-pausing-a-virtual-machine"></a>仮想マシンの一時停止を避ける

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
  
*このサーバーには、一時停止状態の仮想マシンが1つ以上あります。*  
  
## <a name="impact"></a>影響  
  
*使用可能なメモリの量によっては、追加の仮想マシンを実行できない場合があります。*  
  
一時停止した仮想マシンは、割り当てられたメモリを解放しません。つまり、他の仮想マシンを起動するためにメモリが使用できないことを意味します。  
  
## <a name="resolution"></a>解決方法  
  
*これが意図的なものである場合は、それ以上の操作は必要ありません。それ以外の場合は、これらの仮想マシンを再開するか、シャットダウンすることを検討してください。*  
  
#### <a name="use-hyper-v-manager-to-resume-the-virtual-machine"></a>Hyper-v マネージャーを使用して仮想マシンを再開する  
  
1.  Hyper-V マネージャーを開きます。 (サーバーマネージャーの **[ツール]** メニューの **[hyper-v マネージャー]** をクリックします)。  
  
2.  **[Virtual Machines]** ボックスの一覧から、状態が **[一時停止]** になっている仮想マシンを見つけます。  
  
    > [!IMPORTANT]  
    > "**一時停止-重大**" の状態は、その仮想マシンの物理記憶域に残っている空き領域がほとんどない場合に発生します。 この状態でバーチャルマシンを再開する前に、物理記憶域の空き領域を解放してください。  
  
3.  各仮想マシン名を右クリックし、 **[再開]** をクリックします。 これにより、仮想マシンが実行中の状態に戻ります。 その後、仮想マシンをシャットダウンする場合は、仮想マシンをもう一度右クリックし、 **[シャットダウン]** を選択します。  
  
#### <a name="use-windows-powershell-to-resume-the-virtual-machine"></a>Windows PowerShell を使用して仮想マシンを再開する  
  
この操作は、ホスト上のすべての仮想マシンを取得した後、フィルターとパイプラインを使用して1つのコマンドで実行できます。 型:  
  
```  
get-vm | where state -eq 'paused' | resume-vm  
```  
  


