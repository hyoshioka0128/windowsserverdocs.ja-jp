---
title: Windows Server 2012 R2 を実行し、動的メモリで構成された仮想マシンでは、メモリ設定に推奨値を使用する必要があります。
description: このベストプラクティスアナライザー規則によって報告された問題を解決するための手順を示します。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 3a53c197-80ce-4b33-a83e-7e89e657a519
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 32bc30253bfe1f3a968943f0a19195809e92d65e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366611"
---
# <a name="a-virtual-machine-running-windows-server-2012-r2-and-configured-with-dynamic-memory-should-use-recommended-values-for-memory-settings"></a>Windows Server 2012 R2 を実行し、動的メモリで構成された仮想マシンでは、メモリ設定に推奨値を使用する必要があります。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|Warning|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*1つ以上の仮想マシンが動的メモリを使用するように構成されていますが、Windows Server 2012 R2 で推奨されるメモリ量よりも少なくなっています。*  
  
## <a name="impact"></a>影響  
*次の仮想マシン上のゲストオペレーティングシステムが実行されていないか、または信頼性の高い動作をしていない可能性があります。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
*Hyper-v マネージャーを使用して、最小メモリを 256 MB 以上に増やし、起動メモリを少なくとも 512 MB、最大メモリをこの仮想マシンに対して 2 GB 以上にします。*  
  
#### <a name="increase-memory-using-hyper-v-manager"></a>Hyper-v マネージャーを使用してメモリを増やす  
  
1.  Hyper-V マネージャーを開きます。 (サーバー マネージャーで、クリックして **ツールの** > **Hyper V マネージャー**.)  
  
2.  仮想マシンの一覧から目的のものを右クリックし、 **[設定]** をクリックします。  
  
3.  ナビゲーションウィンドウで、 **[メモリ]** をクリックします。  
  
4.  **RAM**を 512 MB 以上に変更します。  
  
5.  **動的メモリ**で、**最小 RAM**を 256 MB 以上、**最大 ram**を 2 GB に変更します。  
  
6.  **[OK]** をクリックします。  
  
### <a name="increase-memory-using-windows-powershell"></a>Windows PowerShell を使用してメモリを増やす  
  
1.  Windows PowerShell を開きます。 (デスクトップから **[スタート]** をクリックし、「 **Windows PowerShell**」と入力を開始します)。  
  
2.  右クリック **Windows PowerShell**  をクリック **管理者として実行**します。  
  
3.  次のようなコマンドを実行します。 MyVM は仮想マシンの名前に、メモリ値は少なくとも以下の値に置き換えてください。  
  
```  
Get-VM MyVM | Set-VMMemory -DynamicMemoryEnabled $True -MaximumBytes 2GB -MinimumBytes 256MB -StartupBytes 512MB  
```  
  


