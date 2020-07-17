---
title: 仮想 SAN は、物理ホストバスアダプターに関連付けられている必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 14bca69b-e779-4e90-b5c1-1b015625572f
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 10a17f8661f1436f5b4db317648edde57a0dfe74
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857935"
---
# <a name="a-virtual-san-should-be-associated-with-a-physical-host-bus-adapter"></a>仮想 SAN は、物理ホストバスアダプターに関連付けられている必要があります。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|［警告］|  
|**カテゴリ**|構成|  
  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*ホストバスアダプター (HBA) に関連付けられていない仮想記憶域エリアネットワーク (SAN) が構成されています。*  
  
## <a name="impact"></a>**よる**  
*構成が正しくない仮想 SAN に接続された仮想ファイバーチャネルアダプターを使用して構成されている場合、仮想マシンは起動しません。これは、次の仮想 San に影響します。*  
  
  
仮想 San > の一覧 \<  
  
  
## <a name="resolution"></a>**解決方法**  
*ホストバスアダプターに接続して、仮想 SAN を再構成します。*  
  
  
  


