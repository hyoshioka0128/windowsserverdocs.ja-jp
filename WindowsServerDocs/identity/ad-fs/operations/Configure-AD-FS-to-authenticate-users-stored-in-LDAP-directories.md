---
ms.assetid: e863ab80-4e4c-48d3-bdaa-31815ef36bae
title: LDAP ディレクトリに保存されたユーザーを認証するように AD FS を構成する
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: bef2cac726b1c4ea9b30f9a2086e3a2670339228
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189826"
---
# <a name="configure-ad-fs-to-authenticate-users-stored-in-ldap-directories"></a>LDAP ディレクトリに保存されたユーザーを認証するように AD FS を構成する

次のトピックでは、id が、ライトウェイト ディレクトリ アクセス プロトコル (LDAP) v3 に準拠しているディレクトリに格納されているユーザーを認証する、AD FS インフラストラクチャを有効にするために必要な構成について説明します。

多くの組織で id 管理ソリューションは、Active Directory、AD LDS、またはサード パーティ製の LDAP ディレクトリの組み合わせで構成されています。 LDAP v3 に準拠しているディレクトリに格納されているユーザーを認証するための AD FS サポートの追加を得ることができます全体のエンタープライズ レベルから AD FS 機能のセット、ユーザー id を格納する場所に関係なく。 AD FS には、LDAP v3 準拠の任意のディレクトリがサポートしています。

> [!NOTE]
> シングル サインオン (SSO)、デバイス認証の場合は、柔軟な条件付きアクセス ポリシーが含まれて、作業から、あらゆる場所で、Web アプリケーション プロキシとの統合により、シームレスなサポート、AD FS の機能の一部で Azure AD とのフェデレーション有効にして、ユーザーが Office 365 や他の SaaS アプリケーションなど、クラウドを利用します。  詳細については、次を参照してください。 [Active Directory フェデレーション サービスの概要](../../ad-fs/AD-FS-2016-Overview.md)します。

AD FS を LDAP ディレクトリからユーザーを認証するためには、する必要がありますに接続するこの LDAP ディレクトリ、AD FS ファームを作成して、**ローカル要求プロバイダー信頼**します。  ローカル要求プロバイダー信頼では、AD FS ファームに LDAP ディレクトリを表す信頼オブジェクトです。 ローカルの要求プロバイダー信頼の識別子、名前、およびローカルのフェデレーション サービスには、この LDAP ディレクトリを識別するルールのさまざまなオブジェクトで構成されます。

複数の LDAP ディレクトリで複数追加することで、同じ AD FS ファーム内の独自の構成では、それぞれをサポートする**ローカル要求プロバイダー信頼**します。 さらに、AD FS に在住のフォレストによって信頼されていない AD DS フォレストは、ローカルの要求プロバイダー信頼としてモデルにも化できます。 Windows PowerShell を使用して、ローカルの要求プロバイダー信頼を作成できます。

(ローカルの要求プロバイダー信頼) の LDAP ディレクトリと共存できます (要求プロバイダー信頼) の AD ディレクトリと同じ AD FS ファーム内で、同じ AD FS サーバーで、そのため、AD FS の 1 つのインスタンスは認証および承認はユーザーに対してアクセス可能両方の AD に格納されていると非 AD ディレクトリ。

フォーム ベースの認証のみが LDAP ディレクトリからユーザーを認証するためサポートされています。 LDAP ディレクトリでユーザーの認証には、証明書に基づくと、統合 Windows 認証はサポートされていません。

すべての承認のパッシブ プロトコル SAML、Ws-federation などの AD FS でサポートされていると、OAuth は、LDAP ディレクトリに格納されている id もサポートされています。

Ws-trust のアクティブな認証プロトコルは LDAP ディレクトリに格納されている id もサポートされます。

## <a name="configure-ad-fs-to-authenticate-users-stored-in-an-ldap-directory"></a>LDAP ディレクトリに格納されているユーザーの認証に AD FS を構成します。
LDAP ディレクトリからユーザーを認証する AD FS ファームを構成するには、次の手順を実行できます。

1.  最初に、使用する LDAP ディレクトリへの接続を構成、**新規 AdfsLdapServerConnection**コマンドレット。

    ```
    $DirectoryCred = Get-Credential
    $vendorDirectory = New-AdfsLdapServerConnection -HostName dirserver -Port 50000 -SslMode None -AuthenticationMethod Basic -Credential $DirectoryCred
    ```

    > [!NOTE]
    > 接続する各 LDAP サーバーの新しい接続オブジェクトを作成することをお勧めします。 AD FS では、複数のレプリカの LDAP サーバーに接続でき、自動的にフェールオーバー場合は、特定の LDAP サーバーがダウンすることができます。 このような場合には、これらの各レプリカの LDAP サーバーの AdfsLdapServerConnection の 1 つを作成しを使用して、接続オブジェクトの配列を追加することができます-**LdapServerConnection**のパラメーター、 **追加 AdfsLocalClaimsProviderTrust**コマンドレット。

    **注:** LDAP インスタンスにバインドするための DN とパスワードを入力して、Get-credential を使用しようとするがエラーにつながる可能性がありますので、特定の入力形式、たとえば、ドメイン \ ユーザー名のユーザー インターフェイスの要件のまたはuser@domain.tldします。 次のように Convertto-securestring コマンドレットは、代わりに使用できます (次の例には、uid が前提としています = ou の管理者は、LDAP のインスタンスにバインドするための資格情報の DN としてシステムを =)。

    ```
    $ldapuser = ConvertTo-SecureString -string "uid=admin,ou=system" -asplaintext -force
    $DirectoryCred = Get-Credential -username $ldapuser -Message "Enter the credentials to bind to the LDAP instance:"
    ```

    Uid のパスワードを入力し、管理者を = し、残りの手順を完了します。

2.  次に、オプションの手順を使用して既存の AD FS の要求への LDAP 属性のマッピングを行うことができます、**新規 AdfsLdapAttributeToClaimMapping**コマンドレット。 次の例では、givenName、Surname をマップして、CommonName LDAP 属性 AD FS の要求。

    ```
    #Map given name claim
    $GivenName = New-AdfsLdapAttributeToClaimMapping -LdapAttribute givenName -ClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname"
    # Map surname claim
    $Surname = New-AdfsLdapAttributeToClaimMapping -LdapAttribute sn -ClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname"
    # Map common name claim
    $CommonName = New-AdfsLdapAttributeToClaimMapping -LdapAttribute cn -ClaimType "http://schemas.xmlsoap.org/claims/CommonName"
    ```

    このマッピングは、LDAP ストアから AD FS での条件付きアクセス制御規則を作成するには、AD FS での要求として使用可能な属性を作成するために行われます。 また、AD FS の要求に LDAP 属性をマップする簡単な方法を提供することで、LDAP ストア内のカスタム スキーマを使用することもできます。

3.  最後に、登録する必要あります LDAP ストア AD FS を使用したように、ローカルの要求プロバイダー信頼を使用して、**追加 AdfsLocalClaimsProviderTrust**コマンドレット。

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

    上記の例では、「ベンダー」と呼ばれるローカルの要求プロバイダー信頼を作成します。 割り当てることによってこのローカル要求プロバイダー信頼を表す LDAP ディレクトリへの接続に AD FS の接続情報を指定する`$vendorDirectory`を`-LdapServerConnection`パラメーター。 手順 1. で割り当てたに注意してください。 `$vendorDirectory` 、特定の LDAP ディレクトリに接続するときに使用する接続文字列。 最後に、指定したが、 `$GivenName`、`$Surname`と`$CommonName`(これは、AD FS の要求にマップすると)、LDAP 属性が多要素認証ポリシーの発行などの条件付きアクセス制御に使用するには承認規則もと AD FS が発行したセキュリティ トークンのクレームを使用して発行します。 で AD FS を Ws-trust などのアクティブなプロトコルを使用するためには、これにより、作業中の承認要求を処理するときにローカルの要求プロバイダーの信頼間を明確に AD FS OrganizationalAccountSuffix パラメーターを指定する必要があります。

## <a name="see-also"></a>関連項目
[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md)


