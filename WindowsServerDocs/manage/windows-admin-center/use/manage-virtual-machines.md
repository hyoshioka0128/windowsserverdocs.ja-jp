---
title: Windows 管理センターを使用した Virtual Machines の管理
description: Windows 管理センター (Project ホノルル) での Hyper-v ホストと仮想マシンの管理
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 02a33383b466e8bade2db0bbddaff66f0196954c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356860"
---
# <a name="managing-virtual-machines-with-windows-admin-center"></a>Windows 管理センターを使用した Virtual Machines の管理

>適用先:Windows Admin Center、Windows Admin Center Preview

サーバーまたはクラスターで Hyper-v の役割が有効になっている場合は、[サーバー](manage-servers.md)、[フェールオーバークラスター](manage-failover-clusters.md) 、または[ハイパー収束クラスター](manage-hyper-converged.md)接続で Virtual Machines ツールを使用できます。 Virtual Machines ツールを使用して、Windows Server 2012 以降を実行している Hyper-v ホストを、デスクトップエクスペリエンスまたは Server Core と共にインストールすることができます。 Hyper-v Server 2012、2016、および2019もサポートされています。

## <a name="key-features"></a>主な機能

Windows 管理センターの Virtual Machines ツールの主な内容は次のとおりです。

- **高レベルの Hyper-v ホストリソースの監視。** 1つのダッシュボードで、Hyper-v ホストサーバーまたはクラスター全体の CPU とメモリの使用量、IO パフォーマンスメトリック、VM の正常性に関するアラートとイベントを表示します。
- **Hyper-v マネージャーとフェールオーバークラスターマネージャー機能が統合されています。** クラスター全体のすべての仮想マシンを表示し、高度な管理とトラブルシューティングのために1つの仮想マシンにドリルダウンします。
- **シンプルで、仮想マシンの管理のための強力なワークフローです。** 仮想マシンを作成、管理、レプリケートするための IT 管理シナリオに合わせた新しい UI エクスペリエンス。

Windows 管理センターで実行できる Hyper-v のタスクの一部を次に示します。

- [Hyper-v ホストのリソースとパフォーマンスの監視](#monitor-hyper-v-host-resources-and-performance)
- [バーチャルマシンのインベントリの表示](#view-virtual-machine-inventory)
- [新しい仮想マシンの作成](#create-a-new-virtual-machine)
- [バーチャルマシンの設定の変更](#change-virtual-machine-settings)
- [別のクラスターノードへの仮想マシンのライブマイグレーション](#live-migrate-a-virtual-machine-to-another-cluster-node)
- [1台の仮想マシンの高度な管理とトラブルシューティング](#advanced-management-and-troubleshooting-for-a-single-virtual-machine)
- [Hyper-v ホスト (VMConnect) を使用して仮想マシンを管理する](#manage-a-virtual-machine-through-the-hyper-v-host-vmconnect)
- [Hyper-v ホストの設定を変更する](#change-hyper-v-host-settings)
- [Hyper-v イベントログの表示](#view-hyper-v-event-logs)
- [Azure Site Recovery を使用して仮想マシンを保護する](#protect-virtual-machines-with-azure-site-recovery)

## <a name="monitor-hyper-v-host-resources-and-performance"></a>Hyper-v ホストのリソースとパフォーマンスの監視

![Virtual Machines の概要画面](../media/manage-virtual-machines/virtual-machines-summary.png)

1. 左側のナビゲーションウィンドウで **[Virtual Machines]** ツールをクリックします。
2. **Virtual Machines**ツールの上部には、 **[概要]** タブと **[インベントリ]** タブの2つのタブがあります。 **[概要]** タブには、次のように、現在のサーバーまたはクラスター全体の hyper-v ホストのリソースとパフォーマンスの総合的なビューが表示されます。
    - 状態 (実行中、オフ、一時停止、および保存) でグループ化された Vm の数
    - 最近の正常性アラートまたは Hyper-v イベントログのイベント (アラートは、Windows Server 2016 以降を実行しているハイパー収束クラスターでのみ使用できます)
    - ホストとゲストの間の CPU およびメモリの使用率の内訳
    - 最も CPU リソースとメモリリソースを消費している上位の Vm
    - IOPS と IO スループットのライブおよび履歴データ折れ線グラフ (ストレージパフォーマンス折れ線グラフは、Windows Server 2016 以降を実行しているハイパー収束クラスターでのみ使用できます。 履歴データは、Windows Server 2019 を実行しているハイパー収束クラスターでのみ使用できます)

## <a name="view-virtual-machine-inventory"></a>バーチャルマシンのインベントリの表示

![Virtual Machines インベントリ画面](../media/manage-virtual-machines/virtual-machines-inventory.png)

1. 左側のナビゲーションウィンドウで **[Virtual Machines]** ツールをクリックします。
2. **Virtual Machines**ツールの上部には、 **[概要]** タブと **[インベントリ]** タブの2つのタブがあります。 **[インベントリ]** タブには、現在のサーバーまたはクラスター全体で使用可能な仮想マシンが一覧表示され、個々の仮想マシンを管理するためのコマンドが表示されます。 可能な代替手段としては以下の方法があります。
    - 現在のサーバーまたはクラスターで実行されている仮想マシンの一覧を表示します。
    - クラスターの仮想マシンを表示している場合は、仮想マシンの状態とホストサーバーを表示します。 また、メモリ不足、メモリの需要と割り当てられたメモリ、バーチャルマシンの稼働時間、ハートビートの状態、および Azure Site Recovery を使用した保護の状態など、ホストの観点からの CPU とメモリの使用量も表示します。
    - [新しい仮想マシンを作成](#create-a-new-virtual-machine)します。
    - 仮想マシンの削除、開始、無効化、シャットダウン、一時停止、再開、リセット、または名前の変更を行います。 また、仮想マシンを保存したり、保存された状態を削除したり、チェックポイントを作成したりします。
    - [バーチャルマシンの設定を変更](#change-virtual-machine-settings)します。
    - Hyper-v ホスト経由で VMConnect を使用して、バーチャルマシンコンソールに接続します。
    - [Azure Site Recovery を使用して仮想マシンをレプリケート](#protect-virtual-machines-with-azure-site-recovery)します。
    - 複数の Vm で実行できる操作 ([開始]、[シャットダウン]、[保存]、[一時停止]、[削除]、[リセット] など) では、複数の Vm を選択し、一度に操作を実行できます。

注: クラスターに接続している場合、仮想マシンツールはクラスター化された仮想マシンのみを表示します。 今後、クラスター化されていない仮想マシンも表示する予定です。

## <a name="create-a-new-virtual-machine"></a>新しい仮想マシンを作成する

![新しい仮想マシンの作成画面](../media/manage-virtual-machines/new-vm.png)

1. 左側のナビゲーションウィンドウで **[Virtual Machines]** ツールをクリックします。
2. Virtual Machines ツールの上部で、 **[インベントリ]** タブを選択し、 **[新規]** をクリックして新しい仮想マシンを作成します。
3. 仮想マシン名を入力し、第1世代と第2世代の仮想マシンを選択します。
4. クラスター上に仮想マシンを作成する場合は、最初に仮想マシンを作成するホストを選択できます。 Windows Server 2016 以降を実行している場合は、このツールによってホストの推奨事項が提供されます。
5. 仮想マシンファイルのパスを選択します。 ドロップダウンリストからボリュームを選択するか、 **[参照]** をクリックしてフォルダーピッカーを使用してフォルダーを選択します。 仮想マシンの構成ファイルと仮想ハードディスクファイルは、選択したボリュームまたはパス`\Hyper-V\\[virtual machine name]`のパスにある1つのフォルダーに保存されます。

   >[!Tip]
   > フォルダーピッカーで、 **[フォルダー名]** フィールドに ```\\server\share``` というパスを入力すると、ネットワーク上の利用可能な SMB 共有を参照できます。 VM ストレージにネットワーク共有を使用するには[CredSSP](../understand/faq.md#does-windows-admin-center-use-credssp)が必要です。

6. 仮想プロセッサの数を選択して、入れ子になった仮想化を有効にするかどうか、メモリ設定、ネットワークアダプター、仮想ハードディスクを構成し、.iso イメージファイルからオペレーティングシステムをインストールするか、ネットワークからインストールするかを選択します。
7. **[作成]** をクリックして、仮想マシンを作成します。
8. 仮想マシンが作成され、仮想マシンの一覧に表示されたら、仮想マシンを起動できます。
9. 仮想マシンが起動したら、VMConnect を使用して仮想マシンのコンソールに接続し、オペレーティングシステムをインストールできます。 一覧から仮想マシンを選択し、[**その他** > の**接続**] をクリックして .rdp ファイルをダウンロードします。 リモートデスクトップ接続アプリで .rdp ファイルを開きます。 これは仮想マシンのコンソールに接続しているため、Hyper-v ホストの管理者の資格情報を入力する必要があります。

## <a name="change-virtual-machine-settings"></a>バーチャルマシンの設定の変更

![仮想マシンの設定画面](../media/manage-virtual-machines/vm-settings.png)

1. 左側のナビゲーションウィンドウで **[Virtual Machines]** ツールをクリックします。
2. Virtual Machines ツールの上部で、 **[インベントリ]** タブを選択します。一覧から仮想マシンを選択し、[**その他**の  >  の**設定**] をクリックします。
3. **[全般**]、 **[セキュリティ]** 、 **[メモリ]** 、 **[プロセッサ]** 、 **[ディスク]** 、 **[ネットワーク]** 、 **[ブート順序]** 、 **[チェックポイント]** タブを切り替えて、必要な設定を構成し、 **[保存]** をクリックして保存します。現在のタブの設定。 使用できる設定は、仮想マシンの世代によって異なります。 また、実行中の仮想マシンの一部の設定は変更できないため、最初に仮想マシンを停止する必要があります。

## <a name="live-migrate-a-virtual-machine-to-another-cluster-node"></a>別のクラスターノードへの仮想マシンのライブマイグレーション

クラスターに接続している場合は、仮想マシンを別のクラスターノードにライブマイグレーションできます。

1. フェールオーバークラスターまたはハイパー集約されたクラスター接続から、左側のナビゲーションウィンドウにある **[Virtual Machines]** ツールをクリックします。
2. Virtual Machines ツールの上部で、 **[インベントリ]** タブを選択します。一覧から仮想マシンを選択し、[ **More** > **Move**] をクリックします。
3. 使用可能なクラスターノードの一覧からサーバーを選択し、 **[移動]** をクリックします。
4. 移動の進行状況に関する通知は、Windows 管理センターの右上隅に表示されます。 移動が成功した場合は、バーチャルマシンの一覧でホストサーバー名が変更されていることがわかります。

## <a name="advanced-management-and-troubleshooting-for-a-single-virtual-machine"></a>1台の仮想マシンの高度な管理とトラブルシューティング

![単一の仮想マシンの詳細画面](../media/manage-virtual-machines/vm-details.png)

単一の仮想マシンの詳細情報とパフォーマンスグラフは、単一の仮想マシンページから表示できます。

1. 左側のナビゲーションウィンドウで **[Virtual Machines]** ツールをクリックします。
2. Virtual Machines ツールの上部で、 **[インベントリ]** タブを選択します。仮想マシンの一覧から仮想マシンの名前をクリックします。
3. [単一の仮想マシン] ページでは、次のことができます。
    - 仮想マシンの詳細情報を表示します。
    - CPU、メモリ、ネットワーク、IOPS、IO スループットのライブデータと履歴データの折れ線グラフを表示します (履歴データは、Windows Server 2019 を実行しているハイパー収束クラスターでのみ使用できます)
    - チェックポイントの表示、作成、適用、名前変更、削除を行います。
    - 仮想マシンの仮想ハードディスク (.vhd) ファイル、ネットワークアダプター、およびホストサーバーの詳細を表示します。
    - 仮想マシンの削除、開始、オフ、シャットダウン、一時停止、再開、リセット、または名前の変更を行います。 また、仮想マシンを保存したり、保存された状態を削除したり、チェックポイントを作成したりします。
    - [仮想マシンの設定を変更](#change-virtual-machine-settings)します。
    - Hyper-v ホスト経由で VMConnect を使用して仮想マシンコンソールに接続します。
    - [Azure Site Recovery を使用して仮想マシンをレプリケート](#protect-virtual-machines-with-azure-site-recovery)します。

## <a name="manage-a-virtual-machine-through-the-hyper-v-host-vmconnect"></a>Hyper-v ホスト (VMConnect) を使用して仮想マシンを管理する

![Web ブラウザーを使用した VM の接続](../media/manage-virtual-machines/vm-connect.png)

1. 左側のナビゲーションウィンドウで **[Virtual Machines]** ツールをクリックします。
2. Virtual Machines ツールの上部で、 **[インベントリ]** タブを選択します。一覧から仮想マシンを選択し、 **[その他]**  >  **[接続]** または **[RDP ファイルのダウンロード]** をクリックします。 **[接続]** を使用すると、Windows 管理センターに統合されたリモートデスクトップ web コンソールを使用してゲスト VM と対話できます。 **Rdp ファイルをダウンロード**すると、リモートデスクトップ接続アプリケーション (mstsc.exe) を使用して開くことができる .rdp ファイルがダウンロードされます。 どちらのオプションでも、VMConnect を使用して Hyper-v ホストを介してゲスト VM に接続し、Hyper-v ホストサーバーの管理者の資格情報を入力する必要があります。

## <a name="change-hyper-v-host-settings"></a>Hyper-v ホストの設定を変更する

![Hyper-v ホストの設定画面](../media/manage-virtual-machines/host-settings.png)

1. サーバー、ハイパー収束クラスター、またはフェールオーバークラスター接続で、左側のナビゲーションウィンドウの下部にある **[設定]** メニューをクリックします。
2. Hyper-v ホストサーバーまたはクラスターに、次のセクションを含む**Hyper-v ホスト設定**グループが表示されます。
    - ［全般］:仮想ハードディスクと仮想マシンのファイルパス、およびハイパーバイザーのスケジュールの種類を変更する (サポートされている場合)
    - 拡張セッションモード
    - NUMA ノードにまたがるメモリ割り当て
    - ライブ マイグレーション
    - 記憶域の移行
3. ハイパー収束クラスターまたはフェールオーバークラスター接続で Hyper-v ホスト設定を変更した場合、変更はすべてのクラスターノードに適用されます。

## <a name="view-hyper-v-event-logs"></a>Hyper-v イベントログの表示

Hyper-v イベントログは、Virtual Machines ツールから直接表示できます。

1. 左側のナビゲーションウィンドウで **[Virtual Machines]** ツールをクリックします。
2. Virtual Machines ツールの上部にある **[概要]** タブを選択します。右上の イベント セクションで、 **[すべてのイベントの表示]** をクリックします。
3. イベントビューアーツールでは、左側のウィンドウに Hyper-v イベントチャンネルが表示されます。 右ペインでイベントを表示するには、チャネルを選択します。 フェールオーバークラスターまたはハイパー集約クラスターを管理している場合、イベントログには、すべてのクラスターノードのイベントが表示され、ホストサーバーが [コンピューター] 列に表示されます。

## <a name="protect-virtual-machines-with-azure-site-recovery"></a>Azure Site Recovery を使用して仮想マシンを保護する

Windows 管理センターを使用して Azure Site Recovery を構成し、オンプレミスの仮想マシンを Azure にレプリケートすることができます。 [詳細](../azure/azure-site-recovery.md)

## <a name="more-coming"></a>その他の準備

Windows 管理センターでは、仮想マシンの管理が積極的に開発されており、近い将来に新機能が追加される予定です。 UserVoice の機能の状態と投票を確認できます。

- [仮想マシンのインポート/エクスポート](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31481971--virtual-machines-import-export-vms)
- [フォルダー内のバーチャルマシンの並べ替え](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31494712--virtual-machines-ability-to-sort-vm-into-folder)
- [追加の仮想マシン設定のサポート](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31915264--virtual-machines-expose-all-configurable-setting)
- [Hyper-v レプリカのサポート](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/32040253--virtual-machines-setup-and-manage-hyper-v-replic)
- [仮想マシンの所有権を委任する](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31663837--virtual-machines-owner-delegation)
- [バーチャルマシンの複製](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31783288--virtual-machines-add-a-button-to-clone-a-vm)
- [既存の仮想マシンからテンプレートを作成する](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31494649--virtual-machines-create-a-template-from-an-exist)
- [Hyper-v ホスト間での仮想マシンの表示](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31734559--virtual-machines-find-vms-on-host-screen)
- [[新しいバーチャルマシン] ウィンドウで VLAN を構成する](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31710979--virtual-machines-new-new-vm-pane-need-vlan-opt)

[すべてを表示するか、新しい機能を提案](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5Bvirtual%20machines%5D)します。
