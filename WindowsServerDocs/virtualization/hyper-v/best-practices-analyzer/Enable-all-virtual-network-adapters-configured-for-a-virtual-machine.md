---
title: 仮想マシンに構成されているすべての仮想ネットワークアダプターを有効にする
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: fcd350b7-4240-4359-aadd-93e7ac4d314e
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: bdca25be4af41d0f6ddfafe885f8c2b1301b71fb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393647"
---
# <a name="enable-all-virtual-network-adapters-configured-for-a-virtual-machine"></a>仮想マシンに構成されているすべての仮想ネットワークアダプターを有効にする

>適用対象: Windows Server 2016

ベスト プラクティスとスキャンの詳細については、「 [ベスト プラクティス アナライザー](https://go.microsoft.com/fwlink/?LinkId=122786)」をご覧ください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|Warning|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
  
*1つまたは複数のネットワークアダプターがバーチャルマシンで無効になっている可能性があります。*  
  
## <a name="impact"></a>影響  
  
*次の仮想マシンがネットワークに接続されていない可能性があります。*  
  
仮想マシン名の \<一覧 >  
  
## <a name="resolution"></a>解決方法  
  
*ゲストオペレーティングシステムのデバイスマネージャーを使用して、すべての仮想ネットワークアダプターを有効にします。アダプターが不要な場合は、Hyper-v マネージャーを使用して仮想マシンから削除します。*  
  


