---
title: 1つまたは2つの仮想プロセッサを使用して Windows Vista を実行する仮想マシンを構成する
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: e562bce3-fd68-42c9-821c-12022ae4746c
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: f0fd83122ce148cfa97147a352ebef4f7cc443cf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364933"
---
# <a name="configure-virtual-machines-running-windows-vista-with-1-or-2-virtual-processors"></a>1つまたは2つの仮想プロセッサを使用して Windows Vista を実行する仮想マシンを構成する

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|構成|  
|**カテゴリ**|エラー|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*Windows Vista を実行している仮想マシンは、2つ以上の仮想プロセッサで構成されています。*  
  
## <a name="impact"></a>影響  
  
*Microsoft では、次の仮想マシンの構成をサポートしていません。*  
  
仮想マシン名の \<一覧 >  
  
## <a name="resolution"></a>解決方法  
  
*仮想マシンをシャットダウンし、1つまたは複数の仮想プロセッサを削除します。*  
  
### <a name="to-remove-virtual-processors"></a>仮想プロセッサを削除するには  
  
1.  Hyper-V マネージャーを開きます。 **[スタート]** ボタンをクリックし、 **[管理ツール]** をポイントして **[Hyper-V マネージャー]** をクリックします。  
  
2.  結果ウィンドウで  **仮想マシン**, 、構成する仮想マシンを選択します。 バーチャルマシンの状態は **オフ (オフ**)」と表示されます。 そうでない場合は、バーチャルマシンを右クリックし、 **[シャットダウン]** をクリックします。  
  
3.  **アクション** ウィンドウの 仮想マシン名をクリックして **設定**します。  
  
4.  ナビゲーションウィンドウで、 **[プロセッサ]** をクリックします。  
  
5.  **[プロセッサ]** ページで、プロセッサ数を**1**または**2**に設定し、 **[OK]** をクリックします。  
  


