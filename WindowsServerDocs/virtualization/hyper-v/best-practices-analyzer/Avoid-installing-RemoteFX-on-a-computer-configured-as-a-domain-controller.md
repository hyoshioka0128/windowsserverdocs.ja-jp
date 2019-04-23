---
title: RemoteFX を Active Directory のドメイン コント ローラーとして構成されているコンピューターにインストールしないでください。
description: このベスト プラクティス アナライザー ルールのテキストのオンライン バージョン。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: da58694e-91f6-45d8-a599-18966db165f4
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 9e1c642e3f36b5fe25f34bb417a83b8510adcc02
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832563"
---
# <a name="avoid-installing-remotefx-on-a-computer-that-is-configured-as-an-active-directory-domain-controller"></a>RemoteFX を Active Directory のドメイン コント ローラーとして構成されているコンピューターにインストールしないでください。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|エラー|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>**問題**  
*RemoteFX は、ドメイン コント ローラーにインストールされます。*  
  
## <a name="impact"></a>**影響**  
*RemoteFX 用に構成された仮想コンピューターは、これらのコンピューターでは使用できません。*  
  
## <a name="resolution"></a>**解決方法**  
*このサーバーまたは Active Directory ドメイン コント ローラー、として、HYPER-V に対して RemoteFX のいずれかを構成し、必要に応じてサーバーを再構成するかを決定します。*  
  


