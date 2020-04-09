---
title: System Insights の FAQ
description: System Insights の FAQ
ms.prod: windows-server
ms.technology: system-insights
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 5/23/2018
ms.openlocfilehash: 9d6ddd682def579796089266065be7d39ce361d1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856255"
---
# <a name="system-insights-faq"></a>System Insights の FAQ

>適用対象: Windows Server 2019

## <a name="how-can-you-use-system-insights-with-azure-monitor-or-system-center-operations-manager"></a>Azure Monitor または System Center Operations Manager で System Insights を使用するにはどうすればよいですか。

[Azure Monitor](https://azure.microsoft.com/services/monitor/)と[System Center Operations Manager](https://docs.microsoft.com/system-center/scom/welcome?view=sc-om-1807)により、インフラストラクチャの管理を支援するために、展開全体で運用情報を得ることができます。 これに対して、System Insights は、ローカルの予測分析機能を導入する Windows Server の機能です。 System Insights と Azure Monitor または SCOM を一緒に使用することで、デバイスの作成に関する予測を行うことができます。

 System Insights では、各予測の結果がイベントログに出力されるため、Azure Monitor または SCOM では、System Insights によって作成されたイベントにキーを渡すことができます。 これらのコンピューターでは、これらのコンピューター固有の予測を Windows サーバーに分散させることができるため、サーバーインスタンスのグループ全体でこれらの予測を統合して表示することができます。 
 
 各予測のチャネル Id とイベント Id について[は、こちら](https://docs.microsoft.com/windows-server/manage/system-insights/managing-capabilities#retrieving-capability-results)を参照してください。

## <a name="how-does-system-insights-relate-to-windows-ml"></a>System Insights は Windows ML とどのように関連していますか。

[WINDOWS ML](https://docs.microsoft.com/windows/uwp/machine-learning/)は、開発者が windows デバイスで事前トレーニング済みの機械学習モデルをインポートしてスコア付けできるプラットフォームです。 これらのモデルは、ハードウェアアクセラレーションの恩恵を受け、ローカルでスコア付けすることができます。 

System Insights は、Windows Server 2019 の機能の1つで、PowerShell と Windows 管理センターの統合を含む完全な管理エクスペリエンスと共にローカルの予測機能を提供します。 

## <a name="can-i-use-system-insights-for-my-cluster"></a>クラスターに System Insights を使用できますか。 

はい。 System Insights は、個々のフェールオーバークラスターノードで個別に実行できます。また、ローカルストレージ、ボリューム、CPU、およびネットワークにわたる System Insights の予測使用率の既定の動作も可能です。 **クラスター化された記憶域の予測を有効にすることもでき**ます。これにより、記憶域の予測機能は、クラスター化されたボリュームと記憶域の使用量を予測します。 

これらの設定は、Windows 管理センターまたは PowerShell で管理できます。また、この機能の詳細については、[こちら](https://blogs.technet.microsoft.com/filecab/2018/10/03/using-system-insights-to-forecast-clustered-storage-usage/)を参照してください。
 

## <a name="how-expensive-is-it-to-run-the-default-capabilities"></a>既定の機能を実行するには、どのくらいのコストがかかりますか。

既定の機能の実行は安価です。 各機能は、より多くのデータを収集するときに実行に時間がかかりますが、通常は数秒で完了する必要があります。 

## <a name="see-also"></a>参照
System Insights の詳細については、次のリソースを参照してください。

- [System Insights の概要](overview.md)
- [機能について](understanding-capabilities.md)
- [管理機能](managing-capabilities.md)
- [機能の追加と開発](adding-and-developing-capabilities.md)
