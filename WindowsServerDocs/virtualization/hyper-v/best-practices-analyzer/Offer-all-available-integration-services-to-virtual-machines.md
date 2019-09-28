---
title: 仮想マシンへのすべての利用可能な統合サービスを提供します。
description: このベストプラクティスアナライザー規則によって報告された問題を解決するための手順を示します。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 2c4b2043-ad81-495e-aa7a-467f813bb3d2
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 5ec2dc73cea8b8356d832bf9fdb960985df2df6c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393603"
---
# <a name="offer-all-available-integration-services-to-virtual-machines"></a>仮想マシンへのすべての利用可能な統合サービスを提供します。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、「 [ベスト プラクティス アナライザー](https://go.microsoft.com/fwlink/?LinkId=122786)」をご覧ください。
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*1つ以上の使用可能な統合サービスが仮想マシンで有効になっていません。*  
  
## <a name="impact"></a>影響  
  
*次の仮想マシンでは、一部の機能を使用できません。*  
  
@no__t-仮想マシン名の一覧 >  
  
## <a name="resolution"></a>解決方法  
  
*これが意図的なものである場合は、それ以上の操作は必要ありません。それ以外の場合は、これらの仮想マシンの設定ですべての統合サービスを提供することを検討してください。*  
  
統合サービスの可用性は、仮想マシンの設定を管理できます。   
  
#### <a name="to-manage-the-availability-of-integration-services-to-a-virtual-machine"></a>仮想マシンに統合サービスの可用性を管理するには  
  
1.  Hyper-V マネージャーを開きます。 **[スタート]** ボタンをクリックし、 **[管理ツール]** をポイントして **[Hyper-V マネージャー]** をクリックします。  
  
2.  結果ウィンドウで  **仮想マシン**, 、構成する仮想マシンを選択します。  
  
3.  **アクション** ウィンドウの 仮想マシン名をクリックして **設定**します。  
  
4.  **管理**, 、クリックして **Integration Services**します。  
  
5.  統合サービスの一覧では、仮想マシンを提供する各サービスのチェック ボックスを選択します。 チェック ボックスを使用できない場合、その特定の統合サービスでは、仮想マシンで実行されているゲスト オペレーティング システムでサポートされていません。  
  


