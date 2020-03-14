---
title: 保護されたホストの前提条件
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 8a9273eef906130b11b98148cf1e84f7e18812b0
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/13/2020
ms.locfileid: "79322494"
---
# <a name="prerequisites-for-guarded-hosts"></a>保護されたホストの前提条件

>適用対象: windows server 2019、Windows Server (半期チャネル)、Windows Server 2016

選択した構成証明のモードについてホストの前提条件を確認し、次の手順をクリックして、保護されたホストを追加します。

## <a name="tpm-trusted-attestation"></a>TPM-信頼された構成証明

TPM モードを使用する保護されたホストは、次の前提条件を満たしている必要があります。

-   **ハードウェア**: 初期展開には1つのホストが必要です。 シールドされた Vm の Hyper-v ライブマイグレーションをテストするには、少なくとも2つのホストが必要です。

    ホストには次のものが必要です。
    
    - IOMMU と第2レベルのアドレス変換 (SLAT)
    - TPM 2.0
    - UEFI 2.3.1 以降
    - UEFI (BIOS または "レガシ" モードではなく) を使用して起動するように構成されています
    - セキュアブートが有効
        
-   **オペレーティングシステム**: Windows Server 2016 Datacenter edition 以降

    > [!IMPORTANT]
    > [最新の累積的な更新プログラム](https://support.microsoft.com/help/4000825/windows-10-and-windows-server-2016-update-history)がインストールされていることを確認してください。  

-   **役割と機能**: hyper-v の役割と Host Guardian Hyper-v のサポート機能。 Host Guardian Hyper-v サポート機能は、Windows Server の Datacenter エディションでのみ使用できます。 

> [!WARNING]
> Host Guardian Hyper-v サポート機能を使用すると、一部のデバイスと互換性のない、コードの整合性を仮想化ベースで保護できます。 この機能を有効にする前に、ラボでこの構成をテストすることを強くお勧めします。 そうしないと、データ損失やブルー スクリーン エラー (Stop エラーとも呼ばれます) などを含む予期しないエラーが発生することがあります。 詳細については、「[互換性のあるハードウェアと Windows Server 仮想化によるコードの整合性の保護](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md)」を参照してください。

**次のステップ:** 
> [!div class="nextstepaction"]
> [TPM 情報のキャプチャ](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md)

## <a name="host-key-attestation"></a>ホストキーの構成証明

ホストキーの構成証明を使用する保護されたホストは、次の前提条件を満たす必要があります。

- **ハードウェア**: Windows server 2019 以降で hyper-v を実行できる任意のサーバー
- **オペレーティングシステム**: Windows Server 2019 Datacenter edition
- **役割と機能**: hyper-v の役割と Host Guardian Hyper-v のサポート機能 

ホストをドメインまたはワークグループに参加させることができます。 

ホストキーの構成証明については、HGS は Windows Server 2019 を実行し、v2 構成証明を使用して動作している必要があります。 詳細については、「 [HGS の前提条件](guarded-fabric-prepare-for-hgs.md#prerequisites)」を参照してください。 

**次のステップ:** 
> [!div class="nextstepaction"]
> [キーペアを作成する](guarded-fabric-create-host-key.md)

## <a name="admin-trusted-attestation"></a>管理者-信頼された構成証明

>[!IMPORTANT]
>管理者によって信頼された構成証明 (AD モード) は、Windows Server 2019 以降では非推奨とされます。 TPM の構成証明が不可能な環境では、[ホストキー](#host-key-attestation)の構成証明を構成します。 ホストキーの構成証明により、AD モードと同様の保証が提供され、セットアップが簡単になります。 

Hyper-v ホストは、AD モードに関して次の前提条件を満たしている必要があります。

-   **ハードウェア**: Windows server 2016 以降で hyper-v を実行できる任意のサーバー。 初期デプロイには1つのホストが必要です。 シールドされた Vm の Hyper-v ライブマイグレーションをテストするには、少なくとも2つのホストが必要です。

-   **オペレーティングシステム**: Windows Server 2016 Datacenter edition

    > [!IMPORTANT]
    > 最新の[累積的な更新プログラム](https://support.microsoft.com/help/4000825/windows-10-and-windows-server-2016-update-history)をインストールします。

-   **役割と機能**: hyper-v の役割と Host Guardian hyper-v サポート機能。これは、Windows Server 2016 Datacenter edition でのみ使用できます。 

> [!WARNING]
> Host Guardian Hyper-v サポート機能を使用すると、一部のデバイスと互換性のない、コードの整合性を仮想化ベースで保護できます。 この機能を有効にする前に、ラボでこの構成をテストすることを強くお勧めします。 そうしないと、データ損失やブルー スクリーン エラー (Stop エラーとも呼ばれます) などを含む予期しないエラーが発生することがあります。 詳細については、「[互換性のあるハードウェアと Windows Server 2016 の仮想化によるコードの整合性の保護](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md)」を参照してください。

**次のステップ:** 
> [!div class="nextstepaction"]
> [保護されたホストをセキュリティグループに配置する](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md)