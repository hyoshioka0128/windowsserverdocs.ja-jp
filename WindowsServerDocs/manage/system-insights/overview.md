---
title: システム インサイトの概要
description: System Insights は、Windows Server 2019 の新しい予測分析機能です。 機械学習モデルによって支えられている System Insights の予測機能は、パフォーマンスカウンターやイベントなどの Windows Server システムデータをローカルで分析して、サーバーの機能に関する洞察を提供し、デプロイの問題をリアクティブに管理するための運用コストの削減に役立ちます。
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 5/23/2018
ms.openlocfilehash: 9bedd593cdd26b67e6e16ddea73955bb926a87a5
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996675"
---
# <a name="system-insights-overview"></a>システム インサイトの概要

>適用先:Windows Server 2019

System Insights は、Windows Server 2019 の新しい予測分析機能です。 機械学習モデルによって支えられている System Insights の予測機能は、パフォーマンスカウンターやイベントなどの Windows Server システムデータをローカルで分析して、サーバーの機能に関する洞察を提供し、デプロイの問題をリアクティブに管理するための運用コストの削減に役立ちます。

Windows Server 2019 では、容量予測に焦点を合わせた4つの既定の機能が搭載されており、以前の使用パターンに基づいて、コンピューティング、ネットワーク、ストレージの将来のリソースが予測されます。 また、system Insights には[拡張可能なインフラストラクチャ](adding-and-developing-capabilities.md)が付属しているため、Microsoft とサードパーティはオペレーティングシステムを更新しなくても、新しい予測機能を System Insights に追加できます。

System Insights は、直感的な[Windows 管理センター](../windows-admin-center/overview.md)の拡張機能または[PowerShell を使用](https://aka.ms/SystemInsightsPowerShell)して直接管理できます。また、system insights では、デプロイのニーズに応じて各予測機能を個別に構成できます。 すべての予測結果がイベントログに発行されます。これにより、 [Azure Monitor](https://azure.microsoft.com/services/monitor/)または[System Center Operations Manager](/system-center/scom/welcome?view=sc-om-1807)を使用して、コンピューターグループ全体の予測を簡単に集計および表示できます。

![Windows 管理センターの System Insights 拡張機能。予測をプロットしたグラフで CPU 容量予測機能を表示](media/cpu-forecast-2.png)

## <a name="local-functionality"></a>ローカル機能
System Insights は、Windows Server 上で完全にローカルに実行されます。 Windows Server 2019 で導入された新しい機能を使用すると、すべてのデータがコンピューター上で直接収集、保存、および分析されるため、クラウド接続なしで予測分析機能を実現できます。

システムデータはコンピューターに保存され、このデータはクラウドでの再トレーニングを必要としない予測機能によって分析されます。 System Insights を使用すると、コンピューター上のデータを保持しながら、予測分析機能を活用できます。

## <a name="get-started"></a>はじめに

<iframe src=https://www.youtube-nocookie.com/embed/AJxQkx5WSaA width=560 height=315 allowfullscreen></iframe>

>[!TIP]
>これらの短いビデオをご覧になり、System Insights の使用を開始し、自信を持って管理するために必要な情報をご確認ください。 [10 分で System insights を使ってみる](https://blogs.technet.microsoft.com/filecab/2018/07/24/getting-started-with-system-insights-in-10-minutes/)

### <a name="requirements"></a>要件
System Insights は、任意の Windows Server 2019 インスタンスで使用できます。 ホストとゲストの両方のコンピューター、すべてのハイパーバイザー、および任意のクラウドで実行されます。

### <a name="install-system-insights"></a>System Insights のインストール
>[!IMPORTANT]
>System Insights は、最大で1年分のデータをローカルに収集して保存します。 オペレーティングシステムをアップグレードするときにデータを保持する場合は、**インプレースアップグレードを使用する**ようにしてください。

#### <a name="install-the-feature"></a>機能のインストール
Windows 管理センター内の拡張機能を使用して、System Insights をインストールできます。

![System Insights 拡張機能の日0エクスペリエンス。](media/day-0-2.png)

System insights は、**システムインサイト**機能を追加するか、PowerShell を使用して、サーバーマネージャーから直接インストールすることもできます。

```PowerShell
Add-WindowsFeature System-Insights -IncludeManagementTools
```

## <a name="provide-feedback"></a>フィードバックの提供
この機能を改善するために、皆様からのフィードバックをお寄せください。 次のチャネルを使用して、フィードバックを送信できます。
- **フィードバックハブ**: Windows 10 のフィードバックハブツールを使用して、バグやフィードバックをファイルに登録します。 その場合は、次のように指定します。
    - **カテゴリ**: サーバー
    - **サブカテゴリ**: System Insights
- **Uservoice**: [uservoice ページ](https://windowsserver.uservoice.com/forums/295071-management-tools)から機能要求を送信します。 自分にとって重要なアップ投票項目に同僚と共有します。
- **電子メール**: 機能チームにプライベートでフィードバックを送信する場合は、に電子メールを送信し system-insights-feed@microsoft.com ます。 まだフィードバックハブまたは UserVoice の使用を要求される場合があることに注意してください。

## <a name="additional-references"></a>その他の参照情報
System Insights の詳細については、次のリソースを参照してください。

- [機能について](understanding-capabilities.md)
- [管理機能](managing-capabilities.md)
- [機能の追加と開発](adding-and-developing-capabilities.md)
- [System Insights の FAQ](faq.md)