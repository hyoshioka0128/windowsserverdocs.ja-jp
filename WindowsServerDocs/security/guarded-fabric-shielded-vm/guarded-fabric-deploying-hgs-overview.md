---
title: ホストガーディアンサービスの展開
ms.topic: article
ms.assetid: 310b63d9-5ac7-4961-98ef-103af45d706a
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 01/14/2020
ms.openlocfilehash: e8077655717db3f6700b0e0a3d12792465b41299
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939773"
---
# <a name="deploying-the-host-guardian-service"></a>ホストガーディアンサービスの展開

>適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

ホスト環境を提供する最も重要な目標の1つは、環境で実行されている仮想マシンのセキュリティを保証することです。 クラウド サービス プロバイダーやエンタープライズ プライベート クラウド管理者は、保護されたファブリックを使用して、セキュリティが強化された VM 環境を実現できます。 保護されたファブリックは、1 つホスト ガーディアン サービス (HGS)、通常は、3 ノードのクラスターと、1 つまたは複数の保護されたホスト、シールドされた仮想マシン (VM) のセットで構成されます。

## <a name="video-deploying-a-guarded-fabric"></a>ビデオ: 保護されたファブリックのデプロイ

> [!VIDEO https://www.microsoft.com/videoplayer/embed/dcd8e99f-36f1-4bc8-b3d2-9576da38d9f1?autoplay=false]

## <a name="deployment-tasks-for-guarded-fabrics-and-shielded-vms"></a>保護されたファブリックとシールドされた Vm の展開タスク

次の表は、保護されたファブリックをデプロイし、さまざまな管理者ロールに従ってシールドされた Vm を作成するためのタスクを示しています。 HGS 管理者が承認された Hyper-v ホストで HGS を構成すると、ファブリック管理者は、ホストに関する識別情報を同時に収集して提供することに注意してください。

| コンテンツへのステップアンドリンク | Image |
|--|--|--|
| 1- [HGS の前提条件を確認](guarded-fabric-prepare-for-hgs.md)する | ![手順 1. 前提条件を確認する](../media/Guarded-Fabric-Shielded-VM/guarded-host-verify.png) |
| 2-[最初の HGS ノードを構成する](guarded-fabric-choose-where-to-install-hgs.md) | ![手順 2. 最初の HGS ノードを構成する](../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-first-hgs-node.png) |
| 3-[追加の HGS ノードを構成する](guarded-fabric-configure-additional-hgs-nodes.md) | ![手順 3. 追加の HGS ノードを構成する](../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-secondary-hgs-nodes.png) |
| 4-[ファブリック DNS を構成する](guarded-fabric-configuring-fabric-dns.md) | ![手順 4. ファブリック DNS を構成する](../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-fabric-dns.png) |
| 5-[ホストの前提条件 (キー) を確認](guarded-fabric-guarded-host-prerequisites.md#host-key-attestation)し、[ホストの前提条件を確認する (TPM)](guarded-fabric-guarded-host-prerequisites.md#tpm-trusted-attestation) | ![手順 5. ホストの前提条件のキーとホストの前提条件となる TPM を確認する](../media/Guarded-Fabric-Shielded-VM/guarded-host-verify.png) |
| 6-[ホストキー (キー) を作成](guarded-fabric-create-host-key.md)し、[ホスト情報 (TPM) を収集](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md)する | ![手順 6. ホストキーを作成してホスト情報を収集する](../media/Guarded-Fabric-Shielded-VM/guarded-host-collect-info-from-hosts.png) |
| 7- [HGS にホスト情報を構成する](guarded-fabric-add-host-information-to-hgs.md) | ![手順 7. HGS にホスト情報を追加する](../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-hgs-with-host-info.png) |
| 8-[ホストが証明できることを確認する](guarded-fabric-confirm-hosts-can-attest-successfully.md) | ![手順 8. ホストが証明できることを確認する](../media/Guarded-Fabric-Shielded-VM/guarded-host-confirm-hosts-attest.png) |
| 9- [VMM を構成する (省略可能)](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-overview) | ![手順 9. VMM を構成する (省略可能)](../media/Guarded-Fabric-Shielded-VM/guarded-host-configure-vmm.png) |
| 10-[テンプレートディスクを作成する](guarded-fabric-create-a-shielded-vm-template.md) | ![手順 10. テンプレートディスクを作成する](../media/Guarded-Fabric-Shielded-VM/guarded-host-create-template-disk.png) |
| 11- [VMM 用の VM シールドヘルパーディスクを作成する (省略可能)](guarded-fabric-vm-shielding-helper-vhd.md) | ![手順 11. VMM 用の VM シールドヘルプディスクを作成する](../media/Guarded-Fabric-Shielded-VM/guarded-host-create-helper-disk.png) |
| 12- [Windows Azure Pack の設定 (省略可能)](guarded-fabric-shielded-vm-windows-azure-pack.md) | ![手順 12. Windows Azure Pack を設定する (省略可能)](../media/Guarded-Fabric-Shielded-VM/guarded-host-windows-azure-pack.png) |
| 13-[シールドデータファイルを作成する](guarded-fabric-tenant-creates-shielding-data.md) | ![手順 13. シールドデータファイルを作成する](../media/Guarded-Fabric-Shielded-VM/guarded-host-shielding-data-file.png) |
| 14- [Windows Azure Pack を使用してシールドされた vm を作成する](guarded-fabric-shielded-vm-windows-azure-pack.md) | ![手順 14. Windows Azure Pack を使用してシールドされた Vm を作成する](../media/Guarded-Fabric-Shielded-VM/guarded-host-shielded-vms.png) |
| 15- [VMM を使用してシールドされた vm を作成する](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-vms) | ![手順 15. VMM を使用してシールドされた Vm を作成する](../media/Guarded-Fabric-Shielded-VM/guarded-host-shielded-vms.png) |

## <a name="additional-references"></a>その他の参照情報

- [保護されたファブリックとシールドされた VM](guarded-fabric-and-shielded-vms-top-node.md)
