---
title: 仮想ファイバー チャネル アダプターで構成された仮想マシンをファイバー チャネル ベースの記憶域を高可用性を構成してください。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 73127bdd-8086-4268-a93c-2fdf1623e91b
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 60a96d6e559f3fefe6f8c1c52c2d145efa006c99
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960185"
---
# <a name="virtual-machines-configured-with-a-virtual-fibre-channel-adapter-should-be-configured-for-high-availability-to-the-fibre-channel-based-storage"></a>仮想ファイバー チャネル アダプターで構成された仮想マシンをファイバー チャネル ベースの記憶域を高可用性を構成してください。

>適用先:Windows Server 2016

ベスト プラクティスおよびスキャンの詳細については、「[ベスト プラクティス アナライザー スキャンの実行とスキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|情報|
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>**問題点**
*1 つまたは複数の仮想マシンでは、これらの仮想マシンが 1 つだけのホスト バス アダプター (HBA) に接続されている仮想ファイバー チャネル アダプターで構成されているために、ファイバー チャネル ベースの記憶域への接続を高可用性が不足しています。*

## <a name="impact"></a>**影響**
*ホストバスアダプターで障害が発生すると、記憶域と仮想マシン間のファイバーチャネル接続がブロックされる可能性があります。これは、次の仮想マシンに影響します。*

\<list of virtual machines>

## <a name="resolution"></a>**解決策**
*仮想マシンからホスト バス アダプターに別の接続を追加し、ファイバー チャネルの冗長な接続を確立するためにゲスト オペレーティング システムにマルチパス I/O (MPIO) を構成します。*



