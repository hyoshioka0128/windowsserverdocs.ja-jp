---
title: SR-IOV 用に構成された仮想マシンの実行の数は仮想マシンで使用できる仮想関数の数を超えることはできません。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 8bd4af5e-9e7d-4710-8950-39435a8bb373
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 16126118cdbf2341059fb0871ee7c33b62dc6b94
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960385"
---
# <a name="the-number-of-running-virtual-machines-configured-for-sr-iov-should-not-exceed-the-number-of-virtual-functions-available-to-the-virtual-machines"></a>SR-IOV 用に構成された仮想マシンの実行の数は仮想マシンで使用できる仮想関数の数を超えることはできません。

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
*利用していない十分な仮想関数をシングル ルート I/O 仮想化 (SR-IOV) 用に構成された仮想マシンの実行の数。*

## <a name="impact"></a>影響
*ネットワークのパフォーマンスは、次の仮想マシンに最適でない可能性があります。*

\<list of virtual machines>

## <a name="resolution"></a>解決方法
*SR-IOV 仮想機能を必要としない 1 つまたは複数の仮想マシンで SR-IOV を無効にすることを検討してください。*



