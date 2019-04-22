---
title: Windows Admin Center でのフェールオーバー クラスターを管理します。
description: Windows Admin Center (プロジェクト ホノルル) でのフェールオーバー クラスターを管理します。
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: f7e14581f7f6b14b0cf39308de236b68a07e8c9f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824073"
---
# <a name="manage-failover-clusters-with-windows-admin-center"></a>Windows Admin Center でのフェールオーバー クラスターを管理します。

>適用先:Windows Admin Center、Windows Admin Center プレビュー

> [!Tip]
> Windows Admin Center を初めて使用する場合
> [Windows Admin Center についての詳細を確認する](../understand/windows-admin-center.md)か、[今すぐダウンロード](https://aka.ms/windowsadmincenter)してください。

## <a name="managing-failover-clusters"></a>フェールオーバー クラスターの管理
[フェールオーバー クラスタ リング](https://docs.microsoft.com/windows-server/failover-clustering/failover-clustering-overview)Windows Server の機能をアプリケーションとスケール アウト ファイル サーバー、HYPER-V などのサービスの可用性とスケーラビリティを高めるフォールト トレラント クラスターに複数のサーバーをグループ化することができますが、Microsoft SQL Server。

として追加することで、個々 のサーバーとしてのフェールオーバー クラスター ノードを管理できる[サーバー接続](manage-servers.md)Windows Admin Center で追加することもそれらを表示および管理クラスターのリソース、ストレージ、ネットワーク、ノードのフェールオーバー クラスター役割、仮想マシンおよび仮想スイッチ。

![フェールオーバー クラスターの概要画面](../media/manage-failover-clusters/fcm-overview.png)

## <a name="adding-a-failover-cluster-to-windows-admin-center"></a>Windows Admin Center へのフェールオーバー クラスターの追加
クラスターを Windows Admin Center に追加します。

1. クリックして **+ 追加**すべての接続。
2. 追加することも、**フェールオーバー接続**します。
3. クラスターの名前を入力し、使用する資格情報を求められた場合。
4. Windows Admin Center での個々 のサーバー接続とクラスター ノードを追加することが必要です。
5. クリックして**送信**を完了します。

クラスターは、[概要] ページの接続一覧に追加されます。 クラスターに接続するようにクリックします。

> [!NOTE]
> 管理することも、ハイパーコンバージド クラスターとしてクラスターを追加することで、 [Hyper-Converged クラスター接続](manage-hyper-converged.md)Windows Admin Center でします。

## <a name="tools"></a>ツール

次のツールは、フェールオーバー クラスターの接続の場合に。

| ツール | 説明 |
| ---- | ----------- |
| 概要 | フェールオーバー クラスターの詳細を表示し、クラスター リソースの管理 |
| ディスク | ビューのクラスター共有ディスクとボリューム |
| ネットワーク | クラスターのネットワークの表示 |
| ノード | 表示し、クラスター ノードの管理 |
| ロール | クラスターの役割を管理または空のロールを作成します。 |
| 更新プログラム | クラスター対応更新プログラムを管理します。 |
| [仮想マシン](manage-virtual-machines.md) | 表示し、仮想マシンの管理 |
| 仮想スイッチ | 表示し、仮想スイッチの管理 |

## <a name="more-coming"></a>今後追加されます。

Windows Admin Center でのフェールオーバー クラスターの管理は開発中にアクティブにし、新しい機能が、近い将来に追加します。 UserVoice では、状態と機能の投票を表示できます。

|機能のリクエスト|
|-------|
| [クラスター化されたディスクの詳細を表示します。](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31740424--cluster-more-disk-info-in-failover-cluster-manag) |
| [追加のクラスター操作をサポートします。](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/33558076--fcm-full-csv-management-cycle-in-one-place) |
| [Hyper-v ホストとスケール アウト ファイル サーバーを別のクラスターで実行されている収束のクラスターをサポートします。](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31729741--cluster-support-for-converged-architecture) |
| [ビューに CSV ブロック キャッシュ](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31669477--cluster-csv-block-cache) |
| [すべてを参照するか、新しい機能の提案](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5Bcluster%5D) |