---
title: 仮想ネットワークの暗号化を構成します。
description: このトピックの「仮想ネットワーク暗号化に Windows Server でネットワーク定義ソフトウェア情報を提供します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 378213f5-2d59-4c9b-9607-1fc83f8072f1
ms.author: pashort
author: grcusanz
ms.openlocfilehash: 7d1de535e7758793e5ddaa7eeefada0aa55d3328
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="configure-encryption-for-a-virtual-subnet"></a>仮想サブネット用の暗号化を構成します。

>Windows Server の適用対象:

このトピックには、仮想ネットワーク上の暗号化を有効にするための手順を説明する次のセクションが含まれています。

- [暗号化証明書を作成します。](#bkmk_Certificate)
- [証明書資格情報の作成](#bkmk_credential)
- [暗号化用の仮想ネットワークを構成します。](#bkmk_vnet)

## <a name="bkmk_Certificate"></a>暗号化証明書を作成します。
暗号化証明書は、暗号化が使用される各ホストにインストールする必要があります。  すべてのテナントでは、同じ証明書を使用したり、必要な場合に、一意の証明書テナントごとを生成できます。

手順 1: 証明書を生成します。

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

上記を実行した後で、新しい証明書が表示されます、スクリプトを実行するコンピューターの My ストア。

    PS D:\> dir cert:\\localmachine\my


    PSParentPath: Microsoft.PowerShell.Security\Certificate::localmachine\my

    Thumbprint                                Subject
    ----------                                -------
    84857CBBE7A1C851A80AE22391EB2C39BF820CE7  CN=MyNetwork
    5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks

手順 2: は、2 つのコピーと秘密キーとなしの証明書の必要がありますファイルに証明書をエクスポートします。

    $subjectName = "EncryptedVirtualNetworks"
    $cert = Get-ChildItem cert:\localmachine\my | ? {$_.Subject -eq "CN=$subjectName"}
    [System.io.file]::WriteAllBytes("c:\$subjectName.pfx", $cert.Export("PFX", "secret"))
    Export-Certificate -Type CERT -FilePath "c:\$subjectName.cer" -cert $cert

上記の実行後に 2 つの証明書ファイルが表示されます。  これらは、hyper-v ホスト用のそれぞれにインストールする必要があります。

    PS C:\> dir c:\$subjectname.*


        Directory: C:\


    Mode                LastWriteTime         Length Name
    ----                -------------         ------ ----
    -a----        9/22/2017   4:54 PM            543 EncryptedVirtualNetworks.cer
    -a----        9/22/2017   4:54 PM           1706 EncryptedVirtualNetworks.pfx

手順 3: Hyper-V ホストにインストールします。

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
        $certificate.import($certFullPath){$_}

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

        # Important: Remove the certficate files when finished
        remove-item C:\$SubjectName.cer
        remove-item C:\$SubjectName.pfx
    }    

環境内では、各サーバーについて繰り返します。  ルートと各 Hyper-V ホストの my ストアにインストールされている証明書が作成されました

内容を確認して、証明書のインストールを確認することができます、My 証明書と証明書ストアのルートします。

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

必要があるため、ネットワーク コントローラーに証明書資格情報オブジェクトを作成するため、拇印を書き留めておきます。

## <a name="bkmk_Certificate"></a>証明書資格情報の作成

各ネットワーク コントローラーに接続されている Hyper-V ホストに、証明書のインストールが完了した後は、それを使用するネットワーク コントローラーを構成できます。

証明書の拇印を含む資格情報オブジェクトを作成する必要があります。  これを行うコンピューターからインストールされているネットワーク コントローラーの powershell モジュールがある必要があります。

    # Replace with thumbprint from your certificate
    $thumbprint = "5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6"  
    
    # Replace with your Network Controller URI
    $uri = "https://nc.contoso.com"

    Import-module networkcontroller
    
    $credproperties = new-object Microsoft.Windows.NetworkController.CredentialProperties
    $credproperties.Type = "X509Certificate"
    $credproperties.Value = $thumbprint
    New-networkcontrollercredential -connectionuri $uri -resourceid "EncryptedNetworkCertificate" -properties $credproperties -force

各暗号化された仮想 netwokr のこの資格情報を再利用することができます、または展開して、テナントごとに一意の証明書を使用することができます。

## <a name="bkmk_Certificate"></a>暗号化用の仮想ネットワークを構成します。

この手順は、仮想ネットワーク名「マイ ネットワーク」を既に作成しているし、少なくとも 1 つの仮想サブネットが含まれていると仮定します。  仮想ネットワークを作成する方法の詳細については、次を参照してください。[作成、削除、または更新プログラムのテナント仮想ネットワーク](../Manage/Create,-Delete,-or-Update-Tenant-Virtual-Networks.md)します。

手順 1: ネットワーク コントローラーから、仮想ネットワークおよび資格情報オブジェクトを取得します。

    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "MyNetwork"
    $certcred = Get-NetworkControllerCredential -ConnectionUri $uri -ResourceId "EncryptedNetworkCertificate"

手順 2: は、証明書資格情報への参照を追加し、個別のサブネット上の暗号化を有効にします。

    $vnet.properties.EncryptionCredential = $certcred

    # Replace the Subnets index with the value corresponding to the subnet you want encrypted.  
    # Repeat for each subnet where encryption is needed
    $vnet.properties.Subnets[0].properties.EncryptionEnabled = $true

手順 3: ネットワーク コントローラーに更新された仮想ネットワーク オブジェクトを格納します。

    New-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId $vnet.ResourceId -Properties $vnet.Properties -force

この処理が完了したら、追加の手順は必要ありません。  現在接続されているすべての VM と、上記のサブネットに後で接続されている任意の VM のトラフィックが、同じサブネット上の別のバーチャル マシンと通信するときに自動的に暗号化があります。


