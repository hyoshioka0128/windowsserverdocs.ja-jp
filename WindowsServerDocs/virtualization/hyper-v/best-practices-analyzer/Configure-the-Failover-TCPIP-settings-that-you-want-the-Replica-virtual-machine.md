---
title: フェールオーバーの発生時に使用するレプリカ仮想マシンをフェールオーバー TCP/IP 設定を構成します。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: c16fbc95c9d679611d57327992a6621d58d4e201
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855753"
---
# <a name="configure-the-failover-tcpip-settings-that-you-want-the-replica-virtual-machine-to-use-in-the-event-of-a-failover"></a>フェールオーバーの発生時に使用するレプリカ仮想マシンをフェールオーバー TCP/IP 設定を構成します。

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
*静的 IP アドレスで構成されているレプリカ仮想マシンは、フェールオーバーが発生した場合、プライマリ仮想マシンの対応するから別の IP アドレスを使用するように構成する必要があります。*  
  
## <a name="impact"></a>影響  
*プライマリ仮想マシンでサポートされているワークロードを使用したクライアントはできない、フェールオーバー後に、レプリカ仮想マシンに接続することがあります。また、プライマリ仮想マシンの元の IP アドレスは無効になります、レプリカ仮想マシンのネットワーク トポロジ内。これには、次の仮想マシンに影響します。*  
  
\<仮想マシンの一覧 >  
  
## <a name="resolution"></a>解決方法  
*フェールオーバーが発生した場合、レプリカ仮想マシンが使用する IP アドレスを構成するのにには、HYPER-V マネージャーを使用します。*  
  


