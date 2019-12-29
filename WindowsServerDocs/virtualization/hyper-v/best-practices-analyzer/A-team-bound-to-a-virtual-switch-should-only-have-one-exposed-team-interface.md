---
title: 仮想スイッチにバインドされたチームには、公開されているチームインターフェイスが1つだけ必要です
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 1074f086-1a2e-42e1-b58c-f55e657d5ce1
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 6baa9e4ae900c9b671003872b4eb4589efb2f085
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365405"
---
# <a name="a-team-bound-to-a-virtual-switch-should-only-have-one-exposed-team-interface"></a>仮想スイッチにバインドされたチームには、公開されているチームインターフェイスが1つだけ必要です

>適用先:Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*1つ以上の仮想スイッチが、複数のチームインターフェイスを持つチームにバインドされています。*  
  
## <a name="impact"></a>**よる**  
*次の仮想スイッチは、他のチームインターフェイスで使用されている Vlan および帯域幅にアクセスできない可能性があります。*  
  
\<list スイッチの一覧 >  
  
## <a name="resolution"></a>**解決方法**  
*Windows PowerShell コマンドレット NetLbfoTeamNic を使用して、既定のチームインターフェイス以外のチームのすべてのチームインターフェイスを削除します。*  
  


