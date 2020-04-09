---
ms.assetid: e863ab80-4e4c-48d3-bdaa-31815ef36bae
title: LDAP ディレクトリに保存されたユーザーを認証するように AD FS を構成する
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 9c194128cb5d96bf84e19b11b9d8803c61e34490
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859905"
---
# <a name="configure-ad-fs-to-authenticate-users-stored-in-ldap-directories"></a>LDAP ディレクトリに保存されたユーザーを認証するように AD FS を構成する

次のトピックでは、ライトウェイトディレクトリアクセスプロトコル (LDAP) v3 に準拠したディレクトリに id が格納されているユーザーを AD FS インフラストラクチャで認証できるようにするために必要な構成について説明します。

多くの組織では、id 管理ソリューションは、Active Directory、AD LDS、またはサードパーティの LDAP ディレクトリの組み合わせで構成されています。 LDAP v3 準拠のディレクトリに格納されているユーザーを認証するための AD FS サポートを追加すると、ユーザー id が格納されている場所に関係なく、エンタープライズレベルの AD FS 機能セット全体を活用できます。 AD FS は、すべての LDAP v3 準拠のディレクトリをサポートします。

> [!NOTE]
> AD FS の一部の機能には、シングルサインオン (SSO)、デバイスの認証、柔軟な条件付きアクセスポリシー、Web アプリケーションプロキシとの統合による、どこからでも機能をサポートする機能、および Azure AD とのシームレスなフェデレーションがあります。これにより、Office 365 などの SaaS アプリケーションを含むクラウドを利用できます。  詳細については、「 [Active Directory フェデレーションサービス (AD FS) の概要](../../ad-fs/AD-FS-2016-Overview.md)」を参照してください。

AD FS が LDAP ディレクトリからユーザーを認証できるようにするには、**ローカル要求プロバイダー信頼**を作成することによって、この ldap ディレクトリを AD FS ファームに接続する必要があります。  ローカル要求プロバイダー信頼は、AD FS ファーム内の LDAP ディレクトリを表す信頼オブジェクトです。 ローカル要求プロバイダー信頼オブジェクトは、ローカルのフェデレーションサービスに対してこの LDAP ディレクトリを識別するさまざまな識別子、名前、および規則で構成されます。

複数の**ローカル要求プロバイダー信頼**を追加することにより、同じ AD FS ファーム内で、それぞれが独自の構成を持つ複数の LDAP ディレクトリをサポートできます。 また、AD FS 存在するフォレストによって信頼されていない AD DS フォレストは、ローカル要求プロバイダー信頼としてモデル化することもできます。 Windows PowerShell を使用して、ローカルの要求プロバイダー信頼を作成できます。

LDAP ディレクトリ (ローカル要求プロバイダー信頼) は同じ AD FS サーバー上の AD ディレクトリ (要求プロバイダー信頼) と共存できます。そのため、同じ AD FS ファーム内で、AD FS の1つのインスタンスが、AD ディレクトリと非 AD ディレクトリの両方に格納されているユーザーの認証と承認を行うことができるようになります。

LDAP ディレクトリからのユーザーの認証では、フォームベースの認証のみがサポートされています。 LDAP ディレクトリでのユーザーの認証では、証明書ベースの認証と統合 Windows 認証はサポートされていません。

SAML、WS-FEDERATION、OAuth など、AD FS でサポートされているすべてのパッシブ認証プロトコルは、LDAP ディレクトリに格納されている id でもサポートされます。

WS-TRUST active authorization プロトコルは、LDAP ディレクトリに格納されている id に対してもサポートされています。

## <a name="configure-ad-fs-to-authenticate-users-stored-in-an-ldap-directory"></a>LDAP ディレクトリに格納されているユーザーを認証するように AD FS を構成する
LDAP ディレクトリからユーザーを認証するように AD FS ファームを構成するには、次の手順を実行します。

1. まず、 **AdfsLdapServerConnection**コマンドレットを使用して、LDAP ディレクトリへの接続を構成します。

   ```
   $DirectoryCred = Get-Credential
   $vendorDirectory = New-AdfsLdapServerConnection -HostName dirserver -Port 50000 -SslMode None -AuthenticationMethod Basic -Credential $DirectoryCred
   ```

   > [!NOTE]
   > 接続先の LDAP サーバーごとに新しい接続オブジェクトを作成することをお勧めします。 AD FS は、複数のレプリカ LDAP サーバーに接続し、特定の LDAP サーバーがダウンした場合に自動的にフェールオーバーすることができます。 このような場合は、これらのレプリカ LDAP サーバーごとに1つの AdfsLdapServerConnection を作成してから、 **AdfsLocalClaimsProviderTrust**コマンドレットの-**ldapserverconnection**パラメーターを使用して接続オブジェクトの配列を追加します。

   **注:** LDAP インスタンスにバインドするために使用する DN とパスワードを取得するために、資格情報を使用し、パスワードを入力しようとすると、特定の入力形式 (たとえば、domain\username や user@domain.tldなど) のユーザーインターフェイスが必要になるため、エラーが発生する可能性があります。 代わりに、次のように Convertto-html コマンドレットを使用することができます (次の例では、LDAP インスタンスにバインドするために使用する資格情報の DN として uid = admin, ou = system を想定しています)。

   ```
   $ldapuser = ConvertTo-SecureString -string "uid=admin,ou=system" -asplaintext -force
   $DirectoryCred = Get-Credential -username $ldapuser -Message "Enter the credentials to bind to the LDAP instance:"
   ```

   次に、uid = admin のパスワードを入力し、残りの手順を完了します。

2. 次に、 **AdfsLdapAttributeToClaimMapping**コマンドレットを使用して、既存の AD FS 要求に LDAP 属性をマッピングするオプションの手順を実行できます。 次の例では、givenName、姓、および CommonName LDAP 属性を AD FS 要求にマップします。

   ```
   #Map given name claim
   $GivenName = New-AdfsLdapAttributeToClaimMapping -LdapAttribute givenName -ClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname"
   # Map surname claim
   $Surname = New-AdfsLdapAttributeToClaimMapping -LdapAttribute sn -ClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname"
   # Map common name claim
   $CommonName = New-AdfsLdapAttributeToClaimMapping -LdapAttribute cn -ClaimType "http://schemas.xmlsoap.org/claims/CommonName"
   ```

   このマッピングは、AD FS で条件付きアクセス制御規則を作成するために、LDAP ストアの属性を AD FS の要求として使用できるようにするために行われます。 また、LDAP 属性を信頼性情報にマップする簡単な方法を提供することで、LDAP ストア内のカスタムスキーマを使用して AD FS することもできます。

3. 最後に、 **AdfsLocalClaimsProviderTrust**コマンドレットを使用して、LDAP ストアをローカル要求プロバイダーの信頼として AD FS に登録する必要があります。

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

   上記の例では、"ベンダ" という名前のローカル要求プロバイダー信頼を作成しています。 `-LdapServerConnection` パラメーターに `$vendorDirectory` を割り当てることによって、このローカル要求プロバイダー信頼が表す LDAP ディレクトリに接続するための AD FS の接続情報を指定します。 手順 1. では、特定の LDAP ディレクトリに接続するときに使用する接続文字列を `$vendorDirectory` 割り当てました。 最後に、`$GivenName`、`$Surname`、および `$CommonName` の LDAP 属性 (AD FS の要求にマップしたもの) を条件付きアクセスの制御に使用するように指定します。これには、多要素認証ポリシーと発行承認規則が含まれます。また、AD FS 発行されたセキュリティトークンの要求を使用して発行することもできます。 Ws-trust などのアクティブなプロトコルを AD FS と共に使用するには、OrganizationalAccountSuffix パラメーターを指定する必要があります。これにより、アクティブな承認要求を処理するときに、AD FS がローカル要求プロバイダー信頼を明確に区別できるようになります。

## <a name="see-also"></a>参照
[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md)


