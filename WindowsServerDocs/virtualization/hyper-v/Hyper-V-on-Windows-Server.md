---
title: Windows Server 上の Hyper-V
description: Hyper-v の実行、計画、展開、および管理に関する主要な記事へのリンクを提供します。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0baef6b8-598c-4fe0-9f31-5869fc4e0f69
author: KBDAzure
ms.author: kathydav
ms.date: 10/07/2016
ms.openlocfilehash: 558733e3472578d1df413fe220f1846debc0f358
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366845"
---
# <a name="hyper-v-on-windows-server"></a>Windows Server 上の Hyper-V

>適用先:Windows Server 2016、Windows Server 2019

Windows Server での Hyper-V ロール、仮想化のコンピューティング環境を作成および、仮想マシンの管理を作成します。 1 つの物理コンピューターで複数のオペレーティング システムを実行し、個々 のオペレーティング システムを分離できます。 このテクノロジで、コンピューティング リソースの効率を向上し、ハードウェア リソースを解放できます。

Windows Server の Hyper-v の詳細については、次の表のトピックを参照してください。

## <a name="hyper-v-resources-for-it-pros"></a>IT プロフェッショナル向けの HYPER-V のリソース

|タスク |リソース|
|---|---|
|![要件が満たされていることを示すチェックマークとドキュメントアイコン](media/All_Symbols_MeetsRequirements.png)|**Hyper-v の評価**<br /><br />- [Hyper-v テクノロジの概要](Hyper-V-Technology-Overview.md)<br />- [Windows Server での hyper-v の新機能](What-s-new-in-Hyper-V-on-Windows.md)<br />- [Windows Server 上の hyper-v のシステム要件](System-requirements-for-Hyper-V-on-Windows.md)<br />-  で[サポートされている Windows ゲストオペレーティングシステム (hyper-v)](Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows.md) <br />-  で[サポートされている Linux および FreeBSD の仮想マシン](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)<br />- [世代とゲストの機能の互換性](Hyper-V-feature-compatibility-by-generation-and-guest.md) <br /><br />**Hyper-v の計画**<br /><br />-  は、[hyper-v に第1世代または第2世代の仮想マシンを作成する必要がありますか。](plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md) <br />- [Windows Server での hyper-v のスケーラビリティの計画](plan/plan-hyper-v-scalability-in-windows-server.md) <br />- [Windows Server での hyper-v ネットワークの計画](plan/plan-hyper-v-networking-in-windows-server.md) <br />- [Windows Server での hyper-v セキュリティの計画](plan/plan-hyper-v-security-in-windows-server.md)|
|![カーソルとサンバースト アイコン](media/All_Symbols_GetStarted.png)|**Hyper-v を使ってみる**<br /><br />- [Windows Server 2019 をダウンロードしてインストールし](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019)ます。<br /><br />**バーチャルマシンホストとしての Windows Server 2019 の server Core または GUI インストールオプション**<br /><br />- [Windows Server に hyper-v の役割をインストールする](get-started/Install-the-Hyper-V-role-on-Windows-Server.md)<br />- [hyper-v 仮想マシンの仮想スイッチを作成する](get-started/Create-a-virtual-switch-for-Hyper-V-virtual-machines.md)<br />- [hyper-v で仮想マシンを作成する](get-started/Create-a-virtual-machine-in-Hyper-V.md)|
|![人とツール アイコン](media/All_Symbols_Administrator.png)|**Hyper-v ホストと仮想マシンのアップグレード**<br /><br />- [Windows Server クラスターノードのアップグレード](../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md)<br />- [仮想マシンのバージョンのアップグレード](deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md)<br /><br />**Hyper-v の構成と管理**<br /><br />- [フェールオーバークラスタリングを使用しないライブマイグレーション用にホストを設定する](deploy/Set-up-hosts-for-live-migration-without-Failover-Clustering.md)<br />- [Nano Server をリモートで管理する](../../get-started/manage-nano-server.md)<br />- [標準チェックポイントまたは運用チェックポイントを選択し](manage/Choose-between-standard-or-production-checkpoints-in-Hyper-V.md)ます<br />- [チェックポイントを有効または無効に](manage/Enable-or-disable-checkpoints-in-Hyper-V.md)します<br />- [PowerShell Direct を使用して Windows 仮想マシンを管理](manage/Manage-Windows-virtual-machines-with-PowerShell-Direct.md)する<br />- [Hyper-v レプリカのセットアップ](manage/Set-up-Hyper-V-Replica.md)|
|![メッセージ交換バブル アイコン](media/All_Symbols_Chat.png)|**Blog**<br /><br />マイクロソフトの仮想化と HYPER-V チームのプログラム マネージャー、プロダクト マネージャー、開発者およびテスト担当者から、最新の投稿をご覧ください。<br /><br />- [仮想化のブログ](https://blogs.technet.com/b/virtualization/)<br />- [Windows Server ブログ](https://blogs.technet.com/b/windowsserver/)<br />- [Ben Armstrong の仮想化ブログ](https://blogs.msdn.com/b/virtual_pc_guy/)(アーカイブ済み)|
|![ユーザー グループのアイコン](media/All_Symbols_Users_Group.png)|**フォーラムとニュースグループ**<br /><br />質問がある場合 ディスカッションに役立てて、Mvp、および HYPER-V の製品チームに問い合わせてください。<br /><br />- [Windows Server コミュニティ](https://techcommunity.microsoft.com/t5/Windows-Server/ct-p/Windows-Server)<br />- [Windows Server Hyper-v TechNet フォーラム](https://social.technet.microsoft.com/Forums/windowsserver/home?forum=winserverhyperv)|

## <a name="related-technologies"></a>関連テクノロジ

次の表には、コンピューティング環境の仮想化に使用する場合がありますテクノロジが一覧表示します。

|テクノロジ|説明|
|--------------|---------------|
|[クライアント Hyper-v](https://docs.microsoft.com/virtualization/hyper-v-on-windows/index)|Windows 8、Windows 8.1 およびを使ってインストールできる Windows 10 に含まれている仮想化テクノロジ **プログラムと機能** で、 **コントロール パネルの**します。|
|[フェールオーバー クラスタリング](https://docs.microsoft.com/windows-server/failover-clustering/whats-new-in-failover-clustering)|HYPER-V ホストと仮想マシンの高可用性を提供する Windows Server 機能です。|
|[Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/overview)|仮想化されたデータ センターの管理ソリューションを提供する system Center コンポーネント。 構成して作成および仮想マシンとサービスを作成したプライベート クラウドに展開できるように、仮想化ホスト、ネットワーク、および記憶域リソースを管理します。|
|[Windows コンテナー](https://docs.microsoft.com/virtualization/windowscontainers/)|Windows Server と HYPER-V のコンテナーを使用して、開発、テスト、および運用チームのための標準化された環境を提供します。|