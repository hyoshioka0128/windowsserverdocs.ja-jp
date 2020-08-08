---
title: SR-IOV を使用するように仮想マシンが構成されている場合、仮想関数ドライバーが正しく動作することを確認します。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: d21e4b93-29bf-423a-a635-71c6d48dc49e
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 8fc14e14ff66b59099ebad1f3b9643b94427346a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954489"
---
# <a name="ensure-that-the-virtual-function-driver-operates-correctly-when-a-virtual-machine-is-configured-to-use-sr-iov"></a>SR-IOV を使用するように仮想マシンが構成されている場合、仮想関数ドライバーが正しく動作することを確認します。

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
*仮想関数ドライバーが、1つまたは複数の仮想マシンのゲストオペレーティングシステムで正しく動作していません。*

## <a name="impact"></a>影響
*次の仮想マシンでは、ネットワークのパフォーマンスは最適ではありません。*

\<list of virtual machines>

## <a name="resolution"></a>解決方法
*ゲストオペレーティングシステムで、次の手順を実行します。適切なドライバーがインストールされており、すべてのネットワークデバイスが有効になっていることを確認し、イベントログにエラーまたは警告がないかどうかを確認します。*



