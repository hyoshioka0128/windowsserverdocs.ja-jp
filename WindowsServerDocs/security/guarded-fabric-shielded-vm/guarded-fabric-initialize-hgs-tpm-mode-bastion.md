---
title: 要塞フォレスト内の TPM のモードを使用して HGS クラスターを初期化します。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: ac6407f9f23780dc62ff7d99fe0daf0f81f79f72
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832143"
---
# <a name="initialize-the-hgs-cluster-using-tpm-mode-in-an-existing-bastion-forest"></a>既存の要塞フォレスト内の TPM のモードを使用して HGS クラスターを初期化します。

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

Active Directory Domain Services は、コンピューターにインストールされますが、構成されていないままにする必要があります。

[!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)]

続行する前にいることを確認するが、ホスト ガーディアン サービスのクラスター オブジェクトを事前設定されたユーザーでログオンしたを付与**フルコントロール**Active Directory 内の VCO と CNO オブジェクト。
渡される必要がある仮想コンピューター オブジェクトの名前、`-HgsServiceName`パラメーター、およびクラスター名を`-ClusterName`パラメーター。

> [!TIP]
> 再確認、AD ドメイン コント ローラー、クラスター オブジェクトにが続行する前に、すべての Dc にレプリケートします。

PFX に基づく証明書を使用している場合は、HGS サーバーで次のコマンドを実行します。

```powershell
$signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
$encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

Install-ADServiceAccount -Identity 'HGSgMSA'

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustTpm
```

(証明書の HSM を基盤と証明書をエクスポートできない) など、ローカル コンピューターにインストールされている証明書を使用している場合は、使用、`-SigningCertificateThumbprint`と`-EncryptionCertificateThumbprint`パラメーター代わりにします。

## <a name="next-step"></a>次の手順

>[!div class="nextstepaction"]
[TPM のルート証明書をインストールします。](guarded-fabric-install-trusted-tpm-root-certificates.md)