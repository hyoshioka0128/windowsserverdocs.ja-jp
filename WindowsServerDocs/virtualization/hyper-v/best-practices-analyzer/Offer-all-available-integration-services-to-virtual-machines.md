---
title: バーチャル マシンへのすべての利用可能な統合サービスを提供します。
description: このベスト プラクティス アナライザー ルールによって報告された問題を解決する方法を説明します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 2c4b2043-ad81-495e-aa7a-467f813bb3d2
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: c2b5137594f78980f87f6520ae4b4af8203aef32
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59883783"
---
# <a name="offer-all-available-integration-services-to-virtual-machines"></a>バーチャル マシンへのすべての利用可能な統合サービスを提供します。

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
  
*1 つまたは複数の使用可能な統合サービスは、仮想マシンでは無効です。*  
  
## <a name="impact"></a>影響  
  
*いくつかの機能は、次の仮想マシンにできなくなります。*  
  
\<仮想マシン名の一覧 >  
  
## <a name="resolution"></a>解決方法  
  
*これが意図的な場合は、これ以上の操作は必要ありません。それ以外の場合、これらの仮想マシンの設定ですべての統合サービスを提供する検討してください。*  
  
統合サービスの可用性は、仮想マシンの設定を管理できます。   
  
#### <a name="to-manage-the-availability-of-integration-services-to-a-virtual-machine"></a>仮想マシンに統合サービスの可用性を管理するには  
  
1.  Hyper-V マネージャーを開きます。 **[スタート]** ボタンをクリックし、**[管理ツール]** をポイントして **[Hyper-V マネージャー]** をクリックします。  
  
2.  結果ウィンドウで  **仮想マシン**, 、構成する仮想マシンを選択します。  
  
3.  **アクション** ウィンドウの 仮想マシン名をクリックして **設定**します。  
  
4.  **管理**, 、クリックして **Integration Services**します。  
  
5.  統合サービスの一覧では、仮想マシンを提供する各サービスのチェック ボックスを選択します。 チェック ボックスを使用できない場合、その特定の統合サービスでは、仮想マシンで実行されているゲスト オペレーティング システムでサポートされていません。  
  


