---
ms.assetid: 24c4b9bb-928a-4118-acf1-5eb06c6b08e5
title: AD FS 2016 と Azure MFA を構成する
ms.author: billmath
author: billmath
manager: mtillman
ms.date: 01/28/2019
ms.topic: article
ms.openlocfilehash: 5847b2fe6846fb4f89dcb0239167ea2ce55af1e0
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87966839"
---
# <a name="configure-azure-mfa-as-authentication-provider-with-ad-fs"></a>AD FS を使用して Azure MFA を認証プロバイダーとして構成する

組織が Azure AD とフェデレーションされている場合は、オンプレミスとクラウドの両方で、Azure Multi-Factor Authentication を使用して AD FS リソースをセキュリティ保護することができます。 Azure MFA を使用すると、パスワードを排除し、より安全な認証方法を提供できます。  Windows Server 2016 以降では、プライマリ認証用に Azure MFA を構成したり、追加の認証プロバイダーとして使用したりできるようになりました。

Windows Server 2012 R2 の AD FS とは異なり、AD FS 2016 Azure MFA アダプターは Azure AD と直接統合されており、オンプレミスの Azure MFA Server は必要ありません。   Azure MFA アダプターは Windows Server 2016 に組み込まれているため、追加のインストールは必要ありません。


## <a name="registering-users-for-azure-mfa-with-ad-fs"></a>AD FS を使用した Azure MFA へのユーザーの登録

AD FS は、インライン &#34;証明&#34;、または電話番号やモバイルアプリなどの Azure MFA セキュリティ検証情報の登録をサポートしていません。 つまり、ユーザーは、 [https://account.activedirectory.windowsazure.com/Proofup.aspx](https://account.activedirectory.windowsazure.com/Proofup.aspx) AZURE MFA を使用して AD FS アプリケーションに対して認証を行う前に、にアクセスして校正を取得する必要があります。
Azure AD にまだ校正していないユーザーが AD FS で Azure MFA による認証を試行した場合、AD FS エラーが発生します。  AD FS の管理者は、このエラーエクスペリエンスをカスタマイズして、ユーザーを proofup ページに導くことができます。  これを行うには onload.js カスタマイズを使用して AD FS ページ内のエラーメッセージ文字列を検出し、ユーザーにアクセスを指示する新しいメッセージを表示して [https://aka.ms/mfasetup](https://aka.ms/mfasetup) から、認証を再試行します。 詳細については、この記事の「ユーザーが MFA の検証方法を登録できるように、AD FS web ページをカスタマイズする」を参照してください。

>[!NOTE]
> 以前は、ユーザーは、登録のために MFA で認証する必要がありました (ショートカットを使用するなど [https://account.activedirectory.windowsazure.com/Proofup.aspx](https://account.activedirectory.windowsazure.com/Proofup.aspx) [https://aka.ms/mfasetup](https://aka.ms/mfasetup) )。  これで、MFA 検証情報をまだ登録していない AD FS ユーザーは、 [https://aka.ms/mfasetup](https://aka.ms/mfasetup) プライマリ認証のみ (Windows 統合認証、ユーザー名と AD FS パスワードなど) を使用して、ショートカット経由で Azure AD&#34;s proofup ページにアクセスできるようになります。  ユーザーに検証方法が構成されていない場合、Azure AD はインライン登録を実行します。これにより、管理者は、追加のセキュリティ確認&#34; のためにこのアカウントを設定する必要がある &#34;、ユーザーはこのアカウントを設定して &#34;設定を&#34; することができます。
> 少なくとも1つの MFA 検証方法が既に構成されているユーザーは、proofup ページにアクセスするときに MFA を提供するように求められます。

## <a name="recommended-deployment-topologies"></a>推奨されている展開トポロジ

### <a name="azure-mfa-as-primary-authentication"></a>プライマリ認証としての Azure MFA

AD FS で Azure MFA をプライマリ認証として使用するには、いくつかの利点があります。

 - Azure AD、Office 365、およびその他の AD FS アプリへのサインインにパスワードを使用しないようにするには
 - パスワードの前に確認コードなどの追加の要因を要求してパスワードベースのサインインを保護するには

これらの利点を実現するために AD FS のプライマリ認証方法として Azure MFA を使用する場合は、AD FS で追加の要因を確認することによって、&#34;true MFA&#34; を含む Azure AD 条件付きアクセスを使用することもできます。

これを行うには、オンプレミスで MFA を実行するように Azure AD ドメイン設定を構成します (&#34;SupportsMfa&#34; を $True に設定します)。  この構成では、Azure AD によって、追加の認証を実行するか、必要な条件付きアクセスのシナリオに対して真の MFA&#34; を &#34;するように AD FS ことが求められます。

前述のように、まだ登録していない (MFA 検証情報を構成した) AD FS ユーザーは、カスタマイズされた AD FS のエラーページを使用して、確認情報を構成してから AD FS ログインを再試行するように求められ [https://aka.ms/mfasetup](https://aka.ms/mfasetup) ます。
Azure MFA をプライマリとして扱うのは1つの要素であるため、初期構成の後、ユーザーは、Azure AD での確認情報の管理や更新、または MFA を必要とする他のリソースへのアクセスについて、追加の要素を提供する必要があります。

>[!NOTE]
> ADFS 2019 では、Active Directory 要求プロバイダー信頼のアンカー要求の種類を変更して、windowsaccountname から UPN に変更する必要があります。 次の PowerShell コマンドレットを実行します。 これは、AD FS ファームの内部機能には影響しません。 この変更が行われると、いくつかのユーザーに資格情報の再入力を求めるメッセージが表示される場合があります。 もう一度ログインしても、エンドユーザーには違いはありません。

```powershell
Set-AdfsClaimsProviderTrust -AnchorClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn" -TargetName "Active Directory"
```

### <a name="azure-mfa-as-additional-authentication-to-office-365"></a>Office 365 に対する追加認証としての Azure MFA

以前は、Office 365 またはその他の証明書利用者に対して AD FS の追加の認証方法として Azure MFA を使用する場合は、複合 MFA を実行するように Azure AD を構成し、AD FS でプライマリ認証がオンプレミスで実行され、MFA が Azure AD によってトリガーされるようにすることが最善の方法でした。
これで、ドメインの SupportsMfa 設定が $True に設定されている場合に AD FS での追加認証として Azure MFA を使用できるようになりました。

前述のように、まだ登録していない (MFA 検証情報を構成した) AD FS ユーザーは、カスタマイズされた AD FS のエラーページを使用して、確認情報を構成してから AD FS ログインを再試行するように求められ [https://aka.ms/mfasetup](https://aka.ms/mfasetup) ます。

## <a name="pre-requisites"></a>前提条件

AD FS での認証に Azure MFA を使用する場合は、次の前提条件が必要です。

- [Azure Active Directory がある Azure サブスクリプション](https://azure.microsoft.com/pricing/free-trial/)。
- [Azure Multi-Factor Authentication](/azure/active-directory/authentication/concept-mfa-howitworks)


> [!NOTE]
> Azure AD と Azure MFA は Azure AD Premium と Enterprise Mobility Suite (EMS) に含まれています。  これらのいずれかを使用している場合は、個々のサブスクリプションは必要ありません。

- Windows Server 2016 AD FS オンプレミス環境。
   - サーバーは、ポート443経由で次の Url と通信できる必要があります。
      - https://adnotifications.windowsazure.com
      - https://login.microsoftonline.com
- オンプレミス環境は[Azure AD とフェデレーションされます。](/azure/active-directory/hybrid/how-to-connect-install-custom#configuring-federation-with-ad-fs)
- Windows [PowerShell 用 windows Azure Active Directory モジュール](/powershell/module/azuread/?view=azureadps-2.0)。
- Azure AD PowerShell を使用して構成する Azure AD インスタンスのグローバル管理者のアクセス許可。
- Azure MFA の AD FS ファームを構成するためのエンタープライズ管理者の資格情報。

## <a name="configure-the-ad-fs-servers"></a>AD FS サーバーを構成する

AD FS のために Azure MFA の構成を完了するには、説明されている手順を使用して各 AD FS サーバーを構成する必要があります。

>[!NOTE]
>ファーム内の**すべて**の AD FS サーバーでこれらの手順が実行されていることを確認します。 ファーム内に複数の AD FS サーバーがある場合は Azure AD PowerShell を使用して必要な構成をリモートで実行できます。

### <a name="step-1-generate-a-certificate-for-azure-mfa-on-each-ad-fs-server-using-the-new-adfsazuremfatenantcertificate-cmdlet"></a>手順 1: コマンドレットを使用して、各 AD FS サーバーで Azure MFA の証明書を生成する `New-AdfsAzureMfaTenantCertificate`

まず、Azure MFA で使用する証明書を生成する必要があります。  これは、PowerShell を使用して行うことができます。  生成された証明書は、ローカルコンピューターの証明書ストアにあり、Azure AD ディレクトリの TenantID を含むサブジェクト名でマークされます。

![AD FS と MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA3.png)

TenantID は Azure AD 内のディレクトリの名前であることに注意してください。  次の PowerShell コマンドレットを使用して、新しい証明書を生成します。
    `$certbase64 = New-AdfsAzureMfaTenantCertificate -TenantID <tenantID>`

![AD FS と MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA1.PNG)

### <a name="step-2-add-the-new-credentials-to-the-azure-multi-factor-auth-client-service-principal"></a>手順 2: Azure Multi-factor Auth クライアントのサービスプリンシパルに新しい資格情報を追加する

AD FS サーバーが Azure Multi-factor Auth クライアントと通信できるようにするには、Azure Multi-factor Auth クライアントのサービスプリンシパルに資格情報を追加する必要があります。 コマンドレットを使用して生成された証明書 `New-AdfsAzureMFaTenantCertificate` は、これらの資格情報として機能します。 PowerShell を使用して次の操作を実行し、Azure Multi-factor Auth クライアントのサービスプリンシパルに新しい資格情報を追加します。

> [!NOTE]
> この手順を完了するには、を使用して PowerShell を使用して Azure AD のインスタンスに接続する必要があり `Connect-MsolService` ます。  これらの手順では、既に PowerShell を使用して接続していることを前提とします  詳細については、を参照してください[ `Connect-MsolService` 。](/previous-versions/azure/dn194123(v=azure.100))

**Azure Multi-factor Auth クライアントに対する新しい資格情報として証明書を設定する**

`New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type asymmetric -Usage verify -Value $certBase64`

> [!IMPORTANT]
> このコマンドは、ファーム内のすべての AD FS サーバーで実行する必要があります。  Azure Multi-factor Auth クライアントに対して証明書が新しい資格情報として設定されていないサーバーでは、Azure AD MFA は失敗します。

> [!NOTE]
> 981f26a1-7f43-403b-a875-f8b09b8cd720 は、Azure Multi-factor Auth クライアントの GUID です。

## <a name="configure-the-ad-fs-farm"></a>AD FS ファームの構成

各 AD FS サーバーで前のセクションを完了したら、 [AdfsAzureMfaTenant](/powershell/module/adfs/export-adfsauthenticationproviderconfigurationdata)コマンドレットを使用して Azure テナント情報を設定します。 このコマンドレットは、AD FS ファームに対して1回だけ実行する必要があります。

PowerShell プロンプトを開き、 [AdfsAzureMfaTenant](/powershell/module/adfs/export-adfsauthenticationproviderconfigurationdata)コマンドレットを使用して独自の*tenantId*を入力します。 Microsoft Azure Government cloud を使用しているお客様の場合は、パラメーターを追加し `-Environment USGov` ます。

> [!NOTE]
> これらの変更を反映するには、ファーム内の各サーバーで AD FS サービスを再起動する必要があります。 影響を最小限に抑えるには、各 AD FS サーバーを1つずつ NLB ローテーションから取り出し、すべての接続がドレインされるのを待ちます。

```powershell
Set-AdfsAzureMfaTenant -TenantId <tenant ID> -ClientId 981f26a1-7f43-403b-a875-f8b09b8cd720
```

![AD FS と MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA5.png)

最新の Service Pack のない Windows Server では、 `-Environment` [AdfsAzureMfaTenant](/powershell/module/adfs/export-adfsauthenticationproviderconfigurationdata)コマンドレットのパラメーターはサポートされていません。 Azure Government cloud を使用していて、前の手順で、不足しているパラメーターのために Azure テナントを構成できなかった場合は `-Environment` 、次の手順を実行してレジストリエントリを手動で作成します。 前のコマンドレットでテナント情報が正しく登録されているか、Azure Government クラウドに登録されていない場合は、この手順をスキップします。

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
既定では、Azure MFA で AD FS を構成すると、PowerShell コマンドレットを使用して生成された証明書 `New-AdfsAzureMfaTenantCertificate` は2年間有効になります。  証明書の有効期限が近づいていることを確認し、新しい証明書を更新してインストールするには、次の手順を使用します。

### <a name="assess-ad-fs-azure-mfa-certificate-expiration-date"></a>Azure MFA 証明書の有効期限日を評価 AD FS

各 AD FS サーバーでは、[ローカルコンピューターマイストア] に自己署名証明書があります。これには、発行者とサブジェクトで &#34;OU = Microsoft AD FS Azure MFA&#34; が含まれます。  これは、Azure MFA 証明書です。  有効期限を確認するには、各 AD FS サーバーでこの証明書の有効期間を調べます。

### <a name="create-new-ad-fs-azure-mfa-certificate-on-each-ad-fs-server"></a>各 AD FS サーバーに新しい AD FS Azure MFA 証明書を作成する

証明書の有効期間が間もなく終了する場合は、各 AD FS サーバーに新しい Azure MFA 証明書を生成して、更新プロセスを開始します。 PowerShell コマンドウィンドウで、次のコマンドレットを使用して、各 AD FS サーバーに新しい証明書を生成します。

> [!CAUTION]
> 証明書の有効期限が既に切れている場合は、次のコマンドにパラメーターを追加しないで `-Renew $true` ください。 このシナリオでは、既存の有効期限が切れた証明書は、そのまま残され、追加の証明書が作成されるのではなく、新しい証明書に置き換えられます。

```
PS C:\> $newcert = New-AdfsAzureMfaTenantCertificate -TenantId <tenant id such as contoso.onmicrosoft.com> -Renew $true
```

証明書の有効期限がまだ切れていない場合は、2日後2日 + 2 年後に有効な新しい証明書が生成されます。 AD FS と Azure MFA の操作は、このコマンドレットまたは新しい証明書の影響を受けません。 (注: 2 日間の遅延は意図的であり、以下の手順を実行して、テナントの新しい証明書を構成するための時間を提供します。 AD FS は、Azure MFA でその証明書を使用して開始します)。

### <a name="configure-each-new-ad-fs-azure-mfa-certificate-in-the-azure-ad-tenant"></a>Azure AD テナントでの新しい AD FS Azure MFA 証明書の構成

Azure AD PowerShell モジュールを使用して、(各 AD FS サーバー上の) 新しい証明書ごとに、次のように Azure AD テナント設定を更新します (注: 最初にを使用してテナントに接続し `Connect-MsolService` 、次のコマンドを実行する必要があります)。

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

このエラーをキャッチしてユーザーのカスタムガイダンスを表示するには、AD FS web テーマの一部である onload.js ファイルの末尾に javascript を追加するだけです。  これにより、次の操作を行うことができます。
 - 識別エラー文字列を検索します
 - カスタム web コンテンツを提供します。

> [!NOTE]
> onload.js ファイルをカスタマイズする方法に関する一般的なガイダンスについては、「 [AD FS サインインページの高度なカスタマイズ](advanced-customization-of-ad-fs-sign-in-pages.md)」を参照してください。

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
4. onload.js ファイルの末尾に次のコードを追加します。

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
    > "<YOUR_DOMAIN_NAME_HERE>" を変更する必要があります。ドメイン名を使用します。 例: `var domain_hint = "contoso.com";`

5. onload.js ファイルを保存する
6. 次の Windows PowerShell コマンドを入力して、onload.js ファイルをカスタムテーマにインポートします。

    ``` PowerShell
    Set-AdfsWebTheme -TargetName ProofUp -AdditionalFileResource @{Uri='/adfs/portal/script/onload.js';path="c:\theme\script\onload.js"}
    ```
7. 最後に、次の Windows PowerShell コマンドを入力して、カスタム AD FS Web テーマを適用します。

    ``` PowerShell
    Set-AdfsWebConfig -ActiveThemeName "ProofUp"
    ```

## <a name="next-steps"></a>次のステップ

[AD FS と Azure MFA によって使用される TLS/SSL プロトコルと暗号スイートを管理する](manage-ssl-protocols-in-ad-fs.md)
