---
title: レプリケーションに参加するには、フェールオーバー クラスター内のサーバーが構成されている HYPER-V レプリカ ブローカーをいる必要があります。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 5ec88ce5-a8b2-4ece-9062-366523c8b17f
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: d4966396af955f9c8bad34b5b2892115e93c3b85
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887973"
---
# <a name="to-participate-in-replication-servers-in-failover-clusters-must-have-a-hyper-v-replica-broker-configured"></a>レプリケーションに参加するには、フェールオーバー クラスター内のサーバーが構成されている HYPER-V レプリカ ブローカーをいる必要があります。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|エラー|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*フェールオーバー クラスターで HYPER-V レプリカには、個々 のサーバー名ではなく、HYPER-V レプリカ ブローカー名の使用が必要です。*  
  
## <a name="impact"></a>影響  
*かどうか、仮想マシンは別のフェールオーバー クラスター ノードに移動、レプリケーションを続行できません。*  
  
## <a name="resolution"></a>解決方法  
*HYPER-V レプリカ ブローカーを構成するには、フェールオーバー クラスター マネージャーを使用します。HYPER-V マネージャーでは、レプリケーションの構成がサーバー名として、HYPER-V レプリカ ブローカーの名前を使用することを確認します。*  
  


