---
title: Windows 7 を実行して、動的メモリで構成されているバーチャル マシンは、メモリの設定の推奨値を使用する必要があります。
description: このベスト プラクティス アナライザー ルールによって報告された問題を解決する方法を説明します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: c3a0292a-a619-4d1c-8f9d-391c741411c1
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: d252f314db0e068a06c9f6dfb050747a160576f1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59885013"
---
# <a name="a-virtual-machine-running-windows-7-and-configured-with-dynamic-memory-should-use-recommended-values-for-memory-settings"></a>Windows 7 を実行して、動的メモリで構成されているバーチャル マシンは、メモリの設定の推奨値を使用する必要があります。

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
*Windows 7 の推奨されるメモリの量よりも少ないリソースで動的メモリを使用する 1 つまたは複数の仮想マシンが構成されます。*  
  
### <a name="impact"></a>影響  
*次の仮想マシンのゲスト オペレーティング システムは実行されない可能性または含んで実行可能性があります。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*256 MB 以上の最小メモリと、起動メモリと、少なくとも 512 MB の最大メモリ量を増やすには、HYPER-V マネージャーまたは Windows PowerShell を使用します。*  
  
#### <a name="increase-memory-using-hyper-v-manager"></a>HYPER-V マネージャーを使用してメモリを増やす  
  
1.  Hyper-V マネージャーを開きます。 (サーバー マネージャーで、クリックして **ツールの** > **Hyper V マネージャー**.)  
  
2.  選択し、クリックして 1 つを右クリックし、仮想マシンの一覧から**設定**します。  
  
3.  ナビゲーション ウィンドウで、**メモリ**します。  
  
4.  変更、 **RAM**少なくとも 512 MB にします。  
  
5.  **動的メモリ**、変更、**最小 RAM** 256 MB 以上に、**最大 ram 容量**を 512 MB  
  
6.  **[OK]** をクリックします。  
  
### <a name="increase-memory-using-windows-powershell"></a>Windows PowerShell を使用してメモリを増やす  
  
1.  Windows PowerShell を開きます。 (デスクトップで、次のようにクリックします**開始**の入力を開始および**Windows PowerShell**。)。  
  
2.  右クリック **Windows PowerShell**  をクリック **管理者として実行**します。  
  
3.  次のようなコマンドを実行して、少なくとも以下の値ので値 MyVM を仮想マシンと、メモリの名前に置き換えます。  
  
```  
Get-VM MyVM | Set-VMMemory -DynamicMemoryEnabled $True -MaximumBytes 512MB -MinimumBytes 256MB -StartupBytes 512MB  
```  
  


