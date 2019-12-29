---
title: SR-IOV を使用するように仮想マシンが構成されている場合、仮想関数ドライバーが正しく動作することを確認します。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: d21e4b93-29bf-423a-a635-71c6d48dc49e
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 5e2c666973aa1ac0d5eb2c4e0d5d29793dc0ce75
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393616"
---
# <a name="ensure-that-the-virtual-function-driver-operates-correctly-when-a-virtual-machine-is-configured-to-use-sr-iov"></a>SR-IOV を使用するように仮想マシンが構成されている場合、仮想関数ドライバーが正しく動作することを確認します。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|Warning|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*仮想関数ドライバーが、1つまたは複数の仮想マシンのゲストオペレーティングシステムで正しく動作していません。*  
  
## <a name="impact"></a>影響  
*次の仮想マシンでは、ネットワークのパフォーマンスは最適ではありません。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>解決方法  
*ゲストオペレーティングシステムで、次の手順を実行します。適切なドライバーがインストールされており、すべてのネットワークデバイスが有効になっていることを確認し、イベントログにエラーまたは警告がないかどうかを確認します。*  
  


