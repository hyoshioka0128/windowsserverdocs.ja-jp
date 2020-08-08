---
title: VSS ベースのバックアップ用のゲストオペレーティングシステムを構成して、Hyper-v レプリカのアプリケーション整合性スナップショットを有効にする
description: このベストプラクティスアナライザールールのテキストのオンラインバージョン。
manager: dongill
ms.author: kathydav
ms.topic: article
ms.assetid: 7638e996-d42d-47b8-a670-1e09e7183850
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 5270584b6213ad59ef43c378e5aa7a5dbcc30a4e
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939106"
---
# <a name="configure-guest-operating-systems-for-vss-based-backups-to-enable-application-consistent-snapshots-for-hyper-v-replica"></a>VSS ベースのバックアップ用のゲストオペレーティングシステムを構成して、Hyper-v レプリカのアプリケーション整合性スナップショットを有効にする

>適用先:Windows Server 2016

ベスト プラクティスおよびスキャンの詳細については、「[ベスト プラクティス アナライザー スキャンの実行とスキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。

|プロパティ|詳細|
|-|-|
|**オペレーティング システム**|Windows Server 2016|
|**製品/機能**|Hyper-V|
|**重大度**|エラー|
|**カテゴリ**|構成|

次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。

## <a name="issue"></a>問題
*アプリケーション整合性スナップショットを使用するには、レプリケーションに参加している仮想マシンのゲストオペレーティングシステムで、ボリュームシャドウコピーサービス (VSS) が有効になっていて構成されている必要があります。*

## <a name="impact"></a>影響
*レプリケーション構成でアプリケーション整合性スナップショットが指定されている場合でも、VSS が構成されていないと、Hyper-v はそれらを使用しません。これは、次の仮想マシンに影響します。*

\<list of virtual machines>

## <a name="resolution"></a>解決方法
*仮想マシン接続を使用すると、仮想マシンで統合サービスをインストールできます。*



