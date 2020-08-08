---
title: ビデオ機能を提供するために、仮想マシンでディスプレイアダプターを有効にする必要があります
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: ac5992e6-3c0b-46c2-a48e-6ef37b679228
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: ba22545a0e1d66a0f0d8f03dd7f7a42054a41d44
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960615"
---
# <a name="display-adapters-should-be-enabled-in-virtual-machines-to-provide-video-capabilities"></a>ビデオ機能を提供するために、仮想マシンでディスプレイアダプターを有効にする必要があります

>適用先:Windows Server 2016



*ベストプラクティスとスキャンの詳細については、「ベストプラクティスアナライザー」を参照してください* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786)。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|警告|
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>問題

*仮想マシンで Microsoft Virtual Machine Bus ビデオデバイスが無効になっている可能性があります。*

Microsoft 仮想マシンバスビデオデバイスは、Hyper-v 仮想マシンで使用するために最適化された仮想ビデオアダプターです。 Microsoft Virtual Machine Bus ビデオデバイスを使用するように仮想マシンが構成されていない場合は、従来のビデオアダプターが使用されます。 Microsoft Virtual Machine Bus ビデオデバイスは、従来のビデオアダプターよりもパフォーマンスが優れています。

## <a name="impact"></a>影響

*次の仮想マシンのビデオパフォーマンスが低下します:*

\<list of virtual machine names>

## <a name="resolution"></a>解決方法

*ゲストオペレーティングシステムのデバイスマネージャーを使用して、Microsoft Virtual Machine Bus ビデオデバイスを有効にします。*

デバイスマネージャーの使用に必要な手順は、オペレーティングシステムによって異なります。 手順については、ゲストオペレーティングシステムのヘルプを参照してください。



