---
title: Windows Admin Center での仮想マシンの管理
description: HYPER-V ホストと Windows Admin Center (プロジェクト ホノルル) を持つ仮想マシンの管理
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 41767b9e53c0106931e78f86f8675e413cca0d0a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816883"
---
# <a name="managing-virtual-machines-with-windows-admin-center"></a>Windows Admin Center での仮想マシンの管理

>適用先:Windows Admin Center、Windows Admin Center プレビュー

仮想マシンのツールが表示されます。[サーバー](manage-servers.md)、[フェイル オーバー クラスター](manage-failover-clusters.md)または[Hyper-Converged クラスター](manage-hyper-converged.md)サーバーまたはクラスター上で Hyper-v ロールが有効になっている場合に接続します。 Windows Server 2012 を実行している HYPER-V ホストを管理する仮想マシンのツールを使用するまたは Server Core、デスクトップ エクスペリエンス搭載以降、いずれかをインストールします。 また、Hyper-V Server 2012 および 2016 もサポートされます。

## <a name="key-features"></a>主な機能

Windows Admin Center での仮想マシンのツールの主な特徴は次のとおりです。

- **高度な HYPER-V ホスト リソースを監視します。** 単一のダッシュ ボードで、全体的な CPU とメモリ使用量、IO パフォーマンス メトリック、VM の正常性アラート、および HYPER-V ホスト サーバーまたはクラスター全体のイベントを表示します。
- **統合された操作は、HYPER-V マネージャーとフェールオーバー クラスター マネージャーの機能を統合すること。** クラスター全体ですべての仮想マシンを表示し、単一の仮想マシンの高度な管理およびトラブルシューティングにドリル ダウンします。
- **仮想マシンの管理、単純かつ強力なワークフローです。** 新しい UI エクスペリエンスは、作成、管理、および仮想マシンをレプリケートする IT 管理のシナリオに合わせて調整します。

Windows Admin Center で行うことができます、HYPER-V のタスクの一部を次に示します。

- [HYPER-V ホストのリソースとパフォーマンスを監視します。](#monitor-hyper-v-host-resources-and-performance)
- [仮想マシンのインベントリを表示します。](#view-virtual-machine-inventory)
- [新しい仮想マシンを作成します。](#create-a-new-virtual-machine)
- [仮想マシンの設定を変更します。](#change-virtual-machine-settings)
- [仮想マシンを別のクラスター ノードにライブ移行します。](#live-migrate-a-virtual-machine-to-another-cluster-node)
- [高度な管理と単一の仮想マシンのトラブルシューティング](#advanced-management-and-troubleshooting-for-a-single-virtual-machine)
- [HYPER-V イベント ログの表示](#view-hyper-v-event-logs)
- [Azure Site Recovery で仮想マシンを保護します。](#protect-virtual-machines-with-azure-site-recovery)

## <a name="monitor-hyper-v-host-resources-and-performance"></a>HYPER-V ホストのリソースとパフォーマンスを監視します。

![仮想マシンの概要 画面](../media/manage-virtual-machines/virtual-machines-summary.png)

1. をクリックして、**仮想マシン**、左側のナビゲーション ウィンドウからのツール。
2. 上部にある 2 つのタブがある、**仮想マシン**ツール、**概要** タブおよび**インベントリ** タブ。**概要** タブは、HYPER-V ホストのリソースと、現在のサーバーまたは、次を含め、クラスター全体のパフォーマンスの全体像を提供します。
    - 状態 - 実行して、グループ化された Vm の数が一時停止し、保存
    - 最近の正常性アラートまたは HYPER-V イベント ログのイベント (アラートは Windows Server 2016 を実行しているハイパー コンバージド クラスター使用可能なまたはそれ以降)
    - ホストとゲストの内訳と CPU およびメモリの使用
    - CPU とメモリ リソースを消費して最上位の Vm
    - ライブおよび過去のデータ行の IOPS、IO スループットのグラフ (記憶域のパフォーマンスの折れ線グラフはのみ以降 Windows Server 2016 を実行するハイパーコンバージド クラスターに使用できます。 履歴データは、Windows Server 2019 を実行するハイパー コンバージド クラスターの使用のみ)

## <a name="view-virtual-machine-inventory"></a>仮想マシンのインベントリを表示します。

![仮想マシンのインベントリの画面](../media/manage-virtual-machines/virtual-machines-inventory.png)

1. をクリックして、**仮想マシン**、左側のナビゲーション ウィンドウからのツール。
2. 上部にある 2 つのタブがある、**仮想マシン**ツール、**概要** タブおよび**インベントリ** タブ。**インベントリ**タブは、現在のサーバーまたはクラスター全体で使用できる仮想マシンを一覧表示され、個々 の仮想マシンを管理するコマンドを提供します。 可能な代替手段としては以下の方法があります。
    - 現在のサーバーまたはクラスター上で実行する仮想マシンの一覧を表示します。
    - クラスターの仮想マシンを表示している場合は、仮想マシンの状態とホスト サーバーを表示します。 メモリ不足、必要なメモリと割り当てられたメモリは、および仮想マシンの稼働時間、ハートビートの状態および Azure Site Recovery を使用して保護の状態を含む、ホストの視点から、CPU とメモリの使用量を表示もできます。
    - [新しい仮想マシンを作成する](#create-a-new-virtual-machine)します。
    - 削除、開始、オフにする、シャット ダウン、一時停止、再開、リセットまたは仮想マシンの名前を変更します。 仮想マシンを保存も保存済みの状態を削除、またはチェックポイントを作成します。
    - [仮想マシンの設定を変更](#change-virtual-machine-settings)します。
    - VMConnect を使用して、HYPER-V ホストを使用して仮想マシンのコンソールに接続します。
    - [Azure Site Recovery を使用して仮想マシンをレプリケート](#protect-virtual-machines-with-azure-site-recovery)します。

注: クラスターに接続している場合、仮想マシンのツールはクラスター化された仮想マシンのみ表示されます。 仮想マシンの非クラスター化を今後も表示する予定です。

## <a name="create-a-new-virtual-machine"></a>新しい仮想マシンを作成する

![新しい仮想マシンの画面を作成します。](../media/manage-virtual-machines/new-vm.png)

1. をクリックして、**仮想マシン**、左側のナビゲーション ウィンドウからのツール。
2. 仮想マシンのツールの上部にある次のように選択します。、**インベントリ** タブの 、 をクリックし、**新規**新しい仮想マシンを作成します。
3. 仮想マシンの名前を入力し、世代 1 および 2 世代仮想マシンを選択します。
4. クラスターで仮想マシンを作成する場合に最初に、仮想マシンを作成するには、どのホストを選択できます。 2016 以降、Windows Server を実行する場合のホストの推奨事項が提供されます。
5. 仮想マシン ファイルのパスを選択します。 ドロップダウン リストからボリュームを選択するかクリックして**参照**フォルダー ピッカーを使用してフォルダーを選択します。 仮想マシン構成ファイルとバーチャル ハード ディスク ファイルは、1 つのフォルダーの下に保存されます、`\Hyper-V\\[virtual machine name]`パスの選択したボリュームのパス。
6. 入れ子になった仮想化が有効にする、メモリの設定、ネットワーク アダプタ、バーチャル ハード_ディスクを構成し、.iso イメージ ファイルから、またはネットワークからオペレーティング システムをインストールするかどうかを選択するかどうか、仮想プロセッサの数を選択します。
7. **[作成]** をクリックして、バーチャル マシンを作成します。
8. 仮想マシンを作成し、仮想マシンの一覧に表示される、仮想マシンを開始できます。
9. 仮想マシンが開始されると、オペレーティング システムをインストールする VMConnect を使用して、仮想マシンのコンソールに接続できます。 一覧から仮想マシンを選択し、 をクリックして**詳細** > **Connect** .rdp ファイルをダウンロードします。 Remote Desktop Connection アプリでは、.rdp ファイルを開きます。 これは、仮想マシンのコンソールに接続する、ため、HYPER-V ホストの管理者の資格情報を入力する必要があります。

## <a name="change-virtual-machine-settings"></a>仮想マシンの設定を変更します。

![仮想マシンの設定 画面](../media/manage-virtual-machines/vm-settings.png)

1. をクリックして、**仮想マシン**、左側のナビゲーション ウィンドウからのツール。
2. 仮想マシンのツールの上部にある選択、**インベントリ**タブ。一覧から仮想マシンを選択およびクリックして**詳細** > **設定**します。
3. 間の切り替え、**全般**、**メモリ**、**プロセッサ**、**ディスク**、**ネットワーク**、 **ブート順**と**チェックポイント**タブし、必要な設定を構成しをクリックして**保存**現在のタブの設定を保存します。 使用可能な設定については、仮想マシンの世代によって異なります。 また、仮想マシンの実行に一部の設定を変更することはできません、まず仮想マシンを停止する必要があります。

## <a name="live-migrate-a-virtual-machine-to-another-cluster-node"></a>仮想マシンを別のクラスター ノードにライブ移行します。

クラスターに接続している場合は、別のクラスター ノードに仮想マシンをライブ移行できます。

1. フェールオーバー クラスターまたはハイパーコンバージド クラスターの接続では、をクリックして、**仮想マシン**、左側のナビゲーション ウィンドウからのツール。
2. 仮想マシンのツールの上部にある選択、**インベントリ**タブ。一覧から仮想マシンを選択およびクリックして**詳細** > **移動**します。
3. 使用可能なクラスター ノードの一覧からサーバーを選択し、をクリックして**移動**します。
4. Windows Admin Center の右上隅で、移動の進行状況の通知が表示されます。 移動が成功した場合は、仮想マシンの一覧で変更されたホスト サーバーの名前が表示されます。

## <a name="advanced-management-and-troubleshooting-for-a-single-virtual-machine"></a>高度な管理と単一の仮想マシンのトラブルシューティング

![単一の仮想マシンの詳細 画面](../media/manage-virtual-machines/vm-details.png)

詳細な情報と、単一の仮想マシン ページから単一の仮想マシンのパフォーマンス グラフを表示することができます。

1. をクリックして、**仮想マシン**、左側のナビゲーション ウィンドウからのツール。
2. 仮想マシンのツールの上部にある選択、**インベントリ**タブ。仮想マシンの一覧から仮想マシンの名前をクリックします。
3. 単一の仮想マシン ページで、次の操作を実行できます。
    - 仮想マシンの詳細情報を表示します。
    - CPU、メモリ、ネットワーク、IOPS、IO スループットのライブおよび履歴データの折れ線グラフを表示 (履歴データは Windows Server 2019 を実行するハイパーコンバージド クラスターに使用できるのみです)
    - 表示、作成、適用、名前を変更およびチェックポイントを削除します。
    - 仮想マシンの仮想ハード_ディスク (.vhd) ファイル、ネットワーク アダプターとホスト サーバーの詳細を表示します。
    - 削除、開始、オフにする、シャット ダウン、一時停止、再開、リセットまたは仮想マシンの名前を変更します。 仮想マシンを保存も保存済みの状態を削除、またはチェックポイントを作成します。
    - [仮想マシンの設定を変更](#change-virtual-machine-settings)します。
    - VMConnect を使用して、HYPER-V ホストを使用して仮想マシンのコンソールに接続します。
    - [Azure Site Recovery を使用して仮想マシンをレプリケート](#protect-virtual-machines-with-azure-site-recovery)します。

## <a name="view-hyper-v-event-logs"></a>HYPER-V イベント ログの表示

仮想マシン ツールから直接、HYPER-V イベント ログを表示することができます。

1. をクリックして、**仮想マシン**、左側のナビゲーション ウィンドウからのツール。
2. 仮想マシンのツールの上部にある選択、**概要**タブ。最上位の適切なイベント の **ビューのすべてのイベント**します。
3. イベント ビューアー ツールは、左側のウィンドウで、HYPER-V のイベント チャネルに表示されます。 右側のウィンドウで、イベントを表示するためのチャネルを選択します。 フェールオーバー クラスターまたはハイパーコンバージド クラスターを管理している場合、マシン列で、ホスト サーバーを表示するすべてのクラスター ノードのイベントがイベント ログに表示されます。

## <a name="protect-virtual-machines-with-azure-site-recovery"></a>Azure Site Recovery で仮想マシンを保護します。

Windows Admin Center を使用して、Azure Site Recovery を構成して、オンプレミスの仮想マシンを Azure にレプリケートすることができます。 [詳細情報](azure-services.md)

## <a name="more-coming"></a>今後追加されます。

Windows Admin Center での仮想マシンの管理は開発中にアクティブにし、新しい機能が、近い将来に追加します。 UserVoice では、状態と機能の投票を表示できます。

|機能のリクエスト|
|-------|
|[仮想マシンのインポート/エクスポート](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31481971--virtual-machines-import-export-vms)|
|[フォルダー内の仮想マシンの並べ替え](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31494712--virtual-machines-ability-to-sort-vm-into-folder)|
|[追加の仮想マシンの設定をサポートします。](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31915264--virtual-machines-expose-all-configurable-setting)|
|[HYPER-V レプリカのサポート](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/32040253--virtual-machines-setup-and-manage-hyper-v-replic)|
|[仮想マシンの所有権の委任](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31663837--virtual-machines-owner-delegation)|
|[バーチャル マシンの複製](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31783288--virtual-machines-add-a-button-to-clone-a-vm)|
|[既存の仮想マシンからテンプレートを作成します。](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31494649--virtual-machines-create-a-template-from-an-exist)|
|[HYPER-V ホスト間で仮想マシンの表示](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31734559--virtual-machines-find-vms-on-host-screen)|
|[新しい仮想マシンのウィンドウで VLAN を構成します。](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31710979--virtual-machines-new-new-vm-pane-need-vlan-opt)|
|[**すべてを参照するか、新しい機能の提案**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5Bvirtual%20machines%5D)|
