---
title: 仮想 SAN は、物理ホストバスアダプターに関連付けられている必要があります。
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 14bca69b-e779-4e90-b5c1-1b015625572f
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 9e86f8d9b9a4a87fd6457954c3a4723857faac3b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366691"
---
# <a name="a-virtual-san-should-be-associated-with-a-physical-host-bus-adapter"></a>仮想 SAN は、物理ホストバスアダプターに関連付けられている必要があります。

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
*ホストバスアダプター (HBA) に関連付けられていない仮想記憶域エリアネットワーク (SAN) が構成されています。*  
  
## <a name="impact"></a>**よる**  
構成されている仮想 SAN に接続されている仮想ファイバーチャネルアダプターが構成されている場合、*A 仮想マシンは起動しません。これは、次の仮想 San に影響します:*  
  
  
\<list San > の一覧  
  
  
## <a name="resolution"></a>**解決方法**  
*ホストバスアダプターに接続して、仮想 SAN を再構成します。*  
  
  
  


