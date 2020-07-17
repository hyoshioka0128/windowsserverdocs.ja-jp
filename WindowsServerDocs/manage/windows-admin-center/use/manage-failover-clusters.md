---
title: Windows 管理センターを使用してフェールオーバークラスターを管理する
description: Windows 管理センター (Project ホノルル) を使用してフェールオーバークラスターを管理する
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: b7f015ac4c9906447069501bf0922b36306a51d7
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950495"
---
# <a name="manage-failover-clusters-with-windows-admin-center"></a>Windows 管理センターを使用してフェールオーバークラスターを管理する

>適用対象: Windows Admin Center、Windows Admin Center Preview

> [!Tip]
> Windows Admin Center を初めて使用する場合
> [Windows 管理センターの詳細については、](../overview.md)こちらを参照してください。

## <a name="managing-failover-clusters"></a>フェールオーバークラスターの管理
[フェールオーバークラスタリング](https://docs.microsoft.com/windows-server/failover-clustering/failover-clustering-overview)は、複数のサーバーを1つのフォールトトレラントクラスターにグループ化して、スケールアウトファイルサーバー、hyper-v、Microsoft SQL Server などのアプリケーションとサービスの可用性とスケーラビリティを向上させることができる Windows Server の機能です。

フェールオーバークラスターノードは、Windows 管理センターで[サーバー接続](manage-servers.md)として追加することで、個々のサーバーとして管理できますが、フェールオーバークラスターとして追加して、クラスターリソース、記憶域、ネットワーク、ノード、役割、仮想マシン、仮想スイッチを表示および管理することもできます。

![フェールオーバークラスターの概要画面](../media/manage-failover-clusters/fcm-overview.png)

## <a name="adding-a-failover-cluster-to-windows-admin-center"></a>Windows 管理センターへのフェールオーバークラスターの追加
Windows 管理センターにクラスターを追加するには:

1. すべての接続 の下にある  **+ 追加** をクリックします。
2. **フェールオーバー接続**を追加することを選択します。
3. クラスターの名前を入力し、メッセージが表示されたら、使用する資格情報を入力します。
4. Windows 管理センターでクラスターノードを個々のサーバー接続として追加することもできます。
5. **[送信]** をクリックして完了します。

クラスターが [概要] ページの接続リストに追加されます。 クラスターに接続するには、これをクリックします。

> [!NOTE]
> Windows 管理センターでクラスターをハイパー集約された[クラスター接続](manage-hyper-converged.md)として追加することで、ハイパー収束クラスターを管理することもできます。

## <a name="tools"></a>ツール

フェールオーバークラスター接続では、次のツールを使用できます。

| ツール | 説明 |
| ---- | ----------- |
| 概要 | フェールオーバークラスターの詳細の表示とクラスターリソースの管理 |
| ディスク | クラスターの共有ディスクとボリュームを表示する |
| ネットワーク | クラスター内のネットワークを表示する |
| ノード | クラスターノードの表示と管理 |
| 役割 | クラスターの役割を管理するか、空の役割を作成する |
| 更新 | クラスター対応更新の管理 ( [CredSSP](../understand/faq.md#does-windows-admin-center-use-credssp)が必要) |
| [仮想マシン](manage-virtual-machines.md) | バーチャルマシンの表示と管理 |
| 仮想スイッチ | 仮想スイッチの表示と管理 |

## <a name="more-coming"></a>その他の準備

Windows 管理センターでのフェールオーバークラスター管理は積極的に開発中であり、新しい機能は近い将来追加される予定です。 UserVoice の機能の状態と投票を確認できます。

|機能の要求|
|-------|
| [クラスター化されたディスク情報の表示](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31740424--cluster-more-disk-info-in-failover-cluster-manag) |
| [追加のクラスターアクションのサポート](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/33558076--fcm-full-csv-management-cycle-in-one-place) |
| [異なるクラスターで Hyper-v とスケールアウトファイルサーバーを実行する収束クラスターをサポートする](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31729741--cluster-support-for-converged-architecture) |
| [CSV ブロックキャッシュの表示](https://windowsserver.uservoice.com/forums/295071-management-tools/suggestions/31669477--cluster-csv-block-cache) |
| [すべて表示するか、新しい機能を提案します](https://windowsserver.uservoice.com/forums/295071/filters/top?category_id=319162&query=%5Bcluster%5D) |