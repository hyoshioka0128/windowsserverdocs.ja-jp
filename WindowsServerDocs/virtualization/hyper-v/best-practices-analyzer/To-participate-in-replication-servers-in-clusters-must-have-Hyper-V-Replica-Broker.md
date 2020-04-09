---
title: レプリケーションに参加するには、フェールオーバークラスター内のサーバーに Hyper-v レプリカブローカーが構成されている必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 5ec88ce5-a8b2-4ece-9062-366523c8b17f
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 921d31aa63bcaaf0946c487d327144f5e29bcfe0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854585"
---
# <a name="to-participate-in-replication-servers-in-failover-clusters-must-have-a-hyper-v-replica-broker-configured"></a>レプリケーションに参加するには、フェールオーバークラスター内のサーバーに Hyper-v レプリカブローカーが構成されている必要があります。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|エラー|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*フェールオーバークラスターの場合、Hyper-v レプリカでは、個々のサーバー名の代わりに Hyper-v レプリカブローカー名を使用する必要があります。*  
  
## <a name="impact"></a>影響  
*仮想マシンが別のフェールオーバークラスターノードに移動された場合、レプリケーションを続行できません。*  
  
## <a name="resolution"></a>解決方法  
*フェールオーバークラスターマネージャーを使用して、Hyper-v レプリカブローカーを構成します。Hyper-v マネージャーで、レプリケーション構成で Hyper-v レプリカブローカー名がサーバー名として使用されていることを確認します。*  
  


