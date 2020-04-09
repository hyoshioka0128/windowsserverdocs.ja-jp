---
title: ポート ミラーリングの宛先として 1 つまたは複数のネットワーク アダプターを構成する必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: b83c166d-f010-47c4-a4bb-02167f2e3361
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: b0b9ce90c9614332ca12ddb6a1467d38425d6ddf
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861875"
---
# <a name="one-or-more-network-adapters-should-be-configured-as-the-destination-for-port-mirroring"></a>ポート ミラーリングの宛先として 1 つまたは複数のネットワーク アダプターを構成する必要があります。

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
*1つまたは複数の仮想マシンに、ポートミラーリングのソースとして構成されたネットワークアダプターがありますが、仮想スイッチに対応する宛先がありません。*  
  
## <a name="impact"></a>**よる**  
*次の仮想スイッチと仮想マシンでは、ポートミラーリングが正しく動作しません。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>**解決方法**  
*Windows PowerShell または Hyper-v マネージャーを使用して、ポートミラーリングの構成を完了または修正します。*  
  


