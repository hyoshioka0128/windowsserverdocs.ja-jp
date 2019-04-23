---
title: 圧縮はレプリケーション トラフィックをお勧めします。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: cf8be6e9-2909-4e4a-bb63-d1e1ebbc6930
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 802f11355bec8903e7f6ab81bf337d38e64513f0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833513"
---
# <a name="compression-is-recommended-for-replication-traffic"></a>圧縮はレプリケーション トラフィックをお勧めします。

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
*レプリカ サーバーにプライマリ サーバーから、ネットワーク経由で送信するレプリケーション トラフィックが圧縮されていません。*  
  
## <a name="impact"></a>影響  
*レプリケーション トラフィックでは、必要に応じてより多くの帯域幅を使用します。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*HYPER-V マネージャーで仮想マシンの設定でネットワーク経由で転送されるデータを圧縮する、HYPER-V レプリカを構成します。圧縮を実行するのに HYPER-V の外部でツールを使用することもできます。*  
  


