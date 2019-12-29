---
title: 要塞フォレストでキーモードを使用して HGS クラスターを初期化する
ms.custom: na
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: e72de1c85e0a9c3decf1fd3b5085363b57ca387c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403633"
---
# <a name="initialize-the-hgs-cluster-using-key-mode-in-an-existing-bastion-forest"></a>既存の要塞フォレストでキーモードを使用して HGS クラスターを初期化する

> 適用対象: Windows Server 2019
> 
> [!div class="step-by-step"]
> [«新しいフォレストに HGS をインストール](guarded-fabric-install-hgs-in-a-bastion-forest.md)
> [ホストキーの作成»](guarded-fabric-create-host-key.md)

Active Directory Domain Services はコンピューターにインストールされますが、未構成のままにしておく必要があります。

[!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)] 

続行する前に、ホストガーディアンサービスのクラスターオブジェクトを事前設定し、Active Directory の VCO および CNO オブジェクトに対して、ログインしているユーザーに**フルコントロール**を付与したことを確認してください。
仮想コンピューターのオブジェクト名は `-HgsServiceName` パラメーターに、クラスター名を `-ClusterName` パラメーターに渡す必要があります。

> [!TIP]
> 続行する前に、AD ドメインコントローラーを再確認して、クラスターオブジェクトがすべての Dc にレプリケートされていることを確認してください。

PFX ベースの証明書を使用している場合は、HGS サーバーで次のコマンドを実行します。

```powershell
$signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
$encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

Install-ADServiceAccount -Identity 'HGSgMSA'

Initialize-HgsServer -UseExistingDomain -ServiceAccount 'HGSgMSA' -JeaReviewersGroup 'HgsJeaReviewers' -JeaAdministratorsGroup 'HgsJeaAdmins' -HgsServiceName 'HgsService' -ClusterName 'HgsCluster' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustHostKey
```

ローカルコンピューターにインストールされている証明書 (HSM ベースの証明書やエクスポートされていない証明書など) を使用している場合は、代わりに `-SigningCertificateThumbprint` パラメーターと `-EncryptionCertificateThumbprint` パラメーターを使用します。

