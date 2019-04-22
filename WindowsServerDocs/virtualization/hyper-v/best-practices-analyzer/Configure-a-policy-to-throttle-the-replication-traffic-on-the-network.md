---
title: ネットワーク上のレプリケーション トラフィックを制限するポリシーを構成します。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 82cb1aef-cdc3-4d0a-88d4-ef497ab79606
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 2c1f1865fa1d611c0b5baaf981140f9807b51458
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818693"
---
# <a name="configure-a-policy-to-throttle-the-replication-traffic-on-the-network"></a>ネットワーク上のレプリケーション トラフィックを制限するポリシーを構成します。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*制限を表示できない可能性がありますを使用するネットワーク帯域幅の量にレプリケーションが許可されています。*  
  
## <a name="impact"></a>影響  
*ネットワーク帯域幅は、他の重要なネットワーク アクティビティに影響を与えず、レプリケーション トラフィックを完全に優位になる可能性があります。これは、次のポートに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*ネットワーク トラフィックを制限するもう 1 つのメソッドを使用する場合は、これを無視できます。それ以外の場合、レプリカ サーバーの適切なポートへのネットワーク トラフィックを制限するポリシーを構成するグループ ポリシー エディターを使用します。*  
  
  


