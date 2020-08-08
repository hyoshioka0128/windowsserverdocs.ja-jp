---
title: 仮想マシンでの記憶域スペースダイレクトの使用
description: Microsoft Azure など、仮想マシンのゲストクラスターに記憶域スペースダイレクトを展開する方法。
ms.author: eldenc
manager: eldenc
ms.topic: article
author: eldenchristensen
ms.date: 07/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: d124e26f0605b8e1a4678abebb9039b597f1c18a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971059"
---
# <a name="using-storage-spaces-direct-in-guest-virtual-machine-clusters"></a>ゲスト仮想マシンクラスターでの記憶域スペースダイレクトの使用

> 適用先:Windows Server 2019、Windows Server 2016

このトピックで説明するように、物理サーバーのクラスターまたは仮想マシンのゲストクラスターに記憶域スペースダイレクト (S2D と呼ばれることもあります) を展開できます。 この種類のデプロイは、プライベートクラウドまたはパブリッククラウド上の一連の Vm で仮想共有記憶域を提供し、アプリケーションの高可用性ソリューションを使用してアプリケーションの可用性を高めることができます。

代わりに、ゲスト仮想マシンに Azure 共有ディスクを使用するには、「 [Azure 共有ディスク](/azure/virtual-machines/windows/disks-shared)」を参照してください。

![記憶域スペース ダイレクトの図](media/storage-spaces-direct-in-vm/storage-spaces-direct-in-vm.png)

## <a name="deploying-in-azure-iaas-vm-guest-clusters"></a>Azure Iaas VM ゲストクラスターでのデプロイ

Azure[テンプレート](https://github.com/robotechredmond/301-storage-spaces-direct-md)が発行されているため、AZURE Iaas VM での記憶域スペースダイレクトデプロイの複雑さが軽減され、ベストプラクティスと速度が構成されます。 これは、Azure にデプロイする場合に推奨されるソリューションです。

<iframe src="https://channel9.msdn.com/Series/Microsoft-Hybrid-Cloud-Best-Practices-for-IT-Pros/Step-by-Step-Deploy-Windows-Server-2016-Storage-Spaces-Direct-S2D-Cluster-in-Microsoft-Azure/player" width="960" height="540" allowfullscreen></iframe>

## <a name="requirements-for-guest-clusters"></a>ゲストクラスターの要件

仮想化環境に記憶域スペースダイレクトを展開する場合は、次の考慮事項が適用されます。

> [!TIP]
> Azure テンプレートでは、以下の考慮事項が自動的に構成されます。 Azure IaaS Vm にデプロイする場合は、推奨されるソリューションです。

- 最低2ノードと最大3ノード

- 2-ノードデプロイでミラーリング監視サーバー (クラウド監視またはファイル共有監視) を構成する必要があります。

- 3-ノード展開では、1つのノードがダウンし、別のノードで1つ以上のディスクが失われることが許容されます。  2つのノードがシャットダウンされた場合、仮想ディスクはノードのいずれかが返されるまでオフラインになります。

- 障害ドメイン間でデプロイされるように仮想マシンを構成する

    - Azure –可用性セットの構成

    - Hyper-v – Vm で AntiAffinityClassNames を構成して、ノード間で Vm を分離します。

    - VMware – ESX ホスト間で Vm を分離するために、"個別の Virtual Machines" という種類の DRS ルールを作成して、VM と VM の間のアンチアフィニティルールを構成します。 記憶域スペースダイレクトで使用するために提示されたディスクでは、準仮想化 SCSI (PVSCSI) アダプタを使用する必要があります。 Windows Server での PVSCSI のサポートについては、「」を参照 https://kb.vmware.com/s/article/1010398 してください。

- 低待機時間/高パフォーマンスストレージの活用-Azure Premium Storage managed disks が必要です

- キャッシュデバイスが構成されていないフラットストレージ設計を展開する

- 各 VM に提示される最低2つの仮想データディスク (VHD/VHDX/VMDK)

    この数は、物理障害の影響を受けやすいファイルとして仮想ディスクを実装できるため、ベアメタル展開とは異なります。

- 次の PowerShell コマンドレットを実行して、ヘルスサービスのドライブ交換の自動機能を無効にします。

    ```powershell
    Get-storagesubsystem clus* | set-storagehealthsetting -name "System.Storage.PhysicalDisk.AutoReplace.Enabled" -value "False"
    ```

- ゲストクラスターにおける VHD/VHDX/VMDK ストレージの待機時間の回復性を高めるには、記憶域スペースの i/o タイムアウト値を増やします。

    `HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\spaceport\\Parameters\\HwTimeout`

    `dword: 00007530`

    16進数の7530に相当する10進数は、3万です。これは30秒です。 既定値は 1770 16 進数、つまり、6秒の 6000 Decimal であることに注意してください。

## <a name="not-supported"></a>サポートなし

- ホストレベルの仮想ディスクのスナップショット/復元

    代わりに、従来のゲストレベルのバックアップソリューションを使用して、記憶域スペースダイレクトボリューム上のデータをバックアップおよび復元します。

- ホストレベルの仮想ディスクサイズの変更

    仮想マシンを介して公開される仮想ディスクは、同じサイズと特性を保持する必要があります。 記憶域プールに容量を追加するには、各仮想マシンに仮想ディスクを追加し、プールに追加します。 現在の仮想ディスクと同じサイズおよび特性の仮想ディスクを使用することを強くお勧めします。

## <a name="additional-references"></a>その他の参照情報

- [記憶域スペースダイレクト、ビデオ、ステップバイステップガイドをデプロイするための追加の Azure IAAS VM テンプレート](https://techcommunity.microsoft.com/t5/Failover-Clustering/Deploying-IaaS-VM-Guest-Clusters-in-Microsoft-Azure/ba-p/372126)。

- [その他の記憶域スペースダイレクトの概要](./storage-spaces-direct-overview.md)
