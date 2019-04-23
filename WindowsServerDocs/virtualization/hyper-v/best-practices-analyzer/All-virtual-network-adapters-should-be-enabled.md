---
title: すべての仮想ネットワーク アダプターを有効にします。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: b17d647d-a34a-44de-ada6-01a2bf5eeb48
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 0a769c3203f6c6946f01cd91b66fbec38af83bbd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837133"
---
# <a name="all-virtual-network-adapters-should-be-enabled"></a>すべての仮想ネットワーク アダプターを有効にします。

>適用先:Windows Server 2016


  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*管理オペレーティング システムでは、物理ネットワーク アダプターに関連付けられている 1 つまたは複数の仮想ネットワーク アダプターが無効になります。*  
  
## <a name="impact"></a>影響  
  
*このサーバーの構成は、最適ではありません。*  
  
管理オペレーティング システムは、無効な仮想ネットワーク アダプターと関連付けるために、このコンピューターで使用、物理ネットワーク アダプターのいずれかの物理 (外部) ネットワークに接続できません。  
  
## <a name="resolution"></a>解決方法  
  
*仮想ネットワーク アダプターを有効にするのにには、ネットワークとインターネットの設定を使用します。または、仮想スイッチ マネージャーを使用して、外部仮想スイッチを再構成して、管理オペレーティング システムとは共有しないようにします。*  
  


