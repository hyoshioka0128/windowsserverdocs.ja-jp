---
title: 仮想ネットワークの暗号化を構成します。
description: 仮想ネットワークの暗号化では、' 暗号化を有効にします ' としてマークされているサブネット内で互いと通信する仮想マシン間の仮想ネットワーク トラフィックの暗号化
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 378213f5-2d59-4c9b-9607-1fc83f8072f1
ms.author: pashort
author: shortpatti
ms.date: 08/08/2018
ms.openlocfilehash: 90fb33eb4c4b63fdd5c84bf3ffc2447fd52a809b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845493"
---
# <a name="configure-encryption-for-a-virtual-subnet"></a>仮想サブネット用の暗号化を構成します。

>適用対象:Windows Server

'暗号化を有効にします' としてマークされているサブネット内で互いと通信する Vm 間で仮想ネットワークのトラフィックの暗号化により、仮想ネットワークの暗号化 また、この機能は、仮想サブネットのデータグラム トランスポート層セキュリティ (DTLS) を利用して、パケットを暗号化します。 DTLS は、物理ネットワークへのアクセスを持つユーザーによる盗聴、改ざん、偽造に対する保護を提供します。

仮想ネットワークの暗号化が必要です。
- 各 SDN 対応の HYPER-V ホストにインストールされている暗号化証明書。
- その証明書の拇印を参照しているネットワーク コント ローラー内の資格情報オブジェクト。
- 各仮想ネットワークの構成には、暗号化が必要なサブネットが含まれます。

サブネット上の暗号化を有効にすると場合がありますも行われるアプリケーション レベルの暗号化に加えて、そのサブネット内のすべてのネットワーク トラフィックが自動的に暗号化されます。  暗号化された、としてマークされている場合でも、サブネット間を通過するトラフィックは、自動的に暗号化されていないに送信されます。 仮想ネットワークの境界を越える任意のトラフィックも送信される暗号化されていません。

>[!NOTE]
>ときに自動的に暗号化を取得、現在接続されている、または後のトラフィックで接続されているかどうか、同じサブネット上の別の VM と通信します。

>[!TIP]
>暗号化されたサブネット上でのみ通信するのにアプリケーションを制限する必要があります場合、アクセス制御リスト (Acl) を使用だけが、現在のサブネット内の通信を許可できます。 詳細については、次を参照してください。[使用へのアクセス制御リスト (Acl) を管理データ センター ネットワーク トラフィックのフローを](https://docs.microsoft.com/windows-server/networking/sdn/manage/use-acls-for-traffic-flow)します。


## <a name="step-1-create-the-encryption-certificate"></a>手順 1. 暗号化証明書を作成します。
各ホストには、暗号化証明書はインストールされている必要があります。 同じ証明書を使用して、すべてのテナントまたはテナントごとに一意の 1 つを生成できます。 

1.  証明書を生成します。  

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

スクリプトを実行した後、新しい証明書が表示されます、My ストア。

    PS D:\> dir cert:\\localmachine\my


    PSParentPath: Microsoft.PowerShell.Security\Certificate::localmachine\my

    Thumbprint                                Subject
    ----------                                -------
    84857CBBE7A1C851A80AE22391EB2C39BF820CE7  CN=MyNetwork
    5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks

2.  証明書をファイルにエクスポートします。<p>2 つのコピーと秘密キーとなしの証明書の必要があります。

    $subjectName = "EncryptedVirtualNetworks" $cert = Get-ChildItem cert:\localmachine\my | ? {$_.Subject -eq "CN=$subjectName"} [System.io.file]::WriteAllBytes("c:\$subjectName.pfx", $cert.Export("PFX", "secret")) Export-Certificate -Type CERT -FilePath "c:\$subjectName.cer" -cert $cert

3.  Hyper-v ホストの各証明書をインストールします。 

    PS c:\> dir c:\$subjectname.*


        Directory: C:\


    モード LastWriteTime 長さ名
    ----                -------------         ------ ----
    -a----        9/22/2017   4:54 PM            543 EncryptedVirtualNetworks.cer -a----        9/22/2017   4:54 PM           1706 EncryptedVirtualNetworks.pfx

4.  HYPER-V ホストにインストールします。

    $server = "Server01"

    $subjectname ="EncryptedVirtualNetworks"コピーの c:\$SubjectName.* \\$server\c$ 呼び出しコマンド-computername $server-argumentlist $subjectname、「シークレット」{param ([string] $SubjectName、[string] $Secret) $certFullPath ="c:\$SubjectName.cer"

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

5.  環境内の各サーバーについて繰り返します。<p>サーバーごとに繰り返し後、は、ルートと各 HYPER-V ホストの my ストアにインストールされている証明書が必要です。 

6.  証明書のインストールを確認します。<p>内容をチェックして、証明書を確認します。、、および証明書ストアのルート。

    PS c:\>入力 pssession Server1

    [Server1]:PS c:\> get-childitem cert://localmachine/my、cert://localmachine/root | か? {$_.Subject -eq "CN=EncryptedVirtualNetworks"}

    PSParentPath:Microsoft.PowerShell.Security\Certificate::localmachine\my

    拇印の件名
    ----------                                -------
    5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks


    PSParentPath:Microsoft.PowerShell.Security\Certificate::localmachine\root

    拇印の件名
    ----------                                -------
    5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6  CN=EncryptedVirtualNetworks

7.  拇印をメモしてをおきます。<p>ネットワーク コント ローラーで証明書の資格情報オブジェクトを作成する必要があるため、拇印をメモしてを行う必要があります。

## <a name="step-2-create-the-certificate-credential"></a>手順 2.  証明書資格情報を作成します。

ネットワーク コント ローラーに接続されている HYPER-V ホストの各証明書をインストールした後は、それを使用するネットワーク コント ローラーを構成する必要がありますようになりました。  これを行うには、インストールされているネットワーク コント ローラーの PowerShell モジュールをコンピューターから証明書の拇印を含む資格情報オブジェクトを作成する必要があります。 


    # Replace with thumbprint from your certificate
    $thumbprint = "5EFF2CE51EACA82408572A56AE1A9BCC7E0843C6"  
    
    # Replace with your Network Controller URI
    $uri = "https://nc.contoso.com"

    Import-module networkcontroller
    
    $credproperties = new-object Microsoft.Windows.NetworkController.CredentialProperties
    $credproperties.Type = "X509Certificate"
    $credproperties.Value = $thumbprint
    New-networkcontrollercredential -connectionuri $uri -resourceid "EncryptedNetworkCertificate" -properties $credproperties -force

>[!TIP]
>暗号化された仮想ネットワークはごとにこの資格情報を再利用できる、または展開して、各テナントの一意の証明書を使用することができます。


## <a name="step-3-configuring-a-virtual-network-for-encryption"></a>手順 3. 仮想ネットワークの暗号化の構成

この手順では、既に仮想ネットワーク名「マイ ネットワーク」を作成しているし、少なくとも 1 つの仮想サブネットが含まれている前提としています。  仮想ネットワークを作成する方法の詳細については、次を参照してください。 [Create、Delete、またはテナントの仮想ネットワークを更新](../Manage/Create,-Delete,-or-Update-Tenant-Virtual-Networks.md)します。

>[!NOTE]
>ときに自動的に暗号化を取得、現在接続されている、または後のトラフィックで接続されているかどうか、同じサブネット上の別の VM と通信します。

1.  ネットワーク コント ローラーから仮想ネットワークと資格情報オブジェクトを取得します。

    $vnet = Get-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId "MyNetwork" $certcred = Get-NetworkControllerCredential -ConnectionUri $uri -ResourceId "EncryptedNetworkCertificate"

2.  証明書資格情報への参照を追加し、個々 のサブネットでの暗号化を有効にします。

    $vnet.properties.EncryptionCredential = $certcred

    # <a name="replace-the-subnets-index-with-the-value-corresponding-to-the-subnet-you-want-encrypted"></a>サブネットのインデックスを暗号化サブネットに対応する値に置き換えます。  
    # <a name="repeat-for-each-subnet-where-encryption-is-needed"></a>暗号化が必要なサブネットごとに繰り返します
    $vnet.properties.Subnets[0].properties.EncryptionEnabled = $true

3.  ネットワーク コント ローラーに更新された仮想ネットワーク オブジェクトを配置します。

    New-NetworkControllerVirtualNetwork -ConnectionUri $uri -ResourceId $vnet.ResourceId -Properties $vnet.Properties -force


_**おめでとうございます!**_ 次の手順を完了すると完了します。 


## <a name="next-steps"></a>次のステップ



