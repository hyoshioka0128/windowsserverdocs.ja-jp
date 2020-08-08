---
title: Active Directory ドメインコントローラーとして構成されているコンピューターに RemoteFX をインストールしないようにする
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: da58694e-91f6-45d8-a599-18966db165f4
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 5a5c2d23794ba2328da9a2a8c668a8525f6c6322
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960675"
---
# <a name="avoid-installing-remotefx-on-a-computer-that-is-configured-as-an-active-directory-domain-controller"></a>Active Directory ドメインコントローラーとして構成されているコンピューターに RemoteFX をインストールしないようにする

>適用先:Windows Server 2016

ベスト プラクティスおよびスキャンの詳細については、「[ベスト プラクティス アナライザー スキャンの実行とスキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|エラー|
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>**問題点**
*RemoteFX はドメインコントローラーにインストールされます。*

## <a name="impact"></a>**影響**
*RemoteFX 用に構成された仮想コンピューターは、これらのコンピューターでは使用できません。*

## <a name="resolution"></a>**解決策**
*このサーバーを Hyper-v 用 RemoteFX または Active Directory ドメインコントローラーとして構成するかどうかを決定し、必要に応じてサーバーを再構成します。*



