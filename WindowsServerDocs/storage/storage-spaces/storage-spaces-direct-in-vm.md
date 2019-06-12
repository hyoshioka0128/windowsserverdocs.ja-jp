---
title: 仮想マシンでの記憶域スペース ダイレクトの使用
ms.prod: windows-server-threshold
ms.author: eldenc
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 10/25/2017
description: 仮想マシンのゲスト クラスターで - たとえば、Microsoft Azure で記憶域スペース ダイレクトをデプロイする方法。
ms.localizationpriority: medium
ms.openlocfilehash: b99e750b78654df48ad3b412269511d047e3057c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447809"
---
# <a name="using-storage-spaces-direct-in-guest-virtual-machine-clusters"></a>仮想マシンのゲスト クラスターでの記憶域スペース ダイレクトの使用

> 適用対象:Windows Server 2019、Windows Server 2016

物理サーバーのクラスターまたはこのトピックで説明したように、仮想マシン ゲスト クラスターに記憶域スペース ダイレクトを展開できます。 この種類の展開は、アプリケーションの高可用性ソリューションは、アプリケーションの可用性を高めるために使用できるように、プライベートまたはパブリック クラウド上に Vm のセット間で仮想共有記憶域を提供します。

![](media/storage-spaces-direct-in-vm/storage-spaces-direct-in-vm.png)

## <a name="deploying-in-azure-iaas-vm-guest-clusters"></a>Azure Iaas VM ゲスト クラスターに展開します。

[Azure テンプレート](https://github.com/robotechredmond/301-storage-spaces-direct-md)パブリッシュの短縮に複雑さをされている、最適な構成プラクティス、および Azure Iaas VM で、記憶域スペース ダイレクトの展開の速度。 これは、Azure に配置するための推奨されるソリューションです。

<iframe src="https://channel9.msdn.com/Series/Microsoft-Hybrid-Cloud-Best-Practices-for-IT-Pros/Step-by-Step-Deploy-Windows-Server-2016-Storage-Spaces-Direct-S2D-Cluster-in-Microsoft-Azure/player" width="960" height="540" allowfullscreen></iframe>

## <a name="requirements"></a>要件

仮想化環境で記憶域スペース ダイレクトを展開するときに、次の考慮事項が適用されます。

> [!TIP]
> Azure テンプレートは自動的に構成されているとは、Azure IaaS Vm でデプロイする場合は、推奨されるソリューションの考慮事項の下。

-   2 つのノードの最小値と最大 3 つのノード

-   2 つのノードの展開は、ミラーリング監視サーバー (クラウド ミラーリング監視サーバーまたはファイル共有監視) を構成する必要があります。

-   3 ノードのデプロイには、1 つのノードがダウンし、別のノードの 1 つ以上のディスクの損失を許容できます。  2 つのノードがシャット ダウンし、仮想ディスク オフラインになるまで、ノードのいずれかを返します。  

-   障害ドメイン間でデプロイする仮想マシンの構成します。

    -   Azure 可用性セットの構成

    -   Hyper-v – ノード間で Vm を分離する Vm で構成 AntiAffinityClassNames

    -   VMware の型の DRS ルールを作成して構成する VM のアンチ アフィニティ ルール ' 別々 の仮想マシン"ESX のホスト間で Vm を分離します。 ディスク記憶域スペース ダイレクトで使用するための表示には、Paravirtual SCSI (PVSCSI) アダプタを使用する必要があります。 Windows Server、PVSCSI サポートを参照して https://kb.vmware.com/s/article/1010398します。

-   低待機時間を活用して高パフォーマンス ストレージ - Azure Premium Storage の管理/ディスクが必要です

-   構成されているキャッシュ デバイスなしで、フラットなストレージ設計を展開します。

-   各 VM に表示される 2 つの仮想データ ディスクの最小値 (VHD または VHDX/VMDK)

    この数は、仮想ディスクを物理的な障害を受けやすくはないファイルとして実装できるため、ベア メタルの展開とは異なります。

-   次の PowerShell コマンドレットを実行して、ヘルス サービスでドライブの自動置換機能を無効にします。

    ```powershell
    Get-storagesubsystem clus* | set-storagehealthsetting -name “System.Storage.PhysicalDisk.AutoReplace.Enabled” -value “False”
    ```

-   サポートしていないバージョン:ホスト レベルの仮想ディスク スナップショットの復元

    代わりに従来のゲスト レベルのバックアップ ソリューションを使用して、バックアップし、記憶域スペース ダイレクトのボリューム上のデータを復元します。

-   可能な VHD への回復性が高いを付与する/VHDX ゲスト クラスターで VMDK ストレージの待機時間は、記憶域スペースの I/O のタイムアウト値を大きく/。

    `HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\spaceport\\Parameters\\HwTimeout`

    `dword: 00007530`

    7530 の 16 進数の 10 進値は 30000 は 30 秒です。 既定値は 1770 16 進数、または 6000 の 10 進数は 6 秒であることに注意してください。

## <a name="see-also"></a>関連項目

[記憶域スペース ダイレクト、ビデオ、およびステップ バイ ステップ ガイドをデプロイするための他の Azure Iaas VM テンプレート](https://blogs.msdn.microsoft.com/clustering/2017/02/14/deploying-an-iaas-vm-guest-clusters-in-microsoft-azure/)します。

[追加の記憶域スペース ダイレクトの概要](https://docs.microsoft.com/en-us/windows-server/storage/storage-spaces/storage-spaces-direct-overview)
