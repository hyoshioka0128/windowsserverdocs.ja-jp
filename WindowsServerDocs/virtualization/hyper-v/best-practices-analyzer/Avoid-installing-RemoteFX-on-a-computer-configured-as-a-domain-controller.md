---
title: Active Directory ドメインコントローラーとして構成されているコンピューターに RemoteFX をインストールしないようにする
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: da58694e-91f6-45d8-a599-18966db165f4
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 67fd8e2568691b7e9be4b46e30b64bf44558d6d0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366471"
---
# <a name="avoid-installing-remotefx-on-a-computer-that-is-configured-as-an-active-directory-domain-controller"></a>Active Directory ドメインコントローラーとして構成されているコンピューターに RemoteFX をインストールしないようにする

>適用先:Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|Error|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*RemoteFX はドメインコントローラーにインストールされます。*  
  
## <a name="impact"></a>**よる**  
*RemoteFX 用に構成された仮想コンピューターは、これらのコンピューターでは使用できません。*  
  
## <a name="resolution"></a>**解決方法**  
*このサーバーを Hyper-v 用 RemoteFX または Active Directory ドメインコントローラーとして構成するかどうかを決定し、必要に応じてサーバーを再構成します。*  
  


