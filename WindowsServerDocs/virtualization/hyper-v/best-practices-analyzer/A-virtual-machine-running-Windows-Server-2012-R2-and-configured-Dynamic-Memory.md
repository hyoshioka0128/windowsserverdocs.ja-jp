---
title: Windows Server 2012 R2 を実行していると、動的メモリで構成されているバーチャル マシンは、メモリの設定の推奨値を使用する必要があります。
description: このベスト プラクティス アナライザー ルールによって報告された問題を解決する方法を説明します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 3a53c197-80ce-4b33-a83e-7e89e657a519
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 9ea9b1c2ae377b39a93e332ea1d403388769b2fd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890163"
---
# <a name="a-virtual-machine-running-windows-server-2012-r2-and-configured-with-dynamic-memory-should-use-recommended-values-for-memory-settings"></a>Windows Server 2012 R2 を実行していると、動的メモリで構成されているバーチャル マシンは、メモリの設定の推奨値を使用する必要があります。

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
*Windows Server 2012 R2 の推奨されるメモリの量よりも少ないリソースで動的メモリを使用する 1 つまたは複数の仮想マシンが構成されます。*  
  
## <a name="impact"></a>影響  
*次の仮想マシンのゲスト オペレーティング システムは実行されない可能性または含んで実行可能性があります。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*HYPER-V マネージャーを使用して、256 MB 以上、512 MB 以上に起動メモリと最大メモリ量をこの仮想マシンの少なくとも 2 GB に最低限のメモリを増やします。*  
  
#### <a name="increase-memory-using-hyper-v-manager"></a>HYPER-V マネージャーを使用してメモリを増やす  
  
1.  Hyper-V マネージャーを開きます。 (サーバー マネージャーで、クリックして **ツールの** > **Hyper V マネージャー**.)  
  
2.  選択し、クリックして 1 つを右クリックし、仮想マシンの一覧から**設定**します。  
  
3.  ナビゲーション ウィンドウで、**メモリ**します。  
  
4.  変更、 **RAM**少なくとも 512 MB にします。  
  
5.  **動的メモリ**、変更、**最小 RAM** 256 MB 以上に、**最大 ram 容量**2 GB にします。  
  
6.  **[OK]** をクリックします。  
  
### <a name="increase-memory-using-windows-powershell"></a>Windows PowerShell を使用してメモリを増やす  
  
1.  Windows PowerShell を開きます。 (デスクトップで、次のようにクリックします**開始**の入力を開始および**Windows PowerShell**。)。  
  
2.  右クリック **Windows PowerShell**  をクリック **管理者として実行**します。  
  
3.  次のようなコマンドを実行して、少なくとも以下の値ので値 MyVM を仮想マシンと、メモリの名前に置き換えます。  
  
```  
Get-VM MyVM | Set-VMMemory -DynamicMemoryEnabled $True -MaximumBytes 2GB -MinimumBytes 256MB -StartupBytes 512MB  
```  
  


