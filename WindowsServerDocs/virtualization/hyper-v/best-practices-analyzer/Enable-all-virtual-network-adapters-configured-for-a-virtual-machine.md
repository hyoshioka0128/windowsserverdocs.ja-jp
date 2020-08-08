---
title: 仮想マシンに構成されているすべての仮想ネットワークアダプターを有効にする
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: fcd350b7-4240-4359-aadd-93e7ac4d314e
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 7958bf5ced635c344ded45f8fde54bd7779ccbe9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960575"
---
# <a name="enable-all-virtual-network-adapters-configured-for-a-virtual-machine"></a>仮想マシンに構成されているすべての仮想ネットワークアダプターを有効にする

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、「 [ベスト プラクティス アナライザー](https://go.microsoft.com/fwlink/?LinkId=122786)」をご覧ください。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|警告|
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>問題

*1つまたは複数のネットワークアダプターがバーチャルマシンで無効になっている可能性があります。*

## <a name="impact"></a>影響

*次の仮想マシンがネットワークに接続されていない可能性があります。*

\<list of virtual machine names>

## <a name="resolution"></a>解決方法

*ゲストオペレーティングシステムのデバイスマネージャーを使用して、すべての仮想ネットワークアダプターを有効にします。アダプターが不要な場合は、Hyper-v マネージャーを使用して仮想マシンから削除します。*



