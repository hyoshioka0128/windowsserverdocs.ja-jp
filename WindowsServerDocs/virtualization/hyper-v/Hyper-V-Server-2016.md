---
title: Microsoft Hyper-V Server 2016
ms.topic: get-started-article
ms.assetid: f815ada0-4c63-4e73-9c24-dc5eb21526c7
author: kbdazure
ms.author: kathydav
ms.date: 07/26/2017
ms.openlocfilehash: e99750caea4948f51f5f660f3b6f4b42766e833d
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997069"
---
# <a name="microsoft-hyper-v-server-2016"></a>Microsoft Hyper-V Server 2016

Microsoft Hyper-V Server 2016 は、 \- windows ハイパーバイザー、Windows Server ドライバーモデル、および仮想化コンポーネントのみを含むスタンドアロン製品です。 シンプルで信頼性の高い仮想化ソリューションを提供し、サーバー使用率の向上とコスト削減を支援します。

Microsoft Hyper-V Server 2016 の Windows ハイパーバイザーテクノロジは、 \- Windows server 2016 の hyper-v の役割と同じです。 そのため、Windows Server 2016 の Hyper-v ロールで利用できるコンテンツの多くは、 \- Microsoft Hyper-V Server 2016 にも適用されます。

## <a name="hyper-v-server-resources-for-it-pros"></a>\-IT 担当者向けの Hyper-v Server リソース

|[タスク]|リソース|
|-|-|
|![要件シンボルを満たす](media/All_Symbols_MeetsRequirements.png)|**Hyper V を評価します。**<p>-   [Hyper-v テクノロジの概要](hyper-v-technology-overview.md)<br />- [Windows Server 2016 での Hyper-v の新機能](what-s-new-in-hyper-v-on-windows.md)<br />-   [Windows Server 2016 の Hyper-v のシステム要件](system-requirements-for-hyper-v-on-windows.md)<br />-   [Hyper-v でサポートされている Windows ゲストオペレーティングシステム](supported-windows-guest-operating-systems-for-hyper-v-on-windows.md)<br />-   [サポートされている Linux および FreeBSD Virtual Machines](supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows.md)<br />-   [世代とゲストによる機能の互換性](hyper-v-feature-compatibility-by-generation-and-guest.md)<p>**HYPER-V の計画**<p>-ニーズを満たす[仮想マシンの世代](plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v.md)を決定します。 <br/>-仮想マシンを移動またはインポートしている場合は、バージョンをいつ[アップグレード](deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md)するかを決定します。 <br />- [高い](plan/plan-hyper-v-scalability-in-windows-server.md) <br />- [機能](plan/plan-hyper-v-networking-in-windows-server.md) <br />- [保護](plan/plan-hyper-v-security-in-windows-server.md)|
|![開始シンボル](media/All_Symbols_GetStarted.png)|**Hyper-v Server を使ってみる**<p>[Microsoft hyper-v \- のダウンロードとインストールV Server 2016](https://www.microsoft.com/evalcenter/evaluate-hyper-v-server-2016)。 これにより、Windows ハイパーバイザー、Windows Server ドライバーモデル、および仮想化コンポーネントがインストールされます。 これは、Windows Server 2016 および Hyper-v の役割の Server Core インストールオプションを実行することと似て \- います。|
|![シンボルの管理](media/All_Symbols_Administrator.png)|**Hyper-v Server の構成と管理**<p>Hyper-v \- Server にはグラフィカルユーザーインターフェイス GUI がありません \( \) 。 次のツールを使用して、Hyper-v サーバーを構成および管理でき \- ます。<p>-   [Sconfig.cmd を使用して Windows server 2016 の Server Core インストールを構成](../../get-started/sconfig-on-ws2016.md)し、ドメインまたはワークグループの設定を更新したり、Windows Update 設定を変更したり、リモート管理を有効にしたりします。<br />-Sconfig.cmd で使用できないコマンドには、通常の[コマンドプロンプト](../../administration/windows-commands/windows-commands.md)を使用します。<br />-Hyper-v [ \- マネージャー](./manage/remotely-manage-hyper-v-hosts.md)または[Virtual Machine Manager](/system-center/vmm)を使用して、hyper-v サーバーをリモートで管理し \- ます。 Hyper-v マネージャーを使用するには \- 、 [ \- windows 10](/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)または[windows Server 2016](get-started/install-the-hyper-v-role-on-windows-server.md)に hyper-v の役割をインストールします。<br />Hyper-v に固有ではない基本的なサーバー機能の追加の管理オプションについては、「 [Server Core のインストール](../../get-started/getting-started-with-server-core.md)」を参照してください \- 。 ここに記載されているほとんどの管理方法は、Hyper-v サーバーでも動作 \- します。<p>**Hyper-v 仮想マシンの構成と管理 \-**<p>-   [Hyper-v 仮想マシンの仮想スイッチを作成する](get-started/create-a-virtual-switch-for-hyper-v-virtual-machines.md)<br />-   [Hyper-v での仮想マシンの作成](get-started/create-a-virtual-machine-in-hyper-v.md)<br />-   [標準チェックポイントまたは運用チェックポイントの選択](manage/choose-between-standard-or-production-checkpoints-in-hyper-v.md)<br />-   [チェックポイントを有効または無効にする](manage/enable-or-disable-checkpoints-in-hyper-v.md)<br />-   [PowerShell Direct を使用して Windows 仮想マシンを管理する](manage/manage-windows-virtual-machines-with-powershell-direct.md) <p>**デプロイする**<p>-   [フェールオーバークラスタリングを使用しないライブマイグレーションのホストの設定](deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)<br />- [Windows Server クラスターノードのアップグレード](../../failover-clustering/cluster-operating-system-rolling-upgrade.md)<br />- [仮想マシンのバージョンのアップグレード](deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md)<br />|