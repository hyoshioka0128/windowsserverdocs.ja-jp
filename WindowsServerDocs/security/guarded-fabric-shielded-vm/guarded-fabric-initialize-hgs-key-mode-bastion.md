---
title: 要塞フォレストでキーモードを使用して HGS クラスターを初期化する
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.date: 08/29/2018
ms.openlocfilehash: b526895f9b9e819523ee459701c2f09988565544
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87965999"
---
# <a name="initialize-the-hgs-cluster-using-key-mode-in-an-existing-bastion-forest"></a>既存の要塞フォレストでキーモードを使用して HGS クラスターを初期化する

> 適用対象:Windows Server 2019
>
> [!div class="step-by-step"]
> [«新しいフォレスト](guarded-fabric-install-hgs-in-a-bastion-forest.md) 
>  に HGS をインストールする[ホストキーの作成»](guarded-fabric-create-host-key.md)

Active Directory Domain Services はコンピューターにインストールされますが、未構成のままにしておく必要があります。

[!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)]

続行する前に、ホストガーディアンサービスのクラスターオブジェクトを事前設定し、Active Directory の VCO および CNO オブジェクトに対して、ログインしているユーザーに**フルコントロール**を付与したことを確認してください。
仮想コンピューターのオブジェクト名は、パラメーターに、クラスター名をパラメーターに渡す必要があり `-HgsServiceName` `-ClusterName` ます。

> [!TIP]
> 続行する前に、AD ドメインコントローラーを再確認して、クラスターオブジェクトがすべての Dc にレプリケートされていることを確認してください。

PFX ベースの証明書を使用している場合は、HGS サーバーで次のコマンドを実行します。

```powershell
$signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
$encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

Install-ADServiceAccount -Identity 'HGSgMSA'

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -ClusterName 'HgsCluster' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustHostKey
```

ローカルコンピューターにインストールされている証明書 (HSM ベースの証明書やエクスポートできない証明書など) を使用している場合は、 `-SigningCertificateThumbprint` 代わりにパラメーターとパラメーターを使用し `-EncryptionCertificateThumbprint` ます。

