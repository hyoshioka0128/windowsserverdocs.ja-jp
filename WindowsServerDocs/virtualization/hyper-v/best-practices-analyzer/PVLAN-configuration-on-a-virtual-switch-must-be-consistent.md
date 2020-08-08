---
title: 仮想スイッチ上 PVLAN 構成は、一貫性のあるである必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 4db63bcc-7a54-4f19-98a6-c274c3956d51
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 63780266fa23187e12bfd5d503a1f3c0306bc364
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939029"
---
# <a name="pvlan-configuration-on-a-virtual-switch-must-be-consistent"></a>仮想スイッチ上 PVLAN 構成は、一貫性のあるである必要があります。

>適用先:Windows Server 2016

ベスト プラクティスおよびスキャンの詳細については、「[ベスト プラクティス アナライザー スキャンの実行とスキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|エラー|
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>**問題点**
*プライベート仮想ローカル エリア ネットワーク (PVLAN) は、1 つまたは複数の仮想ネットワーク アダプターで正しく構成されていません。*

## <a name="impact"></a>**影響**
*PVLAN では、仮想マシン間のネットワーク トラフィックを正しく特定可能性があります。*

## <a name="resolution"></a>**解決策**
*PVLAN を正しく構成するのにには、Windows PowerShell コマンドレット、Set-vmnetworkadaptervlan を使用します。*



