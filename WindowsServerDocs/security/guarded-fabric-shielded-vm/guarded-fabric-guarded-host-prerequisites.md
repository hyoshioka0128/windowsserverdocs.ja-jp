---
title: 保護されたホストの前提条件
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 5f2c3ec4b2c434ea945d86c4b1593e2e416a5123
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819233"
---
# <a name="prerequisites-for-guarded-hosts"></a>保護されたホストの前提条件

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

ホストの前提条件の構成証明モードを選択したらを確認し、保護されたホストを追加するには、次の手順をクリックします。

## <a name="tpm-trusted-attestation"></a>TPM によって信頼された構成証明

TPM のモードを使用して保護されたホストは、次の前提条件を満たす必要があります。

-   **ハードウェア**:1 つのホストは、最初の展開に必要です。 シールドされた Vm の HYPER-V のライブ マイグレーションをテストするには、少なくとも 2 つのホストが必要です。

    ホストが必要です。
    
    - IOMMU と 2 番目のレベルのアドレス変換 (SLAT)
    - TPM 2.0
    - UEFI 2.3.1 以降
    - ブート UEFI (BIOS や「レガシ」モード) を使用するように構成
    - セキュア ブートが有効になっています。
        
-   **オペレーティング システム**:Windows Server 2016 Datacenter edition またはそれ以降

    > [!IMPORTANT]
    > インストールするかどうかを確認、[最新の累積的な更新プログラム](https://support.microsoft.com/help/4000825/windows-10-and-windows-server-2016-update-history)します。  

-   **役割と機能**:Hyper-v の役割と Host Guardian HYPER-V サポート機能。 Host Guardian HYPER-V サポート機能は、Windows Server の Datacenter の各エディションで使用できるのみです。 

> [!WARNING]
> Host Guardian HYPER-V サポート機能は、一部のデバイスと互換性がない可能性があります、コードの整合性の仮想化ベースの保護を使用できます。 この機能を有効にする前に、ラボでこの構成のテストを強くお勧めします。 そうしないと、データ損失やブルー スクリーン エラー (Stop エラーとも呼ばれます) などを含む予期しないエラーが発生することがあります。 詳細については、次を参照してください。[コードの整合性の Windows Server 仮想化ベースの保護との互換性のあるハードウェア](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md)します。

**次の手順:** 
>[!div class="nextstepaction"]
[TPM の情報をキャプチャします。](guarded-fabric-tpm-trusted-attestation-capturing-hardware.md)

## <a name="host-key-attestation"></a>ホスト キーの構成証明

ホスト キーの構成証明を使用して保護されたホストは、次の前提条件を満たす必要があります。

- **ハードウェア**:Windows Server 2019 で HYPER-V の先頭を実行できる任意のサーバー
- **オペレーティング システム**:Windows Server 2019 Datacenter edition
- **役割と機能**:HYPER-V の役割と Host Guardian HYPER-V サポート機能 

ホストは、ドメインまたはワークグループに参加することができます。 

ホスト キーの構成証明は、HGS を Windows Server 2019 を実行していると v2 の構成証明で動作する必要があります。 詳細については、次を参照してください。 [HGS の前提条件](guarded-fabric-prepare-for-hgs.md#prerequisites)します。 

**次の手順:** 
>[!div class="nextstepaction"]
[キーのペアを作成します。](guarded-fabric-create-host-key.md)

## <a name="admin-trusted-attestation"></a>管理者によって信頼された構成証明

>[!IMPORTANT]
>管理者によって信頼された構成証明 (AD モード) では、Windows Server 2019 以降推奨されていません。 TPM 構成証明が可能な環境では、次のように構成します。[ホスト キーの構成証明](#host-key-attestation)します。 ホスト キーの構成証明は、AD モードのような保証しを設定する方が簡単です。 

HYPER-V ホストには、AD モードの次の前提条件を満たす必要があります。

-   **ハードウェア**:任意のサーバーは Windows Server 2016 で HYPER-V の先頭を実行できます。 1 つのホストは、最初の展開に必要です。 シールドされた Vm の HYPER-V のライブ マイグレーションをテストするには、少なくとも 2 つのホストが必要です。

-   **オペレーティング システム**:Windows Server 2016 Datacenter edition

    > [!IMPORTANT]
    > インストール、[最新の累積的な更新プログラム](https://support.microsoft.com/help/4000825/windows-10-and-windows-server-2016-update-history)します。

-   **役割と機能**:Hyper-v の役割と Host Guardian HYPER-V サポート機能は、Windows Server 2016 Datacenter edition でのみ使用します。 

> [!WARNING]
> Host Guardian HYPER-V サポート機能は、一部のデバイスと互換性がない可能性があります、コードの整合性の仮想化ベースの保護を使用できます。 この機能を有効にする前に、ラボでこの構成のテストを強くお勧めします。 そうしないと、データ損失やブルー スクリーン エラー (Stop エラーとも呼ばれます) などを含む予期しないエラーが発生することがあります。 詳細については、次を参照してください。[コードの整合性の Windows Server 2016 の仮想化ベースの保護との互換性のあるハードウェア](guarded-fabric-compatible-hardware-with-virtualization-based-protection-of-code-integrity.md)します。

**次の手順:** 
>[!div class="nextstepaction"]
[セキュリティ グループに保護されたホストを配置します。](guarded-fabric-admin-trusted-attestation-creating-a-security-group.md)