---
title: 外部仮想スイッチにバインドされている VMQ 対応の物理ネットワーク アダプターで VMQ を有効にする必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 93d1b155-bf44-46b0-bb69-d34d5b30e574
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: e8607ee891ef693d4e4e7a868540237855aebd2e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393287"
---
# <a name="vmq-should-be-enabled-on-vmq-capable-physical-network-adapters-bound-to-an-external-virtual-switch"></a>外部仮想スイッチにバインドされている VMQ 対応の物理ネットワーク アダプターで VMQ を有効にする必要があります。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|Warning|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*次のネットワークアダプターは、バーチャルマシンキュー (VMQ) に対応していますが、機能が無効になっています。*  
  
## <a name="impact"></a>**よる**  
*Windows は、次のネットワークアダプターで使用可能なハードウェアオフロードを最大限に活用することができません。*  
  
ネットワークアダプターの一覧を \<>  
  
## <a name="resolution"></a>**解決方法**  
*Get-netadaptervmq Windows PowerShell コマンドレットを使用するか、ネットワークアダプターの詳細プロパティユーザーインターフェイスを使用して、VMQ を有効にします。*  
  


