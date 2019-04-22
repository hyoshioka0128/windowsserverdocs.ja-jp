---
title: 1 つまたは 2 の仮想プロセッサを搭載した Windows Vista を実行する仮想マシンの構成します。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: e562bce3-fd68-42c9-821c-12022ae4746c
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: fae7d5e437fd83b9c00afcceaaf0eb7e8a7b909b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812073"
---
# <a name="configure-virtual-machines-running-windows-vista-with-1-or-2-virtual-processors"></a>1 つまたは 2 の仮想プロセッサを搭載した Windows Vista を実行する仮想マシンの構成します。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|構成|  
|**カテゴリ**|エラー|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*2 つ以上の仮想プロセッサを搭載した Windows Vista を実行する仮想マシンが構成されます。*  
  
## <a name="impact"></a>影響  
  
*Microsoft は、次の仮想マシンの構成をサポートしていません。*  
  
\<仮想マシン名の一覧 >  
  
## <a name="resolution"></a>解決方法  
  
*仮想マシンをシャット ダウンし、1 つまたは複数の仮想プロセッサを削除します。*  
  
### <a name="to-remove-virtual-processors"></a>仮想プロセッサを削除するには  
  
1.  Hyper-V マネージャーを開きます。 **[スタート]** ボタンをクリックし、**[管理ツール]** をポイントして **[Hyper-V マネージャー]** をクリックします。  
  
2.  結果ウィンドウで  **仮想マシン**, 、構成する仮想マシンを選択します。 仮想マシンの状態として表示されるはず**オフ**します。 そうでない場合は、仮想マシンを右クリックし、順にクリックします**シャット ダウン**します。  
  
3.  **アクション** ウィンドウの 仮想マシン名をクリックして **設定**します。  
  
4.  ナビゲーション ウィンドウで、**プロセッサ**します。  
  
5.  **プロセッサ**するプロセッサの数を設定 ページで、 **1**または**2**順にクリックします**OK**します。  
  


