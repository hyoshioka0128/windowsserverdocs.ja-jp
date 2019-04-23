---
title: 要塞フォレストの AD モードを使用して、HGS クラスターを初期化します。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 98003745823cf780a38487dff997798ebef12fc9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870093"
---
# <a name="initialize-the-hgs-cluster-using-ad-mode-in-an-existing-bastion-forest"></a>既存の要塞フォレストの AD モードを使用して、HGS クラスターを初期化します。

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)


>[!IMPORTANT]
>管理者によって信頼された構成証明 (AD モード) では、Windows Server 2019 以降推奨されていません。 TPM 構成証明が可能な環境では、次のように構成します。[ホスト キーの構成証明](guarded-fabric-initialize-hgs-key-mode-bastion.md)します。 ホスト キーの構成証明は、AD モードのような保証しを設定する方が簡単です。 

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

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -ClusterName 'HgsCluster' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustActiveDirectory
```

(証明書の HSM を基盤と証明書をエクスポートできない) など、ローカル コンピューターにインストールされている証明書を使用している場合は、使用、`-SigningCertificateThumbprint`と`-EncryptionCertificateThumbprint`パラメーター代わりにします。

## <a name="next-step"></a>次の手順

>[!div class="nextstepaction"]
[Fabric DNS を構成します。](guarded-fabric-configuring-fabric-dns-ad.md)

