---
title: 保護されたファブリックとシールドされた VM
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 5c7ada81-2d97-41d4-87cf-1a7ccf06cd20
manager: dongill
author: rpsqrd
ms.author: justinha
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: c2c16574439569eeb1181977f23bae238f43865c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59857433"
---
# <a name="guarded-fabric-and-shielded-vms"></a>保護されたファブリックとシールドされた VM

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

ホスト環境を提供するための最も重要な目標の 1 つは、環境で実行する仮想マシンのセキュリティを保証することです。 クラウド サービス プロバイダーやエンタープライズ プライベート クラウド管理者は、保護されたファブリックを使用して、セキュリティが強化された VM 環境を実現できます。 保護されたファブリックは、1 つホスト ガーディアン サービス (HGS)、通常は、3 ノードのクラスターと、1 つまたは複数の保護されたホスト、シールドされた仮想マシン (VM) のセットで構成されます。

> [!IMPORTANT]
> 運用環境でのシールドされた仮想マシンを展開する前に最新の累積的な更新プログラムがインストールされていることを確認します。

## <a name="videos-blog-and-overview-topic-about-guarded-fabrics-and-shielded-vms"></a>ビデオ、ブログ、および概要のトピックについて保護され、ファブリックとシールドされた Vm

- ビデオ:[Windows Server 2019 と内部の脅威から仮想化ファブリックを保護する方法](https://myignite.techcommunity.microsoft.com/sessions/64690)
- ビデオ:[Windows Server 2016 のシールドされた仮想マシンの概要](https://channel9.msdn.com/Shows/Mechanics/Introduction-to-Shielded-Virtual-Machines-in-Windows-Server-2016)
- ビデオ:[Windows でのシールドされた Vm を極める Server 2016 Hyper-v の概要](https://channel9.msdn.com/events/Ignite/2016/BRK3124)
- ビデオ:[シールドされた Vm と Windows Server 2016 で保護されたファブリックを展開します。](https://mva.microsoft.com/en-US/training-courses/deploying-shielded-vms-and-a-guarded-fabric-with-windows-server-2016-17131?l=WFLef7vUD_4604300474)
- ブログ:[データ センターおよびプライベート クラウドのセキュリティ ブログ](https://blogs.technet.microsoft.com/datacentersecurity/)
- 概要:[保護されたファブリックとシールドされた Vm の概要](Guarded-Fabric-and-Shielded-VMs.md)

## <a name="planning-topics"></a>計画に関するトピック

- [ホスト側の計画ガイド](guarded-fabric-planning-for-hosters.md)
- [テナント用の計画ガイド](guarded-fabric-shielded-vm-planning-for-tenants.md)

## <a name="deployment-topics"></a>展開に関するトピック

- [展開ガイド](guarded-fabric-deploying-hgs-overview.md)
    - [クイック スタート](guarded-fabric-deployment-overview.md)
    - [HGS をデプロイします。](guarded-fabric-setting-up-the-host-guardian-service-hgs.md)
    - [保護されたホストを展開します。](guarded-fabric-configure-hgs-with-authorized-hyper-v-hosts.md)
        - [保護されたホストとなるホストの fabric の DNS を構成します。](guarded-fabric-configuring-fabric-dns.md)
        - [AD モードを使用して保護されたホストを展開します。](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md)
        - [TPM のモードを使用して保護されたホストを展開します。](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md)
        - [保護されたホストを証明できることを確認します。](guarded-fabric-confirm-hosts-can-attest-successfully.md)
        - [シールドされた Vm - ホスティング サービス プロバイダーが VMM で保護されたホストを展開します。](https://technet.microsoft.com/system-center-docs/vmm/scenario/guarded-hosts)
    - [シールドされた Vm をデプロイします。](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
        - [シールドされた VM テンプレートを作成します。](guarded-fabric-create-a-shielded-vm-template.md)
        - [VM シールド ヘルパー VHD を準備します。](guarded-fabric-vm-shielding-helper-vhd.md)
        - [Windows Azure Pack をセットアップします。](guarded-fabric-hoster-sets-up-windows-azure-pack.md)
        - [シールド データ ファイルを作成します。](guarded-fabric-tenant-creates-shielding-data.md)
        - [Windows Azure Pack を使用して、シールドされた VM をデプロイします。](guarded-fabric-shielded-vm-windows-azure-pack.md)
        - [Virtual Machine Manager を使用して、シールドされた VM をデプロイします。](guarded-fabric-tenant-deploys-shielded-vm-using-vmm.md)

## <a name="operations-and-management-topic"></a>操作と管理のトピック

- [ホスト ガーディアン サービスの管理](guarded-fabric-manage-hgs.md)
