---
title: 保護されたファブリックとシールドされた VM
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 5c7ada81-2d97-41d4-87cf-1a7ccf06cd20
manager: dongill
author: rpsqrd
ms.author: justinha
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: c06432a039341978956066344710920652187b97
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403671"
---
# <a name="guarded-fabric-and-shielded-vms"></a>保護されたファブリックとシールドされた VM

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

ホスト環境を提供する最も重要な目標の1つは、環境で実行されている仮想マシンのセキュリティを保証することです。 クラウド サービス プロバイダーやエンタープライズ プライベート クラウド管理者は、保護されたファブリックを使用して、セキュリティが強化された VM 環境を実現できます。 保護されたファブリックは、1 つホスト ガーディアン サービス (HGS)、通常は、3 ノードのクラスターと、1 つまたは複数の保護されたホスト、シールドされた仮想マシン (VM) のセットで構成されます。

> [!IMPORTANT]
> 運用環境でシールドされた仮想マシンを展開する前に、最新の累積的な更新プログラムがインストールされていることを確認します。

## <a name="videos-blog-and-overview-topic-about-guarded-fabrics-and-shielded-vms"></a>保護されたファブリックとシールドされた Vm に関するビデオ、ブログ、概要トピック

- ビデオ:[Windows Server 2019 で insider の脅威から仮想化ファブリックを保護する方法](https://myignite.techcommunity.microsoft.com/sessions/64690)
- ビデオ:[Windows Server 2016 でのシールドされた Virtual Machines の概要](https://channel9.msdn.com/Shows/Mechanics/Introduction-to-Shielded-Virtual-Machines-in-Windows-Server-2016)
- ビデオ:[Windows Server 2016 Hyper-v を使用したシールドされた Vm の詳細](https://channel9.msdn.com/events/Ignite/2016/BRK3124)
- ビデオ:[Windows Server 2016 でシールドされた Vm と保護されたファブリックを展開する](https://mva.microsoft.com/en-US/training-courses/deploying-shielded-vms-and-a-guarded-fabric-with-windows-server-2016-17131?l=WFLef7vUD_4604300474)
- ブログ[データセンターとプライベートクラウドのセキュリティに関するブログ](https://blogs.technet.microsoft.com/datacentersecurity/)
- 概要:[保護されたファブリックとシールドされた VM の概要](Guarded-Fabric-and-Shielded-VMs.md)

## <a name="planning-topics"></a>計画に関するトピック

- [ホストの計画ガイド](guarded-fabric-planning-for-hosters.md)
- [テナントの計画ガイド](guarded-fabric-shielded-vm-planning-for-tenants.md)

## <a name="deployment-topics"></a>展開に関するトピック

- [展開ガイド](guarded-fabric-deploying-hgs-overview.md)
    - [クイック スタート](guarded-fabric-deployment-overview.md)
    - [HGS の展開](guarded-fabric-setting-up-the-host-guardian-service-hgs.md)
    - [保護されたホストの展開](guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)
        - [保護されたホストになるホストのファブリック DNS を構成する](guarded-fabric-configuring-fabric-dns.md)
        - [AD モードを使用して保護されたホストを展開する](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md)
        - [TPM モードを使用して保護されたホストを展開する](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md)
        - [保護されたホストが証明できることを確認する](guarded-fabric-confirm-hosts-can-attest-successfully.md)
        - [シールドされた Vm-ホスティングサービスプロバイダーが VMM で保護されたホストを展開する](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-hosts)
    - [シールドされた VMの展開](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
        - [シールドされた VM テンプレートを作成する](guarded-fabric-create-a-shielded-vm-template.md)
        - [VM シールドヘルパー VHD を準備する](guarded-fabric-vm-shielding-helper-vhd.md)
        - [Windows Azure Pack の設定](guarded-fabric-hoster-sets-up-windows-azure-pack.md)
        - [シールドデータファイルを作成する](guarded-fabric-tenant-creates-shielding-data.md)
        - [Windows Azure Pack を使用してシールドされた VM をデプロイする](guarded-fabric-shielded-vm-windows-azure-pack.md)
        - [Virtual Machine Manager を使用してシールドされた VM をデプロイする](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)

## <a name="operations-and-management-topic"></a>操作と管理に関するトピック

- [ホストガーディアンサービスの管理](guarded-fabric-manage-hgs.md)
