---
title: 新しい専用フォレストでキーモードを使用して HGS クラスターを初期化する (既定)
ms.prod: windows-server
ms.topic: article
manager: dongill
author: rpsqrd
ms.author: ryanpu
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: feae5230eec6b3f3c0471f75199970a47016a583
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856665"
---
# <a name="initialize-the-hgs-cluster-using-key-mode-in-a-new-dedicated-forest-default"></a>新しい専用フォレストでキーモードを使用して HGS クラスターを初期化する (既定)

>適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016


1.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-one.md)] 
2.  [!INCLUDE [Obtain certificates for HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-two.md)]

3.  最初の HGS ノードで、管理者特権の PowerShell ウィンドウで[HgsServer](https://technet.microsoft.com/library/mt652185.aspx)を実行します。 このコマンドレットの構文では、多くの異なる入力がサポートされていますが、最も一般的な2つの呼び出しは次のとおりです。

    -   署名証明書と暗号化証明書に PFX ファイルを使用している場合は、次のコマンドを実行します。

        ```powershell
        $signingCertPass = Read-Host -AsSecureString -Prompt "Signing certificate password"
        $encryptionCertPass = Read-Host -AsSecureString -Prompt "Encryption certificate password"

        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificatePath '.\signCert.pfx' -SigningCertificatePassword $signingCertPass -EncryptionCertificatePath '.\encCert.pfx' -EncryptionCertificatePassword $encryptionCertPass -TrustHostkey
        ```

    -   ローカル証明書ストアにインストールされているエクスポートできない証明書を使用している場合は、次のコマンドを実行します。 証明書の拇印がわからない場合は、`Get-ChildItem Cert:\LocalMachine\My`を実行して、使用可能な証明書を一覧表示できます。

        ```powershell
        Initialize-HgsServer -HgsServiceName 'MyHgsDNN' -SigningCertificateThumbprint '1A2B3C4D5E6F...' -EncryptionCertificateThumbprint '0F9E8D7C6B5A...' --TrustHostKey
        ```

4.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-four.md)]  

5.  [!INCLUDE [Initialize HGS](../../../includes/guarded-fabric-initialize-hgs-default-step-five.md)]


## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ホストキーの作成](guarded-fabric-create-host-key.md)