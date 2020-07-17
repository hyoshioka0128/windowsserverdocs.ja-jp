---
title: Microsoft Hyper-V Server 2016
ms.prod: windows-server
ms.technology: compute-hyper-v
ms.topic: get-started-article
ms.assetid: f815ada0-4c63-4e73-9c24-dc5eb21526c7
author: kbdazure
ms.author: kathydav
ms.date: 07/26/2017
ms.openlocfilehash: f5c68f260ff90a07a17a39fdbb881ddcbdb857ab
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853265"
---
# <a name="microsoft-hyper-v-server-2016"></a>Microsoft Hyper-V Server 2016

Microsoft Hyper-V Server 2016 は、Windows ハイパーバイザー、Windows Server ドライバーモデル、および仮想化コンポーネントのみを含むスタンド\-アロン製品です。 シンプルで信頼性の高い仮想化ソリューションを提供し、サーバー使用率の向上とコスト削減を支援します。

Microsoft Hyper-V Server 2016 の Windows ハイパーバイザーテクノロジは、Windows Server 2016 のハイパー\-V ロールの内容と同じです。 そのため、Windows Server 2016 のハイパー\-V ロールで利用できるコンテンツの多くは Microsoft Hyper-V サーバー2016にも適用されます。

## <a name="hyper-v-server-resources-for-it-pros"></a>IT 担当者向けのハイパー\-V Server リソース

|タスク|リソース|
|-|-|
|![要件シンボルを満たす](media/All_Symbols_MeetsRequirements.png)|**Hyper V を評価する**<p>-   [Hyper-v テクノロジの概要](hyper-v-technology-overview.md)<br />[Windows Server 2016 での hyper-v の新機能](what-s-new-in-hyper-v-on-windows.md)の - <br />[Windows Server 2016 の hyper-v の -   システム要件](system-requirements-for-hyper-v-on-windows.md)<br />[hyper-v でサポートされている Windows ゲストオペレーティングシステム](supported-windows-guest-operating-systems-for-hyper-v-on-windows.md)-   <br />-   [サポートされている Linux および FreeBSD Virtual Machines](supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows.md)<br />[生成とゲストによる機能の互換性の](hyper-v-feature-compatibility-by-generation-and-guest.md)-   <p>**Hyper-v の計画**<p>-ニーズを満たす[仮想マシンの世代](plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v.md)を決定します。 <br/>-仮想マシンを移動またはインポートしている場合は、バージョンをいつ[アップグレード](deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md)するかを決定します。 <br />- の[スケーラビリティ](plan/plan-hyper-v-scalability-in-windows-server.md) <br />- [ネットワーク](plan/plan-hyper-v-networking-in-windows-server.md) <br />- の[セキュリティ](plan/plan-hyper-v-security-in-windows-server.md)|
|![開始シンボル](media/All_Symbols_GetStarted.png)|**Hyper-v Server を使ってみる**<p>[Microsoft ハイパー\-V Server 2016 をダウンロードしてインストール](https://www.microsoft.com/evalcenter/evaluate-hyper-v-server-2016)します。 これにより、Windows ハイパーバイザー、Windows Server ドライバーモデル、および仮想化コンポーネントがインストールされます。 これは、Windows Server 2016 の Server Core インストールオプションと\-Hyper-v ロールを実行するのと似ています。|
|![シンボルの管理](media/All_Symbols_Administrator.png)|**Hyper-v Server の構成と管理**<p>\-hyper-v サーバーには GUI\)\(グラフィカルユーザーインターフェイスがありません。 次のツールを使用して、\-Hyper-v サーバーの構成と管理を行うことができます。<p>[sconfig.cmd を使用して Windows server 2016 の Server Core インストールを構成](../../get-started/sconfig-on-ws2016.md)し、ドメインまたはワークグループの設定を更新したり、Windows Update の設定を変更したり、リモート管理を有効にしたりする -   ます。<br />-Sconfig.cmd で使用できないコマンドには、通常の[コマンドプロンプト](../../administration/windows-commands/windows-commands.md)を使用します。<br />-ハイパー [\-v Manager](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/remote_host_management)または[Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm)を使用して、ハイパー\-v Server をリモートで管理します。 Hyper-v\-V Manager を使用するには、Windows 10 または[Windows Server 2016](get-started/install-the-hyper-v-role-on-windows-server.md)[に\-hyper-v の役割をインストール](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)します。<br />\-Hyper-v に固有ではない基本的なサーバー機能の追加の管理オプションについては、「 [Server Core のインストール](../../get-started/getting-started-with-server-core.md)」を参照してください。 ここに記載されているほとんどの管理方法は、ハイパー\-V Server とも連携して動作します。<p>**\-Hyper-v 仮想マシンを構成して管理する**<p>[hyper-v 仮想マシンの仮想スイッチを作成 -   には](get-started/create-a-virtual-switch-for-hyper-v-virtual-machines.md)<br />[hyper-v で仮想マシンを作成 -   には](get-started/create-a-virtual-machine-in-hyper-v.md)<br />[標準チェックポイントまたは運用チェックポイントを選択](manage/choose-between-standard-or-production-checkpoints-in-hyper-v.md)-   <br />[チェックポイントを有効または無効に -   には](manage/enable-or-disable-checkpoints-in-hyper-v.md)<br />[PowerShell Direct を使用して Windows 仮想マシンを管理 -   に](manage/manage-windows-virtual-machines-with-powershell-direct.md)は <p>**展開**<p>[フェールオーバークラスタリングを使用せずにライブマイグレーション用にホストをセットアップ -   には](deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)<br />[Windows Server クラスターノードのアップグレード](../../failover-clustering/cluster-operating-system-rolling-upgrade.md)- <br />[仮想マシンのバージョンをアップグレード](deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md)- には<br />|
