---
title: Microsoft Hyper-V Server 2016
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f815ada0-4c63-4e73-9c24-dc5eb21526c7
author: KBDAzure
ms.author: kathydav
ms.date: 07/26/2017
ms.openlocfilehash: c9e1b5e2d30276bf89bc2d56482ec76d1c2241a2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365576"
---
# <a name="microsoft-hyper-v-server-2016"></a>Microsoft Hyper-V Server 2016

Microsoft Hyper-V Server 2016 は、Windows ハイパーバイザー、Windows Server ドライバーモデル、および仮想化コンポーネントのみを含む、スタンドアロンの no__t 製品です。 シンプルで信頼性の高い仮想化ソリューションを提供し、サーバー使用率の向上とコスト削減を支援します。

Microsoft Hyper-V Server 2016 の Windows ハイパーバイザーテクノロジは、Windows Server 2016 のハイパー @ no__t-0V ロールと同じです。 そのため、Windows Server 2016 のハイパー @ no__t-0V ロールで利用できるコンテンツの多くは、Microsoft Hyper-V Server 2016 にも適用されます。

## <a name="hyper-v-server-resources-for-it-pros"></a>IT 担当者向けのハイパー @ no__t-0V Server リソース

|処理手順|リソース|
|-|-|
|![要件シンボルを満たす](media/All_Symbols_MeetsRequirements.png)|**Hyper-v の評価**<br /><br />-   [Hyper-v テクノロジの概要](hyper-v-technology-overview.md)<br />- [Windows Server 2016 での hyper-v の新機能](what-s-new-in-hyper-v-on-windows.md)<br />-   [Windows Server 2016 の hyper-v のシステム要件](system-requirements-for-hyper-v-on-windows.md)<br />-    で[サポートされている Windows ゲストオペレーティングシステム (hyper-v)](supported-windows-guest-operating-systems-for-hyper-v-on-windows.md)<br />-    で[サポートされている Linux および FreeBSD Virtual Machines](supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows.md)<br />-   [世代とゲストの機能の互換性](hyper-v-feature-compatibility-by-generation-and-guest.md)<br /><br />**Hyper-v の計画**<br /><br />-ニーズを満たす[仮想マシンの世代](plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v.md)を決定します。 <br/>-仮想マシンを移動またはインポートしている場合は、バージョンをいつ[アップグレード](deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md)するかを決定します。 <br />-  の[スケーラビリティ](plan/plan-hyper-v-scalability-in-windows-server.md) <br />- [ネットワーク](plan/plan-hyper-v-networking-in-windows-server.md) <br />- [セキュリティ](plan/plan-hyper-v-security-in-windows-server.md)|
|![開始シンボル](media/All_Symbols_GetStarted.png)|**Hyper-v Server を使ってみる**<br /><br />[Microsoft ハイパー @ no__t-1V Server 2016 をダウンロードしてインストール](https://www.microsoft.com/evalcenter/evaluate-hyper-v-server-2016)します。 これにより、Windows ハイパーバイザー、Windows Server ドライバーモデル、および仮想化コンポーネントがインストールされます。 これは、Windows Server 2016 の Server Core インストールオプションと、ハイパー @ no__t-0V ロールの実行に似ています。|
|![シンボルの管理](media/All_Symbols_Administrator.png)|**Hyper-v Server の構成と管理**<br /><br />ハイパー @ no__t-0V Server には、グラフィカルユーザーインターフェイス \(GUI @ no__t-2 がありません。 次のツールを使用して、ハイパー @ no__t-0V サーバーを構成および管理できます。<br /><br />-   [Windows server 2016 の Server Core インストールを sconfig.cmd で構成](../../get-started/sconfig-on-ws2016.md)し、ドメインまたはワークグループの設定を更新し、Windows Update の設定を変更し、リモート管理を有効にします。<br />-Sconfig.cmd で使用できないコマンドには、通常の[コマンドプロンプト](../../administration/windows-commands/windows-commands.md)を使用します。<br />-ハイパー @ [no__t-1V Manager](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/remote_host_management)または[Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm)を使用して、ハイパー @ No__t-3v Server をリモートで管理します。 ハイパー @ no__t-0V Manager を使用するには、Windows 10 または[Windows Server 2016](get-started/install-the-hyper-v-role-on-windows-server.md)[にハイパー @ No__t-2v ロールをインストール](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v)します。<br />-Hyper-v に固有ではない基本的なサーバー機能の追加の管理オプションについては、「 [Server Core のインストール](../../get-started/getting-started-with-server-core.md)」を参照してください。 ここに記載されているほとんどの管理方法は、ハイパー @ no__t-0V Server とも連携して動作します。<br /><br />**ハイパー @ no__t-1V 仮想マシンの構成と管理**<br /><br />-   [hyper-v 仮想マシンの仮想スイッチを作成する](get-started/create-a-virtual-switch-for-hyper-v-virtual-machines.md)<br />-   [hyper-v で仮想マシンを作成する](get-started/create-a-virtual-machine-in-hyper-v.md)<br />-   [標準チェックポイントまたは運用チェックポイントを選択し](manage/choose-between-standard-or-production-checkpoints-in-hyper-v.md)ます<br />-   [チェックポイントを有効または無効に](manage/enable-or-disable-checkpoints-in-hyper-v.md)します<br />-   [PowerShell Direct を使用して Windows 仮想マシンを管理](manage/manage-windows-virtual-machines-with-powershell-direct.md)する <br /><br />**展開**<br /><br />-   [フェールオーバークラスタリングを使用しないライブマイグレーション用にホストを設定する](deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)<br />- [Windows Server クラスターノードのアップグレード](../../failover-clustering/cluster-operating-system-rolling-upgrade.md)<br />- [仮想マシンのバージョンのアップグレード](deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md)<br />|
