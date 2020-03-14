---
title: ホストガーディアンサービスの展開
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 310b63d9-5ac7-4961-98ef-103af45d706a
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 01/14/2020
ms.openlocfilehash: e66e7f365553f3aa106abbebf372492e0cc08386
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322024"
---
# <a name="deploying-the-host-guardian-service"></a>ホストガーディアンサービスの展開 

>適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

ホスト環境を提供する最も重要な目標の1つは、環境で実行されている仮想マシンのセキュリティを保証することです。 クラウド サービス プロバイダーやエンタープライズ プライベート クラウド管理者は、保護されたファブリックを使用して、セキュリティが強化された VM 環境を実現できます。 保護されたファブリックは、1 つホスト ガーディアン サービス (HGS)、通常は、3 ノードのクラスターと、1 つまたは複数の保護されたホスト、シールドされた仮想マシン (VM) のセットで構成されます。

## <a name="video-deploying-a-guarded-fabric"></a>ビデオ: 保護されたファブリックのデプロイ 

> [!VIDEO https://www.microsoft.com/videoplayer/embed/dcd8e99f-36f1-4bc8-b3d2-9576da38d9f1?autoplay=false]

## <a name="deployment-tasks-for-guarded-fabrics-and-shielded-vms"></a>保護されたファブリックとシールドされた Vm の展開タスク

次の表は、保護されたファブリックをデプロイし、さまざまな管理者ロールに従ってシールドされた Vm を作成するためのタスクを示しています。 HGS 管理者が承認された Hyper-v ホストで HGS を構成すると、ファブリック管理者は、ホストに関する識別情報を同時に収集して提供することに注意してください。    

|<img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-hgs-administrator-tasks.png" alt="Host Guardian Service administrator tasks" width="238" height="62" align="left" /> | <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-fabric-administrator-tasks.png" alt="Fabric administrator tasks" width="300" height="62" align="left" /> | <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-tenant-administrator-tasks.png" alt="Tenant administrator tasks" width="184" height="66" align="left" /> |
|-------------------------------------|--------------------------------|-----------------------------------------|
|(1) [HGS の前提条件を確認](guarded-fabric-prepare-for-hgs.md)する <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-verify.png" alt="Step 1" hspace="8" align="right" />| | |
|(2)[最初の HGS&nbsp;ノード](guarded-fabric-choose-where-to-install-hgs.md)&nbsp; を構成します<img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-first-hgs-node.png" alt="Step 2" hspace="8" align="right" />| | |
|(3)[追加の HGS&nbsp;ノードを構成する](guarded-fabric-configure-additional-hgs-nodes.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-secondary-hgs-nodes.png" alt="Step 3" hspace="8" align="right" />| | |
| &nbsp; |(4)[ファブリック DNS を構成する](guarded-fabric-configuring-fabric-dns.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-fabric-dns.png" alt="Step 4" hspace="8" align="right" />| |
| &nbsp; |(5)[ホスト&nbsp;の前提条件を確認する (キー)](guarded-fabric-guarded-host-prerequisites.md#host-key-attestation)<br>[ホスト&nbsp;前提条件を確認する (TPM)](guarded-fabric-guarded-host-prerequisites.md#tpm-trusted-attestation)<img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-verify.png" alt="Step 5" hspace="8" align="right" />| |
|(7)[ホスト情報を使用して HGS を構成する](guarded-fabric-add-host-information-to-hgs.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-hgs-with-host-info.png" alt="Step 7" hspace="8" align="right" />|(6)[ホストキーの作成 (キー)](guarded-fabric-create-host-key.md)<br>[ホスト情報の収集 (TPM)](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-collect-info-from-hosts.png" alt="Step 6" hspace="8" align="right" />| |
| &nbsp; |(8)[ホストが証明できることを確認する](guarded-fabric-confirm-hosts-can-attest-successfully.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-confirm-hosts-attest.png" alt="Step 8" hspace="8" align="right" />| |
| &nbsp; |(9) [VMM を構成する (省略可能)](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-overview) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-vmm.png" alt="Step 9" hspace="8" align="right" />| |
| &nbsp; |(10)[テンプレートディスクを作成する](guarded-fabric-create-a-shielded-vm-template.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-create-template-disk.png" alt="Step 10" hspace="8" align="right" />| |
| &nbsp; |(11) [VMM 用の VM シールドヘルパーディスクを作成する (省略可能)](guarded-fabric-vm-shielding-helper-vhd.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-create-helper-disk.png" alt="Step 11" hspace="8" align="right" />| |
| &nbsp; |(12) [Windows Azure Pack の設定 (省略可能)](guarded-fabric-shielded-vm-windows-azure-pack.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-windows-azure-pack.png" alt="Step 12" hspace="8" align="right" />| |
| &nbsp; | &nbsp; |(13)[シールドデータファイルの作成](guarded-fabric-tenant-creates-shielding-data.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-shielding-data-file.png" alt="Step 13" hspace="8" align="right" />|
| &nbsp; | &nbsp; |(14) [Windows Azure Pack を使用してシールドされた vm を作成する](guarded-fabric-shielded-vm-windows-azure-pack.md) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-shielded-vms.png" alt="Step 14" hspace="8" align="right" /><br>[VMM を使用してシールドされた Vm を作成する](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-vms) <img src="../media/Guarded-Fabric-Shielded-VM/guarded-host-shielded-vms.png" alt="Step 15" hspace="8" align="right" />|


## <a name="see-also"></a>参照

- [保護されたファブリックとシールドされた VM](guarded-fabric-and-shielded-vms-top-node.md)
