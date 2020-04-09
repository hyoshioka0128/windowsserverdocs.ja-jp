---
title: フェールオーバーが発生した場合にレプリカ仮想マシンが使用するフェールオーバー TCP/IP 設定を構成する
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: d2db5fdedbe2f19c01b7dd172f18b6fec969e828
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80862055"
---
# <a name="configure-the-failover-tcpip-settings-that-you-want-the-replica-virtual-machine-to-use-in-the-event-of-a-failover"></a>フェールオーバーが発生した場合にレプリカ仮想マシンが使用するフェールオーバー TCP/IP 設定を構成する

>適用対象: Windows Server 2016
 
ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|［警告］|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。
  
## <a name="issue"></a>問題  
*静的 IP アドレスで構成されたレプリカ仮想マシンは、フェールオーバーが発生した場合に対応するプライマリ仮想マシンとは異なる IP アドレスを使用するように構成する必要があります。*  
  
## <a name="impact"></a>影響  
*プライマリ仮想マシンでサポートされているワークロードを使用しているクライアントは、フェールオーバー後にレプリカ仮想マシンに接続できない可能性があります。また、プライマリ仮想マシンの元の IP アドレスは、レプリカ仮想マシンのネットワークトポロジでは無効になります。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
*Hyper-v マネージャーを使用して、フェールオーバーが発生したときにレプリカ仮想マシンが使用する IP アドレスを構成します。*  
  


