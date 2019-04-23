---
title: ディスプレイ アダプターは仮想マシンでビデオの機能を提供する有効にする必要があります。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: ac5992e6-3c0b-46c2-a48e-6ef37b679228
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 8d61461db471a876ddf46c1e5fec6992ffa80373
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870693"
---
# <a name="display-adapters-should-be-enabled-in-virtual-machines-to-provide-video-capabilities"></a>ディスプレイ アダプターは仮想マシンでビデオの機能を提供する有効にする必要があります。

>適用先:Windows Server 2016


  
*ベスト プラクティスとスキャンの詳細については、次を参照してください。* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*仮想マシンでは、マイクロソフトの仮想マシン バス ビデオ デバイスを無効にすることがあります。*  
  
Microsoft 仮想マシン バス ビデオ デバイスは、HYPER-V 仮想マシンで使用するために最適化された仮想ビデオ アダプターです。 Microsoft の仮想マシン バス ビデオ デバイスを使用して仮想マシンが構成されていない従来のビデオ アダプターが使用されます。 Microsoft 仮想マシン バス ビデオ デバイスが従来のビデオ アダプターよりも優れた実行します。  
  
## <a name="impact"></a>影響  
  
*次の仮想マシンのビデオのパフォーマンスが低下します。*  
  
\<仮想マシン名の一覧 >  
  
## <a name="resolution"></a>解決方法  
  
*ゲスト オペレーティング システムでデバイス マネージャーを使用して、Microsoft の仮想マシン バス ビデオ デバイスを有効にします。*  
  
デバイス マネージャーを使用するための手順は、オペレーティング システムによって異なります。 手順については、ゲスト オペレーティング システムのヘルプを参照してください。  
  


