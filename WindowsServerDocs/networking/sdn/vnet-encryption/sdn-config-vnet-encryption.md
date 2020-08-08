---
title: Virtual Network の暗号化を構成する
description: 仮想ネットワーク暗号化を使用すると、"暗号化が有効になっている" とマークされているサブネット内で相互に通信する仮想マシン間で仮想ネットワークトラフィックを暗号化できます。
manager: grcusanz
ms.topic: get-started-article
ms.assetid: 378213f5-2d59-4c9b-9607-1fc83f8072f1
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/08/2018
ms.openlocfilehash: 41bf68a18a05f97de4cff14651bf98bfa28bc33c
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87990136"
---
# <a name="configure-encryption-for-a-virtual-subnet"></a>仮想サブネットの暗号化の構成

>適用対象: Windows Server

仮想ネットワークの暗号化を使用すると、"暗号化が有効になっている" とマークされているサブネット内で相互に通信する Vm 間の仮想ネットワークトラフィックを暗号化できます。 また、この機能は、仮想サブネットのデータグラム トランスポート層セキュリティ (DTLS) を利用して、パケットを暗号化します。 DTLS は、物理ネットワークへのアクセスを持つユーザーによる盗聴、改ざん、偽造に対する保護を提供します。

仮想ネットワークの暗号化には次のものが必要です。
- SDN が有効になっている各 Hyper-v ホストにインストールされている暗号化証明書。
- ネットワークコントローラーの資格情報オブジェクト。この証明書の拇印を参照しています。
- 各仮想ネットワークの構成には、暗号化が必要なサブネットが含まれています。

サブネットで暗号化を有効にすると、そのサブネット内のすべてのネットワークトラフィックが自動的に暗号化されます。また、アプリケーションレベルの暗号化も行われることになります。  暗号化済みとしてマークされていても、サブネット間を通過するトラフィックは暗号化されずに自動的に送信されます。 仮想ネットワークの境界を越えるすべてのトラフィックも、暗号化されずに送信されます。

>[!NOTE]
>現在接続されているか接続されているかにかかわらず、同じサブネット上の別の VM と通信する場合、トラフィックは自動的に暗号化されます。

>[!TIP]
>暗号化されたサブネット上でのみアプリケーションを通信するように制限する必要がある場合は、現在のサブネット内での通信のみを許可するように Access Control リスト (Acl) のみを使用できます。 詳細については、「 [Access Control リスト (acl) を使用してデータセンターのネットワークトラフィックフローを管理する」を](../manage/use-acls-for-traffic-flow.md)参照してください。


## <a name="step-1-create-the-encryption-certificate"></a>手順 1. 暗号化証明書を作成する
各ホストには、暗号化証明書がインストールされている必要があります。 すべてのテナントに同じ証明書を使用することも、テナントごとに一意の証明書を生成することもできます。

1.  証明書を生成する

    ```
    $subjectName = "EncryptedVirtualNetworks"
    $cryptographicProviderName = "Microsoft Base Cryptographic Provider v1.0";
    [int] $privateKeyLength = 1024;
    $sslServerOidString = "1.3.6.1.5.5.7.3.1";
    $sslClientOidString = "1.3.6.1.5.5.7.3.2";
    [int] $validityPeriodInYear = 5;

    $name = new-object -com "X509Enrollment.CX500DistinguishedName.1"
    $name.Encode("CN=" + $SubjectName, 0)

    #Generate Key
    $key = new-object -com "X509Enrollment.CX509PrivateKey.1"
    $key.ProviderName = $cryptographicProviderName
    $key.KeySpec = 1 #X509KeySpec.XCN_AT_KEYEXCHANGE
    $key.Length = $privateKeyLength
    $key.MachineContext = 1
    $key.ExportPolicy = 0x2 #X509PrivateKeyExportFlags.XCN_NCRYPT_ALLOW_EXPORT_FLAG
    $key.Create()

    #Configure Eku
    $serverauthoid = new-object -com "X509Enrollment.CObjectId.1"
    $serverauthoid.InitializeFromValue($sslServerOidString)
    $clientauthoid = new-object -com "X509Enrollment.CObjectId.1"
    $clientauthoid.InitializeFromValue($sslClientOidString)
    $ekuoids = new-object -com "X509Enrollment.CObjectIds.1"
    $ekuoids.add($serverauthoid)
    $ekuoids.add($clientauthoid)
    $ekuext = new-object -com "X509Enrollment.CX509ExtensionEnhancedKeyUsage.1"
    $ekuext.InitializeEncode($ekuoids)

    # Set the hash algorithm to sha512 instead of the default sha1
    $hashAlgorithmObject = New-Object -ComObject X509Enrollment.CObjectId
    $hashAlgorithmObject.InitializeFromAlgorithmName( $ObjectIdGroupId.XCN_CRYPT_HASH_ALG_OID_GROUP_ID, $ObjectIdPublicKeyFlags.XCN_CRYPT_OID_INFO_PUBKEY_ANY, $AlgorithmFlags.AlgorithmFlagsNone, "SHA512")


    #Request Certificate
    $cert = new-object -com "X509Enrollment.CX509CertificateRequestCertificate.1"

    $cert.InitializeFromPrivateKey(2, $key, "")
    $cert.Subject = $name
    $cert.Issuer = $cert.Subject
    $cert.NotBefore = (get-date).ToUniversalTime()
    $cert.NotAfter = $cert.NotBefore.AddYears($validityPeriodInYear);
    $cert.X509Extensions.Add($ekuext)
    $cert.HashAlgorithm = $hashAlgorithmObject
    $cert.Encode()

    $enrollment = new-object -com "X509Enrollment.CX509Enrollment.1"
    $enrollment.InitializeFromRequest($cert)
    $certdata = $enrollment.CreateRequest(0)
    $enrollment.InstallResponse(2, $certdata, 0, "")
    ```

    スクリプトを実行すると、[マイストア] に新しい証明書が表示されます。

    ```
    PS D:\> dir cert:\\localmachine\my
    PSParentPath: Microsoft.PowerShell.Security\Certificate::localmachine\my

    Thumbprint                                Subject
    ----------                                -------
    84857CBBE7A1C851A80AE22391EB2C39BF820CE7  CN=MyNetwork
    5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks
    ```

1. 証明書をファイルにエクスポートします。<p>証明書には2つのコピーが必要です。1つは秘密キー、もう1つはありません。

    ```
   $subjectName = "EncryptedVirtualNetworks"
   $cert = Get-ChildItem cert:\localmachine\my | ? {$_.Subject -eq "CN=$subjectName"}
   [System.io.file]::WriteAllBytes("c:\$subjectName.pfx", $cert.Export("PFX", "secret"))
   Export-Certificate -Type CERT -FilePath "c:\$subjectName.cer" -cert $cert
    ```

3. 各 hyper-v ホストに証明書をインストールする

    ```
    PS C:\> dir c:\$subjectname.*

    Directory: C:\

    Mode                LastWriteTime         Length Name
    ----                -------------         ------ ----
    -a----        9/22/2017   4:54 PM            543 EncryptedVirtualNetworks.cer
    -a----        9/22/2017   4:54 PM           1706 EncryptedVirtualNetworks.pfx
    ```

1. Hyper-v ホストへののインストール

    ```
    $server = "Server01"

    $subjectname = "EncryptedVirtualNetworks"
    copy c:\$SubjectName.* \\$server\c$
    invoke-command -computername $server -ArgumentList $subjectname,"secret" {
        param (
            [string] $SubjectName,
            [string] $Secret
        )
        $certFullPath = "c:\$SubjectName.cer"

        # create a representation of the certificate file
        $certificate = new-object System.Security.Cryptography.X509Certificates.X509Certificate2
        $certificate.import($certFullPath)

        # import into the store
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("Root", "LocalMachine")
        $store.open("MaxAllowed")
        $store.add($certificate)
        $store.close()

        $certFullPath = "c:\$SubjectName.pfx"
        $certificate = new-object System.Security.Cryptography.X509Certificates.X509Certificate2
        $certificate.import($certFullPath, $Secret, "MachineKeySet,PersistKeySet")

        # import into the store
        $store = new-object System.Security.Cryptography.X509Certificates.X509Store("My", "LocalMachine")
        $store.open("MaxAllowed")
        $store.add($certificate)
        $store.close()

        # Important: Remove the certificate files when finished
        remove-item C:\$SubjectName.cer
        remove-item C:\$SubjectName.pfx
    }
    ```

5. 環境内の各サーバーに対して、この手順を繰り返します。<p>各サーバーに対してを繰り返した後、各 Hyper-v ホストのルートとマイストアに証明書がインストールされている必要があります。

6. 証明書がインストールされていることを確認します。<p>My および Root 証明書ストアの内容を確認して、証明書を確認します。

    ```
    PS C:\> enter-pssession Server1

    [Server1]: PS C:\> get-childitem cert://localmachine/my,cert://localmachine/root | ? {$_.Subject -eq "CN=EncryptedVirtualNetworks"}

    PSParentPath: Microsoft.PowerShell.Security\Certificate::localmachine\my

    Thumbprint                                Subject
    ----------                                -------
    5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks

    PSParentPath: Microsoft.PowerShell.Security\Certificate::localmachine\root

    Thumbprint                                Subject
    ----------                                -------
    5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks
    ```

7. サムプリントをメモしておきます。<p>ネットワークコントローラーに証明書資格情報オブジェクトを作成するために必要なため、拇印を書き留めておく必要があります。

## <a name="step-2-create-the-certificate-credential"></a>手順 2. 証明書の資格情報を作成する

ネットワークコントローラーに接続されている各 Hyper-v ホストに証明書をインストールしたら、それを使用するようにネットワークコントローラーを構成する必要があります。  これを行うには、ネットワークコントローラーの PowerShell モジュールがインストールされているコンピューターから、証明書の拇印を含む資格情報オブジェクトを作成する必要があります。

```
///Replace with the thumbprint from your certificate
$thumbprint = "5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6"

$uri = "https://nc.contoso.com"

///Replace with your Network Controller URI
Import-module networkcontroller

$credproperties = new-object Microsoft.Windows.NetworkController.CredentialProperties
$credproperties.Type = "X509Certificate"
$credproperties.Value = $thumbprint
New-networkcontrollercredential -connectionuri $uri -resourceid "EncryptedNetworkCertificate" -properties $credproperties -force
```

> [!TIP]
> 暗号化された仮想ネットワークごとにこの資格情報を再利用できます。また、テナントごとに一意の証明書を展開して使用することもできます。

## <a name="step-3-configuring-a-virtual-network-for-encryption"></a>手順 3. 暗号化のための Virtual Network の構成

この手順では、仮想ネットワーク名 "My Network" が既に作成されており、仮想サブネットが少なくとも1つ含まれていることを前提としています。  仮想ネットワークの作成の詳細については、「[テナント仮想ネットワークの作成、削除、または更新](../Manage/Create,-Delete,-or-Update-Tenant-Virtual-Networks.md)」を参照してください。

>[!NOTE]
>現在接続されているか接続されているかにかかわらず、同じサブネット上の別の VM と通信する場合、トラフィックは自動的に暗号化されます。

1.  ネットワークコントローラーから Virtual Network および資格情報オブジェクトを取得します。

    ```
    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "MyNetwork"
    $certcred = Get-NetworkControllerCredential -ConnectionUri $uri -ResourceId "EncryptedNetworkCertificate"
    ```

2.  証明書資格情報への参照を追加し、個々のサブネットでの暗号化を有効にします。

    ```
    $vnet.properties.EncryptionCredential = $certcred

    # Replace the Subnets index with the value corresponding to the subnet you want encrypted.
    # Repeat for each subnet where encryption is needed
    $vnet.properties.Subnets[0].properties.EncryptionEnabled = $true
    ```

3.  更新された Virtual Network オブジェクトをネットワークコントローラーに配置します。

    ```
    New-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId $vnet.ResourceId -Properties $vnet.Properties -force
    ```

*おめでとうございました。** これらの手順を完了したら、次の手順を実行します。