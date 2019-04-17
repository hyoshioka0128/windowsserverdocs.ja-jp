---
title: サーバーを監視し、Windows Admin Center から Azure モニターでアラートを構成します。
description: Windows Admin Center (Project Honolulu) と Azure モニターの統合します。
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 03/24/2019
ms.openlocfilehash: 6ada708bf7dd8cd08e1bc2620be5244a07beac7d
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297021"
---
# サーバーを監視し、Windows Admin Center から Azure モニターでアラートを構成します。

[Windows Admin Center での Azure 統合の詳細](../plan/azure-integration-options.md)

[Azure モニター](https://docs.microsoft.com/azure/azure-monitor/overview)は、収集、分析、およびさまざまな Windows サーバーと、オンプレミスの Vm をなどのリソースとクラウドの利用統計情報で動作するソリューションです。 ただし、Azure モニターでは、Azure Vm では、その他の Azure リソースからデータを取得、この記事では、オンプレミス サーバーと Windows Admin Center で具体的には、Vm の Azure モニターのしくみについて説明します。 Azure のモニターを使って、ハイパーコンバージド クラスターの電子メール アラートを取得する方法について説明します。 興味があるなら、[ヘルス サービスの障害のメールを送信する Azure モニターの使用](https://docs.microsoft.com/windows-server/storage/storage-spaces/configure-azure-monitor)に関する参照してください。

## Azure モニターのしくみ
![img](../media/azure-monitor-diagram.png) Azure モニターで Log Analytics ワークスペースで、オンプレミスの Windows サーバーから生成されたデータを収集します。 ワークスペース内には、さまざまな監視ソリューションを有効にできます: 特定のシナリオの情報を提供するロジックを設定します。 たとえば、Azure Update Management、Azure Security Center、Vm を監視する Azure はすべての監視ソリューション ワークスペース内で有効にすることができます。 

有効にすると、監視ソリューション Log Analytics ワークスペースでそのワークスペースへの報告のすべてのサーバーに関連するデータの収集を開始は、そのソリューションできるように、ソリューションがワークスペースでのすべてのサーバーの情報を生成できます。 

オンプレミス サーバー上の利用統計情報データの収集を Log Analytics ワークスペースにプッシュするには、Azure のモニターには、Microsoft Monitoring Agent や、MMA のインストールが必要です。 特定の監視ソリューションでは、セカンダリ エージェントも必要です。 たとえば、Vm を監視する Azure は、このソリューションを提供する追加の機能のための ServiceMap エージェントにも依存します。 

Azure 更新プログラムの管理など、いくつかのソリューションは、Azure および Azure 以外の環境の間でリソースを一元的に管理できるように、Azure の自動化にも依存します。 たとえば、Azure の更新プログラムの管理では、Azure オートメーションを使用して、スケジュールを設定し、Azure ポータルから一元的に、環境内のコンピューターの間で更新プログラムのインストールを調整します。


## 方法は Windows Admin Center を有効にする Azure モニターを使用するかどうか。

WAC、内から 2 つの監視ソリューションを有効ことができます。

- [Azure の更新プログラムの管理](azure-update-management.md)([更新プログラム] ツール)
- (サーバーの設定) で Vm を監視する azure、仮想マシン インサイトの別名

これらのツールのいずれかの Azure モニターを使用して開始することができます。 Log Analytics ワークスペース (と Azure オートメーション アカウント、必要な場合)、WAC が自動的にプロビジョニングする前に Azure モニターを初めて使用する場合をインストールし、対象のサーバーで Microsoft Monitoring Agent (MMA) を構成します。 ワークスペースに対応するソリューションがインストールされます。 

たとえば、Azure アップデート管理の設定を更新ツールに最初に移動する場合は、WAC が行います。

1. コンピューターで、MMA をインストールします。
2. (Azure オートメーション アカウントは、ここで必要な) ために、Log Analytics ワークスペースと Azure オートメーション アカウントを作成します。
3. 新しく作成したワークスペースで、更新プログラムの管理ソリューションをインストールします。

同じサーバーに WAC 内から別の監視ソリューションを追加するには、WAC はそのサーバーが接続されている既存のワークスペースにそのソリューションをインストールだけです。 WAC は、他のために必要なエージェントをさらにインストールされます。

別のサーバーに接続を既にセットアップ (使うか、WAC または手動で Azure Portal で) Log Analytics ワークスペースがある場合も MMA エージェントをサーバーにインストールし、既存のワークスペースまでに接続します。 接続すると、サーバーをワークスペースに、データの収集とそのワークスペースにインストールされているソリューションへの報告が自動的に開始します。

## Azure 仮想マシン (別名用の監視します。 仮想マシンの情報)
>適用対象: Windows Admin Center Preview

設定したモニターの Azure Vm のサーバーの設定、Windows Admin Center を有効に Azure モニターに Vm ソリューションでは、仮想マシン インサイトとも呼ばれます。 このソリューションを使用すると、サーバーの正常性とイベントを監視、メール通知を作成、環境全体にわたってサーバーのパフォーマンスの統合ビューの取得およびアプリ、システム、および特定のサーバーに接続されているサービスを視覚化できます。

> [!NOTE]
> その名前にもかかわらず VM インサイトは、物理サーバーと仮想マシンの動作します。

Azure モニターの空き 5 GB のデータ/月/ユーザーの許容量、簡単にこれを試してサーバーまたは課金の心配せず 2 つのします。 環境内でサーバー間でシステムのパフォーマンスの統合ビューの取得など Azure モニター、サーバーのオンボーディングの追加のメリットを参照して読み込みます。

### **Azure モニターで使用するため、サーバーのセットアップします。**

サーバー接続の概要ページで、新しいボタン「通知の管理」をクリックしてまたは _gt のサーバーの設定に移動監視と通知されます。 このページ内でオンボード] をクリックして Azure のモニターにサーバー「設定」とセットアップ ウィンドウを完了します。 Admin Center が処理、Azure Log Analytics ワークスペースでのプロビジョニングのために必要なエージェントのインストールと構成されている VM インサイト ソリューションを確認します。 完了すると、サーバーに送信されますパフォーマンス カウンター データ、Azure のモニターを表示し、Azure ポータルからこのサーバーに基づくメール アラートを作成することができます。

### **メール アラートを作成します。**

サーバーは、Azure のモニターにアタッチしたは、Azure ポータルに移動する設定 _gt 監視およびアラート ページ内でインテリジェントなハイパーリンクを使用することができます。 Admin Center には、パフォーマンス カウンターを収集することができます簡単に[新しいアラートを作成する](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-log)多くの事前に定義されたクエリのいずれかをカスタマイズするか、独自の書き込みによって自動的に有効にします。

### * * 複数のサーバーにまとめて表示を取得する * *

場合は、オンボード Azure モニター内で 1 つの Log Analytics ワークスペースに複数のサーバーから取得できますこれらすべてのサーバーの統合ビュー Azure モニター内での[仮想マシン インサイト ソリューション](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-overview)です。  (Azure モニターの仮想マシン インサイトのパフォーマンスとマップのタブのみが、オンプレミス サーバー – Azure Vm でのみの正常性] タブの関数で動作することに注意してください)。Azure portal では、これを表示するには、Azure モニター _gt (インサイト)、下の仮想マシンに移動し、"Performance"や「マップは、」タブに移動します。

### **アプリ、システム、および特定のサーバーに接続されているサービスを視覚化します。**

とき Admin Center onboards、VM インサイトのソリューションに Azure モニター内のサーバーでは、それも点灯[サービス マップ](https://docs.microsoft.com/azure/azure-monitor/insights/service-map)と呼ばれる機能します。 この機能は自動的にアプリケーション コンポーネントを検出し、サービス間の通信にマップできるように、Azure ポータルから詳しくとサーバー間の接続を簡単に視覚化できます。 Azure ポータル _gt Azure モニター _gt (インサイト)、下の仮想マシンに移動し、「マップ」] タブに移動するには、これを検索します。

> [!NOTE]
> Azure モニターの仮想マシン インサイトの視覚エフェクトが現在の 6 パブリック地域で提供されます。  最新情報については、 [Vm のドキュメントを監視する Azure](https://docs.microsoft.com/azure/azure-monitor/insights/vminsights-onboard#log-analytics)を確認します。  上記で説明した仮想マシン インサイト ソリューションによって提供される追加のメリットを取得するのにサポートされている領域のいずれかで Log Analytics ワークスペースを展開する必要があります。

## 監視を無効にします。

完全に切断するには、サーバー Log Analytics ワークスペースから MMA エージェントをアンインストールします。 これは、このサーバーのワークスペースにデータを送信しなくなったこととそのワークスペースにインストールされているソリューションは不要になったすべて収集し、そのサーバーからデータを処理することを意味します。 ただし、これを行うためにそのワークスペースへの報告のリソースは引き続きすべてワークスペース自体 – は影響しません。 WAC 内 MMA エージェントをアンインストールするに & 機能をアプリに移動し、Microsoft Monitoring Agent を見つけてアンインストール] をクリックします。

ワークスペース内の特定のソリューションを無効にする場合は、 [Azure ポータルから監視ソリューションを削除](https://docs.microsoft.com/azure/azure-monitor/insights/solutions#remove-a-management-solution)する必要があります。 監視ソリューションを削除することに関してによって作成された_任意_のワークスペースにレポート サーバーのソリューションが生成されるしなくなったことを意味します。 たとえば、Vm ソリューションの Azure モニターをアンインストールした場合はしなくなった表示マイ ワークスペースに接続されているコンピューターのいずれかから VM またはサーバーのパフォーマンスに関する情報。