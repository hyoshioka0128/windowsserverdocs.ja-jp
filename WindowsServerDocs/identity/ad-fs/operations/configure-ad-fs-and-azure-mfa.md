---
ms.assetid: 24c4b9bb-928a-4118-acf1-5eb06c6b08e5
title: AD FS 2016 と Azure MFA を構成する
description: ''
ms.author: billmath
author: billmath
manager: mtillman
ms.date: 01/28/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: b658644d1ba7cec1b02a2a51331cd7b7152efc77
ms.sourcegitcommit: 75e611fd5de8b8aa03fc26c2a3d5dbf8211b8ce3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/11/2020
ms.locfileid: "77145491"
---
# <a name="configure-azure-mfa-as-authentication-provider-with-ad-fs"></a>AD FS を使用して Azure MFA を認証プロバイダーとして構成する

組織が Azure AD とフェデレーションされている場合は、Azure Multi-Factor Authentication を使用して、オンプレミスとクラウドの両方で、AD FS リソースをセキュリティで保護することができます。 Azure MFA を使用すると、パスワードを排除し、より安全な認証方法を提供できます。  Windows Server 2016 以降では、プライマリ認証用に Azure MFA を構成したり、追加の認証プロバイダーとして使用したりできるようになりました。 
  
Windows Server 2012 R2 の AD FS とは異なり、AD FS 2016 Azure MFA アダプターは Azure AD と直接統合されており、オンプレミスの Azure MFA Server は必要ありません。   Azure MFA アダプターは Windows Server 2016 に組み込まれているため、追加のインストールは必要ありません。


## <a name="registering-users-for-azure-mfa-with-ad-fs"></a>AD FS を使用した Azure MFA へのユーザーの登録

AD FS では&#34;、インライン&#34;での証明をサポートしたり、電話番号やモバイルアプリなどの Azure MFA セキュリティ検証情報を登録したりすることはできません。 つまり、ユーザーは、Azure MFA を使用して AD FS アプリケーションに対して認証する前に、 [https://account.activedirectory.windowsazure.com/Proofup.aspx](https://account.activedirectory.windowsazure.com/Proofup.aspx)にアクセスして校正を取得する必要があります。 Azure AD にまだ校正していないユーザーが AD FS で Azure MFA による認証を試行した場合、AD FS エラーが発生します。  AD FS の管理者は、このエラーエクスペリエンスをカスタマイズして、ユーザーを proofup ページに導くことができます。  これを行うには、[AD FS] ページ内のエラーメッセージ文字列を検出し、ユーザーに[https://aka.ms/mfasetup](https://aka.ms/mfasetup)アクセスして認証を再実行するように指示する新しいメッセージを表示します。 詳細については、この記事の「ユーザーが MFA の検証方法を登録できるように、AD FS web ページをカスタマイズする」を参照してください。

>[!NOTE]
> 以前は、ユーザーは、登録のために MFA で認証する必要がありました (たとえば、ショートカット[https://aka.ms/mfasetup](https://aka.ms/mfasetup)を使用して、 [https://account.activedirectory.windowsazure.com/Proofup.aspx](https://account.activedirectory.windowsazure.com/Proofup.aspx)にアクセスしています)。  これで、MFA の検証情報をまだ登録していない AD FS ユーザー&#34;は、ショートカット[https://aka.ms/mfasetup](https://aka.ms/mfasetup) (Windows 統合認証、ユーザー名とパスワードなど、AD FS web ページを介して) Azure AD s proofup ページにアクセスできるようになりました。  ユーザーに検証方法が構成されていない場合、Azure AD はインライン登録を実行します&#34;&#34;&#34;。これにより、管理者は、追加のセキュリティ確認のためにこのアカウントを設定する必要&#34;があるというメッセージが表示されます。その後、ユーザーはこれを選択して設定できます。
> 少なくとも1つの MFA 検証方法が既に構成されているユーザーは、proofup ページにアクセスするときに MFA を提供するように求められます。

## <a name="recommended-deployment-topologies"></a>推奨される展開トポロジ

### <a name="azure-mfa-as-primary-authentication"></a>プライマリ認証としての Azure MFA

AD FS で Azure MFA をプライマリ認証として使用するには、いくつかの利点があります。

 - Azure AD、Office 365、およびその他の AD FS アプリへのサインインにパスワードを使用しないようにするには
 - パスワードの前に確認コードなどの追加の要因を要求してパスワードベースのサインインを保護するには

これらの利点を実現するために AD FS のプライマリ認証方法として Azure MFA を使用する場合は、AD FS で追加の要素を要求すること&#34;によっ&#34;て、真の mfa を含む Azure AD 条件付きアクセスを使用することもできます。

これを行うには、オンプレミスで MFA を実行するように Azure AD ドメイン&#34;設定を構成&#34;します (supportsmfa を $True に設定します)。  この構成では、必要な条件付きアクセスのシナリオに対して&#34;追加の&#34;認証または真の MFA を実行するために、Azure AD によって AD FS が求められます。  

前述のように、まだ登録していない (MFA 検証情報を構成した) AD FS ユーザーは、カスタマイズされた AD FS のエラーページを通じて、 [https://aka.ms/mfasetup](https://aka.ms/mfasetup)にアクセスして確認情報を構成してから AD FS ログインを再試行するように求めるメッセージを表示する必要があります。  
Azure MFA をプライマリとして扱うのは1つの要素であるため、初期構成の後、ユーザーは、Azure AD での確認情報の管理や更新、または MFA を必要とする他のリソースへのアクセスについて、追加の要素を提供する必要があります。

>[!NOTE]
> ADFS 2019 では、Active Directory 要求プロバイダー信頼のアンカー要求の種類を変更して、windowsaccountname から UPN に変更する必要があります。 次の PowerShell コマンドレットを実行します。 これは、AD FS ファームの内部機能には影響しません。 この変更が行われると、いくつかのユーザーに資格情報の再入力を求めるメッセージが表示される場合があります。 もう一度ログインしても、エンドユーザーには違いはありません。 

```powershell
Set-AdfsClaimsProviderTrust -AnchorClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn" -TargetName "Active Directory"
```

### <a name="azure-mfa-as-additional-authentication-to-office-365"></a>Office 365 に対する追加認証としての Azure MFA

以前は、Office 365 または他の証明書利用者の AD FS で、Azure MFA を追加の認証方法として使用する場合は、複合 MFA を実行するように Azure AD を構成することをお勧めします。これは AD FS でプライマリ認証がオンプレミスで実行され、MFA が tr です。Azure AD によってピアリングされます。 これで、ドメインの SupportsMfa 設定が $True に設定されている場合に AD FS での追加認証として Azure MFA を使用できるようになりました。  

前述のように、まだ登録していない (MFA 検証情報を構成した) AD FS ユーザーは、カスタマイズされた AD FS のエラーページを通じて、 [https://aka.ms/mfasetup](https://aka.ms/mfasetup)にアクセスして確認情報を構成してから AD FS ログインを再試行するように求めるメッセージを表示する必要があります。  

## <a name="pre-requisites"></a>前提条件

AD FS での認証に Azure MFA を使用する場合は、次の前提条件が必要です。  
  
- [Azure Active Directory がある Azure サブスクリプション](https://azure.microsoft.com/pricing/free-trial/)。  
- [Azure Multi-Factor Authentication](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/) 


> [!NOTE]
> Azure AD と Azure MFA は Azure AD Premium と Enterprise Mobility Suite (EMS) に含まれています。  これらのいずれかを使用している場合は、個々のサブスクリプションは必要ありません。

- Windows Server 2016 AD FS オンプレミス環境。  
   - サーバーは、ポート443経由で次の Url と通信できる必要があります。
      - https://adnotifications.windowsazure.com
      - https://login.microsoftonline.com
- オンプレミス環境は[Azure AD とフェデレーションされます。](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#configuring-federation-with-ad-fs)  
- Windows [PowerShell 用 windows Azure Active Directory モジュール](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0)。  
- Azure AD PowerShell を使用して構成する Azure AD インスタンスのグローバル管理者のアクセス許可。  
- Azure MFA の AD FS ファームを構成するためのエンタープライズ管理者の資格情報。

## <a name="configure-the-ad-fs-servers"></a>AD FS サーバーを構成する

AD FS のために Azure MFA の構成を完了するには、説明されている手順を使用して各 AD FS サーバーを構成する必要があります。 

>[!NOTE]
>ファーム内の**すべて**の AD FS サーバーでこれらの手順が実行されていることを確認します。 ファーム内に複数の AD FS サーバーがある場合は Azure AD PowerShell を使用して必要な構成をリモートで実行できます。  

### <a name="step-1-generate-a-certificate-for-azure-mfa-on-each-ad-fs-server-using-the-new-adfsazuremfatenantcertificate-cmdlet"></a>手順 1: `New-AdfsAzureMfaTenantCertificate` コマンドレットを使用して、各 AD FS サーバーで Azure MFA の証明書を生成する

まず、Azure MFA で使用する証明書を生成する必要があります。  これは、PowerShell を使用して行うことができます。  生成された証明書は、ローカルコンピューターの証明書ストアにあり、Azure AD ディレクトリの TenantID を含むサブジェクト名でマークされます。

![AD FS と MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA3.png)  

TenantID は Azure AD 内のディレクトリの名前であることに注意してください。  次の PowerShell コマンドレットを使用して、新しい証明書を生成します。  
    `$certbase64 = New-AdfsAzureMfaTenantCertificate -TenantID <tenantID>`  

![AD FS と MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA1.PNG)  
  
### <a name="step-2-add-the-new-credentials-to-the-azure-multi-factor-auth-client-service-principal"></a>手順 2: Azure Multi-factor Auth クライアントのサービスプリンシパルに新しい資格情報を追加する

AD FS サーバーが Azure Multi-factor Auth クライアントと通信できるようにするには、Azure Multi-factor Auth クライアントのサービスプリンシパルに資格情報を追加する必要があります。 `New-AdfsAzureMFaTenantCertificate` コマンドレットを使用して生成された証明書は、これらの資格情報として機能します。 PowerShell を使用して次の操作を実行し、Azure Multi-factor Auth クライアントのサービスプリンシパルに新しい資格情報を追加します。  

> [!NOTE]
> この手順を完了するには、`Connect-MsolService`を使用して、PowerShell を使用して Azure AD のインスタンスに接続する必要があります。  これらの手順では、既に PowerShell を使用して接続していることを前提とします  詳細については、「`Connect-MsolService`」を参照してください[。](https://msdn.microsoft.com/library/dn194123.aspx)  

**Azure Multi-factor Auth クライアントに対する新しい資格情報として証明書を設定する**  

`New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type asymmetric -Usage verify -Value $certBase64`

> [!IMPORTANT]
> このコマンドは、ファーム内のすべての AD FS サーバーで実行する必要があります。  Azure Multi-factor Auth クライアントに対して証明書が新しい資格情報として設定されていないサーバーでは、Azure AD MFA は失敗します。

> [!NOTE]  
> 981f26a1-7f43-403b-a875-f8b09b8cd720 は、Azure Multi-factor Auth クライアントの GUID です。  
  
## <a name="configure-the-ad-fs-farm"></a>AD FS ファームの構成  
  
各 AD FS サーバーで前のセクションを完了したら、 [AdfsAzureMfaTenant](https://docs.microsoft.com/powershell/module/adfs/export-adfsauthenticationproviderconfigurationdata)コマンドレットを使用して Azure テナント情報を設定します。 このコマンドレットは、AD FS ファームに対して1回だけ実行する必要があります。

PowerShell プロンプトを開き、 [AdfsAzureMfaTenant](https://docs.microsoft.com/powershell/module/adfs/export-adfsauthenticationproviderconfigurationdata)コマンドレットを使用して独自の*tenantId*を入力します。 Microsoft Azure Government cloud を使用しているお客様の場合は、`-Environment USGov` パラメーターを追加します。

> [!NOTE]
> これらの変更を反映するには、ファーム内の各サーバーで AD FS サービスを再起動する必要があります。 影響を最小限に抑えるには、各 AD FS サーバーを1つずつ NLB ローテーションから取り出し、すべての接続がドレインされるのを待ちます。

```powershell
Set-AdfsAzureMfaTenant -TenantId <tenant ID> -ClientId 981f26a1-7f43-403b-a875-f8b09b8cd720
```

![AD FS と MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA5.png)

最新の Service Pack のない Windows Server では、 [AdfsAzureMfaTenant](https://docs.microsoft.com/powershell/module/adfs/export-adfsauthenticationproviderconfigurationdata)コマンドレットの `-Environment` パラメーターはサポートされていません。 Azure Government cloud を使用していて、前の手順で `-Environment` パラメーターが指定されていないために Azure テナントを構成できなかった場合は、次の手順を実行してレジストリエントリを手動で作成します。 前のコマンドレットでテナント情報が正しく登録されているか、Azure Government クラウドに登録されていない場合は、この手順をスキップします。

1. AD FS サーバーで**レジストリエディター**を開きます。
1. `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ADFS` に移動します。 次のレジストリキー値を作成します。

    | レジストリ キー       | 値 |
    |--------------------|-----------------------------------|
    | SasUrl             | https://adnotifications.windowsazure.us/StrongAuthenticationService.svc/Connector |
    | StsUrl             | https://login.microsoftonline.us |
    | ResourceUri        | https://adnotifications.windowsazure.us/StrongAuthenticationService.svc/Connector |

1. これらの変更が反映される前に、ファーム内の各サーバーで AD FS サービスを再起動します。 影響を最小限に抑えるには、各 AD FS サーバーを1つずつ NLB ローテーションから取り出し、すべての接続がドレインされるのを待ちます。

その後、Azure MFA は、イントラネットおよびエクストラネットで使用するための主要な認証方法として使用できることがわかります。

![AD FS と MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA6.png)  

## <a name="renew-and-manage-ad-fs-azure-mfa-certificates"></a>Azure MFA 証明書 AD FS の更新と管理

次のガイダンスでは、AD FS サーバー上の Azure MFA 証明書を管理する方法について説明します。
既定では、Azure MFA で AD FS を構成すると、`New-AdfsAzureMfaTenantCertificate` の PowerShell コマンドレットを使用して生成された証明書は2年間有効になります。  証明書の有効期限が近づいていることを確認し、新しい証明書を更新してインストールするには、次の手順を使用します。

### <a name="assess-ad-fs-azure-mfa-certificate-expiration-date"></a>Azure MFA 証明書の有効期限日を評価 AD FS

各 AD FS サーバーでは、[ローカルコンピューターマイストア] に、発行者とサブジェクトに " &#34;OU = Microsoft AD FS Azure MFA&#34; " という自己署名入り証明書があります。  これは、Azure MFA 証明書です。  各 AD FS サーバーでこの証明書の有効期間を確認して、有効期限を確認します。  

### <a name="create-new-ad-fs-azure-mfa-certificate-on-each-ad-fs-server"></a>各 AD FS サーバーに新しい AD FS Azure MFA 証明書を作成する

証明書の有効期間が間もなく終了する場合は、各 AD FS サーバーに新しい Azure MFA 証明書を生成して、更新プロセスを開始します。 PowerShell コマンドウィンドウで、次のコマンドレットを使用して、各 AD FS サーバーに新しい証明書を生成します。

> [!CAUTION]
> 証明書の有効期限が既に切れている場合は、次のコマンドに `-Renew $true` パラメーターを追加しないでください。 このシナリオでは、既存の有効期限が切れた証明書は、そのまま残され、追加の証明書が作成されるのではなく、新しい証明書に置き換えられます。

```
PS C:\> $newcert = New-AdfsAzureMfaTenantCertificate -TenantId <tenant id such as contoso.onmicrosoft.com> -Renew $true
```

証明書の有効期限がまだ切れていない場合は、2日後2日 + 2 年後に有効な新しい証明書が生成されます。 AD FS と Azure MFA の操作は、このコマンドレットまたは新しい証明書の影響を受けません。 (注: 2 日間の遅延は意図的であり、以下の手順を実行して、テナントの新しい証明書を構成するための時間を提供します。 AD FS は、Azure MFA でその証明書を使用して開始します)。

### <a name="configure-each-new-ad-fs-azure-mfa-certificate-in-the-azure-ad-tenant"></a>Azure AD テナントでの新しい AD FS Azure MFA 証明書の構成

Azure AD PowerShell モジュールを使用して、(各 AD FS サーバー上の) 新しい証明書ごとに、次のように Azure AD テナント設定を更新します (注: まず、`Connect-MsolService` を使用してテナントに接続し、次のコマンドを実行する必要があります)。

```
PS C:/> New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type Asymmetric -Usage Verify -Value $newcert
```

以前の証明書の有効期限が既に切れている場合は、AD FS サービスを再起動して新しい証明書を取得します。 期限切れになる前に証明書を更新した場合は、AD FS サービスを再起動する必要はありません。

### <a name="verify-that-the-new-certificates-will-be-used-for-azure-mfa"></a>新しい証明書が Azure MFA に使用されることを確認する

新しい証明書が有効になると、AD FS によって取得され、数時間以内に Azure MFA 用の各証明書の使用が開始されます。  このエラーが発生すると、各サーバーで、AD FS 管理者イベントログに記録されたイベントが、次の情報と共に表示されます。

```
Log Name:      AD FS/Admin
Source:        AD FS
Date:          2/27/2018 7:33:31 PM
Event ID:      547
Task Category: None
Level:         Information
Keywords:      AD FS
User:          DOMAIN\adfssvc
Computer:      ADFS.domain.contoso.com
Description:
The tenant certificate for Azure MFA has been renewed.  

TenantId: contoso.onmicrosoft.com.
Old thumbprint: 7CC103D60967318A11D8C51C289EF85214D9FC63.
Old expiration date: 9/15/2019 9:43:17 PM.
New thumbprint: 8110D7415744C9D4D5A4A6309499F7B48B5F3CCF.
New expiration date: 2/27/2020 2:16:07 AM.
```

## <a name="customize-the-ad-fs-web-page-to-guide-users-to-register-mfa-verification-methods"></a>AD FS web ページをカスタマイズして、ユーザーが MFA の検証方法を登録できるようにする

次の例を使用して、まだ校正していない (MFA の検証情報を構成している) ユーザーの AD FS web ページをカスタマイズします。

### <a name="find-the-error"></a>エラーを見つける

最初に、ユーザーが検証情報を持っていない場合に返さ AD FS エラーメッセージがいくつかあります。
Azure MFA をプライマリ認証として使用している場合、校正ユーザーには、次のメッセージを含む AD FS のエラーページが表示されます。
```
    <div id="errorArea">
        <div id="openingMessage" class="groupMargin bigText">
            An error occurred
        </div>
        <div id="errorMessage" class="groupMargin">
            Authentication attempt failed. Select a different sign in option or close the web browser and sign in again. Contact your administrator for more information.
        </div>
```
追加の認証が試行されると Azure AD、校正ユーザーには、次のメッセージを含む AD FS のエラーページが表示されます。
```
<div id='mfaGreetingDescription' class='groupMargin'>For security reasons, we require additional information to verify your account (mahesh@jenfield.net)</div>
    <div id="errorArea">
        <div id="openingMessage" class="groupMargin bigText">
            An error occurred
        </div>
        <div id="errorMessage" class="groupMargin">
            The selected authentication method is not available for &#39;username@contoso.com&#39;. Choose another authentication method or contact your system administrator for details.
        </div>
```

### <a name="catch-the-error-and-update-the-page-text"></a>エラーをキャッチし、ページテキストを更新します。

エラーをキャッチしてユーザーのカスタムガイダンスを表示するには、AD FS web テーマの一部である onload ファイルの末尾に javascript を追加するだけです。  これにより、次の操作を行うことができます。
 - 識別エラー文字列を検索します
 - カスタム web コンテンツを提供します。  

> [!NOTE]
> Onload ファイルをカスタマイズする方法に関する一般的なガイダンスについては、「 [AD FS サインインページの高度なカスタマイズ](advanced-customization-of-ad-fs-sign-in-pages.md)」を参照してください。

単純な例を次に示します。

1. プライマリ AD FS サーバーで Windows PowerShell を開き、次のコマンドを実行して新しい AD FS Web テーマを作成します。
    
    ``` PowerShell
        New-AdfsWebTheme –Name ProofUp –SourceName default
    ``` 
2. 次に、フォルダーを作成し、既定の AD FS Web テーマをエクスポートします。

    ``` PowerShell
       New-Item -Path 'c:\Theme' -ItemType Directory;Export-AdfsWebTheme –Name default –DirectoryPath c:\Theme
    ```
3. テキストエディターで C:\Theme\script\onload.js ファイルを開きます。
4. 次のコードを、onload ファイルの末尾に追加します。
    
    ``` JavaScript
    //Custom Code
    //Customize MFA exception
    //Begin

    var domain_hint = "<YOUR_DOMAIN_NAME_HERE>";
    var mfaSecondFactorErr = "The selected authentication method is not available for";
    var mfaProofupMessage = "You will be automatically redirected in 5 seconds to set up your account for additional security verification. Once you have completed the setup, please return to the application you are attempting to access.<br><br>If you are not redirected automatically, please click <a href='{0}'>here</a>."
    var authArea = document.getElementById("authArea");
    if (authArea) {
        var errorMessage = document.getElementById("errorMessage");
        if (errorMessage) {
            if (errorMessage.innerHTML.indexOf(mfaSecondFactorErr) >= 0) {

                //Hide the error message
                var openingMessage = document.getElementById("openingMessage");
                if (openingMessage) {
                    openingMessage.style.display = 'none'
                }
                var errorDetailsLink = document.getElementById("errorDetailsLink");
                if (errorDetailsLink) {
                    errorDetailsLink.style.display = 'none'
                }

                //Provide a message and redirect to Azure AD MFA Registration Url
                var mfaRegisterUrl = "https://account.activedirectory.windowsazure.com/proofup.aspx?proofup=1&whr=" + domain_hint;
                errorMessage.innerHTML = "<br>" + mfaProofupMessage.replace("{0}", mfaRegisterUrl);
                window.setTimeout(function () { window.location.href = mfaRegisterUrl; }, 5000);
            }
        }
    }

    //End Customize MFA Exception
    //End Custom Code
    ```
    > [!IMPORTANT]
    > "< YOUR_DOMAIN_NAME_HERE >" を変更する必要があります。ドメイン名を使用します。 たとえば次のようになります。`var domain_hint = "contoso.com";`
    
5. Onload ファイルを保存します。
6. 次の Windows PowerShell コマンドを入力して、カスタムテーマに onload ファイルをインポートします。
    
    ``` PowerShell
    Set-AdfsWebTheme -TargetName ProofUp -AdditionalFileResource @{Uri='/adfs/portal/script/onload.js';path="c:\theme\script\onload.js"}
    ```
7. 最後に、次の Windows PowerShell コマンドを入力して、カスタム AD FS Web テーマを適用します。
    
    ``` PowerShell
    Set-AdfsWebConfig -ActiveThemeName "ProofUp"
    ```

## <a name="next-steps"></a>次のステップ:

[AD FS と Azure MFA によって使用される TLS/SSL プロトコルと暗号スイートを管理する](manage-ssl-protocols-in-ad-fs.md)
