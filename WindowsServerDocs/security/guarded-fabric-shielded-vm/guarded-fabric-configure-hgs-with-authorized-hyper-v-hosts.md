---
title: 保護されたホストの展開
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 2379ca26-b32d-4055-8b4b-99d1f2df37e1
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 3b20a7eb2b5097d8ddb7381fd0304581ca4e6722
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845353"
---
# <a name="deploy-guarded-hosts"></a>保護されたホストの展開

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

このセクションのトピックでは、ファブリック管理者は、ホスト ガーディアン サービス (HGS) で動作する HYPER-V ホストを構成する手順について説明します。 次の手順では、少なくとも 1 つのノードを開始する前に、[を HGS クラスターを設定する必要があります](guarded-fabric-setting-up-the-host-guardian-service-hgs.md)します。

**TPM によって信頼された構成証明のため**:
1. [Fabric の DNS を構成する](guarded-fabric-configuring-fabric-dns.md):HGS のドメインに fabric ドメインの DNS フォワーダーを設定する方法を示します。
2. [HGS で必要な情報をキャプチャ](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md):TPM の識別子 (プラットフォーム識別子とも呼ばれます) をキャプチャ、コード整合性ポリシーを作成および TPM ベースラインを作成する方法を指示します。 構成証明書を構成する HGS 管理者にこの情報を提供します。
3. [保護されたホストを証明できることを確認します。](guarded-fabric-confirm-hosts-can-attest-successfully.md)

**ホスト キーの構成証明の**:
1. [ホスト キーを作成する](guarded-fabric-create-host-key.md#create-a-host-key):HGS のドメインに fabric ドメインの DNS フォワーダーを設定する方法を示します。
2. [ホスト キー構成証明サービスを追加する](guarded-fabric-create-host-key.md#add-the-host-key-to-the-attestation-service):、そのグループのメンバーとして保護されたホストを追加、ファブリック ドメインで Active Directory セキュリティ グループを設定およびグループ識別子を HGS 管理者に提供する方法を指示します。 
3. [保護されたホストを証明できることを確認します。](guarded-fabric-confirm-hosts-can-attest-successfully.md)


**管理者によって信頼された構成証明のため**:
1. [Fabric の DNS を構成する](guarded-fabric-configuring-fabric-dns.md):HGS のドメインに fabric ドメインの DNS フォワーダーを設定する方法を示します。
2. [セキュリティ グループを作成する](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md):、そのグループのメンバーとして保護されたホストを追加、ファブリック ドメインで Active Directory セキュリティ グループを設定およびグループ識別子を HGS 管理者に提供する方法を指示します。 
3. [保護されたホストを証明できることを確認します。](guarded-fabric-confirm-hosts-can-attest-successfully.md)


## <a name="see-also"></a>関連項目

- [展開タスクが保護され、ファブリックとシールドされた Vm](guarded-fabric-deploying-hgs-overview.md#deployment-tasks-for-guarded-fabrics-and-shielded-vms)
