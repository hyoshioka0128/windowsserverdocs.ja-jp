---
title: ホスト ガーディアン サービスを展開します。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 310b63d9-5ac7-4961-98ef-103af45d706a
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: c6b891cee905f917fab16869cd6deccc66d91a2e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857423"
---
# <a name="deploying-the-host-guardian-service"></a>ホスト ガーディアン サービスを展開します。 

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

ホスト環境を提供するための最も重要な目標の 1 つは、環境で実行する仮想マシンのセキュリティを保証することです。 クラウド サービス プロバイダーやエンタープライズ プライベート クラウド管理者は、保護されたファブリックを使用して、セキュリティが強化された VM 環境を実現できます。 保護されたファブリックは、1 つホスト ガーディアン サービス (HGS)、通常は、3 ノードのクラスターと、1 つまたは複数の保護されたホスト、シールドされた仮想マシン (VM) のセットで構成されます。

## <a name="video-deploying-a-guarded-fabric"></a>ビデオ:保護されたファブリックを展開します。 

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/dcd8e99f-36f1-4bc8-b3d2-9576da38d9f1?autoplay=false]

## <a name="deployment-tasks-for-guarded-fabrics-and-shielded-vms"></a>展開タスクが保護され、ファブリックとシールドされた Vm

次の表は、保護されたファブリックを展開し、別の管理者の役割に応じて、シールドされた Vm を作成するタスクを中断します。 メモを HGS 管理者は、承認された HYPER-V ホストを HGS を構成、するときに、ファブリック管理者が収集され、同時にホストに関する識別情報を提供します。    

|<img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-hgs-administrator-tasks.png" alt="Host Guardian Service administrator tasks" width="238" height="62" align="left" /> | <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-fabric-administrator-tasks.png" alt="Fabric administrator tasks" width="300" height="62" align="left" /> | <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-tenant-administrator-tasks.png" alt="Tenant administrator tasks" width="184" height="66" align="left" /> |
|-------------------------------------|--------------------------------|-----------------------------------------|
|<img src="../media/Guarded-Fabric-Shielded-VM/1111.png" alt="Step 1" hspace="8" align="left" /> [HGS の前提条件を確認します。](guarded-fabric-prepare-for-hgs.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-verify.png" alt="Step 1" hspace="8" align="right" />| | |
|<img src="../media/Guarded-Fabric-Shielded-VM/2222.png" alt="Step 2" hspace="8" align="left" /> [最初の HGS の構成&nbsp;ノード](guarded-fabric-choose-where-to-install-hgs.md)&nbsp;<img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-first-hgs-node.png" alt="Step 2" hspace="8" align="right" />| | |
|<img src="../media/Guarded-Fabric-Shielded-VM/3333.png" alt="Step 3" hspace="8" align="left" /> [追加の HGS の構成&nbsp;ノード](guarded-fabric-configure-additional-hgs-nodes.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-secondary-hgs-nodes.png" alt="Step 3" hspace="8" align="right" />| | |
|<img src="../media/Guarded-Fabric-Shielded-VM/4444.png" alt="Step 4" hspace="8" align="left" /> [HGS の構成を確認します。](guarded-fabric-verify-hgs-configuration.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-verify-hgs-configuration.png" alt="Step 4" hspace="8" align="right" />| | |
| &nbsp; |<img src="../media/Guarded-Fabric-Shielded-VM/5555.png" alt="Step 5" hspace="8" align="left" /> [Fabric DNS を構成します。](guarded-fabric-configuring-fabric-dns.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-fabric-dns.png" alt="Step 5" hspace="8" align="right" />| |
| &nbsp; |<img src="../media/Guarded-Fabric-Shielded-VM/6666.png" alt="Step 6" hspace="8" align="left" /> [ホストを検証&nbsp;(キー) の前提条件](guarded-fabric-guarded-host-prerequisites.md#host-key-attestation)<br>[ホストを検証&nbsp;(TPM) の前提条件](guarded-fabric-guarded-host-prerequisites.md#tpm-trusted-attestation)<img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-verify.png" alt="Step 6" hspace="8" align="right" />| |
|<img src="../media/Guarded-Fabric-Shielded-VM/8888.png" alt="Step 8" hspace="8" align="left" /> [ホスト情報での HGS を構成します。](guarded-fabric-add-host-information-to-hgs.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-hgs-with-host-info.png" alt="Step 8" hspace="8" align="right" />|<img src="../media/Guarded-Fabric-Shielded-VM/7777.png" alt="Step 7" hspace="8" align="left" /> [ホスト キー (キー) を作成します。](guarded-fabric-create-host-key.md)<br>[ホスト情報 (TPM) の収集します。](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-collect-info-from-hosts.png" alt="Step 7" hspace="8" align="right" />| |
| &nbsp; |<img src="../media/Guarded-Fabric-Shielded-VM/9999.png" alt="Step 9" hspace="8" align="left" /> [ホストに証明できることを確認します。](guarded-fabric-confirm-hosts-can-attest-successfully.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-confirm-hosts-attest.png" alt="Step 9" hspace="8" align="right" />| |
| &nbsp; |<img src="../media/Guarded-Fabric-Shielded-VM/101010.png" alt="Step 10" hspace="8" align="left" /> [(省略可能) の VMM を構成します。](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-overview) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-vmm.png" alt="Step 10" hspace="8" align="right" />| |
| &nbsp; |<img src="../media/Guarded-Fabric-Shielded-VM/11eleven.png" alt="Step 11" hspace="8" align="left" /> [テンプレート ディスクを作成します。](guarded-fabric-create-a-shielded-vm-template.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-create-template-disk.png" alt="Step 11" hspace="8" align="right" />| |
| &nbsp; |<img src="../media/Guarded-Fabric-Shielded-VM/121212.png" alt="Step 12" hspace="8" align="left" /> [(省略可能) の VMM の VM シールド ヘルパー ディスクを作成します。](guarded-fabric-vm-shielding-helper-vhd.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-create-helper-disk.png" alt="Step 12" hspace="8" align="right" />| |
| &nbsp; |<img src="../media/Guarded-Fabric-Shielded-VM/131313.png" alt="Step 13" hspace="8" align="left" /> [Windows Azure Pack の設定 (省略可)](guarded-fabric-shielded-vm-windows-azure-pack.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-windows-azure-pack.png" alt="Step 13" hspace="8" align="right" />| |
| &nbsp; | &nbsp; |<img src="../media/Guarded-Fabric-Shielded-VM/141414.png" alt="Step 14" hspace="8" align="left" /> [シールド データ ファイルを作成します。](guarded-fabric-tenant-creates-shielding-data.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-shielding-data-file.png" alt="Step 14" hspace="8" align="right" />|
| &nbsp; | &nbsp; |<img src="../media/Guarded-Fabric-Shielded-VM/151515.png" alt="Step 15" hspace="8" align="left" /> [Windows Azure Pack を使用して、シールドされた Vm を作成します。](guarded-fabric-shielded-vm-windows-azure-pack.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-shielded-vms.png" alt="Step 15" hspace="8" align="right" /><br>[VMM を使用して、シールドされた Vm を作成します。](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-vms) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-shielded-vms.png" alt="Step 15" hspace="8" align="right" />|


## <a name="see-also"></a>関連項目

- [保護されたファブリックとシールドされた Vm](guarded-fabric-and-shielded-vms-top-node.md)
