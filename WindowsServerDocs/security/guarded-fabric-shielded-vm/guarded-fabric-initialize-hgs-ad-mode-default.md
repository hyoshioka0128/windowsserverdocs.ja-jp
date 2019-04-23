---
title: AD モードを使用して、新しい専用フォレスト (既定値) での HGS クラスターを初期化します。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 4ef70ab9ce8150a9a3ed774d6df407da097880e9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59865673"
---
# <a name="initialize-the-hgs-cluster-using-ad-mode-in-a-new-dedicated-forest-default"></a>AD モードを使用して、新しい専用フォレスト (既定値) での HGS クラスターを初期化します。

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

>[!IMPORTANT]
>管理者によって信頼された構成証明 (AD モード) では、Windows Server 2019 以降推奨されていません。 TPM 構成証明が可能な環境では、次のように構成します。[ホスト キーの構成証明](guarded-fabric-initialize-hgs-key-mode-default.md)します。 ホスト キーの構成証明は、AD モードのような保証しを設定する方が簡単です。 

1.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-one.md)] 
2.  [!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)]

3.  実行[Initialize HgsServer](https://technet.microsoft.com/library/mt652185.aspx) HGS の最初のノード上の管理者特権で PowerShell ウィンドウでします。 このコマンドレットの構文は、多くの異なる入力をサポートしていますが、2 つの最も一般的な呼び出しを次に。

    -   署名と暗号化証明書を PFX ファイルを使用している場合は、次のコマンドを実行します。

        ```powershell
        $signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
        $encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signingCertPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustActiveDirectory
        ```

    -   ローカル証明書ストアにインストールされているエクスポートできない証明書を使用している場合は、次のコマンドを実行します。 実行して利用できる証明書を一覧表示には、証明書の拇印がわからない場合`Get-ChildItem Cert:\LocalMachine\My`します。

        ```powershell
        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificateThumbprint '1A2B3C4D5E6F...' -EncryptionCertificateThumbprint '0F9E8D7C6B5A...' --TrustActiveDirectory
        ```

4.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-four.md)]  

5.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-five.md)]

## <a name="next-step"></a>次の手順

>[!div class="nextstepaction"]
[Fabric DNS を構成します。](guarded-fabric-configuring-fabric-dns-ad.md)