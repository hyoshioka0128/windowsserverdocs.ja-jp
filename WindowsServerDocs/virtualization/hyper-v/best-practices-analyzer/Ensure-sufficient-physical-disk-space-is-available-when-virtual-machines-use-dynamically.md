---
title: 仮想マシンが容量可変の拡張バーチャルハードディスクを使用する場合に、十分な物理ディスク領域が使用可能であることを確認します。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 9e3e3e64-4b3a-4b9d-acf1-e4df61a04f1e
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 089cc19190d3da9280062d3f1019645fd3cd81de
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950276"
---
# <a name="ensure-sufficient-physical-disk-space-is-available-when-virtual-machines-use-dynamically-expanding-virtual-hard-disks"></a>仮想マシンが容量可変の拡張バーチャルハードディスクを使用する場合に、十分な物理ディスク領域が使用可能であることを確認します。

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
*1つ以上の仮想マシンで、動的に拡張される仮想ハードディスクが使用されています。*

## <a name="impact"></a>影響
*容量可変の拡張バーチャルハードディスクでは、バーチャルハードディスクへの書き込みが発生したときに領域を割り当てることができるように、ホストボリュームに使用可能な領域が必要です。使用可能な領域が不足している場合は、物理記憶域に依存しているすべての仮想マシンが影響を受ける可能性があります。これは、次の仮想マシンに影響します。*

\<list of virtual machines>

## <a name="resolution"></a>解決方法
*使用可能なディスク領域を監視して、十分な領域を拡張できることを確認します。仮想マシンをシャットダウンし、Hyper-v マネージャーのディスクの編集ウィザードを使用して、この仮想マシンの容量可変の拡張仮想ハードディスクを固定サイズの仮想ハードディスクに変換することを検討してください。*



