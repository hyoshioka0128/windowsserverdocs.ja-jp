---
title: Windows 管理センターからサーバーを監視し、Azure Monitor でアラートを構成する
description: Windows 管理センター (プロジェクトホノルル) は Azure Monitor と統合されます
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 03/24/2019
ms.openlocfilehash: d6c18e3c4ef052b2e2d274f491762d8e31de4758
ms.sourcegitcommit: c40c29683d25ed75b439451d7fa8eda9d8d9e441
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85833315"
---
# <a name="monitor-servers-and-configure-alerts-with-azure-monitor-from-windows-admin-center"></a>Windows 管理センターからサーバーを監視し、Azure Monitor でアラートを構成する

[Azure と Windows 管理センターとの統合の詳細については、こちらを参照してください。](../plan/azure-integration-options.md)

[Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview)は、オンプレミスとクラウドの両方の Windows サーバーと vm を含むさまざまなリソースからテレメトリを収集、分析、および処理するソリューションです。 この記事では、Azure Vm やその他の Azure リソースからデータをプル Azure Monitor ますが、この記事では、Azure Monitor がオンプレミスのサーバーと Vm (特に Windows 管理センター) でどのように機能するかについて重点的に説明します。 Azure Monitor を使用して、ハイパー収束クラスターに関する電子メールアラートを取得する方法については、 [Azure Monitor を使用したヘルスサービスエラーに](https://docs.microsoft.com/windows-server/storage/storage-spaces/configure-azure-monitor)関する電子メールの送信に関するページを参照してください。

## <a name="how-does-azure-monitor-work"></a>Azure Monitor のしくみ
![](../media/azure-monitor-diagram.png)オンプレミスの Windows server から生成された img データは、Azure Monitor の Log Analytics ワークスペースで収集されます。 ワークスペース内では、さまざまな監視ソリューション (特定のシナリオに関する分析情報を示す一連のロジック) を有効にすることができます。 たとえば、Azure Update Management、Azure Security Center、Azure Monitor for VMs はすべて、ワークスペース内で有効にできる監視ソリューションです。 

Log Analytics ワークスペースで監視ソリューションを有効にすると、そのワークスペースに報告を行うすべてのサーバーが、そのソリューションに関連するデータの収集を開始します。これにより、このソリューションはワークスペース内のすべてのサーバーに関する分析情報を生成できます。 

オンプレミスのサーバーでテレメトリデータを収集し、Log Analytics ワークスペースにプッシュするには、Azure Monitor に Microsoft Monitoring Agent または MMA をインストールする必要があります。 特定の監視ソリューションではセカンダリ エージェントも必要です。 たとえば、Azure Monitor for VMs は、このソリューションで提供される追加機能のために ServiceMap エージェントにも依存しています。 

Azure Update Management などの一部のソリューションは Azure Automation にも依存しています。これにより、Azure 環境と非 Azure 環境でリソースを一元的に管理できます。 たとえば、Azure Update Management では Azure Automation を使用することで、Azure portal から一元的に、環境内のコンピューター間で更新プログラムのインストールをスケジュール設定し、調整します。


## <a name="how-does-windows-admin-center-enable-you-to-use-azure-monitor"></a>Windows Admin Center で Azure Monitor を使用できるようにする方法

WAC 内から、次の2つの監視ソリューションを有効にすることができます。

- [Azure Update Management](azure-update-management.md) (更新プログラム ツール内)
- Azure Monitor for VMs (サーバーの設定で)、a. k. a Virtual Machines insights

これらのツールのいずれからでも Azure Monitor の使用を開始できます。 以前に Azure Monitor を使用したことがない場合、WAC は Log Analytics ワークスペース (および必要に応じて Azure Automation アカウント) を自動的にプロビジョニングし、ターゲットサーバーに Microsoft Monitoring Agent (MMA) をインストールして構成します。 その後に、対応するソリューションがワークスペースにインストールされます。 

たとえば、Azure Update Management をセットアップするために最初に更新ツールにアクセスした場合、WAC は次のようになります。

1. コンピューターに MMA をインストールする
2. Log Analytics ワークスペースと Azure Automation アカウントを作成します (この場合は Azure Automation アカウントが必要であるため)。
3. 新しく作成されたワークスペースに Update Management ソリューションがインストールされる。

同じサーバーの WAC 内から別の監視ソリューションを追加する場合、WAC は、そのサーバーが接続されている既存のワークスペースにそのソリューションをインストールするだけです。 WAC では、その他の必要なエージェントもインストールされます。

別のサーバーに接続していても (WAC を使用して、または Azure Portal で手動で) Log Analytics ワークスペースを設定している場合は、MMA エージェントをサーバーにインストールして、既存のワークスペースに接続することもできます。 サーバーをワークスペースに接続すると、サーバーは自動的にデータの収集と、そのワークスペースにインストールされているソリューションへの報告を開始します。

## <a name="azure-monitor-for-virtual-machines-aka-virtual-machine-insights"></a>仮想マシン用の Azure Monitor (別名: 仮想マシン分析情報)
>適用対象: Windows 管理センタープレビュー

サーバーの設定で Azure Monitor for VMs を設定すると、Windows 管理センターでは、仮想マシンの洞察とも呼ばれる Azure Monitor for VMs ソリューションが有効になります。 このソリューションでは、サーバーの正常性とイベントの監視、電子メール アラートの作成、環境全体のサーバー パフォーマンスの統合ビューの取得、および特定のサーバーに接続されているアプリ、システム、およびサービスの視覚化を行うことができます。

> [!NOTE]
> 名前にかかわらず、VM insights は、物理サーバーと仮想マシンに対しても機能します。

Azure Monitor の顧客ごとの 1 か月あたり 5 GB の無料データを使用すると、課金されることを心配をせずに、1 台か 2 台のサーバーでこれを試すことができます。 引き続き、環境内のサーバー全体のシステム パフォーマンスの統合ビューの取得など、サーバーを Azure Monitor にオンボードすることによるその他のメリットを見ていきます。

### <a name="set-up-your-server-for-use-with-azure-monitor"></a>**Azure Monitor で使用できるようにサーバーを設定する**

サーバー接続の [概要] ページで、[新規] ボタンをクリックして [アラートの管理] をクリックするか、[サーバーの設定] > [監視とアラート] の順にクリックします。 このページで、[セットアップ] をクリックしてセットアップウィンドウを完了することにより、サーバーを Azure Monitor にオンボードします。 管理センターは、Azure Log Analytics ワークスペースのプロビジョニング、必要なエージェントのインストール、および VM insights ソリューションの構成を行います。 完了すると、サーバーから Azure Monitor にパフォーマンス カウンター データが送信され、Azure portal から、このサーバーに基づいて電子メール アラートを表示および作成できるようになります。

### <a name="create-email-alerts"></a>**電子メールアラートの作成**

サーバーを Azure Monitor にアタッチしたら、[設定 > の監視とアラート] ページ内のインテリジェントなハイパーリンクを使用して、Azure Portal に移動できます。 管理センターでは、自動的にパフォーマンスカウンターが収集されるようになります。そのため、定義済みの多くのクエリのいずれかをカスタマイズしたり、独自のクエリを作成したりして、[新しいアラートを](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-log)簡単に作成できます。

### <a name="get-a-consolidated-view-across-multiple-servers-"></a>* * 複数のサーバー間で統合ビューを取得する * *

Azure Monitor 内の1つの Log Analytics ワークスペースに複数のサーバーをオンボードする場合、Azure Monitor 内の[Virtual Machines Insights ソリューション](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview)から、これらすべてのサーバーの統合ビューを取得できます。  (Azure Monitor の Virtual Machines Insights の [パフォーマンス] タブと [マップ] タブのみがオンプレミスのサーバーで機能します。 [正常性] タブは、Azure Vm でのみ機能します)。Azure portal でこれを表示するには、[Azure Monitor > Virtual Machines ([インサイト] の下) に移動し、[パフォーマンス] または [マップ] タブに移動します。

### <a name="visualize-apps-systems-and-services-connected-to-a-given-server"></a>**特定のサーバーに接続されているアプリ、システム、およびサービスを視覚化する**

管理センターがサーバーを Azure Monitor 内の VM insights ソリューションに配置すると、 [Service Map](https://docs.microsoft.com/azure/azure-monitor/insights/service-map)と呼ばれる機能も利用できるようになります。 この機能によってアプリケーション コンポーネントが自動的に検出され、サービス間の通信がマップされるため、Azure portal から簡単に、サーバー間の接続を詳細に視覚化できます。 これを見つけるには、[Azure portal > Azure Monitor > Virtual Machines ([洞察] の下) に移動し、[マップ] タブに移動します。

> [!NOTE]
> Azure Monitor の Virtual Machines Insights の視覚化は、現在6つのパブリックリージョンで提供されています。  最新情報については、[Azure Monitor for VMs のドキュメント](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-onboard#log-analytics)を参照してください。  前述の Virtual Machines Insights ソリューションで提供されるその他の利点を得るには、サポートされているリージョンのいずれかで Log Analytics ワークスペースをデプロイする必要があります。

## <a name="disabling-monitoring"></a>監視の無効化

Log Analytics ワークスペースからサーバーを完全に切断するには、MMA エージェントをアンインストールします。 これは、このサーバーがデータをワークスペースに送信しなくなり、そのワークスペースにインストールされたすべてのソリューションが、そのサーバーからのデータの収集と処理を行わなくなることを意味します。 ただし、ワークスペース自体には影響しません。そのワークスペースに報告するすべてのリソースが引き続き機能します。 Windows 管理センター内で MMA エージェントをアンインストールするには、サーバーに接続して [**インストールされているアプリ**] にアクセスし、Microsoft Monitoring Agent を見つけて、[**削除**] を選択します。

ワークスペース内の特定のソリューションを無効にする場合は、[Azure portal から監視ソリューションを削除する](https://docs.microsoft.com/azure/azure-monitor/insights/solutions#remove-a-management-solution)必要があります。 監視ソリューションを削除すると、そのソリューションによって作成される分析情報が、そのワークスペースに報告を行う_どのサーバーでも_生成されなくなります。 たとえば、Azure Monitor for VMs ソリューションをアンインストールしても、マイワークスペースに接続されているどのコンピューターからも VM またはサーバーのパフォーマンスに関する洞察は得られなくなります。
