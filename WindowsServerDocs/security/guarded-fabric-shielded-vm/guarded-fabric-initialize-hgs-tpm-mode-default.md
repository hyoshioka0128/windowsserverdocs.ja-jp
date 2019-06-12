---
title: TPM のモードを使用して、新しい専用フォレスト (既定値) での HGS クラスターを初期化します。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: f2fb970cdc215df06dd9dee2e20b5466d7e42dcb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447412"
---
# <a name="initialize-the-hgs-cluster-using-tpm-mode-in-a-new-dedicated-forest-default"></a>TPM のモードを使用して、新しい専用フォレスト (既定値) での HGS クラスターを初期化します。

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

1.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-one.md)]

2.  [!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)]

3.  実行[Initialize HgsServer](https://technet.microsoft.com/library/mt652185.aspx) HGS の最初のノード上の管理者特権で PowerShell ウィンドウでします。 このコマンドレットの構文は、多くの異なる入力をサポートしていますが、2 つの最も一般的な呼び出しを次に。

    -   署名と暗号化証明書を PFX ファイルを使用している場合は、次のコマンドを実行します。

        ```powershell
        $signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
        $encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signingCertPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustTpm
        ```

    -   ローカル証明書ストアにインストールされているエクスポートできない証明書を使用している場合は、次のコマンドを実行します。 実行して利用できる証明書を一覧表示には、証明書の拇印がわからない場合`Get-ChildItem Cert:\LocalMachine\My`します。

        ```powershell
        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificateThumbprint '1A2B3C4D5E6F...' -EncryptionCertificateThumbprint '0F9E8D7C6B5A...' -TrustTpm
        ```

4.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-four.md)]

5.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-five.md)]

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [TPM ルート証明書のインストール](guarded-fabric-install-trusted-tpm-root-certificates.md)
  