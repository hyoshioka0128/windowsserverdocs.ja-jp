---
title: システム Insights の概要
description: システム Insights は、Windows Server 2019 で新しい予測分析機能です。 システム Insights 予測機能 - - 機械学習モデルによって各バックアップがローカルでのパフォーマンス カウンターと、サーバーに機能しており、減少するための洞察を提供する、イベントなどの Windows Server システム データを分析します運用の費用は事後対応的に展開の問題の管理に関連します。
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
ms.openlocfilehash: ca471e5e747c7aaa369f5725290e16deab7a6660
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887243"
---
# <a name="system-insights-overview"></a>システム Insights の概要

>適用先:Windows Server 2019

システム Insights は、Windows Server 2019 で新しい予測分析機能です。 システム Insights 予測機能 - - 機械学習モデルによって各バックアップがローカルでのパフォーマンス カウンターと、サーバーに機能しており、減少するための洞察を提供する、イベントなどの Windows Server システム データを分析します運用の費用は事後対応的に展開の問題の管理に関連します。 

Windows Server の 2019 システム Insights は、容量の予測、コンピューティング、ネットワーク、および、前の使用パターンに基づく記憶域のリソースが将来の予測に重点を置いた 4 つの既定の機能に同梱されています。 Insights のシステムにも付属、[拡張性のあるインフラストラクチャ](adding-and-developing-capabilities.md)マイクロソフトとサード パーティを追加できるように新しい予測機能をシステム Insights にオペレーティング システムを更新することがなく、します。 

Insights のシステムを管理するには直観的で[Windows Admin Center](https://docs.microsoft.com/windows-server/manage/windows-admin-center/overview)拡張機能または[PowerShell から直接](https://aka.ms/SystemInsightsPowerShell)Insights のシステムでは、各予測機能を構成することができます配置のニーズに従って個別にします。 すべての予測結果を使用することができるイベント ログに発行されます[Azure Monitor](https://azure.microsoft.com/services/monitor/)または[System Center Operations Manager](https://docs.microsoft.com/system-center/scom/welcome?view=sc-om-1807)簡単に集計され、マシンのグループ間で予測を参照してください。

![機能の予測、予測をプロットするグラフを CPU 容量を示す、Windows Admin Center でシステム Insights 拡張機能](media/cpu-forecast-2.png)

## <a name="local-functionality"></a>ローカルの機能
システム Insights は、Windows Server で完全にローカルで実行されます。 Windows Server 2019 で導入された新しい機能を使用して、すべてのデータを収集、永続化、および分析直接コンピューターに、クラウドの接続なしの予測分析機能を実現することができます。

コンピューターに、システムのデータが格納されているし、クラウドでの再トレーニングを必要としない予測機能によってこのデータを分析します。 Insights のシステム、コンピューターにデータを保持し、予測分析機能からメリットを得ることができます。 

## <a name="get-started"></a>作業開始

<iframe src="https://www.youtube-nocookie.com/embed/AJxQkx5WSaA" width="560" height="315" allowfullscreen></iframe>

>[!TIP]
>開始して、自信を持ってシステム Insights の管理に必要な情報については、以下のショート ビデオをご覧ください。[10 分後にシステム Insights の概要](https://blogs.technet.microsoft.com/filecab/2018/07/24/getting-started-with-system-insights-in-10-minutes/)

### <a name="requirements"></a>必要条件
システム Insights は、Windows Server 2019 インスタンスで使用できます。 これは、任意のハイパーバイザー上で、任意のクラウド、ホストとゲストの両方のマシンで実行されます。

### <a name="install-system-insights"></a>Insights のシステムをインストールします。
>[!IMPORTANT]
>最大で、1 年分のデータをローカル ストアとシステム Insights の収集。 オペレーティング システムをアップグレードするときに、データを保持したい場合**インプレース アップグレードを使用するかどうかを確認**します。

#### <a name="install-the-feature"></a>機能をインストールします。
Windows Admin Center 内で、拡張機能を使用してインサイトをシステムをインストールすることができます。

![システム Insights 拡張機能の 1 日 0 エクスペリエンス。](media/day-0-2.png)

追加することで、システム Insights サーバー マネージャーから直接をインストールすることも、**システム Insights**機能、または PowerShell を使用しています。

```PowerShell
Add-WindowsFeature System-Insights -IncludeManagementTools
```

## <a name="provide-feedback"></a>フィードバックの提供
この機能の向上にご協力にお客様からのフィードバックを歓迎します。 次のチャネルを使用して、フィードバックを送信できます。
- **フィードバック Hub**:Windows 10 フィードバック Hub ツールを使用して、バグやフィードバックを提出します。 これを行うときに次の項目を指定してください。
    - **カテゴリ**:Server 
    - **Subcategory**:システム インサイト
- **UserVoice**:機能要求を送信、 [UserVoice ページ](https://windowsserver.uservoice.com/forums/295071-management-tools)します。 重要な投稿項目に、同僚と共有します。
- **電子メール**:プライベート機能チームにフィードバックを送信する場合は、電子メールをお送りsystem-insights-feed@microsoft.comします。 私たちも可能性がありますを要求するフィードバック ハブまたは UserVoice を使用することに注意してください。

## <a name="see-also"></a>関連項目
システム Insights に関する詳細については、するには、次のリソースを使用します。

- [機能の理解](understanding-capabilities.md)
- [機能を管理します。](managing-capabilities.md)
- [追加して、機能の開発](adding-and-developing-capabilities.md)
- [システム Insights に関する FAQ](faq.md)