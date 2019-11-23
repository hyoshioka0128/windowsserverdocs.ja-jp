---
title: 仮想スイッチにバインドされているチーム インターフェイスが既定のモードである必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 8c118e1e-865f-4cff-acdc-7c35e45d5da9
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 9bfd0c98e865a0faae8dd70e97696e2c2682531b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393429"
---
# <a name="the-team-interface-bound-to-a-virtual-switch-should-be-in-default-mode"></a>仮想スイッチにバインドされているチーム インターフェイスが既定のモードである必要があります。

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
*一部の仮想スイッチはチームインターフェイスにバインドされていますが、チームインターフェイスは、すべての Vlan 上のトラフィックを仮想スイッチに渡しません。*  
  
## <a name="impact"></a>**よる**  
*次の仮想スイッチは、すべての Vlan にアクセスすることはできません: \n{0}*  
  
## <a name="resolution"></a>**解決方法**  
*サーバーマネージャーまたは Windows PowerShell コマンドレット NetLbfoTeamNic を使用して、チームインターフェイスを既定のモードにリセットします。*  
  


