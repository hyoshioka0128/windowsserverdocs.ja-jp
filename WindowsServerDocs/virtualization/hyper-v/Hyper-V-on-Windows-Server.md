---
title: Windows Server 上の Hyper-V
description: Hyper-v の実行、計画、展開、および管理に関する主要な記事へのリンクを提供します。
manager: dongill
ms.topic: article
ms.assetid: 0baef6b8-598c-4fe0-9f31-5869fc4e0f69
author: kbdazure
ms.author: kathydav
ms.date: 10/07/2016
ms.openlocfilehash: 61ed737c72e65fa040e09c546998542734457e89
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87960815"
---
# <a name="hyper-v-on-windows-server"></a>Windows Server 上の Hyper-V

>適用先:Windows Server 2019、Windows Server 2016

Windows Server での HYPER-V ロール、仮想化のコンピューティング環境を作成および、仮想マシンの管理を作成します。 1 つの物理コンピューターで複数のオペレーティング システムを実行し、個々 のオペレーティング システムを分離できます。 このテクノロジで、コンピューティング リソースの効率を向上し、ハードウェア リソースを解放できます。

Windows Server の Hyper-v の詳細については、次の表のトピックを参照してください。

## <a name="hyper-v-resources-for-it-pros"></a>IT プロフェッショナル向けの HYPER-V のリソース

|タスク |リソース|
|---|---|
|![要件が満たされていることを示すチェックマークとドキュメントアイコン](media/All_Symbols_MeetsRequirements.png)|**Hyper V を評価します。**<p>- [Hyper-v テクノロジの概要](Hyper-V-Technology-Overview.md)<br />- [Windows Server での Hyper-v の新機能](What-s-new-in-Hyper-V-on-Windows.md)<br />- [Windows Server 上の Hyper-v のシステム要件](System-requirements-for-Hyper-V-on-Windows.md)<br />- [Hyper-v でサポートされている Windows ゲストオペレーティングシステム](Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows.md) <br />- [サポートされている Linux および FreeBSD の仮想マシン](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)<br />- [世代とゲストによる機能の互換性](Hyper-V-feature-compatibility-by-generation-and-guest.md) <p>**HYPER-V の計画**<p>- [Hyper-v に第1世代または第2世代の仮想マシンを作成する必要がありますか。](plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md) <br />- [Windows Server での Hyper-v のスケーラビリティの計画](plan/plan-hyper-v-scalability-in-windows-server.md) <br />- [Windows Server での Hyper-v ネットワークの計画](plan/plan-hyper-v-networking-in-windows-server.md) <br />- [Windows Server での Hyper-v セキュリティの計画](plan/plan-hyper-v-security-in-windows-server.md)|
|![カーソルとサンバースト] アイコン](media/All_Symbols_GetStarted.png)|**Hyper-v を使ってみる**<p>- [Windows Server 2019 をダウンロードしてインストールする](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019)<p>**バーチャルマシンホストとしての Windows Server 2019 の server Core または GUI インストールオプション**<p>- [Windows Server に Hyper-v の役割をインストールする](get-started/Install-the-Hyper-V-role-on-Windows-Server.md)<br />- [Hyper-v 仮想マシンの仮想スイッチを作成する](get-started/Create-a-virtual-switch-for-Hyper-V-virtual-machines.md)<br />- [Hyper-v での仮想マシンの作成](get-started/Create-a-virtual-machine-in-Hyper-V.md)|
|![人とツール] アイコン](media/All_Symbols_Administrator.png)|**HYPER-V ホストと仮想マシンをアップグレードします。**<p>- [Windows Server クラスターノードのアップグレード](../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md)<br />- [仮想マシンのバージョンのアップグレード](deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md)<p>**構成および HYPER-V を管理します。**<p>- [フェールオーバークラスタリングを使用しないライブマイグレーションのホストの設定](deploy/Set-up-hosts-for-live-migration-without-Failover-Clustering.md)<br />- [Nano Server のリモート管理](../../get-started/manage-nano-server.md)<br />- [標準チェックポイントまたは運用チェックポイントの選択](manage/Choose-between-standard-or-production-checkpoints-in-Hyper-V.md)<br />- [チェックポイントを有効または無効にする](manage/Enable-or-disable-checkpoints-in-Hyper-V.md)<br />- [PowerShell Direct を使用して Windows 仮想マシンを管理する](manage/Manage-Windows-virtual-machines-with-PowerShell-Direct.md)<br />- [Hyper-v レプリカのセットアップ](manage/Set-up-Hyper-V-Replica.md)|
|![メッセージ交換バブル アイコン](media/All_Symbols_Chat.png)|**ブログ**<p>マイクロソフトの仮想化と HYPER-V チームのプログラム マネージャー、プロダクト マネージャー、開発者およびテスト担当者から、最新の投稿をご覧ください。<p>- [仮想化のブログ](https://blogs.technet.com/b/virtualization/)<br />- [Windows Server ブログ](https://blogs.technet.com/b/windowsserver/)<br />- [Ben Armstrong の仮想化](https://blogs.msdn.com/b/virtual_pc_guy/)に関するブログ (アーカイブ済み)|
|![ユーザー グループのアイコン](media/All_Symbols_Users_Group.png)|**フォーラムやニュースグループ**<p>ご不明な点がある場合は、 ディスカッションに役立てて、Mvp、および HYPER-V の製品チームに問い合わせてください。<p>- [Windows Server コミュニティ](https://techcommunity.microsoft.com/t5/Windows-Server/ct-p/Windows-Server)<br />- [Windows Server Hyper-v TechNet フォーラム](https://docs.microsoft.com/answers/topics/windows-server-hyper-v.html)|

## <a name="related-technologies"></a>関連テクノロジ

次の表には、コンピューティング環境の仮想化に使用する場合がありますテクノロジが一覧表示します。

|テクノロジ|説明|
|--------------|---------------|
|[クライアント Hyper-V](https://docs.microsoft.com/virtualization/hyper-v-on-windows/index)|Windows 8、Windows 8.1 およびを使ってインストールできる Windows 10 に含まれている仮想化テクノロジ **プログラムと機能** で、 **コントロール パネルの [** します。|
|[フェールオーバー クラスタリング](https://docs.microsoft.com/windows-server/failover-clustering/whats-new-in-failover-clustering)|HYPER-V ホストと仮想マシンの高可用性を提供する Windows Server 機能です。|
|[Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/overview)|仮想化されたデータ センターの管理ソリューションを提供する system Center コンポーネント。 構成して作成および仮想マシンとサービスを作成したプライベート クラウドに展開できるように、仮想化ホスト、ネットワーク、および記憶域リソースを管理します。|
|[Windows コンテナー](https://docs.microsoft.com/virtualization/windowscontainers/)|Windows Server と HYPER-V のコンテナーを使用して、開発、テスト、および運用チームのための標準化された環境を提供します。|