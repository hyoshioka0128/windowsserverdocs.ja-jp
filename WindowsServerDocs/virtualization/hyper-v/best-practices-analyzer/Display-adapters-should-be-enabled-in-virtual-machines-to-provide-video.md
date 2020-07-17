---
title: ビデオ機能を提供するために、仮想マシンでディスプレイアダプターを有効にする必要があります
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: ac5992e6-3c0b-46c2-a48e-6ef37b679228
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 1821aae18b1712ba7d839ca9f42318edc5ef8a35
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80862005"
---
# <a name="display-adapters-should-be-enabled-in-virtual-machines-to-provide-video-capabilities"></a>ビデオ機能を提供するために、仮想マシンでディスプレイアダプターを有効にする必要があります

>適用対象: Windows Server 2016


  
*ベストプラクティスとスキャンの詳細については、「ベストプラクティスアナライザー」を参照してください* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786)。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|［警告］|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*仮想マシンで Microsoft Virtual Machine Bus ビデオデバイスが無効になっている可能性があります。*  
  
Microsoft 仮想マシンバスビデオデバイスは、Hyper-v 仮想マシンで使用するために最適化された仮想ビデオアダプターです。 Microsoft Virtual Machine Bus ビデオデバイスを使用するように仮想マシンが構成されていない場合は、従来のビデオアダプターが使用されます。 Microsoft Virtual Machine Bus ビデオデバイスは、従来のビデオアダプターよりもパフォーマンスが優れています。  
  
## <a name="impact"></a>影響  
  
*次の仮想マシンのビデオパフォーマンスが低下します:*  
  
仮想マシン名の \<一覧 >  
  
## <a name="resolution"></a>解決方法  
  
*ゲストオペレーティングシステムのデバイスマネージャーを使用して、Microsoft Virtual Machine Bus ビデオデバイスを有効にします。*  
  
デバイスマネージャーの使用に必要な手順は、オペレーティングシステムによって異なります。 手順については、ゲストオペレーティングシステムのヘルプを参照してください。  
  


