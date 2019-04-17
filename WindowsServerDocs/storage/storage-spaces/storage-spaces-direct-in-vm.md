---
title: 仮想マシンでの記憶域スペース ダイレクトの使用
ms.prod: windows-server-threshold
ms.author: eldenc
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 10/25/2017
description: 仮想マシンのゲスト クラスター - たとえば、Microsoft Azure で記憶域スペース ダイレクトを展開する方法。
ms.localizationpriority: medium
ms.openlocfilehash: a741475d09ab7f7ab29f158ef55378ca9a37beac
ms.sourcegitcommit: 52883945fd6e6bb5c24bd81944ca4bc0c5e6a216
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2018
ms.locfileid: "8964614"
---
# ゲスト仮想マシン クラスターで記憶域スペース ダイレクトの使用

> 適用対象: Windows Server 2019、Windows Server 2016

物理サーバー、クラスターまたはこのトピックで説明したように、仮想マシン ゲスト クラスターに記憶域スペース ダイレクトを展開できます。 この種類の展開は、アプリケーションの可用性を向上させるアプリケーションの高可用性ソリューションを使用できるように、プライベートまたはパブリック クラウド上には、Vm のセット全体で仮想共有記憶域を提供します。

![](media/storage-spaces-direct-in-vm/storage-spaces-direct-in-vm.png)

## Azure Iaas VM ゲスト クラスターでの展開

[Azure のテンプレート](https://github.com/robotechredmond/301-storage-spaces-direct-md)が公開された低下複雑さにされている、最適な構成プラクティス、および Azure vm Iaas、記憶域スペース ダイレクトの展開の速度です。 これは、Azure に展開するための推奨されるソリューションです。

<iframe src="https://channel9.msdn.com/Series/Microsoft-Hybrid-Cloud-Best-Practices-for-IT-Pros/Step-by-Step-Deploy-Windows-Server-2016-Storage-Spaces-Direct-S2D-Cluster-in-Microsoft-Azure/player" width="960" height="540" allowfullscreen></iframe>

## 要件

次の考慮事項は、仮想化された環境で記憶域スペース ダイレクトを展開するときに適用されます。

> [!TIP]
> Azure のテンプレートが自動的に構成されている、次は、推奨されるソリューション Azure IaaS Vm に展開する場合の考慮事項です。

-   2 ノードの最小値と最大 3 つのノードの

-   2 ノードの展開 (クラウド監視またはファイル共有監視) の監視を構成する必要があります。

-   3 ノードの展開には、1 のノードがダウンし、別のノードの 1 つ以上のディスクの損失を許容できます。  2 ノードのシャット ダウンしている場合、仮想ディスクしますオフラインまでに、ノードのいずれかを返します。  

-   障害ドメイン全体で展開する仮想マシンの構成します。

    -   Azure – 使用可能状況の設定を構成します。

    -   Hyper-v – ノード間で Vm を個別に Vm で AntiAffinityClassNames を構成します。

    -   VMware の種類の DRS 規則を作成して構成する VM アンチ アフィニティ ルール ' 別々 の仮想マシン"ESX ホストの間で Vm を個別にします。 記憶域スペース ダイレクトで使用するために表示されるディスクには、Paravirtual SCSI (PVSCSI) アダプターを使用する必要があります。 Windows server のサポートを PVSCSI、参照https://kb.vmware.com/s/article/1010398します。

-   低待機時間を活用してパフォーマンスの高い記憶域の Azure Premium の記憶域の管理/ディスクが必要です。

-   キャッシュ デバイスを構成なしで記憶域のフラットなデザインを展開します。

-   各 VM に表示される 2 つの仮想データ ディスクの最小 (VHD または VHDX/VMDK)

    この番号は、仮想ディスクは物理的な障害の影響を受けやすいファイルとして実装されるため、ベア メタル展開とは異なる。

-   次の PowerShell コマンドレットを実行して、ヘルス サービスで自動ドライブの代替機能を無効にします。

    ```powershell
    Get-storagesubsystem clus* | set-storagehealthsetting -name “System.Storage.PhysicalDisk.AutoReplace.Enabled” -value “False”
    ```

-   サポートされていません: ホスト レベルの仮想ディスクのスナップショット/復元

    代わりにバックアップし、復元の記憶域スペース ダイレクトのボリューム上のデータを従来のゲスト レベルのバックアップ ソリューションを使用します。

-   可能な VHD をより回復性を提供する/VHDX VMDK 記憶域の待機時間、ゲスト クラスターで記憶域スペースの I/O タイムアウト値が大きく/。

    `HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\spaceport\\Parameters\\HwTimeout`

    `dword: 00007530`

    16 進数の 7530 10 進値は 30000 は 30 秒です。 既定値は、1770 16 進数、または 6000 10 進数、6 秒であることに注意してください。

## 関連項目

[展開記憶域スペース ダイレクト、ビデオ、およびステップ バイ ステップ ガイドの他の Azure Iaas VM テンプレート](https://blogs.msdn.microsoft.com/clustering/2017/02/14/deploying-an-iaas-vm-guest-clusters-in-microsoft-azure/)です。

[その他の記憶域スペース ダイレクトの概要](https://docs.microsoft.com/en-us/windows-server/storage/storage-spaces/storage-spaces-direct-overview)
