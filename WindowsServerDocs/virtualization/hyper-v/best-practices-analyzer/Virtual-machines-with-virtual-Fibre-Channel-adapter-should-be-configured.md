---
title: 仮想ファイバー チャネル アダプターで構成された仮想マシンをファイバー チャネル ベースの記憶域を高可用性を構成してください。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 73127bdd-8086-4268-a93c-2fdf1623e91b
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: e04b52fc98fd79024970ed525e902132d97701e6
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855005"
---
# <a name="virtual-machines-configured-with-a-virtual-fibre-channel-adapter-should-be-configured-for-high-availability-to-the-fibre-channel-based-storage"></a>仮想ファイバー チャネル アダプターで構成された仮想マシンをファイバー チャネル ベースの記憶域を高可用性を構成してください。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|情報|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。
  
## <a name="issue"></a>**問題**  
*1つ以上の仮想マシンに、ファイバーチャネルベースの記憶域への高可用性接続がありません。これらの仮想マシンは、1つのホストバスアダプター (HBA) にのみ接続されている仮想ファイバーチャネルアダプターで構成されているためです。*  
  
## <a name="impact"></a>**よる**  
*ホストバスアダプターで障害が発生すると、記憶域と仮想マシン間のファイバーチャネル接続がブロックされる可能性があります。これは、次の仮想マシンに影響します。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>**解決方法**  
*仮想マシンからホストバスアダプターに別の接続を追加し、ゲストオペレーティングシステムでマルチパス i/o (MPIO) を構成して、冗長ファイバーチャネル接続を確立します。*  
  


