---
title: Windows Admin Center でのフェールオーバー クラスターを管理します。
description: Windows Admin Center (Project Honolulu) でのフェールオーバー クラスターを管理します。
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 63f5fca8e7ef63200e01cfc6e00a979e7f045b51
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296674"
---
# Windows Admin Center でのフェールオーバー クラスターを管理します。

>適用対象: Windows Admin Center、Windows Admin Center Preview

> [!Tip]
> Windows Admin Center を初めて使用する場合
> [Windows Admin Center についての詳細を確認する](../understand/windows-admin-center.md)か、[今すぐダウンロード](https://aka.ms/windowsadmincenter)してください。

## フェールオーバー クラスターを管理します。
アプリケーションとスケール アウト ファイル サーバー、HYPER-V などのサービスの可用性とスケーラビリティを向上するフォールト トレラント クラスターに複数のサーバーをグループ化できる Windows Server の機能は、[フェールオーバー クラスタ リング](https://docs.microsoft.com/windows-server/failover-clustering/failover-clustering-overview)とMicrosoft SQL Server します。

個々 のサーバーとしてフェールオーバー クラスターのノードを管理するには、Windows Admin Center で[サーバー接続](manage-servers.md)として追加し、中にすることもに追加するフェールオーバー クラスターの表示およびクラスター リソース、ストレージ、ネットワーク、ノード、仮想の役割を管理するにはコンピューターと仮想スイッチ。

![フェールオーバー クラスターの概要] 画面](../media/manage-failover-clusters/fcm-overview.png)

## Windows Admin Center にフェールオーバー クラスターを追加します。
Windows Admin Center のクラスターを追加します。

1. すべての接続 [ **+ 追加]** をクリックします。
2. 選択すると、**フェールオーバーの接続**を追加します。
3. クラスターの名前を入力し、使用する資格情報を要求します。
4. Windows Admin Center で個々 のサーバーの接続と、クラスター ノードを追加するオプションがあります。
5. 終了するための**送信**] をクリックします。

クラスターは、概要ページで、接続の一覧に追加されます。 クラスターへの接続にクリックします。

> [!NOTE]
> 管理することも、ハイパーコンバージド クラスターとして Windows Admin Center で[ハイパーコンバージド クラスター接続](manage-hyper-converged.md)クラスターに追加します。

## ツール

次のツールは、フェールオーバー クラスターの接続に使用できます。

| ツール | 説明 |
| ---- | ----------- |
| 概要 | フェールオーバー クラスターの詳細を表示およびクラスター リソースの管理 |
| ディスク | ビューのクラスターの共有ディスクとボリューム |
| ネットワーク | クラスターのネットワークの表示 |
| ノード | 表示し、クラスター ノードの管理 |
| ロール | クラスターの役割を管理または空の役割を作成します。 |
| アップデート | ( [CredSSP](../understand/faq.md#does-windows-admin-center-use-credssp)が必要) クラスター対応更新プログラムの管理します。 |
| [仮想マシン](manage-virtual-machines.md) | 表示し、仮想マシンの管理 |
| 仮想スイッチ | 表示し、仮想スイッチの管理 |

## 複数の受信

Windows Admin Center でのフェールオーバー クラスターの管理は、開発中はアクティブにし、新しい機能は、近い将来追加します。 UserVoice では、状態と機能の投票を表示できます。

|機能の要求|
|-------|
| [クラスター化されたディスクの詳細を表示します。](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31740424--cluster-more-disk-info-in-failover-cluster-manag) |
| [追加のクラスター操作をサポートします。](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/33558076--fcm-full-csv-management-cycle-in-one-place) |
| [HYPER-V とスケール アウト ファイル サーバーを別のクラスターで実行されているコンバージド クラスターをサポートします。](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31729741--cluster-support-for-converged-architecture) |
| [ビューの CSV ブロックのキャッシュ](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31669477--cluster-csv-block-cache) |
| [すべてを参照するか、新しい機能を提案します。](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5Bcluster%5D) |