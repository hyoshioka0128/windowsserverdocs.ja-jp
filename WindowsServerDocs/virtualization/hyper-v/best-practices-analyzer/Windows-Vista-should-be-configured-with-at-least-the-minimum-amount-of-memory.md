---
title: Windows Vista をする必要があります最小メモリ量以上で構成
description: このベストプラクティスアナライザー規則によって報告された問題を解決するための手順を示します。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 49f6f9b6-c290-4b1b-b6f3-cc9a0acd8fb2
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 5897b0e363e725b913c8d6492a84df0a957cabb6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860975"
---
# <a name="windows-vista-should-be-configured-with-at-least-the-minimum-amount-of-memory"></a>Windows Vista をする必要があります最小メモリ量以上で構成

>適用対象: Windows Server 2016

ベスト プラクティスとスキャンの詳細については、「 [ベスト プラクティス アナライザー](https://go.microsoft.com/fwlink/?LinkId=122786)」をご覧ください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|エラー|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*Windows Vista を実行する仮想マシンは、RAM の最小容量 (512 MB) 未満で構成されます。*  
  
## <a name="impact"></a>影響  
  
*次の仮想マシン上のゲストオペレーティングシステムが実行されていないか、または信頼性の高い動作をしていない可能性があります。*  
  
仮想マシン名の \<一覧 >  
  
## <a name="resolution"></a>解決方法  
  
*Hyper-v マネージャーを使用して、この仮想マシンに割り当てられているメモリを少なくとも 512 MB に増やします。*  
  
### <a name="to-increase-the-memory-using-hyper-v-manager"></a>Hyper-v マネージャーを使用してメモリを増やすには  
  
1.  Hyper-V マネージャーを開きます。 **[スタート]** ボタンをクリックし、 **[管理ツール]** をポイントして **[Hyper-V マネージャー]** をクリックします。  
  
2.  結果ウィンドウで  **仮想マシン**, 、構成する仮想マシンを選択します。 バーチャルマシンの状態は **オフ (オフ**)」と表示されます。 そうでない場合は、バーチャルマシンを右クリックし、 **[シャットダウン]** をクリックします。  
  
3.  **[操作]** ウィンドウで、仮想マシン名の下の **[設定]** をクリックします。  
  
4.  ナビゲーションウィンドウで、 **[メモリ]** をクリックします。  
  
5.  **[メモリ]** ページで、**スタートアップ RAM**を 512 MB 以上に設定し、[ **OK]** をクリックします。  
  
### <a name="increase-the-memory-using-windows-powershell"></a>Windows PowerShell を使用してメモリを増やす  
  
1.  Windows PowerShell を開きます。 (デスクトップから **[スタート]** をクリックし、「 **Windows PowerShell**」と入力を開始します)。  
  
2.  右クリック **Windows PowerShell**  をクリック **管理者として実行**します。  
  
3.  \<MyVM > を仮想マシンの名前に置き換えた後、次のコマンドを実行します。  
  
```  
Set-VMMemory <MyVM> -StartupBytes 512MB  
```  
  
## <a name="see-also"></a>参照  
[設定-VMMemory](https://technet.microsoft.com/library/hh848572.aspx)  
  


