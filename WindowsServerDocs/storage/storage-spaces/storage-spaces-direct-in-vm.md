---
title: 仮想マシンでの記憶域スペースダイレクトの使用
ms.prod: windows-server
ms.author: eldenc
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: eldenchristensen
ms.date: 10/25/2017
description: Microsoft Azure など、仮想マシンのゲストクラスターに記憶域スペースダイレクトを展開する方法。
ms.localizationpriority: medium
ms.openlocfilehash: 74b1b90a780a0b238a356e942f8348e2a483d94a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856115"
---
# <a name="using-storage-spaces-direct-in-guest-virtual-machine-clusters"></a>ゲスト仮想マシンクラスターでの記憶域スペースダイレクトの使用

> 適用対象: Windows Server 2019、Windows Server 2016

記憶域スペースダイレクトは、このトピックで説明するように、物理サーバーのクラスターまたは仮想マシンのゲストクラスターに展開できます。 この種類のデプロイは、プライベートクラウドまたはパブリッククラウド上の一連の Vm で仮想共有記憶域を提供し、アプリケーションの高可用性ソリューションを使用してアプリケーションの可用性を高めることができます。

![](media/storage-spaces-direct-in-vm/storage-spaces-direct-in-vm.png)

## <a name="deploying-in-azure-iaas-vm-guest-clusters"></a>Azure Iaas VM ゲストクラスターでのデプロイ

Azure[テンプレート](https://github.com/robotechredmond/301-storage-spaces-direct-md)が発行されているため、AZURE Iaas VM での記憶域スペースダイレクトデプロイの複雑さが軽減され、ベストプラクティスと速度が構成されます。 これは、Azure にデプロイする場合に推奨されるソリューションです。

<iframe src="https://channel9.msdn.com/Series/Microsoft-Hybrid-Cloud-Best-Practices-for-IT-Pros/Step-by-Step-Deploy-Windows-Server-2016-Storage-Spaces-Direct-S2D-Cluster-in-Microsoft-Azure/player" width="960" height="540" allowfullscreen></iframe>

## <a name="requirements"></a>要件

仮想化環境に記憶域スペースダイレクトを展開する場合は、次の考慮事項が適用されます。
       
>        !TIP]
>        zure templates will automatically configure the below considerations for you and are the recommended solution when deploying in Azure IaaS VMs.

-   最低2ノードと最大3ノード

-   2-ノードデプロイでミラーリング監視サーバー (クラウド監視またはファイル共有監視) を構成する必要があります。

-   3-ノード展開では、1つのノードがダウンし、別のノードで1つ以上のディスクが失われることが許容されます。  2つのノードがシャットダウンされた場合、仮想ディスクはノードのいずれかが返されるまでオフラインになります。  

-   障害ドメイン間でデプロイされるように仮想マシンを構成する

    -   Azure –可用性セットの構成

    -   Hyper-v – Vm で AntiAffinityClassNames を構成して、ノード間で Vm を分離します。

    -   VMware – ESX ホスト間で Vm を分離するために、"個別の Virtual Machines" という種類の DRS ルールを作成して、VM と VM の間のアンチアフィニティルールを構成します。 記憶域スペースダイレクトで使用するために提示されたディスクでは、準仮想化 SCSI (PVSCSI) アダプタを使用する必要があります。 Windows Server での PVSCSI のサポートについては、 https://kb.vmware.com/s/article/1010398を参照してください。

-   低待機時間/高パフォーマンスストレージの活用-Azure Premium Storage managed disks が必要です

-   キャッシュデバイスが構成されていないフラットストレージ設計を展開する

-   各 VM に提示される最低2つの仮想データディスク (VHD/VHDX/VMDK)

    この数は、物理障害の影響を受けやすいファイルとして仮想ディスクを実装できるため、ベアメタル展開とは異なります。

-   次の PowerShell コマンドレットを実行して、ヘルスサービスでドライブの自動置換を無効にします。

    ```powershell
          Get-storagesubsystem clus* | set-storagehealthsetting -name "System.Storage.PhysicalDisk.AutoReplace.Enabled" -value "False"
          ```

-   To give greater resiliency to possible VHD / VHDX / VMDK storage latency in guest clusters, increase the Storage Spaces I/O timeout value:

    `HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Services\\spaceport\\Parameters\\HwTimeout`

    `dword: 00007530`

    The decimal equivalent of Hexadecimal 7530 is 30000, which is 30 seconds. Note that the default value is 1770 Hexadecimal, or 6000 Decimal, which is 6 seconds.

## Not supported

-   Host level virtual disk snapshot/restore

    Instead use traditional guest level backup solutions to backup and restore the data on the Storage Spaces Direct volumes.

-   Host level virtual disk size change

    The virtual disks exposed through the virtual machine must retain the same size and characteristics. Adding more capacity to the storage pool can be accomplished by adding more virtual disks to each of the virtual machines and adding them to the pool. It's highly recommended to use virtual disks of the same size and characteristics as the current virtual disks.

## See also

[Additional Azure Iaas VM templates for deploying Storage Spaces Direct, videos, and step-by-step guides](https://techcommunity.microsoft.com/t5/Failover-Clustering/Deploying-IaaS-VM-Guest-Clusters-in-Microsoft-Azure/ba-p/372126).

[Additional Storage Spaces Direct Overview](https://docs.microsoft.com/windows-server/storage/storage-spaces/storage-spaces-direct-overview)
""""""''''                                                                                                                                                                        """"""''''                                                                                                                                                                        