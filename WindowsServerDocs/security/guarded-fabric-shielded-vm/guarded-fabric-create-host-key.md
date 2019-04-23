---
title: ホスト キーを作成し、HGS に追加します。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: a12c8494-388c-4523-8d70-df9400bbc2c0
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 82a561d51e9a396dcdc86ee3e37a8d7ffb8efd6e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870783"
---
# <a name="create-a-host-key-and-add-it-to-hgs"></a>ホスト キーを作成し、HGS に追加します。

>適用対象:Windows Server 2019


このトピックでは、ホスト キーの構成証明 (キー モード) を使用して保護されたホストに HYPER-V ホストを準備する方法について説明します。 ユーザー ホスト キー ペアを作成 (または既存の証明書を使用) をキーのパブリックの半分を HGS に追加します。

## <a name="create-a-host-key"></a>ホスト キーを作成します。

1.  HYPER-V ホスト コンピューターで Windows Server 2019 をインストールします。
2.  Hyper-v ホストと Host Guardian HYPER-V サポート機能をインストールします。

    ```powershell
    Install-WindowsFeature Hyper-V, HostGuardian -IncludeManagementTools -Restart
    ``` 

3.  ホスト キーを自動的に生成するか、既存の証明書を選択します。 カスタムの証明書を使用している場合、少なくとも 2048 ビット RSA キー、クライアント認証 EKU およびデジタル署名のキー使用法が必要です。

    ```powershell
    Set-HgsClientHostKey
    ```

    または、独自の証明書を使用する場合は、拇印を指定できます。 
    複数のコンピューター証明書を共有したり、TPM または HSM にバインドされている証明書を使用する場合に役立ちます。 ことができます。 次に、TPM バインド証明書 (秘密キーを盗まれ、別のコンピューターで使用できないし、TPM 1.2 のみが必要です) を作成する例を示します。

    ```powershell
    $tpmBoundCert = New-SelfSignedCertificate -Subject “Host Key Attestation ($env:computername)” -Provider “Microsoft Platform Crypto Provider”
    Set-HgsClientHostKey -Thumbprint $tpmBoundCert.Thumbprint
    ```

4.  HGS サーバーに提供するキーの半分の公開を取得します。 ことができます、次のコマンドレットを使用します、他の場所に格納されている証明書がある場合、パブリックを含む .cer 半分のキー。 私たちとのみを格納するが HGS; にある公開キーを検証することに注意してください。証明書情報を保持しないことも、私たちは証明書チェーンまたは有効期限の日付を検証します。

    ```powershell
    Get-HgsClientHostKey -Path "C:\temp\$env:hostname-HostKey.cer"
    ```

5.  HGS サーバーに、.cer ファイルをコピーします。

## <a name="add-the-host-key-to-the-attestation-service"></a>ホスト キー構成証明サービスを追加します。

この手順では、HGS サーバーでは行われ、ホストでシールドされた Vm を実行します。 FQDN に名前を設定するかに参照できるように簡単にするホストに、キー、ホスト コンピューターのリソース識別子がインストールされていることをお勧めします。

```powershell
Add-HgsAttestationHostKey -Name MyHost01 -Path "C:\temp\MyHost01-HostKey.cer"
``` 

## <a name="next-step"></a>次の手順

>[!div class="nextstepaction"]
[ホストが正常に証明できることを確認します。](guarded-fabric-confirm-hosts-can-attest-successfully.md)

## <a name="see-also"></a>関連項目

- [保護されたホストとシールドされた Vm のホスト ガーディアン サービスを展開します。](guarded-fabric-deploying-hgs-overview.md)
