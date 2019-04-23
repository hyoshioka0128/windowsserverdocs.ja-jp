---
title: Windows server Hyper-v
description: については、試して、計画、展開、および HYPER-V を管理するキーの記事へのリンクを提供します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0baef6b8-598c-4fe0-9f31-5869fc4e0f69
author: KBDAzure
ms.author: kathydav
ms.date: 10/07/2016
ms.openlocfilehash: 1a658b611b68d7ecde64bdf0f8a318cc1af2804c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880263"
---
# <a name="hyper-v-on-windows-server"></a>Windows server Hyper-v

>適用先:Windows Server 2016、Windows Server 2019

Windows Server での HYPER-V ロール、仮想化のコンピューティング環境を作成および、バーチャル マシンの管理を作成します。 1 つの物理コンピューターで複数のオペレーティング システムを実行し、個々 のオペレーティング システムを分離できます。 このテクノロジで、コンピューティング リソースの効率を向上し、ハードウェア リソースを解放できます。

Windows server、HYPER-V の詳細については、次の表の各トピックを参照してください。

## <a name="hyper-v-resources-for-it-pros"></a>IT プロフェッショナル向けの HYPER-V のリソース

|タスク |参考資料|
|---|---|
|![要件を満たしているを表示するマークとドキュメントのアイコンを確認してください。](media/All_Symbols_MeetsRequirements.png)|**Hyper V を評価します。**<br /><br />- [HYPER-V テクノロジの概要](Hyper-V-Technology-Overview.md)<br />- [新機能 Windows server、HYPER-V の新機能](What-s-new-in-Hyper-V-on-Windows.md)<br />- [Windows server、HYPER-V のシステム要件](System-requirements-for-Hyper-V-on-Windows.md)<br />- [HYPER-V 用の Windows ゲスト オペレーティング システムがサポートされています。](Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows.md) <br />- [サポートされている Linux および FreeBSD の仮想マシン](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)<br />- [機能の生成とゲストの互換性](Hyper-V-feature-compatibility-by-generation-and-guest.md) <br /><br />**HYPER-V を計画します。**<br /><br />- [HYPER-V にジェネレーション 1 または 2 仮想マシンを作成する必要があります。](plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md) <br />- [Windows Server での HYPER-V のスケーラビリティの計画します。](plan/plan-hyper-v-scalability-in-windows-server.md) <br />- [Windows server、HYPER-V ネットワークの計画します。](plan/plan-hyper-v-networking-in-windows-server.md) <br />- [Windows server、HYPER-V のセキュリティを計画します。](plan/plan-hyper-v-security-in-windows-server.md)|
|![カーソルとサンバースト アイコン](media/All_Symbols_GetStarted.png)|**HYPER-V を概要します。**<br /><br />- [ダウンロードし、Windows Server 2019 のインストール](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019)<br /><br />**バーチャル マシン ホストとしては、server Core または GUI、Windows Server 2019 のインストール オプション**<br /><br />- [Windows server、HYPER-V の役割をインストールします。](get-started/Install-the-Hyper-V-role-on-Windows-Server.md)<br />- [HYPER-V 仮想マシン用の仮想スイッチを作成します。](get-started/Create-a-virtual-switch-for-Hyper-V-virtual-machines.md)<br />- [HYPER-V で仮想マシンを作成します。](get-started/Create-a-virtual-machine-in-Hyper-V.md)|
|![人とツール アイコン](media/All_Symbols_Administrator.png)|**HYPER-V ホストとバーチャル マシンをアップグレードします。**<br /><br />- [Windows Server クラスター ノードをアップグレードします。](../../failover-clustering/Cluster-Operating-System-Rolling-Upgrade.md)<br />- [仮想マシンのバージョンをアップグレードします。](deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md)<br /><br />**構成および HYPER-V を管理します。**<br /><br />- [フェールオーバー クラスタ リングのないライブ マイグレーションのホストの設定します。](deploy/Set-up-hosts-for-live-migration-without-Failover-Clustering.md)<br />- [Nano Server をリモートで管理します。](../../get-started/manage-nano-server.md)<br />- [標準または実稼働のチェックポイント間での選択します。](manage/Choose-between-standard-or-production-checkpoints-in-Hyper-V.md)<br />- [有効にするか、チェックポイントを無効にします。](manage/Enable-or-disable-checkpoints-in-Hyper-V.md)<br />- [PowerShell ダイレクトでの Windows 仮想マシンを管理します。](manage/Manage-Windows-virtual-machines-with-PowerShell-Direct.md)<br />- [HYPER-V レプリカを設定します。](manage/Set-up-Hyper-V-Replica.md)|
|![メッセージ交換バブル アイコン](media/All_Symbols_Chat.png)|**ブログ**<br /><br />マイクロソフトの仮想化と HYPER-V チームのプログラム マネージャー、プロダクト マネージャー、開発者およびテスト担当者から、最新の投稿をご覧ください。<br /><br />- [仮想化のブログ](https://blogs.technet.com/b/virtualization/)<br />- [Windows Server ブログ](https://blogs.technet.com/b/windowsserver/)<br />- [Ben Armstrong の仮想化ブログ](https://blogs.msdn.com/b/virtual_pc_guy/)(アーカイブ)|
|![ユーザー グループのアイコン](media/All_Symbols_Users_Group.png)|**フォーラムとニュースグループ**<br /><br />質問がある場合 ディスカッションに役立てて、Mvp、および HYPER-V の製品チームに問い合わせてください。<br /><br />- [Windows Server コミュニティ](https://techcommunity.microsoft.com/t5/Windows-Server/ct-p/Windows-Server)<br />- [Windows Server、HYPER-V の TechNet フォーラム](https://social.technet.microsoft.com/Forums/windowsserver/home?forum=winserverhyperv)|

## <a name="related-technologies"></a>関連テクノロジ

次の表には、コンピューティング環境の仮想化に使用する場合がありますテクノロジが一覧表示します。

|テクノロジ|説明|
|--------------|---------------|
|[クライアント Hyper-v](https://docs.microsoft.com/virtualization/hyper-v-on-windows/index)|Windows 8、Windows 8.1 およびを使ってインストールできる Windows 10 に含まれている仮想化テクノロジ **プログラムと機能** で、 **コントロール パネルの **します。|
|[フェールオーバー クラスタ リング](https://docs.microsoft.com/windows-server/failover-clustering/whats-new-in-failover-clustering)|HYPER-V ホストとバーチャル マシンの高可用性を提供する Windows Server 機能です。|
|[Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/overview)|仮想化されたデータ センターの管理ソリューションを提供する system Center コンポーネント。 構成して作成および仮想マシンとサービスを作成したプライベート クラウドに展開できるように、仮想化ホスト、ネットワーク、および記憶域リソースを管理します。|
|[Windows コンテナー](https://docs.microsoft.com/virtualization/windowscontainers/)|Windows Server と HYPER-V のコンテナーを使用して、開発、テスト、および運用チームのための標準化された環境を提供します。|