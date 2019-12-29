---
title: 1 つまたは複数のネットワーク アダプターは、ポート ミラーリングのソースとして構成する必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 147fd00f-1440-44d1-94e3-3a8af63aa7ed
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: a079033608b8af8c63a0d02ae166eb7280fec41d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393565"
---
# <a name="one-or-more-network-adapters-should-be-configured-as-the-source-for-port-mirroring"></a>1 つまたは複数のネットワーク アダプターは、ポート ミラーリングのソースとして構成する必要があります。

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
*1つまたは複数の仮想マシンに、ポートミラーリングの宛先として構成されたネットワークアダプターがありますが、仮想スイッチに対応するソースがありません。*  
  
## <a name="impact"></a>**よる**  
*次の仮想スイッチと仮想マシンでは、ポートミラーリングが正しく動作しません。*  
  
仮想マシンの一覧を \<>  
  
## <a name="resolution"></a>**解決方法**  
*Windows PowerShell または Hyper-v マネージャーを使用して、ポートミラーリングの構成を完了または修正します。*  
  


