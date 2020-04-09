---
title: 保護されたファブリックとシールドされた VM
ms.prod: windows-server
ms.topic: article
ms.assetid: 5c7ada81-2d97-41d4-87cf-1a7ccf06cd20
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 9e76b3081438ae38c6b83b7cdd179d47b1e21a70
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856915"
---
# <a name="guarded-fabric-and-shielded-vms"></a>保護されたファブリックとシールドされた VM

>適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

ホスト環境を提供する最も重要な目標の1つは、環境で実行されている仮想マシンのセキュリティを保証することです。 クラウド サービス プロバイダーやエンタープライズ プライベート クラウド管理者は、保護されたファブリックを使用して、セキュリティが強化された VM 環境を実現できます。 保護されたファブリックは、1 つホスト ガーディアン サービス (HGS)、通常は、3 ノードのクラスターと、1 つまたは複数の保護されたホスト、シールドされた仮想マシン (VM) のセットで構成されます。

> [!IMPORTANT]
> 運用環境でシールドされた仮想マシンを展開する前に、最新の累積的な更新プログラムがインストールされていることを確認します。

## <a name="videos-blog-and-overview-topic-about-guarded-fabrics-and-shielded-vms"></a>保護されたファブリックとシールドされた Vm に関するビデオ、ブログ、概要トピック

- ビデオ: [Windows Server 2019 で insider の脅威から仮想化ファブリックを保護する方法](https://myignite.techcommunity.microsoft.com/sessions/64690)
- ビデオ: [Windows Server 2016 でのシールドされた Virtual Machines の概要](https://channel9.msdn.com/Shows/Mechanics/Introduction-to-Shielded-Virtual-Machines-in-Windows-Server-2016)
- ビデオ: [Windows Server 2016 hyper-v を使用したシールドされた vm の](https://channel9.msdn.com/events/Ignite/2016/BRK3124)詳細
- ビデオ: シールドされた[vm と、Windows Server 2016 を使用した保護されたファブリックの展開](https://mva.microsoft.com/training-courses/deploying-shielded-vms-and-a-guarded-fabric-with-windows-server-2016-17131?l=WFLef7vUD_4604300474)
- ブログ:[データセンターとプライベートクラウドのセキュリティ](https://blogs.technet.microsoft.com/datacentersecurity/)に関するブログ
- 概要: 保護された[ファブリックとシールドされた vm の概要](Guarded-Fabric-and-Shielded-VMs.md)

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
