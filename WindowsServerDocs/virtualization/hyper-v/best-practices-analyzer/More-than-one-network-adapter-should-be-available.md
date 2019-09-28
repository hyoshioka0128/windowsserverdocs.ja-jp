---
title: 1 つ以上のネットワーク アダプターを使用する必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 59940e56-e06a-490f-90ea-cf30d9f80b09
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 6b043900c6fde4522e5805a1f0c1a635de335e31
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364801"
---
# <a name="more-than-one-network-adapter-should-be-available"></a>1 つ以上のネットワーク アダプターを使用する必要があります。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、「 [ベスト プラクティス アナライザー](https://go.microsoft.com/fwlink/?LinkId=122786)」をご覧ください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|Error|  
|**カテゴリ**|構成|  

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>問題  
  
*このサーバーは、1つのネットワークアダプターで構成されます。このアダプターは、管理オペレーティングシステムと、物理ネットワークへのアクセスを必要とするすべての仮想マシンによって共有される必要があります。*  
  
## <a name="impact"></a>影響  
  
*管理オペレーティングシステムのネットワークパフォーマンスが低下している可能性があります。*  
  
## <a name="resolution"></a>解決方法  
  
*Add コンピューターにネットワークアダプターを追加します。管理オペレーティングシステムで使用するために1つのネットワークアダプターを予約するには、外部仮想ネットワークで使用するように構成しないでください。*  
  
コンピューターにネットワーク アダプターを追加する方法の詳細については、コンピューターまたはネットワーク アダプターのドキュメントを参照してください。 次に、管理オペレーティング システム専用に予約する接続しないでください仮想スイッチにします。   
  


