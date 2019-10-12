---
title: ビデオ機能を提供するために、仮想マシンでディスプレイアダプターを有効にする必要があります
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: ac5992e6-3c0b-46c2-a48e-6ef37b679228
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 0c515c7fb1ed160dfee1e1b7303022082e936157
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364910"
---
# <a name="display-adapters-should-be-enabled-in-virtual-machines-to-provide-video-capabilities"></a>ビデオ機能を提供するために、仮想マシンでディスプレイアダプターを有効にする必要があります

>適用先:Windows Server 2016


  
*ベストプラクティスとスキャンの詳細については、「* [ベストプラクティスアナライザー](https://go.microsoft.com/fwlink/?LinkId=122786)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*仮想マシンで Microsoft Virtual Machine Bus ビデオデバイスが無効になっている可能性があります。*  
  
Microsoft 仮想マシンバスビデオデバイスは、Hyper-v 仮想マシンで使用するために最適化された仮想ビデオアダプターです。 Microsoft Virtual Machine Bus ビデオデバイスを使用するように仮想マシンが構成されていない場合は、従来のビデオアダプターが使用されます。 Microsoft Virtual Machine Bus ビデオデバイスは、従来のビデオアダプターよりもパフォーマンスが優れています。  
  
## <a name="impact"></a>影響  
  
*次の仮想マシンのビデオパフォーマンスが低下します:*  
  
@no__t-仮想マシン名の一覧 >  
  
## <a name="resolution"></a>解決方法  
  
*ゲストオペレーティングシステムのデバイスマネージャーを使用して、Microsoft Virtual Machine Bus ビデオデバイスを有効にします。*  
  
デバイスマネージャーの使用に必要な手順は、オペレーティングシステムによって異なります。 手順については、ゲストオペレーティングシステムのヘルプを参照してください。  
  


