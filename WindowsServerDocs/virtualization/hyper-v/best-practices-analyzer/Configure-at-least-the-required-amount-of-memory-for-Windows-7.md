---
title: Windows 7 を実行し、動的メモリに対して有効になっている仮想マシンに対して、少なくとも必要なメモリ容量を構成します。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 119965bf-6154-414d-b3a1-aa5b30eac5f6
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: f0865866c3494a0b3719f49f3dd85e85fb48c4e9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365088"
---
# <a name="configure-at-least-the-required-amount-of-memory-for-a-virtual-machine-running-windows-7-and-enabled-for-dynamic-memory"></a>Windows 7 を実行し、動的メモリに対して有効になっている仮想マシンに対して、少なくとも必要なメモリ容量を構成します。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|エラー|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*1つ以上の仮想マシンが、Windows 7 で必要とされるメモリ量よりも少ない動的メモリを使用するように構成されています。*  
  
## <a name="impact"></a>影響  
*次の仮想マシン上のゲストオペレーティングシステムが実行されていないか、または信頼性の高い動作をしていない可能性があります。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
*Hyper-v マネージャーまたは Windows PowerShell を使用して、最小メモリを 256 MB 以上、起動メモリと最大メモリを 512 MB 以上に増やします。*  
  
### <a name="increase-memory-using-hyper-v-manager"></a>Hyper-v マネージャーを使用してメモリを増やす  
  
1.  Hyper-V マネージャーを開きます。 (サーバー マネージャーで、クリックして **ツールの** > **Hyper V マネージャー**.)  
  
2.  仮想マシンの一覧から目的のものを右クリックし、 **[設定]** をクリックします。  
  
3.  ナビゲーションウィンドウで、 **[メモリ]** をクリックします。  
  
4.  **RAM**を 512 MB 以上に変更します。  
  
5.  **動的メモリ**で、**最小 RAM**を 256 mb 以上、 **ram の最大値**を 512 mb に変更します。  
  
6.  **[OK]** をクリックします。  
  
### <a name="increase-memory-using-windows-powershell"></a>Windows PowerShell を使用してメモリを増やす  
  
1.  Windows PowerShell を開きます。 (デスクトップから **[スタート]** をクリックし、「 **Windows PowerShell**」と入力を開始します)。  
  
2.  右クリック **Windows PowerShell**  をクリック **管理者として実行**します。  
  
3.  次のようなコマンドを実行します。 MyVM は仮想マシンの名前に、メモリ値は少なくとも以下の値に置き換えてください。  
  
```  
Get-VM MyVM | Set-VMMemory -DynamicMemoryEnabled $True -MaximumBytes 512MB -MinimumBytes 256MB -StartupBytes 512MB  
```  
  


