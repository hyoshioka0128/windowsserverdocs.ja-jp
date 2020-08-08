---
title: フェールオーバーが発生した場合にレプリカ仮想マシンが使用するフェールオーバー TCP/IP 設定を構成する
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 713be5cf428617287e0be0bc65b3e2beb2d11400
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87948450"
---
# <a name="configure-the-failover-tcpip-settings-that-you-want-the-replica-virtual-machine-to-use-in-the-event-of-a-failover"></a>フェールオーバーが発生した場合にレプリカ仮想マシンが使用するフェールオーバー TCP/IP 設定を構成する

>適用先:Windows Server 2016

ベスト プラクティスおよびスキャンの詳細については、「[ベスト プラクティス アナライザー スキャンの実行とスキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|警告|
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>問題
*静的 IP アドレスで構成されたレプリカ仮想マシンは、フェールオーバーが発生した場合に対応するプライマリ仮想マシンとは異なる IP アドレスを使用するように構成する必要があります。*

## <a name="impact"></a>影響
*プライマリ仮想マシンでサポートされているワークロードを使用しているクライアントは、フェールオーバー後にレプリカ仮想マシンに接続できない可能性があります。また、プライマリ仮想マシンの元の IP アドレスは、レプリカ仮想マシンのネットワークトポロジでは無効になります。これは、次の仮想マシンに影響します。*

\<list of virtual machines>

## <a name="resolution"></a>解決方法
*Hyper-v マネージャーを使用して、フェールオーバーが発生したときにレプリカ仮想マシンが使用する IP アドレスを構成します。*



