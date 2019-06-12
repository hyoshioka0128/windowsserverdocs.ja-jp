---
title: 要塞フォレスト内のキーのモードを使用して、HGS クラスターを初期化します。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: e785ee17bf68c07d965816480baa0d59062fc434
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447423"
---
# <a name="initialize-the-hgs-cluster-using-key-mode-in-an-existing-bastion-forest"></a>キーのモードを使用して、既存の要塞フォレストの HGS クラスターを初期化します。

> 適用対象:Windows Server 2019
> 
> [!div class="step-by-step"]
> [«HGS を新しいフォレストのインストール](guarded-fabric-install-hgs-in-a-bastion-forest.md)
> [ホスト キーの作成»](guarded-fabric-create-host-key.md)

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

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -ClusterName 'HgsCluster' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustHostKey
```

(証明書の HSM を基盤と証明書をエクスポートできない) など、ローカル コンピューターにインストールされている証明書を使用している場合は、使用、`-SigningCertificateThumbprint`と`-EncryptionCertificateThumbprint`パラメーター代わりにします。

