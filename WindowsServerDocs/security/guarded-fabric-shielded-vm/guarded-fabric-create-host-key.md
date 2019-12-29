---
title: ホストキーを作成して HGS に追加する
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: a12c8494-388c-4523-8d70-df9400bbc2c0
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 2aea6c8416a0f3af04ad6056c5d09a4d07708eaa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386646"
---
# <a name="create-a-host-key-and-add-it-to-hgs"></a>ホストキーを作成して HGS に追加する

>適用対象:Windows Server 2019


このトピックでは、ホストキーの構成証明 (キーモード) を使用して、保護されたホストになるように Hyper-v ホストを準備する方法について説明します。 ホストキーペアを作成し (または既存の証明書を使用して)、キーの公開半分を HGS に追加します。

## <a name="create-a-host-key"></a>ホストキーを作成する

1.  Hyper-v ホストコンピューターに Windows Server 2019 をインストールします。
2.  Hyper-v および Host Guardian Hyper-v サポート機能をインストールします。

    ```powershell
    Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
    ``` 

3.  ホストキーを自動的に生成するか、既存の証明書を選択します。 カスタム証明書を使用している場合は、少なくとも2048ビットの RSA キー、クライアント認証 EKU、およびデジタル署名キーの使用が必要です。

    ```powershell
    Set-HgsClientHostKey
    ```

    また、独自の証明書を使用する場合は、拇印を指定することもできます。 
    これは、複数のコンピューターで証明書を共有する場合や、TPM または HSM にバインドされた証明書を使用する場合に便利です。 次に、TPM バインド証明書を作成する例を示します。これにより、秘密キーが盗まれて別のコンピューターで使用され、TPM 1.2 のみが必要になります。

    ```powershell
    $tpmBoundCert = New-SelfSignedCertificate -Subject “Host Key Attestation ($env:computername)” -Provider “Microsoft Platform Crypto Provider”
    Set-HgsClientHostKey -Thumbprint $tpmBoundCert.Thumbprint
    ```

4.  HGS サーバーに提供するキーの公開半分を取得します。 次のコマンドレットを使用するか、証明書が別の場所に格納されている場合は、キーの公開半分を含む .cer を指定します。 HGS では公開キーの保存と検証のみを行っていることに注意してください。証明書の情報は保持されず、証明書チェーンや有効期限も検証されません。

    ```powershell
    Get-HgsClientHostKey -Path "C:\temp\$env:hostname-HostKey.cer"
    ```

5.  .Cer ファイルを HGS サーバーにコピーします。

## <a name="add-the-host-key-to-the-attestation-service"></a>構成証明サービスにホストキーを追加する

この手順は、HGS サーバーで実行され、ホストがシールドされた Vm を実行できるようにします。 名前はホストコンピューターの FQDN またはリソース識別子に設定することをお勧めします。これにより、キーがインストールされているホストを簡単に参照できるようになります。

```powershell
Add-HgsAttestationHostKey -Name MyHost01 -Path "C:\temp\MyHost01-HostKey.cer"
``` 

## <a name="next-step"></a>次の手順

> [!div class="nextstepaction"]
> [ホストが正常に証明できることを確認する](guarded-fabric-confirm-hosts-can-attest-successfully.md)

## <a name="see-also"></a>関連項目

- [保護されたホストとシールドされた Vm のホストガーディアンサービスの展開](guarded-fabric-deploying-hgs-overview.md)
