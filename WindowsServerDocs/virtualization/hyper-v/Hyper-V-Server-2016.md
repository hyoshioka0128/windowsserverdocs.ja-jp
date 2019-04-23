---
title: Microsoft Hyper-V Server 2016
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f815ada0-4c63-4e73-9c24-dc5eb21526c7
author: KBDAzure
ms.author: kathydav
ms.date: 07/26/2017
ms.openlocfilehash: 9a1b6ea7b9abc94f63a1390b6fa18e4c8d4a1822
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839373"
---
# <a name="microsoft-hyper-v-server-2016"></a>Microsoft Hyper-V Server 2016

Microsoft HYPER-V Server 2016 は、スタンドアロン\-Windows ハイパーバイザーのみ、Windows Server ドライバー モデル、および仮想化コンポーネントを含むだけでの製品です。 これは、サーバー使用率の向上し、コストの削減に役立つシンプルで信頼性の高い仮想化ソリューションを提供します。

Microsoft HYPER-V Server 2016、Windows ハイパーバイザー テクノロジは、ハイパースレッディングがあるものと同じ\-Windows Server 2016 での役割をインストールします。 そのため、多くの Hyper の使用可能なコンテンツ\-Windows Server 2016 での役割のインストールは、Microsoft HYPER-V Server 2016 にも適用されます。

## <a name="hyper-v-server-resources-for-it-pros"></a>ハイパー\-IT プロフェッショナル向けの V サーバー リソース

|処理手順|参考資料|
|-|-|
|![シンボルの要件を満たしています。](media/All_Symbols_MeetsRequirements.png)|**Hyper V を評価します。**<br /><br />-   [HYPER-V テクノロジの概要](hyper-v-technology-overview.md)<br />- [新機能 Windows Server 2016 で HYPER-V の新機能](what-s-new-in-hyper-v-on-windows.md)<br />-   [Windows Server 2016 で HYPER-V のシステム要件](system-requirements-for-hyper-v-on-windows.md)<br />-   [HYPER-V 用の Windows ゲスト オペレーティング システムがサポートされています。](supported-windows-guest-operating-systems-for-hyper-v-on-windows.md)<br />-   [サポートされる Linux と FreeBSD 仮想マシン](supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows.md)<br />-   [機能の生成とゲストの互換性](hyper-v-feature-compatibility-by-generation-and-guest.md)<br /><br />**HYPER-V を計画します。**<br /><br />-決定[仮想マシンの世代](plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v.md)ニーズを満たします。 <br/>移動するか、仮想マシンをインポートしている場合のタイミングを決定[バージョンをアップグレード](deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md)します。 <br />- [スケーラビリティ](plan/plan-hyper-v-scalability-in-windows-server.md) <br />- [ネットワー キング](plan/plan-hyper-v-networking-in-windows-server.md) <br />- [セキュリティ](plan/plan-hyper-v-security-in-windows-server.md)|
|![開始のシンボルを取得します。](media/All_Symbols_GetStarted.png)|**HYPER-V Server を概要します。**<br /><br />[ダウンロードしてインストール マイクロソフト ハイパー\-V Server 2016](https://www.microsoft.com/evalcenter/evaluate-hyper-v-server-2016)します。 Windows ハイパーバイザー、Windows Server ドライバー モデル、および仮想化コンポーネントがインストールされます。 Windows Server 2016、Hyper の Server Core インストール オプションを実行に似ています\-V ロール。|
|![シンボルを管理します。](media/All_Symbols_Administrator.png)|**構成および HYPER-V サーバーの管理**<br /><br />ハイパー\-V サーバーは、グラフィカル ユーザー インターフェイスがない\(GUI\)します。 次のツールを使用して、構成してハイパースレッディングを管理する\-V サーバー。<br /><br />-   [Sconfig.cmd を Windows Server 2016 の Server Core インストールを構成](../../get-started/sconfig-on-ws2016.md)ドメインまたはワークグループの設定を更新する Windows の更新の設定、リモート管理を有効にするなどを変更します。<br />-通常を使用して[コマンド プロンプト](../../administration/windows-commands/windows-commands.md)コマンド Sconfig では使用できません。<br />-使用[ハイパー\-V マネージャー](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/remote_host_management)または[Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm)ハイパースレッディングをリモートで管理する\-V サーバー。 ハイパースレッディングを使用する\-V マネージャー、[ハイパースレッディングをインストール\-Windows 10 での役割のインストール](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)または[Windows Server 2016](get-started/install-the-hyper-v-role-on-windows-server.md)します。<br />-「 [Server Core のインストール](../../get-started/getting-started-with-server-core.md)ハイパーに固有ではない基本的なサーバー機能追加の管理オプション\-V します。 説明がある管理メソッドのほとんどの操作もハイパー\-V サーバー。<br /><br />**構成し、管理のハイパースレッディング\-V 仮想マシン**<br /><br />-   [HYPER-V 仮想マシン用の仮想スイッチを作成します。](get-started/create-a-virtual-switch-for-hyper-v-virtual-machines.md)<br />-   [HYPER-V で仮想マシンを作成します。](get-started/create-a-virtual-machine-in-hyper-v.md)<br />-   [標準または実稼働のチェックポイント間での選択します。](manage/choose-between-standard-or-production-checkpoints-in-hyper-v.md)<br />-   [有効にするか、チェックポイントを無効にします。](manage/enable-or-disable-checkpoints-in-hyper-v.md)<br />-   [PowerShell ダイレクトでの Windows 仮想マシンを管理します。](manage/manage-windows-virtual-machines-with-powershell-direct.md) <br /><br />**展開**<br /><br />-   [フェールオーバー クラスタ リングのないライブ マイグレーションのホストの設定します。](deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)<br />- [Windows Server クラスター ノードをアップグレードします。](../../failover-clustering/cluster-operating-system-rolling-upgrade.md)<br />- [仮想マシンのバージョンをアップグレードします。](deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md)<br />|
