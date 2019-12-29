---
title: レプリケーションに参加するには、フェールオーバークラスター内のサーバーに Hyper-v レプリカブローカーが構成されている必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 5ec88ce5-a8b2-4ece-9062-366523c8b17f
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 2e15d2c4a467807397ef4712d2df1730b40d8024
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364598"
---
# <a name="to-participate-in-replication-servers-in-failover-clusters-must-have-a-hyper-v-replica-broker-configured"></a>レプリケーションに参加するには、フェールオーバークラスター内のサーバーに Hyper-v レプリカブローカーが構成されている必要があります。

>適用先:Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|Error|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*フェールオーバークラスターの場合、Hyper-v レプリカでは、個々のサーバー名の代わりに Hyper-v レプリカブローカー名を使用する必要があります。*  
  
## <a name="impact"></a>影響  
*仮想マシンが別のフェールオーバークラスターノードに移動された場合、レプリケーションを続行できません。*  
  
## <a name="resolution"></a>解決方法  
*Use を使用して Hyper-v レプリカブローカーを構成します。Hyper-v マネージャーで、レプリケーション構成で、サーバー名として Hyper-v レプリカブローカー名が使用されていることを確認してください。*  
  


