---
title: 1 つ以上のネットワーク アダプターを使用する必要があります。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 59940e56-e06a-490f-90ea-cf30d9f80b09
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 678c0161e97b8dd022bbf0037d9add5de0281f77
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884603"
---
# <a name="more-than-one-network-adapter-should-be-available"></a>1 つ以上のネットワーク アダプターを使用する必要があります。

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
  
*このサーバーは、管理オペレーティング システムで共有する必要がありますが、1 つのネットワーク アダプターと物理ネットワークへのアクセスを必要とするすべての仮想マシンで構成されます。*  
  
## <a name="impact"></a>影響  
  
*管理オペレーティング システムでネットワークのパフォーマンスが低下する可能性があります。*  
  
## <a name="resolution"></a>解決方法  
  
*このコンピューターに複数のネットワーク アダプターを追加します。管理オペレーティング システムによって排他的に使用するための 1 つのネットワーク アダプターを予約するには、構成しなかった場合、外部仮想ネットワークで使用するためです。*  
  
コンピューターにネットワーク アダプターを追加する方法の詳細については、コンピューターまたはネットワーク アダプターのドキュメントを参照してください。 次に、管理オペレーティング システム専用に予約する接続しないでください仮想スイッチにします。   
  


