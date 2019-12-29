---
title: 要塞フォレストで TPM モードを使用して HGS クラスターを初期化する
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: b360f0f5195bea3c61f9a181b4b75a681f7e29b9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403604"
---
# <a name="initialize-the-hgs-cluster-using-tpm-mode-in-an-existing-bastion-forest"></a>既存の要塞フォレストで TPM モードを使用して HGS クラスターを初期化する

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

Active Directory Domain Services はコンピューターにインストールされますが、未構成のままにしておく必要があります。

[!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)]

続行する前に、ホストガーディアンサービスのクラスターオブジェクトを事前設定し、Active Directory の VCO および CNO オブジェクトに対して、ログインしているユーザーに**フルコントロール**を付与したことを確認してください。
仮想コンピューターのオブジェクト名は、`-HgsServiceName` パラメーターに、クラスター名を `-ClusterName` パラメーターに渡す必要があります。

> [!TIP]
> 続行する前に、AD ドメインコントローラーを再確認して、クラスターオブジェクトがすべての Dc にレプリケートされていることを確認してください。

PFX ベースの証明書を使用している場合は、HGS サーバーで次のコマンドを実行します。

```powershell
$signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
$encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

Install-ADServiceAccount -Identity 'HGSgMSA'

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustTpm
```

ローカルコンピューターにインストールされている証明書 (HSM ベースの証明書やエクスポートされていない証明書など) を使用している場合は、代わりに `-SigningCertificateThumbprint` と `-EncryptionCertificateThumbprint` のパラメーターを使用します。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [TPM ルート証明書のインストール](guarded-fabric-install-trusted-tpm-root-certificates.md)