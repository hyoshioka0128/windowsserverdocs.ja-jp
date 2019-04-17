---
title: Windows Admin Center で仮想マシンの管理
description: HYPER-V ホストと Windows Admin Center (Project Honolulu) の仮想マシンを管理します。
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 374ee30dcbaf9af3caa60ee85ec59fd3c158206b
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296754"
---
# Windows Admin Center で仮想マシンの管理

>適用対象: Windows Admin Center、Windows Admin Center Preview

仮想マシン ツールは、サーバーまたはクラスター上で HYPER-V の役割が有効になっている場合は、[サーバー](manage-servers.md)、[フェールオーバー クラスター](manage-failover-clusters.md)または[ハイパーコンバージド クラスター](manage-hyper-converged.md)の接続で利用できます。 仮想マシンのツールを使用するには Windows Server 2012 を実行する HYPER-V ホストを管理するまたは Server Core またはデスクトップ エクスペリエンス搭載以降、いずれかをインストールします。 HYPER-V Server 2012 では、2016 および 2019 もサポートします。

## 主な機能

Windows Admin Center で仮想マシンのツールのハイライトは次のとおりです。

- **高度な HYPER-V ホストのリソースを監視します。** 1 つのダッシュ ボードで、全体的な CPU とメモリ使用率、IO パフォーマンス メトリック、VM の正常性アラートおよび HYPER-V ホスト サーバーまたはクラスター全体のイベントを表示します。
- **HYPER-V マネージャーとフェールオーバー クラスター マネージャーの機能を集める統一されたエクスペリエンスです。** クラスター間ですべての仮想マシンを表示し、高度な管理とトラブルシューティングのための単一の仮想マシンにドリルダウンします。
- **仮想マシンの管理の簡略化された、かつ強力なワークフローです。** 新しい UI エクスペリエンスは、作成、管理、仮想マシンをレプリケートする IT 管理のシナリオに合わせて調整します。

ここでは、HYPER-V タスクが Windows Admin Center で行うことができます。

- [HYPER-V ホストのリソースとパフォーマンスを監視します。](#monitor-hyper-v-host-resources-and-performance)
- [仮想マシンのインベントリを表示します。](#view-virtual-machine-inventory)
- [新しい仮想マシンを作成する](#create-a-new-virtual-machine)
- [仮想マシンの設定を変更します。](#change-virtual-machine-settings)
- [別のクラスター ノードに仮想マシンのライブ マイグレーションします。](#live-migrate-a-virtual-machine-to-another-cluster-node)
- [高度な管理と単一の仮想マシンのトラブルシューティング](#advanced-management-and-troubleshooting-for-a-single-virtual-machine)
- [HYPER-V ホスト (VMConnect) を通じて、仮想マシンの管理します。](#manage-a-virtual-machine-through-the-hyper-v-host-vmconnect)
- [HYPER-V ホストの設定を変更します。](#change-hyper-v-host-settings)
- [HYPER-V でイベント ログの表示](#view-hyper-v-event-logs)
- [Azure Site Recovery の仮想マシンを保護します。](#protect-virtual-machines-with-azure-site-recovery)

## HYPER-V ホストのリソースとパフォーマンスを監視します。

![仮想マシンの概要] 画面](../media/manage-virtual-machines/virtual-machines-summary.png)

1. 左側のナビゲーション ウィンドウから**仮想マシン**をクリックします。
2. **仮想マシン**のツール、 **[概要**] タブ、および**インベントリ**] タブの上部にある 2 つのタブがあります。**[概要**] タブでは、HYPER-V ホストのリソースと現在のサーバーまたはクラスター全体を次のパフォーマンスの全体像を提供します。
    - -動作している状態、オフでグループ化された Vm の数が一時停止され、保存
    - 最近の正常性アラートまたは HYPER-V イベント ログのイベント (アラートは Windows Server 2016 を実行しているハイパーコンバージド クラスターの利用可能な以降)
    - ホストとゲストの詳細と CPU とメモリの使用状況
    - CPU とメモリ リソースを消費最上位の Vm
    - ライブ データと履歴データ行 IOPS や IO スループットのグラフ (記憶域のパフォーマンスの線のグラフはのみ以降を Windows Server 2016 を実行しているハイパーコンバージド クラスターを使用します。 履歴データは、Windows Server 2019 を実行しているハイパーコンバージド クラスターのみ)

## 仮想マシンのインベントリを表示します。

![仮想マシンのインベントリ画面](../media/manage-virtual-machines/virtual-machines-inventory.png)

1. 左側のナビゲーション ウィンドウから**仮想マシン**をクリックします。
2. **仮想マシン**のツール、 **[概要**] タブ、および**インベントリ**] タブの上部にある 2 つのタブがあります。[**在庫**] タブでは、現在のサーバーまたはクラスター全体で利用可能な仮想マシンを一覧表示し、個々 の仮想マシンを管理するためのコマンドを提供します。 以下が可能です。
    - 現在のサーバーまたはクラスター上で実行される仮想マシンの一覧を表示します。
    - クラスターの仮想マシンを表示している場合は、仮想マシンの状態とホスト サーバーを表示します。 ホストの観点から、メモリ不足、メモリ要求し、割り当てられたメモリと、仮想マシンの稼働時間、ハートビートの状態および Azure Site Recovery を使用して保護の状態を含む CPU とメモリの使用状況を表示もできます。
    - [新しい仮想マシンを作成](#create-a-new-virtual-machine)します。
    - 削除、起動を無効にする、シャット ダウン、一時停止、再開、リセットまたは仮想マシンの名前を変更します。 仮想マシンを保存、保存した状態では、削除したり、チェックポイントを作成します。
    - [仮想マシンの設定を変更](#change-virtual-machine-settings)します。
    - HYPER-V ホストを経由 VMConnect を使用して仮想マシンのコンソールに接続します。
    - [Azure Site Recovery を使用して仮想マシンをレプリケート](#protect-virtual-machines-with-azure-site-recovery)します。
    - 一時停止、保存をシャット ダウンにスタート画面など、複数の Vm で実行できる操作の削除、リセット、複数の Vm を選択し、一度に操作を実行することができます。

注: クラスターに接続している場合、仮想マシンのみが表示されますクラスター化された仮想マシン。 仮想マシンの非クラスター化を今後も表示を計画しています。

## 新しい仮想マシンを作成する

![新しい仮想マシンの画面を作成します。](../media/manage-virtual-machines/new-vm.png)

1. 左側のナビゲーション ウィンドウから**仮想マシン**をクリックします。
2. 仮想マシンのツールの上部には、**インベントリ**] タブを選択し、新しい仮想マシンの作成を**新規作成**] をクリックします。
3. 仮想マシンの名前を入力し、1 と 2 世代仮想マシン間で選択します。
4. クラスター上で仮想マシンを作成する場合は、最初に、仮想マシンを作成するには、どのホストを選択できます。 Windows Server 2016 を実行している場合、後で、ツールでは、ホストの推奨事項します。
5. 仮想マシンのファイルのパスを選択します。 ドロップダウン リストからボリュームを選択するか、**参照**フォルダー ピッカーを使用してフォルダーを選択する] をクリックします。 仮想マシン構成ファイルと仮想ハード ディスク ファイルは、1 つのフォルダーの下に保存されます、`\Hyper-V\\[virtual machine name]`選択したボリュームまたはパスのパス。

>[!Tip]
> **フォルダー名**フィールドのパスを入力してフォルダー ピッカーで、ネットワーク上の任意の利用可能な SMB 共有を参照できる```\\server\share```します。 VM の記憶域のネットワーク共有を使用すると、 [CredSSP](../understand/faq.md#does-windows-admin-center-use-credssp)をが必要です。

6. 入れ子になった仮想化が有効になっているメモリの設定、ネットワーク アダプター、仮想ハード_ディスクを構成し、.iso イメージ ファイルから、またはネットワークからオペレーティング システムをインストールするかどうかを選択するかどうかは、仮想プロセッサの数を選択します。
7. **作成**仮想マシンを作成する] をクリックします。
8. 仮想マシンを作成し、仮想マシンの一覧に表示される、仮想マシンを開始できます。
9. 仮想マシンが起動されると、オペレーティング システムをインストールする VMConnect 経由で、仮想マシンのコンソールに接続できます。 一覧から、仮想マシンを選択し、[**詳細**] をクリックして > .rdp ファイルをダウンロードして**接続**します。 リモート デスクトップ接続アプリで .rdp ファイルを開きます。 これは、仮想マシンのコンソールに接続しているため、HYPER-V ホストの管理者の資格情報を入力する必要があります。

## 仮想マシンの設定を変更します。

![仮想マシンの設定画面](../media/manage-virtual-machines/vm-settings.png)

1. 左側のナビゲーション ウィンドウから**仮想マシン**をクリックします。
2. 仮想マシンのツールの上部には、選択**インベントリ**タブが、リストから仮想マシンを選択し、[**詳細**] をクリックして > **設定**します。
3. **一般的な****セキュリティ**、**メモリ**、**プロセッサ**、**ディスク**、**ネットワーク****ブート順**および**チェックポイント**のタブの切り替えし、必要な設定を構成、**保存**を保存する] をクリックしてください現在のタブの設定。 利用可能な設定については、仮想マシンの世代によって異なります。 また、仮想マシンを実行するため、一部の設定を変更できません、最初に、仮想マシンを停止する必要があります。

## 別のクラスター ノードに仮想マシンのライブ マイグレーションします。

クラスターに接続している場合は、別のクラスター ノードにライブ仮想マシンを移行できます。

1. フェールオーバー クラスターまたはハイパーコンバージド クラスターの接続では、左側のナビゲーション ウィンドウから**仮想マシン**をクリックします。
2. 仮想マシンのツールの上部には、選択**インベントリ**タブが、リストから仮想マシンを選択し、[**詳細**] をクリックして > **に移動**します。
3. 利用可能なクラスター ノードの一覧から、サーバーを選択し、**移動**] をクリックします。
4. Windows Admin Center の右上隅にある、移動の進行状況の通知が表示されます。 移動が成功した場合は、仮想マシンの一覧で変更ホスト サーバー名が表示されます。

## 高度な管理と単一の仮想マシンのトラブルシューティング

![単一の仮想マシンの詳細情報画面](../media/manage-virtual-machines/vm-details.png)

詳細な情報と、単一の仮想マシンのページから単一の仮想マシンのパフォーマンスのグラフを表示することができます。

1. 左側のナビゲーション ウィンドウから**仮想マシン**をクリックします。
2. 仮想マシンのツールの上部にある、仮想マシンの一覧から、仮想マシンの名前を**インベントリ**タブをクリックを選択します。
3. 単一の仮想マシンのページから、次のことができます。
    - 仮想マシンの詳細情報を表示します。
    - CPU、メモリ、ネットワーク、IOPS や IO スループットの Live との履歴データ行グラフを表示 (履歴データは Windows Server 2019 を実行しているハイパーコンバージド クラスターの利用可能なのみです)
    - 表示、作成、適用、名前を変更およびチェックポイントを削除します。
    - 仮想マシンの仮想ハード_ディスク (.vhd) ファイル、ネットワーク アダプターとホスト サーバーの詳細を表示します。
    - 削除、起動を無効にする、シャット ダウン、一時停止、再開、リセットまたは仮想マシンの名前を変更します。 仮想マシンを保存、保存した状態では、削除したり、チェックポイントを作成します。
    - [仮想マシンの設定を変更](#change-virtual-machine-settings)します。
    - HYPER-V ホストを経由 VMConnect を使用して仮想マシンのコンソールに接続します。
    - [Azure Site Recovery を使用して仮想マシンをレプリケート](#protect-virtual-machines-with-azure-site-recovery)します。

## HYPER-V ホスト (VMConnect) を通じて、仮想マシンの管理します。

![VM は、web ブラウザーから接続](../media/manage-virtual-machines/vm-connect.png)

1. 左側のナビゲーション ウィンドウから**仮想マシン**をクリックします。
2. 仮想マシンのツールの上部には、選択**インベントリ**タブが、リストから仮想マシンを選択し、[**詳細**] をクリックして > **Connect**または**ダウンロード RDP ファイル**。 **接続**を使用して、リモート デスクトップ web コンソール、Windows Admin Center に統合されたゲスト VM を操作するとできます。 **ダウンロード RDP ファイル**には、リモート デスクトップ接続のアプリケーション (mstsc.exe) で開くことができる .rdp ファイルがダウンロードされます。 どちらのオプションは、HYPER-V ホストを経由してゲスト VM の接続に VMConnect を使用して、HYPER-V ホスト サーバー管理者の資格情報を入力する必要があります。

## HYPER-V ホストの設定を変更します。

![HYPER-V ホストの設定画面](../media/manage-virtual-machines/host-settings.png)

1. Server、ハイパーコンバージド クラスターまたはフェールオーバー クラスターの接続では、左側のナビゲーション ウィンドウの下部にある [**設定**] メニューをクリックします。
2. HYPER-V ホスト サーバーまたはクラスターでは、上で次のセクションでは、 **HYPER-V ホストの設定**グループが表示されます。
    - [全般]: 変更仮想ハード ディスクと仮想マシン ファイル パス、およびハイパーバイザー スケジュールの種類 (サポートされる場合)
    - 拡張セッション モード
    - NUMA のカテゴリにわたる
    - ライブ マイグレーション
    - ストレージの移行
3. 任意の HYPER-V ホスト ハイパーコンバージド クラスターまたはフェールオーバー クラスターの接続の設定の変更を加えた場合、変更はすべてのクラスター ノードに適用されます。

## HYPER-V でイベント ログの表示

仮想マシン ツールから直接 HYPER-V イベント ログを確認することができます。

1. 左側のナビゲーション ウィンドウから**仮想マシン**をクリックします。
2. 仮想マシンのツールの上部には、 **[概要**] タブを選択します。上の適切なイベント セクションでは、**すべてのイベントの表示**をクリックします。
3. イベント ビューアー ツールは、左側のウィンドウで HYPER-V イベント チャネルに表示されます。 右側のウィンドウで、イベントを表示するためのチャネルを選択します。 フェールオーバー クラスターまたはハイパーコンバージド クラスターを管理している場合、イベント ログ、マシンの列にホスト サーバーを表示する、すべてのクラスター ノードのイベントが表示されます。

## Azure Site Recovery の仮想マシンを保護します。

Windows Admin Center を使用して、Azure Site Recovery を構成し、オンプレミスの仮想マシンを Azure にレプリケートすることができます。 [詳細情報](../azure/azure-site-recovery.md)

## 複数の受信

Windows Admin Center での仮想マシンの管理は、開発中はアクティブにし、新しい機能は、近い将来追加します。 UserVoice では、状態と機能の投票を表示できます。

|機能の要求|
|-------|
|[仮想マシンのインポート/エクスポート](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31481971--virtual-machines-import-export-vms)|
|[フォルダー内の仮想マシンの並べ替え](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31494712--virtual-machines-ability-to-sort-vm-into-folder)|
|[仮想マシンの設定をサポートします。](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31915264--virtual-machines-expose-all-configurable-setting)|
|[HYPER-V レプリカのサポート](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/32040253--virtual-machines-setup-and-manage-hyper-v-replic)|
|[仮想マシンの所有権を委任します。](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31663837--virtual-machines-owner-delegation)|
|[仮想マシンを複製します。](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31783288--virtual-machines-add-a-button-to-clone-a-vm)|
|[既存の仮想マシンからテンプレートを作成します。](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31494649--virtual-machines-create-a-template-from-an-exist)|
|[HYPER-V ホストの間で仮想マシンの表示](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31734559--virtual-machines-find-vms-on-host-screen)|
|[新しい仮想マシンのウィンドウで VLAN を構成します。](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31710979--virtual-machines-new-new-vm-pane-need-vlan-opt)|
|[**すべてを参照するか、新しい機能を提案します。**](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5Bvirtual%20machines%5D)|
