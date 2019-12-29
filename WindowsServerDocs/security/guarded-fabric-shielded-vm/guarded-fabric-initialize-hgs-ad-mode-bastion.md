---
title: 要塞フォレストで AD モードを使用して HGS クラスターを初期化する
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: c69561f7d17bb1d36d90fc66cf4c1a196072fc72
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402370"
---
# <a name="initialize-the-hgs-cluster-using-ad-mode-in-an-existing-bastion-forest"></a>既存の要塞フォレストの AD モードを使用して HGS クラスターを初期化する

>適用対象:Windows Server (半期チャネル)、Windows Server 2016


>[!IMPORTANT]
>管理者によって信頼された構成証明 (AD モード) は、Windows Server 2019 以降では非推奨とされます。 TPM の構成証明が不可能な環境では、[ホストキー](guarded-fabric-initialize-hgs-key-mode-bastion.md)の構成証明を構成します。 ホストキーの構成証明により、AD モードと同様の保証が提供され、セットアップが簡単になります。 

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

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -ClusterName 'HgsCluster' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustActiveDirectory
```

ローカルコンピューターにインストールされている証明書 (HSM ベースの証明書やエクスポートされていない証明書など) を使用している場合は、代わりに `-SigningCertificateThumbprint` と `-EncryptionCertificateThumbprint` のパラメーターを使用します。

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ファブリック DNS の構成](guarded-fabric-configuring-fabric-dns-ad.md)

