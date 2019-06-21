---
title: サーバーを監視し、Windows Admin Center からの Azure Monitor のアラートを構成します。
description: Windows Admin Center (プロジェクト ホノルル) は、Azure Monitor の統合します。
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 03/24/2019
ms.openlocfilehash: 8f7baba465071cc95ab7492037ff25c5cd58219e
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280434"
---
# <a name="monitor-servers-and-configure-alerts-with-azure-monitor-from-windows-admin-center"></a>サーバーを監視し、Windows Admin Center からの Azure Monitor のアラートを構成します。

[Azure Windows Admin Center との統合について説明します。](../plan/azure-integration-options.md)

[Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview)は収集、分析、およびさまざまなリソース (Windows サーバーとオンプレミスの Vm など) とクラウドからのテレメトリに作用するソリューションです。 Azure Monitor では、Azure Vm、およびその他の Azure リソースからデータをプル、ただし、この記事では、オンプレミス サーバーと Windows Admin Center で具体的には、Vm での Azure Monitor のしくみについて説明します。 Azure Monitor を使用して、ハイパーコンバージド クラスターに関する電子メール アラートを取得する方法について知りたい場合について[Azure Monitor を使用して、ヘルス サービスの障害の電子メールを送信する](https://docs.microsoft.com/windows-server/storage/storage-spaces/configure-azure-monitor)します。

## <a name="how-does-azure-monitor-work"></a>Azure Monitor のしくみ
![img](../media/azure-monitor-diagram.png) Azure Monitor での Log Analytics ワークスペースで、オンプレミスの Windows サーバーから生成されたデータを収集します。 ワークスペース内のさまざまな監視ソリューションを有効にできます: 特定のシナリオの洞察を提供するロジックを設定します。 たとえば、Azure の Update Management、Azure Security Center では、および Vm の Azure Monitor は、ワークスペース内で有効にできるすべての監視ソリューションです。 

Log Analytics ワークスペースで監視ソリューションを有効にすると、すべてのサーバーに報告するそのワークスペースはデータ収集を開始、そのソリューションに関連するソリューションがワークスペースに insights のすべてのサーバーを生成できるようにします。 

オンプレミス サーバーでテレメトリ データを収集する Log Analytics ワークスペースにプッシュすることは、Azure Monitor には、Microsoft Monitoring Agent、または、MMA のインストールが必要です。 特定の監視ソリューションには、セカンダリのエージェントも必要です。 たとえば、Vm の Azure Monitor は、このソリューションを提供する追加の機能の ServiceMap エージェントによっても異なります。 

Azure の Update Management など、一部のソリューションは、Azure Automation は、Azure と Azure 以外の環境全体でリソースを一元的に管理することができますにも依存します。 たとえば、Azure 更新の管理は、スケジュール、Azure portal から一元的に、環境内のコンピューター間で更新プログラムのインストールを調整する Azure Automation を使用します。


## <a name="how-does-windows-admin-center-enable-you-to-use-azure-monitor"></a>方法は Windows Admin Center を有効にする Azure Monitor を使用することですか。

WAC、内から 2 つの監視ソリューションを有効ことができます。

- [Azure の Update Management](azure-update-management.md) (で更新プログラム ツール)
- (サーバーの設定) での Vm の azure Monitor、別名、仮想マシンの洞察

これらのツールのいずれかの Azure Monitor を使用することを開始できます。 Log Analytics ワークスペース (と Azure Automation アカウントを必要に応じて)、WAC が自動的にプロビジョニングする前に Azure Monitor を初めて使用する場合、インストールして、対象サーバーで Microsoft Monitoring Agent (MMA) を構成します。 ワークスペースに対応するソリューションがインストールされます。 

たとえば、Azure の更新プログラム管理をセットアップする更新プログラム ツールに最初に移動する場合、WAC には。

1. コンピューターで、MMA をインストールします。
2. (Azure Automation アカウントはここで必要) のために、Log Analytics ワークスペースと Azure Automation アカウントを作成します。
3. 新しく作成されたワークスペースで、更新プログラム管理ソリューションをインストールします。

同じサーバー上の WAC 内から他の監視ソリューションを追加するには、WAC はそのサーバーが接続されている既存のワークスペースにそのソリューションをインストールだけです。 WAC は、他の必要なエージェントをさらにインストールされます。

別のサーバーに接続 (WAC 経由または Azure ポータルで手動でか) Log Analytics ワークスペースのセットアップが既にある場合は、サーバー上の MMA エージェントをインストールし、既存のワークスペースに接続することもできます。 サーバーをワークスペースに接続するときにデータを収集して、そのワークスペースにインストールされているソリューションにレポートが自動的に開始します。

## <a name="azure-monitor-for-virtual-machines-aka-virtual-machine-insights"></a>Azure 仮想マシン (ルール サブタイプ) の監視します。 仮想マシン insights)
>適用先:Windows Admin Center Preview

構成するときに Azure Monitor の Vm のサーバーの設定で、Windows Admin Center Vm ソリューションでは、仮想マシン insights とも呼ばれる Azure モニタを有効にします。 このソリューションを使用すると、サーバーの正常性とイベントを監視、電子メール アラートを作成、環境全体のサーバーのパフォーマンスの統合ビューを取得、およびアプリ、システム、および特定のサーバーに接続してサービスを視覚化できます。

> [!NOTE]
> その名前にもかかわらず VM insights は、仮想マシンと物理サーバーは機能します。

5 GB のデータ/月/顧客の許容量を無料の Azure Monitor の試すことができます簡単にこれをサーバーまたは課金される心配をせずに 2 つです。 興味のあるサーバーのオンボードの特典を参照してくださいに Azure Monitor など、環境内のサーバー間でシステムのパフォーマンスの統合ビューを取得します。

### <a name="set-up-your-server-for-use-with-azure-monitor"></a>**Azure Monitor で使用するため、サーバーを設定します。**

サーバー接続の [概要] ページから「アラートの管理」の新しいボタンをクリックします。 または、サーバーの設定に移動 > 監視とアラート。 内でのこのページで、オンボードをクリックして Azure Monitor をサーバーの設定、設定 ウィンドウの操作を完了します。 管理センター、Azure Log Analytics ワークスペースのプロビジョニングの必要なエージェントのインストールと構成は VM の insights ソリューションのことを確認できます。 完了すると、サーバーに送信されますパフォーマンス カウンター データ Azure Monitor を表示し、Azure portal からこのサーバーに基づく電子メール アラートを作成できるようにすること。

### <a name="create-email-alerts"></a>**電子メール アラートを作成します。**

設定内で、インテリジェントなハイパーリンクを使用するには、サーバーを Azure Monitor にアタッチした後 > 監視とアラートのページで、Azure Portal に移動します。 管理センターは、簡単にできるように自動的に収集するパフォーマンス カウンターを有効[新しいアラート作成](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-log)を多数の事前定義されたクエリのいずれかをカスタマイズするか独自に作成します。

### <a name="get-a-consolidated-view-across-multiple-servers-"></a>\* * 複数のサーバーで統合ビューを取得する * *

場合するオンボード Azure Monitor 内の 1 つの Log Analytics ワークスペースに複数のサーバーを取得できますからこれらすべてのサーバーの統合ビュー、 [Virtual Machines Insights ソリューション](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview)Azure Monitor 内。  (Azure Monitor の仮想マシンの Insights のパフォーマンスとマップのタブのみが、オンプレミス サーバー – Azure Vm でのみ正常性] タブの機能で動作するに注意してください)。Azure portal では、これを表示するには、Azure Monitor に移動 > (Insights)、[仮想マシンを"Performance"または"Maps"タブに移動します。

### <a name="visualize-apps-systems-and-services-connected-to-a-given-server"></a>**アプリ、システム、および特定のサーバーに接続してサービスを視覚化します。**

ときに管理センターのオンボード、サーバーを Azure Monitor 内の VM insights ソリューションに、これも点灯させると呼ばれる機能[Service Map](https://docs.microsoft.com/azure/azure-monitor/insights/service-map)します。 この機能は自動的にアプリケーション コンポーネントを検出し、Azure portal から詳細な情報を持つサーバー間の接続を簡単に視覚化できるように、サービス間の通信をマップします。 これを検索するには、Azure portal に移動して > Azure Monitor > (Insights) の下の仮想マシンと"Maps" タブに移動します。

> [!NOTE]
> Azure Monitor の仮想マシンの Insights の視覚エフェクトが現在の 6 つのパブリック リージョンで提供されます。  最新情報については、確認、[ドキュメントについては Vm の Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-onboard#log-analytics)します。  上記で説明した仮想マシン Insights ソリューションによって提供される追加の利点を得るためのサポートされているリージョンのいずれかで Log Analytics ワークスペースをデプロイする必要があります。

## <a name="disabling-monitoring"></a>監視の無効化

Log Analytics ワークスペースからサーバーを完全に切断するには、するには、MMA エージェントをアンインストールします。 つまり、このサーバーは、ワークスペースにデータを送信できなく、およびそのワークスペースにインストールされているソリューションが不要になったすべて収集し、そのサーバーからデータを処理します。 ただし、これがそのワークスペースにレポート リソースがこれを行うには引き続きすべて自体 – ワークスペースは影響しません。 WAC 内で、MMA エージェントをアンインストールするには、アプリと機能、するには、Microsoft Monitoring Agent を検索し、[アンインストール] をクリックを移動します。

ワークスペース内の特定のソリューションをオフにするには、する必要があります[監視ソリューションを Azure portal から削除](https://docs.microsoft.com/azure/azure-monitor/insights/solutions#remove-a-management-solution)します。 監視ソリューションを削除することを意味のソリューションで作成される insights のアプリケーションが生成される不要になったこと_任意_のサーバーがそのワークスペースに報告します。 たとえば、Vm ソリューションの Azure Monitor をアンインストールする場合から個人用ワークスペースに接続されているマシンのいずれかの VM またはサーバーのパフォーマンスに関する洞察されなく表示は。