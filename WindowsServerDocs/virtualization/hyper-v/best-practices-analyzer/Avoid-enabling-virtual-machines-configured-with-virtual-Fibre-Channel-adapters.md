---
title: 仮想ファイバーチャネルアダプターで構成された仮想マシンが、コピー先のファイバーチャネル論理ユニット (Lun) へのパスがソースよりも小さい場合にライブマイグレーションを実行できるようにしない
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 2b85793cd5a680b0fd13fca3da5881b8622710fb
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87963678"
---
# <a name="avoid-enabling-virtual-machines-configured-with-virtual-fibre-channel-adapters-to-allow-live-migrations-when-there-are-fewer-paths-to-fibre-channel-logical-units-luns-on-the-destination-than-on-the-source"></a>仮想ファイバーチャネルアダプターで構成された仮想マシンが、コピー先のファイバーチャネル論理ユニット (Lun) へのパスがソースよりも小さい場合にライブマイグレーションを実行できるようにしない

>適用先:Windows Server 2016

ベスト プラクティスおよびスキャンの詳細については、「[ベスト プラクティス アナライザー スキャンの実行とスキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|警告|
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>**問題点**
*1つ以上の仮想マシンで、仮想化 WMI プロバイダーに AllowReducedFcRedunancy プロパティが設定されています。*

## <a name="impact"></a>**影響**
*次の仮想マシンのライブマイグレーションにより、データが失われたり、記憶域への i/o が中断されることがあります。*

\<list of virtual machines>

## <a name="resolution"></a>**解決策**
*影響を受ける仮想マシンで AllowReducedFcRedundancy WMI プロパティをクリアすることを検討してください。このプロパティをオフにすると、仮想ファイバーチャネルアダプターが構成されている仮想マシンでライブマイグレーションを実行できるのは、移行先でファイバーチャネルするパスの数が、ソースのパスの数と同じか、それよりも多い場合のみです。これらのチェックにより、データの損失や記憶域への i/o の中断を防ぐことができます。*