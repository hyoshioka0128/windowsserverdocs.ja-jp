---
title: 仮想マシンは、毎週少なくとも 1 回バックアップする必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 7dbd3dfc-c873-4a77-89f7-3166e18d9531
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: fccc0bb7c46206df210f699cdda84507343c342a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960205"
---
# <a name="virtual-machines-should-be-backed-up-at-least-once-every-week"></a>仮想マシンは、毎週少なくとも 1 回バックアップする必要があります。

>適用先:Windows Server 2016

ベスト プラクティスおよびスキャンの詳細については、「[ベスト プラクティス アナライザー スキャンの実行とスキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|エラー|
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>問題
*過去 1 週間に 1 つまたは複数の仮想マシンがバックアップされてされません。*

## <a name="impact"></a>影響
*仮想マシンで問題が発生し、最新のバックアップが存在しない場合は、大量のデータが失われる可能性があります。これは、次の仮想マシンに影響します。*

\<list of virtual machines>

## <a name="resolution"></a>解決方法
*少なくとも1週間に1回実行するように仮想マシンのバックアップをスケジュールします。この仮想マシンがレプリカで、プライマリ仮想マシンがバックアップされている場合、またはプライマリ仮想マシンであり、そのレプリカがバックアップされている場合、この規則は無視できます。*



