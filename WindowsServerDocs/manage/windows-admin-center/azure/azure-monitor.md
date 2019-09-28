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
ms.openlocfilehash: 28108a79bbdc654f6437a698c158a3f74d4423ba
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407016"
---
# <a name="monitor-servers-and-configure-alerts-with-azure-monitor-from-windows-admin-center"></a>Windows 管理センターからサーバーを監視し、Azure Monitor でアラートを構成する

[Azure と Windows 管理センターとの統合の詳細については、こちらを参照してください。](../plan/azure-integration-options.md)

[Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/overview)は、オンプレミスとクラウドの両方の Windows サーバーと vm を含むさまざまなリソースからテレメトリを収集、分析、および処理するソリューションです。 この記事では、Azure Vm やその他の Azure リソースからデータをプル Azure Monitor ますが、この記事では、Azure Monitor がオンプレミスのサーバーと Vm (特に Windows 管理センター) でどのように機能するかについて重点的に説明します。 Azure Monitor を使用して、ハイパー収束クラスターに関する電子メールアラートを取得する方法については、 [Azure Monitor を使用したヘルスサービスエラーに](https://docs.microsoft.com/windows-server/storage/storage-spaces/configure-azure-monitor)関する電子メールの送信に関するページを参照してください。

## <a name="how-does-azure-monitor-work"></a>Azure Monitor はどのように動作しますか。
オンプレミスの Windows Server から生成された @no__t 0img @ no__t のデータは、Azure Monitor の Log Analytics ワークスペースで収集されます。 ワークスペース内では、さまざまな監視ソリューション (特定のシナリオに関する洞察を提供する一連のロジック) を有効にすることができます。 たとえば、Azure Update Management、Azure Security Center、Azure Monitor for VMs は、ワークスペース内で有効にできるすべての監視ソリューションです。 

Log Analytics ワークスペースで監視ソリューションを有効にすると、そのワークスペースに報告するすべてのサーバーが、そのソリューションに関連するデータの収集を開始します。これにより、ソリューションはワークスペース内のすべてのサーバーについての洞察を得ることができます。 

オンプレミスのサーバーでテレメトリデータを収集し、Log Analytics ワークスペースにプッシュするには、Azure Monitor に Microsoft Monitoring Agent または MMA をインストールする必要があります。 特定の監視ソリューションにも、セカンダリエージェントが必要です。 たとえば、Azure Monitor for VMs は、このソリューションによって提供される追加機能のために、ServiceMap エージェントにも依存します。 

Azure Update Management などの一部のソリューションは Azure Automation にも依存しているため、Azure 環境と非 Azure 環境でリソースを一元的に管理できます。 たとえば、Azure Update Management は Azure Automation を使用して、環境内のコンピューター間での更新プログラムのインストールを、Azure portal から一元的にスケジュール設定し、調整します。


## <a name="how-does-windows-admin-center-enable-you-to-use-azure-monitor"></a>Windows 管理センターで Azure Monitor を使用するにはどうすればよいですか。

WAC 内から、次の2つの監視ソリューションを有効にすることができます。

- [Azure Update Management](azure-update-management.md) (更新プログラムツール)
- Azure Monitor for VMs (サーバーの設定で)、a. k. a Virtual Machines insights

これらのツールのいずれからでも Azure Monitor の使用を開始できます。 以前に Azure Monitor を使用したことがない場合、WAC は Log Analytics ワークスペース (および必要に応じて Azure Automation アカウント) を自動的にプロビジョニングし、ターゲットサーバーに Microsoft Monitoring Agent (MMA) をインストールして構成します。 その後、対応するソリューションがワークスペースにインストールされます。 

たとえば、Azure Update Management をセットアップするために最初に更新ツールにアクセスした場合、WAC は次のようになります。

1. コンピューターに MMA をインストールする
2. Log Analytics ワークスペースと Azure Automation アカウントを作成します (この場合は Azure Automation アカウントが必要であるため)。
3. 新しく作成したワークスペースに Update Management ソリューションをインストールします。

同じサーバーの WAC 内から別の監視ソリューションを追加する場合、WAC は、そのサーバーが接続されている既存のワークスペースにそのソリューションをインストールするだけです。 WAC では、その他の必要なエージェントもインストールされます。

別のサーバーに接続していても (WAC を使用して、または Azure Portal で手動で) Log Analytics ワークスペースを設定している場合は、MMA エージェントをサーバーにインストールして、既存のワークスペースに接続することもできます。 サーバーをワークスペースに接続すると、そのワークスペースにインストールされているソリューションへのデータの収集とレポートが自動的に開始されます。

## <a name="azure-monitor-for-virtual-machines-aka-virtual-machine-insights"></a>仮想マシンの Azure Monitor ( Virtual Machine insights)
>適用先:Windows Admin Center Preview

サーバーの設定で Azure Monitor for VMs を設定すると、Windows 管理センターでは、仮想マシンの洞察とも呼ばれる Azure Monitor for VMs ソリューションが有効になります。 このソリューションでは、サーバーの状態とイベントの監視、電子メールアラートの作成、環境全体でのサーバーパフォーマンスの統合ビューの取得、および特定のサーバーに接続されているアプリ、システム、およびサービスの視覚化を行うことができます。

> [!NOTE]
> 名前にかかわらず、VM insights は、物理サーバーと仮想マシンに対しても機能します。

無料の 5 GB のデータ/月/顧客の許容 Azure Monitor では、課金されることを心配することなく、サーバーまたは2に対して簡単に試すことができます。 サーバーを Azure Monitor にオンボードすることのその他のメリットについては、環境内のサーバー全体でのシステムパフォーマンスの統合ビューの取得などを参照してください。

### <a name="set-up-your-server-for-use-with-azure-monitor"></a>**Azure Monitor で使用できるようにサーバーを設定する**

サーバー接続の [概要] ページで、[新規] ボタンをクリックして [アラートの管理] をクリックするか、[サーバーの設定] > [監視とアラート] の順にクリックします。 このページで、[セットアップ] をクリックしてセットアップウィンドウを完了することにより、サーバーを Azure Monitor にオンボードします。 管理センターは、Azure Log Analytics ワークスペースのプロビジョニング、必要なエージェントのインストール、および VM insights ソリューションの構成を行います。 完了すると、サーバーから Azure Monitor にパフォーマンスカウンターデータが送信され、Azure portal から、このサーバーに基づいて電子メールアラートを表示および作成できるようになります。

### <a name="create-email-alerts"></a>**電子メールアラートの作成**

サーバーを Azure Monitor にアタッチしたら、[設定 > の監視とアラート] ページ内のインテリジェントなハイパーリンクを使用して、Azure Portal に移動できます。 管理センターでは、自動的にパフォーマンスカウンターが収集されるようになります。そのため、定義済みの多くのクエリのいずれかをカスタマイズしたり、独自のクエリを作成したりして、[新しいアラートを](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-log)簡単に作成できます。

### <a name="get-a-consolidated-view-across-multiple-servers-"></a>\* * 複数のサーバー間で統合ビューを取得する * *

Azure Monitor 内の1つの Log Analytics ワークスペースに複数のサーバーをオンボードする場合、Azure Monitor 内の[Virtual Machines Insights ソリューション](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview)から、これらすべてのサーバーの統合ビューを取得できます。  (Azure Monitor の Virtual Machines Insights の パフォーマンス タブと マップ タブのみがオンプレミスのサーバーで機能します。 正常性 タブは、Azure Vm でのみ機能します)。Azure portal でこれを表示するには、Azure Monitor > Virtual Machines (インサイト の下) に移動し、パフォーマンス または マップ タブに移動します。

### <a name="visualize-apps-systems-and-services-connected-to-a-given-server"></a>**特定のサーバーに接続されているアプリ、システム、およびサービスを視覚化する**

管理センターがサーバーを Azure Monitor 内の VM insights ソリューションに配置すると、 [Service Map](https://docs.microsoft.com/azure/azure-monitor/insights/service-map)と呼ばれる機能も利用できるようになります。 この機能は、アプリケーションコンポーネントを自動的に検出し、サービス間の通信をマップして、Azure portal からの優れた詳細情報を使用してサーバー間の接続を簡単に視覚化できるようにします。 これを見つけるには、Azure portal > Azure Monitor > Virtual Machines (洞察 の下) に移動し、マップ タブに移動します。

> [!NOTE]
> Azure Monitor の Virtual Machines Insights の視覚化は、現在6つのパブリックリージョンで提供されています。  最新情報については、 [Azure Monitor for VMs のドキュメント](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-onboard#log-analytics)を参照してください。  前述の Virtual Machines Insights ソリューションで提供されるその他の利点を得るには、サポートされているリージョンのいずれかで Log Analytics ワークスペースをデプロイする必要があります。

## <a name="disabling-monitoring"></a>監視の無効化

Log Analytics ワークスペースからサーバーを完全に切断するには、MMA エージェントをアンインストールします。 これは、このサーバーがワークスペースにデータを送信しなくなり、そのワークスペースにインストールされているすべてのソリューションがそのサーバーからのデータを収集して処理しなくなることを意味します。 ただし、ワークスペース自体には影響しません。そのワークスペースに報告するすべてのリソースが引き続き機能します。 WAC 内で MMA エージェントをアンインストールするには、[アプリ & 機能] にアクセスし、Microsoft Monitoring Agent を見つけて、[アンインストール] をクリックします。

ワークスペース内の特定のソリューションを無効にする場合は、 [Azure portal から監視ソリューションを削除](https://docs.microsoft.com/azure/azure-monitor/insights/solutions#remove-a-management-solution)する必要があります。 監視ソリューションを削除すると、そのソリューションによって作成された洞察が、そのワークスペースに報告しているサーバーのいずれに対して_も_生成されなくなります。 たとえば、Azure Monitor for VMs ソリューションをアンインストールしても、マイワークスペースに接続されているどのコンピューターからも VM またはサーバーのパフォーマンスに関する洞察は得られなくなります。