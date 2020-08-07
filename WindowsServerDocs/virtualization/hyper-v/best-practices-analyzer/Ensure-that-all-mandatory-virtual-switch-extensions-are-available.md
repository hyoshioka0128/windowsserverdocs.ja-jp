---
title: すべての必須の仮想スイッチ拡張機能が使用可能であることを確認する
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 2f2f2698-f5ec-4cad-aa64-d6987e8142a1
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 48c8ee80a0044c067d29730c1ec79bd67fdc062b
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950256"
---
# <a name="ensure-that-all-mandatory-virtual-switch-extensions-are-available"></a>すべての必須の仮想スイッチ拡張機能が使用可能であることを確認する

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
*1つまたは複数の仮想ネットワークアダプターが、無効またはインストールされていない必須の拡張機能を持つ仮想スイッチに接続されています。*

## <a name="impact"></a>影響
*次の仮想マシン上の1つまたは複数の仮想ネットワークアダプターで、ネットワークトラフィックがブロックされています:*

\<list of virtual machines>

## <a name="resolution"></a>解決方法
*まず、必須の拡張機能がホストにインストールされていることを確認し、必要に応じて拡張機能をインストールします。その後、必須の拡張機能が無効になっている場合は、仮想スイッチマネージャーまたは Windows PowerShell コマンドレット VMSwitchExtension を使用して拡張機能を有効にします。*



