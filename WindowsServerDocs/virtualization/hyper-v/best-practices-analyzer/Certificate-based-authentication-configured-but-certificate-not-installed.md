---
title: 証明書ベースの認証が構成されているが、レプリカ サーバーまたはフェールオーバー クラスター ノードで指定された証明書がインストールされていません。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 4cabbce3-9367-4ddc-a108-1e5e1ab2bcff
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: feef30d2f798057e4bd8e53ebab240af6b1d25b8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832943"
---
# <a name="certificate-based-authentication-is-configured-but-the-specified-certificate-is-not-installed-on-the-replica-server-or-failover-cluster-nodes"></a>証明書ベースの認証が構成されているが、レプリカ サーバーまたはフェールオーバー クラスター ノードで指定された証明書がインストールされていません。

>適用先:Windows Server 2016


  
*ベスト プラクティスとスキャンの詳細については、次を参照してください。* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|エラー|  
|**カテゴリ**|構成|  

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>問題  
  
*証明書ベースのレプリケーションがレプリカ サーバー (または任意のフェールオーバー クラスター ノード) にインストールされていないを使用して、HYPER-V レプリカが構成されているセキュリティ証明書。*  
  
## <a name="impact"></a>影響  
  
*クラスターのフェールオーバー、または別のノードへの移行が発生した場合、新しいノードがない、適切な証明書がインストールされている場合、HYPER-V レプリケーションは一時停止します。これは、次のノードに影響します。*  
  
\<ノードの一覧 >  
  
## <a name="resolution"></a>解決方法  
  
*レプリカ サーバー (と存在する場合、フェールオーバー クラスターに関連付けられているすべてのノード) で構成された証明書をインストールします。*  
  


