---
title: Windows Server 2008 は、推奨されるメモリ量を構成する必要があります。
description: このベスト プラクティス アナライザー ルールによって報告された問題を解決する方法を説明します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a98a8594-603b-487a-8739-78887c568e57
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 77410eb545c8c8ce6b02d083c7c875b569c63937
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818793"
---
# <a name="windows-server-2008-should-be-configured-with-the-recommended-amount-of-memory"></a>Windows Server 2008 は、推奨されるメモリ量を構成する必要があります。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、「 [ベスト プラクティス アナライザー](https://go.microsoft.com/fwlink/?LinkId=122786)」をご覧ください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*Windows Server 2008 を実行する仮想マシンは、2 gb の RAM の推奨される量よりも少ないリソースで構成されます。*  
  
## <a name="impact"></a>影響  
  
*ゲスト オペレーティング システムとアプリケーションをも実行しない可能性があります。メモリ不足のため、一度に複数のアプリケーションを実行できない可能性があります。これには、次の仮想マシンに影響します。*  
   
\<仮想マシン名の一覧 >  
  
## <a name="resolution"></a>解決方法  
  
*HYPER-V マネージャーを使用して、この仮想マシンに少なくとも 2 GB に割り当てられたメモリを増やします。*  
  
### <a name="increase-the-memory-using-hyper-v-manager"></a>HYPER-V マネージャーを使用してメモリを増やす  
  
1.  Hyper-V マネージャーを開きます。 **[スタート]** ボタンをクリックし、**[管理ツール]** をポイントして **[Hyper-V マネージャー]** をクリックします。  
  
2.  結果ウィンドウで  **仮想マシン**, 、構成する仮想マシンを選択します。 仮想マシンの状態として表示されるはず**オフ**します。 そうでない場合は、仮想マシンを右クリックし、順にクリックします**シャット ダウン**します。  
  
3.  **アクション** ウィンドウの 仮想マシン名をクリックして **設定**します。  
  
4.  ナビゲーション ウィンドウで、**メモリ**します。  
  
5.  **メモリ** ページで、設定、**スタートアップ RAM**に少なくとも 2 GB を順にクリックします**OK**。  
  
### <a name="increase-memory-using-windows-powershell"></a>Windows PowerShell を使用してメモリを増やす  
  
1.  Windows PowerShell を開きます。 (デスクトップで、次のようにクリックします**開始**の入力を開始および**Windows PowerShell**。)。  
  
2.  右クリック **Windows PowerShell**  をクリック **管理者として実行**します。  
  
3.  次のようなコマンドを実行して、置換\<MyVM > を仮想マシンと、メモリの名前の値で、少なくとも次に示す値。  
  
```  
Set-VMMemory <MyVM> -StartupBytes 2GB  
```  
  
## <a name="see-also"></a>関連項目  
[Set-vmmemory](https://technet.microsoft.com/library/hh848572.aspx)  
  


