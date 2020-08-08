---
title: 証明書ベースの認証が構成されていますが、指定された証明書がレプリカサーバーまたはフェールオーバークラスターノードにインストールされていません
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 4cabbce3-9367-4ddc-a108-1e5e1ab2bcff
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 8205ea267750e3fec78a756da00b0bd063ed8baf
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87948515"
---
# <a name="certificate-based-authentication-is-configured-but-the-specified-certificate-is-not-installed-on-the-replica-server-or-failover-cluster-nodes"></a>証明書ベースの認証が構成されていますが、指定された証明書がレプリカサーバーまたはフェールオーバークラスターノードにインストールされていません

>適用先:Windows Server 2016



*ベストプラクティスとスキャンの詳細については、「ベストプラクティスアナライザー」を参照してください* [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786)。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|エラー|
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>問題

*証明書ベースのレプリケーションを提供するために Hyper-v レプリカが構成されているセキュリティ証明書が、レプリカサーバー (またはフェールオーバークラスターノード) にインストールされていません。*

## <a name="impact"></a>影響

*クラスターのフェールオーバーが発生した場合、または別のノードに移動した場合、新しいノードに適切な証明書がインストールされていないと、Hyper-v レプリケーションが一時停止します。これは、次のノードに影響します。*

\<list of nodes>

## <a name="resolution"></a>解決方法

*構成した証明書をレプリカサーバー (およびフェールオーバークラスター内のすべての関連ノード (存在する場合) にインストールします。*



