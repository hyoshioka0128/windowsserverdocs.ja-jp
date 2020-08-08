---
title: ネットワーク上のレプリケーショントラフィックを調整するためのポリシーを構成する
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 82cb1aef-cdc3-4d0a-88d4-ef497ab79606
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: dcee85911ebcc93e935a7df30d43768a15978ece
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957179"
---
# <a name="configure-a-policy-to-throttle-the-replication-traffic-on-the-network"></a>ネットワーク上のレプリケーショントラフィックを調整するためのポリシーを構成する

>適用先:Windows Server 2016

ベスト プラクティスおよびスキャンの詳細については、「[ベスト プラクティス アナライザー スキャンの実行とスキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|警告|
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>問題
*レプリケーションで使用できるネットワーク帯域幅の量に制限がない可能性があります。*

## <a name="impact"></a>影響
*ネットワーク帯域幅がレプリケーショントラフィックによって完全に左右され、他の重要なネットワークアクティビティに影響を与える可能性があります。これは、次のポートに影響します。*

\<list of virtual machines>

## <a name="resolution"></a>解決方法
*別の方法を使用してネットワークトラフィックを調整する場合は、これを無視してもかまいません。それ以外の場合は、グループポリシーエディターを使用して、レプリカサーバーの関連ポートへのネットワークトラフィックを制限するポリシーを構成します。*




