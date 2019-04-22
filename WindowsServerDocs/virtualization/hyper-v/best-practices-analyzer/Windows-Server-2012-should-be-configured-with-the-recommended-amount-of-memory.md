---
title: Windows Server 2012 には推奨されるメモリ量を構成します。
description: このベスト プラクティス アナライザー ルールによって報告された問題を解決する方法を説明します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 12d0b473-cf6a-4746-b03d-2ceeb701c5d0
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 601682917e242b747d6ed8b9922372aca234cfd9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825803"
---
# <a name="windows-server-2012-should-be-configured-with-the-recommended-amount-of-memory"></a>Windows Server 2012 には推奨されるメモリ量を構成します。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|   
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*Windows Server 2012 を実行する仮想マシンは、2 gb の RAM の推奨される量よりも少ないリソースで構成されます。*  
  
## <a name="impact"></a>**影響**  
*ゲスト オペレーティング システムとアプリケーションをも実行しない可能性があります。メモリ不足のため、一度に複数のアプリケーションを実行できない可能性があります。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>**解決方法**  
*HYPER-V マネージャーを使用して、この仮想マシンに少なくとも 2 GB に割り当てられたメモリを増やします。*  
  
### <a name="increase-the-memory-using-hyper-v-manager"></a>HYPER-V マネージャーを使用してメモリを増やす  
  
1.  Hyper-V マネージャーを開きます。 **[スタート]** ボタンをクリックし、**[管理ツール]** をポイントして **[Hyper-V マネージャー]** をクリックします。  
  
2.  結果ウィンドウで  **仮想マシン**, 、構成する仮想マシンを選択します。 仮想マシンの状態として表示されるはず**オフ**します。 そうでない場合は、仮想マシンを右クリックし、順にクリックします**シャット ダウン**します。  
  
3.  **アクション** ウィンドウの 仮想マシン名をクリックして **設定**します。  
  
4.  ナビゲーション ウィンドウで、**メモリ**します。  
  
5.  **メモリ** ページで、設定、**スタートアップ RAM**に少なくとも 2 GB を順にクリックします**OK**。  
  
### <a name="increase-the-memory-using-windows-powershell"></a>Windows PowerShell を使用してメモリを増やす  
  
1.  Windows PowerShell を開きます。 (デスクトップで、次のようにクリックします**開始**の入力を開始および**Windows PowerShell**。)。  
  
2.  右クリック **Windows PowerShell**  をクリック **管理者として実行**します。  
  
3.  交換した後、次のコマンドを実行\<MyVM > 仮想マシンの名前に置き換えます。  
  
```  
Set-VMMemory <MyVM> -StartupBytes 2GB  
```  
  
## <a name="see-also"></a>関連項目  
[Set-vmmemory](https://technet.microsoft.com/library/hh848572.aspx)  
  


