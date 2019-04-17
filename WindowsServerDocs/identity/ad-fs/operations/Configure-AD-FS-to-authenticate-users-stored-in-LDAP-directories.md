---
ms.assetid: e863ab80-4e4c-48d3-bdaa-31815ef36bae
title: "LDAP ディレクトリに格納されているユーザーの認証に AD FS を構成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 05f8b8991e664a84c3f2b3200de4068af8d1476a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/03/2017
---
# <a name="configure-ad-fs-to-authenticate-users-stored-in-ldap-directories"></a>LDAP ディレクトリに格納されているユーザーの認証に AD FS を構成します。

>Windows Server 2016 の適用対象:

次のトピックでは、id が、ライトウェイト ディレクトリ アクセス プロトコル (LDAP) v3 に準拠したディレクトリに格納されているユーザーの認証に、AD FS インフラストラクチャを有効にするために必要な構成について説明します。

多くの組織で、id 管理ソリューションは、Active Directory、AD lds において、またはサード パーティ LDAP ディレクトリの組み合わせで構成されます。 LDAP v3 に準拠したディレクトリに格納されているユーザーを認証するための AD FS サポートの追加により、メリットが得られる全体のエンタープライズ レベルから AD FS 機能により、ユーザー ID の格納場所に関係なく。 AD FS には、任意の LDAP v3 に準拠したディレクトリがサポートしています。

> [!NOTE]
> AD FS 機能の一部は、シングル サインオン (SSO)、デバイス認証、柔軟な条件付きアクセス ポリシー、サポートを作業-から-任意の場所から Web アプリケーション プロキシとの統合とシームレスなフェデレーションで有効にする Azure AD を有効にして、ユーザーが Office 365 やその他の SaaS アプリケーションなど、クラウドを利用します。  詳細については、次を参照してください。[Active Directory フェデレーション サービスの概要](../../ad-fs/AD-FS-2016-Overview.md)します。

AD FS LDAP ディレクトリからユーザーを認証するためには、必要がありますに接続するこの LDAP ディレクトリ、AD FS ファームを作成して、**ローカル要求プロバイダー信頼**します。  ローカルの要求プロバイダー信頼とは、LDAP ディレクトリの AD FS ファームを表す信頼オブジェクトです。 ローカルの要求プロバイダー信頼オブジェクトは、各種の id、名前、およびローカルのフェデレーション サービスに対してこの LDAP ディレクトリを識別する規則で構成されています。

それぞれが複数追加することで、同じ AD FS ファーム内の独自の構成を持つ複数の LDAP ディレクトリをサポートする**ローカル要求プロバイダー信頼**します。 さらに、AD FS 内に存在するフォレストによって信頼されていない AD DS フォレストは、ローカルの要求プロバイダー信頼とモデルにも化ことができます。 ローカルの要求プロバイダー信頼を作成するには、Windows PowerShell を使用します。

LDAP ディレクトリ (ローカルの要求プロバイダー信頼) と共存できます AD ディレクトリ (要求プロバイダー信頼) 同じ AD FS ファーム内の同じ AD FS サーバーで、そのため、AD FS の単一のインスタンスは認証および承認の両方に格納されているユーザーのアクセス可能な AD と非 AD ディレクトリ。

LDAP ディレクトリからユーザーの認証はフォーム ベース認証のみサポートされます。 LDAP ディレクトリにユーザーの認証には、証明書ベース認証統合 Windows 認証はサポートされていません。

すべての承認のパッシブ プロトコル、Ws-federation、SAML を含む、AD FS によってサポートされていると、OAuth が LDAP ディレクトリに保存されている ID もサポートされています。

Ws-trust active 認証プロトコルは LDAP ディレクトリに保存されている ID もサポートされます。

## <a name="configure-ad-fs-to-authenticate-users-stored-in-an-ldap-directory"></a>LDAP ディレクトリに格納されているユーザーの認証に AD FS を構成します。
LDAP ディレクトリからユーザーを認証する AD FS ファームを構成するのには、次の手順を実行することができます。

1.  最初に、LDAP ディレクトリを使用してへの接続を構成する、**新規 AdfsLdapServerConnection**コマンドレット。

    ```
    $DirectoryCred = Get-Credential
    $vendorDirectory = New-AdfsLdapServerConnection -HostName dirserver -Port 50000 -SslMode None -AuthenticationMethod Basic -Credential $DirectoryCred
    ```

    > [!NOTE]
    > 各 LDAP サーバーに接続するための新しい接続オブジェクトを作成することをお勧めします。 AD FS では、複数のレプリカの LDAP サーバーに接続でき、自動的にフェールオーバーする場合に、特定の LDAP サーバーがダウンすることができます。 このような場合には、これらの各レプリカ LDAP サーバーの 1 つ AdfsLdapServerConnection を作成しを使用して接続オブジェクトの配列を追加することができます、**LdapServerConnection**のパラメーター、**追加 AdfsLocalClaimsProviderTrust**コマンドレット。

    **注:**ために、LDAP インスタンスにバインドするために使用する識別名とパスワードを入力して Get-Credential を使用しようとするがエラーになる可能性があります、特定の入力形式、たとえば、ドメイン \ ユーザー名のユーザー インターフェイスの要件のまたはuser@domain.tldします。 次のように代わりに、ConvertTo-SecureString コマンドレットを使用できます (次の例は、uid を想定しています。管理者は、ou = LDAP インスタンスにバインドするために使用する資格情報の DN としてシステムを =)。

    ```
    $ldapuser = ConvertTo-SecureString -string "uid=admin,ou=system" -asplaintext -force
    $DirectoryCred = Get-Credential -username $ldapuser -Message "Enter the credentials to bind to the LDAP instance:"
    ```

    Uid のパスワードを入力し、管理者 = し、残りの手順を完了します。

2.  次に、オプションの手順を使用して既存の AD FS の要求への LDAP 属性のマッピングを行うことができます、**新規 AdfsLdapAttributeToClaimMapping**コマンドレット。 次の例では、givenName、姓のマップし、は AD FS の要求に CommonName LDAP 属性を使用します。

    ```
    #Map given name claim
    $GivenName = New-AdfsLdapAttributeToClaimMapping -LdapAttribute givenName -ClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname"
    # Map surname claim
    $Surname = New-AdfsLdapAttributeToClaimMapping -LdapAttribute sn -ClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname"
    # Map common name claim
    $CommonName = New-AdfsLdapAttributeToClaimMapping -LdapAttribute cn -ClaimType "http://schemas.xmlsoap.org/claims/CommonName"
    ```

    このマッピングは、AD FS での条件付きアクセス制御のルールを作成するために AD FS の要求として利用可能な LDAP ストアから属性を作成するために行われます。 AD FS の信頼性情報を LDAP 属性をマップする簡単な方法を提供することで、LDAP ストア内のカスタムのスキーマを使用することもできます。

3.  最後に、必要がありますを登録する LDAP ストア AD FS とローカルの要求プロバイダー信頼を使用すると、**追加 AdfsLocalClaimsProviderTrust**コマンドレット。

    ```
    Add-AdfsLocalClaimsProviderTrust -Name "Vendors" -Identifier "urn:vendors" -Type Ldap

    # Connection info
    -LdapServerConnection $vendorDirectory 

    # How to locate user objects in directory
    -UserObjectClass inetOrgPerson -UserContainer "CN=VendorsContainer,CN=VendorsPartition" -LdapAuthenticationMethod Basic 

    # Claims for authenticated users
    -AnchorClaimLdapAttribute mail -AnchorClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn" -LdapAttributeToClaimMapping @($GivenName, $Surname, $CommonName) 

    # General claims provider properties
    -AcceptanceTransformRules "c:[Type != ''] => issue(claim=c);" -Enabled $true 

    # Optional - supply user name suffix if you want to use Ws-Trust
    -OrganizationalAccountSuffix "vendors.contoso.com"

    ```

    上記の例では、「ベンダー」と呼ばれる、ローカルの要求プロバイダー信頼を作成します。 指定した LDAP ディレクトリに接続するための AD FS の接続情報を割り当てることによってこのローカル要求プロバイダー信頼を表す`$vendorDirectory`に、`-LdapServerConnection`パラメーター。 いずれかの手順で割り当てたに注意してください。`$vendorDirectory`、特定の LDAP ディレクトリに接続するときに使用される接続文字列。 最後に、指定したこと、`$GivenName`、`$Surname`、および`$CommonName`(これは、AD FS の要求にマップ) LDAP 属性は、多要素認証ポリシーと、発行承認規則を含む、条件付きアクセス制御および AD FS によって発行されたセキュリティ トークン内のクレームを使用して発行に使用します。 AD FS と Ws-trust のようにアクティブなプロトコルを使用するために、これにより、アクティブな認証要求を処理するときに、ローカルの要求プロバイダー信頼の間で明確に区別する AD FS OrganizationalAccountSuffix パラメーターを指定する必要があります。

## <a name="see-also"></a>参照してください。
[AD FS の操作](../../ad-fs/AD-FS-2016-Operations.md)


