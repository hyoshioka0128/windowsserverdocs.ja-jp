---
title: システム Insights に関する FAQ
description: システム Insights に関する FAQ
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: system-insights
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ''
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 5/23/2018
ms.openlocfilehash: 13767e1336d1ff729d1fbbe6cae3ed57d68cefc4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851063"
---
# <a name="system-insights-faq"></a>システム Insights に関する FAQ

>適用先:Windows Server 2019

## <a name="how-can-you-use-system-insights-with-azure-monitor-or-system-center-operations-manager"></a>Azure Monitor、System Center Operations Manager でシステム Insights を使用するにはどうできますか。

[Azure Monitor](https://azure.microsoft.com/services/monitor/)と[System Center Operations Manager](https://docs.microsoft.com/system-center/scom/welcome?view=sc-om-1807)インフラストラクチャを管理するために、デプロイ全体にわたる操作に関する情報を提供します。 これに対し、システムの Insights は、ローカルの予測分析機能を紹介する Windows Server 機能です。 同時に、システム Insights と Azure Monitor または SCOM 役立つデバイスの母集団全体の予測のサーフェスします。

 Azure Monitor または SCOM は、Insights のシステム イベント ログには、各予測の結果を出力するようシステム Insights によって作成されたイベントをキーことができます。 これらのコンピューターに固有の予測を画面のサーバー インスタンスのグループ全体でこれらの予測の統一されたビューを有効にすると、Windows サーバーのフリート間で、ことができます。 
 
 各予測のチャネルとイベントの Id を参照してください。[ここ](https://docs.microsoft.com/windows-server/manage/system-insights/managing-capabilities#retrieving-capability-results)します。

## <a name="how-does-system-insights-relate-to-windows-ml"></a>Windows の ML にはシステム Insights はどのように関連しますか。

[Windows の ML](https://docs.microsoft.com/windows/uwp/machine-learning/)は開発者がインポートおよび Windows デバイスで事前トレーニング済みの機械学習モデルをスコア付けすることができるプラットフォームです。 ハードウェア アクセラレーションにより、これらのモデルを利用し、ローカルで評価できます。 

システム Insights は、PowerShell と Windows Admin Center の統合を含む、完全な管理エクスペリエンスと共にローカルの予測機能を提供する Windows Server 2019 の機能です。 

## <a name="can-i-use-system-insights-for-my-cluster"></a>私のクラスターのシステム Insights を使用できますか。 

[はい]。 システム Insights できますを別個に実行システム Insights の予測使用率の既定の動作と各個々 のフェールオーバー クラスター ノードでローカル ストレージ、ボリューム、CPU、およびネットワークの間で。 **クラスター化された記憶域を予測することもできます**ので、記憶域の予測機能がクラスター化されたボリュームとストレージの使用量を予測します。 

Windows Admin Center や PowerShell でこれらの設定を管理して、この機能の詳細情報が使用可能な[ここ](https://blogs.technet.microsoft.com/filecab/2018/10/03/using-system-insights-to-forecast-clustered-storage-usage/)します。
 

## <a name="how-expensive-is-it-to-run-the-default-capabilities"></a>既定の機能を実行するようにはコストでしょうか。

既定の各機能は、実行コストが高くはありません。 各機能より多くのデータを収集するように、通常はわずか数秒で完了する必要がありますを実行するがかかります。 

## <a name="see-also"></a>関連項目
システム Insights に関する詳細については、するには、次のリソースを使用します。

- [システム Insights の概要](overview.md)
- [機能の理解](understanding-capabilities.md)
- [機能を管理します。](managing-capabilities.md)
- [追加して、機能の開発](adding-and-developing-capabilities.md)
