---
title: 以上の Windows Server 2008 R2 を実行し、動的メモリを有効には、仮想マシンのメモリ必要量を構成します。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: db0bff4c-39fe-49c1-903a-1f2a0b0db891
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 1d1815a0f1a886362bda5a09eefc5e6f8a687f80
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860973"
---
# <a name="configure-at-least-the-required-amount-of-memory-for-a-virtual-machine-running-windows-server-2008-r2-and-enabled-for-dynamic-memory"></a>以上の Windows Server 2008 R2 を実行し、動的メモリを有効には、仮想マシンのメモリ必要量を構成します。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|エラー|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*Windows Server 2008 R2 に必要なメモリの量よりも少ないリソースで動的メモリを使用する 1 つまたは複数の仮想マシンが構成されます。*  
  
## <a name="impact"></a>影響  
*次の仮想マシンのゲスト オペレーティング システムは実行されない可能性または含んで実行可能性があります。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*256 MB 以上の最小メモリと、起動メモリと、少なくとも 512 MB の最大メモリ量を増やすには、HYPER-V マネージャーまたは Windows PowerShell を使用します。*  
  
### <a name="increase-memory-using-hyper-v-manager"></a>HYPER-V マネージャーを使用してメモリを増やす  
  
1.  Hyper-V マネージャーを開きます。 (サーバー マネージャーで、クリックして **ツールの** > **Hyper V マネージャー**.)  
  
2.  選択し、クリックして 1 つを右クリックし、仮想マシンの一覧から**設定**します。  
  
3.  ナビゲーション ウィンドウで、**メモリ**します。  
  
4.  変更、 **RAM**少なくとも 512 MB にします。  
  
5.  **動的メモリ**、変更、**最小 RAM** 256 MB 以上に、**最大 ram 容量**512 MB にします。  
  
6.  **[OK]** をクリックします。  
  
### <a name="increase-memory-using-windows-powershell"></a>Windows PowerShell を使用してメモリを増やす  
  
1.  Windows PowerShell を開きます。 (デスクトップで、次のようにクリックします**開始**の入力を開始および**Windows PowerShell**。)。  
  
2.  右クリック **Windows PowerShell**  をクリック **管理者として実行**します。  
  
3.  次のようなコマンドを実行して、少なくとも以下の値ので値 MyVM を仮想マシンと、メモリの名前に置き換えます。  
  
```  
Get-VM MyVM | Set-VMMemory -DynamicMemoryEnabled $True -MaximumBytes 512MB -MinimumBytes 256MB -StartupBytes 512MB  
```  
  


