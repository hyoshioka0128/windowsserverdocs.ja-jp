---
title: 仮想マシンでの専用の 1 つまたは複数の外部仮想ネットワークを予約します。
description: このベスト プラクティス アナライザー ルールによって報告された問題を解決する方法を説明します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: f7732258-93f1-44e8-835b-5ad2d1c45cd9
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: c8c90a74352bae0b348608db0fc05107e4d09010
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884743"
---
# <a name="reserve-one-or-more-external-virtual-networks-for-exclusive-use-by-virtual-machines"></a>仮想マシンでの専用の 1 つまたは複数の外部仮想ネットワークを予約します。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、「 [ベスト プラクティス アナライザー](https://go.microsoft.com/fwlink/?LinkId=122786)」をご覧ください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|エラー|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*すべての外部仮想ネットワークは、管理オペレーティング システムと仮想マシンの両方で使用するために構成されます。*  
  
## <a name="impact"></a>影響  
  
*管理オペレーティング システムでネットワークのパフォーマンスが低下する可能性があります。*  
  
## <a name="resolution"></a>解決方法  
  
*仮想スイッチ マネージャーを使用して、管理オペレーティング システムとの外部仮想ネットワークの共有を停止します。*  
  
#### <a name="to-stop-sharing-the-external-virtual-network-with-the-management-operating-system"></a>管理オペレーティング システムとの外部仮想ネットワークの共有を停止するには  
  
1.  Hyper-V マネージャーを開きます。 **[スタート]** ボタンをクリックし、**[管理ツール]** をポイントして **[Hyper-V マネージャー]** をクリックします。  
  
2.  **[操作]** メニューの **[仮想スイッチ マネージャー]** をクリックします。  
  
3.  **仮想スイッチ**, 、外部仮想スイッチの名前をクリックします。  
  
4.  **接続の種類** 物理ネットワーク アダプターの名前の下の領域をオフに、 **管理オペレーティング システムでこのネットワーク アダプタを共有できるように** チェック ボックスをオンします。  
  
5.  **[OK]** をクリックします。  
  


