---
title: Active Directory ドメインコントローラーとして構成されているコンピューターに RemoteFX をインストールしないようにする
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: da58694e-91f6-45d8-a599-18966db165f4
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 597dd26d0a317ca026cd94ab29138ce679d7c3b9
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857765"
---
# <a name="avoid-installing-remotefx-on-a-computer-that-is-configured-as-an-active-directory-domain-controller"></a>Active Directory ドメインコントローラーとして構成されているコンピューターに RemoteFX をインストールしないようにする

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|エラー|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*RemoteFX はドメインコントローラーにインストールされます。*  
  
## <a name="impact"></a>**よる**  
*RemoteFX 用に構成された仮想コンピューターは、これらのコンピューターでは使用できません。*  
  
## <a name="resolution"></a>**解決方法**  
*このサーバーを Hyper-v 用 RemoteFX または Active Directory ドメインコントローラーとして構成するかどうかを決定し、必要に応じてサーバーを再構成します。*  
  


