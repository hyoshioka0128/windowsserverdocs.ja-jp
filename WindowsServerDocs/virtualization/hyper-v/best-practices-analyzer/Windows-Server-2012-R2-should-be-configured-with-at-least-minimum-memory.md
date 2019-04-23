---
title: Windows Server 2012 R2 をする必要があります最小メモリ量以上で構成
description: このベスト プラクティス アナライザー ルールによって報告された問題を解決する方法を説明します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 01da6f02-1a5f-4d3e-9bef-4d122a91c5c2
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 5fcb2ef718f9722cc4d2912b54c281b381eeeeb0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856223"
---
# <a name="windows-server-2012-r2-should-be-configured-with-at-least-the-minimum-amount-of-memory"></a>Windows Server 2012 R2 をする必要があります最小メモリ量以上で構成

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|エラー|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*Windows Server 2012 R2 を実行する仮想マシンは、512 mb の RAM の最小量よりも少ないリソースで構成されます。*  
  
## <a name="impact"></a>**影響**  
*次の仮想マシンのゲスト オペレーティング システムは実行されない可能性または含んで実行可能性があります。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>**解決方法**  
*HYPER-V マネージャーを使用して、少なくとも 512 MB には、この仮想マシンに割り当てられたメモリを増やします。*  
  
### <a name="increase-the-memory-using-hyper-v-manager"></a>HYPER-V マネージャーを使用してメモリを増やす  
  
1.  Hyper-V マネージャーを開きます。 **[スタート]** ボタンをクリックし、**[管理ツール]** をポイントして **[Hyper-V マネージャー]** をクリックします。  
  
2.  結果ウィンドウで  **仮想マシン**, 、構成する仮想マシンを選択します。 仮想マシンの状態として表示されるはず**オフ**します。 そうでない場合は、仮想マシンを右クリックし、順にクリックします**シャット ダウン**します。  
  
3.  **アクション** ウィンドウの 仮想マシン名をクリックして **設定**します。  
  
4.  ナビゲーション ウィンドウで、**メモリ**します。  
  
5.  **メモリ** ページで、設定、**スタートアップ RAM**少なくとも 512 MB をクリックして**ok**します。  
  
### <a name="increase-the-memory-using-windows-powershell"></a>Windows PowerShell を使用してメモリを増やす  
  
1.  Windows PowerShell を開きます。 (デスクトップで、次のようにクリックします**開始**の入力を開始および**Windows PowerShell**。)。  
  
2.  右クリック **Windows PowerShell**  をクリック **管理者として実行**します。  
  
3.  交換した後、次のコマンドを実行\<MyVM > 仮想マシンの名前に置き換えます。  
  
```  
Set-VMMemory <MyVM> -StartupBytes 512MB  
```  
  
## <a name="see-also"></a>関連項目  
[Set-vmmemory](https://technet.microsoft.com/library/hh848572.aspx)  
  


