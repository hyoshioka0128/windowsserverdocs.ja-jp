---
title: 保護されたホストの展開
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 2379ca26-b32d-4055-8b4b-99d1f2df37e1
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: bc79d13b4dda96cd3e760958a6310276d2c45bae
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386752"
---
# <a name="deploy-guarded-hosts"></a>保護されたホストの展開

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

このセクションのトピックでは、ファブリック管理者がホストガーディアンサービス (HGS) を使用するように Hyper-v ホストを構成するために実行する手順について説明します。 これらの手順を開始する前に、HGS クラスター内の少なくとも1つのノードがセットアップされて[いる必要があり](guarded-fabric-setting-up-the-host-guardian-service-hgs.md)ます。

**TPM で信頼された構成証明の場合**:
1. [ファブリック DNS を構成し](guarded-fabric-configuring-fabric-dns.md)ます。DNS フォワーダーを、ファブリックドメインから HGS ドメインに設定する方法について説明します。
2. [HGS で必要な情報のキャプチャ](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md):TPM 識別子 (プラットフォーム id とも呼ばれます) をキャプチャする方法、コード整合性ポリシーを作成する方法、および TPM ベースラインを作成する方法について説明します。 次に、この情報を HGS 管理者に提供して、構成証明を構成します。
3. [保護されたホストが証明できることを確認する](guarded-fabric-confirm-hosts-can-attest-successfully.md)

**ホストキーの構成証明の場合**:
1. [ホストキーを作成し](guarded-fabric-create-host-key.md#create-a-host-key)ます。DNS フォワーダーを、ファブリックドメインから HGS ドメインに設定する方法について説明します。
2. [構成証明サービスにホストキーを追加](guarded-fabric-create-host-key.md#add-the-host-key-to-the-attestation-service)します。ファブリックドメインで Active Directory セキュリティグループを設定し、保護されたホストをそのグループのメンバーとして追加し、そのグループ識別子を HGS 管理者に提供する方法について説明します。 
3. [保護されたホストが証明できることを確認する](guarded-fabric-confirm-hosts-can-attest-successfully.md)


**管理者によって信頼された構成証明の場合**:
1. [ファブリック DNS を構成し](guarded-fabric-configuring-fabric-dns.md)ます。DNS フォワーダーを、ファブリックドメインから HGS ドメインに設定する方法について説明します。
2. [セキュリティグループを作成し](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md)ます。ファブリックドメインで Active Directory セキュリティグループを設定し、保護されたホストをそのグループのメンバーとして追加し、そのグループ識別子を HGS 管理者に提供する方法について説明します。 
3. [保護されたホストが証明できることを確認する](guarded-fabric-confirm-hosts-can-attest-successfully.md)


## <a name="see-also"></a>関連項目

- [保護されたファブリックとシールドされた Vm の展開タスク](guarded-fabric-deploying-hgs-overview.md#deployment-tasks-for-guarded-fabrics-and-shielded-vms)
