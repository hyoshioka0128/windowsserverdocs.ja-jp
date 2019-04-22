---
ms.assetid: 24c4b9bb-928a-4118-acf1-5eb06c6b08e5
title: AD FS 2016 と Azure MFA を構成する
description: ''
ms.author: billmath
author: billmath
manager: mtillman
ms.date: 01/28/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: ae7809089a69ac0ff48168db0aa2e9d61c35257a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814093"
---
# <a name="configure-azure-mfa-as-authentication-provider-with-ad-fs"></a>Azure MFA と AD FS の認証プロバイダーとして構成します。

>適用先:Windows Server 2016、Windows Server 2019

組織が Azure AD と統合されて場合、は、セキュリティで保護された AD FS リソース、オンプレミスとクラウドに Azure Multi-factor Authentication を使用できます。 Azure MFA を使用すると、パスワードを排除し、認証するより安全な方法を提供できます。  以降 Windows Server 2016 では、今すぐ Azure MFA をプライマリ認証用に構成したり、追加の認証プロバイダーとして使用できます。 
  
Windows Server 2012 R2 では、AD FS と AD FS 2016 の Azure MFA アダプターは Azure AD と直接統合し、異なりオンプレミス Azure MFA サーバーには不要します。   Azure MFA アダプターが Windows Server 2016 に組み込まれているし、その他の必要はありません。


## <a name="registering-users-for-azure-mfa-with-ad-fs"></a>Azure MFA と AD FS のユーザーを登録します。

AD FS はインラインをサポートしていません&#34;プルーフ アップ&#34;、または電話番号やモバイル アプリなどのセキュリティ検証の情報を Azure MFA の登録。 つまり、ユーザーを参照してくださいをも取得する必要があります[ https://account.activedirectory.windowsazure.com/Proofup.aspx ](https://account.activedirectory.windowsazure.com/Proofup.aspx) AD FS アプリケーションへの認証に Azure MFA を使用する前にします。 ユーザーがいないまだもを AD FS での Azure MFA で認証しようと Azure AD でユーザー場合、AD FS のエラーが発生します。  AD FS 管理者は、代わりに、追加のセキュリティ確認 ページにユーザーを導くことには、このエラー エクスペリエンスをカスタマイズできます。  これを行う onload.js カスタマイズを使用して、AD FS ページ内のエラー メッセージ文字列を検出して、ガイドにアクセスするユーザーに新しいメッセージを表示する[ https://aka.ms/mfasetup ](https://aka.ms/mfasetup)、認証を再試行します。 詳細なガイダンス、"カスタマイズ、AD FS web ページを参照 MFA の確認方法を登録するユーザーをガイドする"の下の「します。

>[!NOTE]
> ユーザーが登録に MFA で認証を必要する以前は、(訪問[ https://account.activedirectory.windowsazure.com/Proofup.aspx ](https://account.activedirectory.windowsazure.com/Proofup.aspx)、たとえば、ショートカットを使用して[ https://aka.ms/mfasetup ](https://aka.ms/mfasetup))。  ユーザーが AD FS が MFA の検証の情報はまだ登録していないユーザーが Azure AD にアクセスするようになりましたが、&#34;ショートカットを使用して追加のセキュリティ確認ページ[ https://aka.ms/mfasetup ](https://aka.ms/mfasetup)プライマリ認証のみを使用して (Windows 統合認証など、またはユーザー名とパスワードを AD FS を使用して、web ページ)。  Azure AD がユーザーにメッセージが表示されるインライン登録を実行は構成された認証方法、ユーザーがない場合は、 &#34;、管理者にこのアカウントに追加のセキュリティ検査を設定することが必要な&#34;、後でユーザーは、選択する&#34;今すぐセットアップ&#34;します。
> 追加のセキュリティ確認 ページにアクセスしたときに MFA を提供する構成に少なくとも 1 つの MFA 認証方法を既に持っているユーザーも求められます。

## <a name="recommended-deployment-topologies"></a>推奨される展開トポロジ

### <a name="azure-mfa-as-primary-authentication"></a>プライマリ認証と azure MFA

プライマリ認証と AD FS と Azure MFA を使用する大きな理由のいくつがあります。

 - Office 365 やその他の AD FS アプリを Azure AD にサインイン用のパスワードを回避するには
 - パスワードを保護するには、ベースのサインイン、パスワードの前に検証コードなどの他の要素を要求することで

AD FS でのプライマリ認証方法として、これらのメリットを実現するために Azure MFA を使用する場合を Azure AD 条件付きアクセスなどを使用する機能を保持することも必要&#34;true MFA&#34;で AD FS での他の要素の入力を求めます。

今すぐこれを行うオンプレミスの MFA を実行する Azure AD ドメインの設定を構成することで (設定&#34;SupportsMfa&#34;を $True に)。  この構成で AD FS できます求めるメッセージが Azure AD によって追加の認証を実行するか、 &#34;MFA を true&#34;が必要な条件付きアクセス シナリオ用。  

前述のように、AD FS ユーザーが (構成されている MFA 認証情報) はまだ登録していないするように求められますカスタマイズされた AD FS エラー ページを参照してください[ https://aka.ms/mfasetup ](https://aka.ms/mfasetup)し検証情報を構成するにはAD FS ログインを再試行してください。  
後、初期構成のユーザーが管理または Azure ad での検証情報を更新するか、MFA を必要とするその他のリソースにアクセスする他の要素を提供する必要があります、主として、Azure MFA は、1 つの要因と見なされます。

>[!NOTE]
> ADFS の 2019年で Active Directory 要求プロバイダー信頼のアンカー要求の種類に変更を加えて、windowsaccountname から UPN へ変更を求められます。 実行、以下の powershell コマンドレットを次に示します。 これは、AD FS ファームの内部機能に影響を与えません。 この変更が確立されると、資格情報を少数のユーザーを reprompted 可能性がありますに注意してください可能性があります。 後もう一度ログインする、エンドユーザーは違いはわかりません。 

```powershell
Set-AdfsClaimsProviderTrust -AnchorClaimType "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn" -TargetName "Active Directory"
```

### <a name="azure-mfa-as-additional-authentication-to-office-365"></a>Office 365 に追加の認証としての azure MFA

以前は、させる場合 Azure MFA と AD FS での Office 365 またはその他の証明書利用者、最適なオプションの追加の認証方法をプライマリ認証が AD FS と MFA でのオンプレミスで実行される MFA を兼ねたは Azure AD を構成するのには trAzure AD によって iggered します。 現在、ドメイン SupportsMfa 設定が $True に設定されている場合は、AD FS で追加の認証と Azure MFA を使用できます。  

前述のように、AD FS ユーザーが (構成されている MFA 認証情報) はまだ登録していないするように求められますカスタマイズされた AD FS エラー ページを参照してください[ https://aka.ms/mfasetup ](https://aka.ms/mfasetup)し検証情報を構成するにはAD FS ログインを再試行してください。  

## <a name="pre-requisites"></a>前提条件

Azure MFA と AD FS 認証を使用したときに、次の前提条件が必要です。  
  
- [Azure サブスクリプションと Azure Active Directory](https://azure.microsoft.com/pricing/free-trial/)します。  
- [Azure Multi-factor Authentication](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/)  
- ポート 80 と 443 経由で web アプリケーション プロキシが communticate を次にできます。

    - https://adnotifications.windowsazure.com
    - https://login.microsoftonline.com


> [!NOTE]
> Azure AD と Azure MFA は Azure AD Premium や Enterprise Mobility Suite (EMS) に含まれます。  これらのいずれかがある場合、個別のサブスクリプションは必要ありません。
- Windows Server 2016 の AD FS のオンプレミス環境。  
   - サーバーは、ポート 80 と 443 経由で、次の Url と通信できる必要があります。
      - https://adnotifications.windowsazure.com
      - https://login.microsoftonline.com
- お使いのオンプレミス環境が[Azure AD とフェデレーションします。](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#configuring-federation-with-ad-fs)  
- [Windows PowerShell 用 Windows Azure Active Directory モジュール](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0)します。  
- Azure AD PowerShell を使用して構成する Azure AD のインスタンスのグローバル管理者権限。  
- エンタープライズ管理者の資格情報を Azure MFA の AD FS ファームを構成します。  
  
## <a name="configure-the-ad-fs-servers"></a>AD FS サーバーを構成します。

AD FS 用の Azure MFA の構成を完了するために説明されている手順を使用して各 AD FS サーバーを構成する必要があります。 

>[!NOTE]
>これらの手順を実行することを確認**すべて**ファーム内の AD FS サーバー。 ファームの複数の AD FS サーバーがある場合は、リモートで Azure AD Powershell を使用して、必要な構成を実行できます。  

### <a name="step-1-generate-a-certificate-for-azure-mfa-on-each-ad-fs-server-using-the-new-adfsazuremfatenantcertificate-cmdlet"></a>手順 1:Azure MFA の各 AD FS を使用してサーバー証明書の生成、`New-AdfsAzureMfaTenantCertificate`コマンドレット

最初に行う必要があるが、Azure MFA を使用する証明書を生成します。  これ行う PowerShell を使用します。  生成された証明書は、ローカル コンピューターの証明書ストアで見つかるし、Azure AD ディレクトリの TenantID を格納しているサブジェクト名を使用してマークします。

![AD FS と MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA3.png)  

TenantID が、Azure AD のディレクトリの名前をあるに注意してください。  次の PowerShell コマンドレットを使用すると、新しい証明書を生成できます。  
    `$certbase64 = New-AdfsAzureMfaTenantCertificate -TenantID <tenantID>`  

![AD FS と MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA1.PNG)  
  
### <a name="step-2-add-the-new-credentials-to-the-azure-multi-factor-auth-client-service-principal"></a>手順 2:新しい資格情報を Azure Multi-factor Auth クライアント サービス プリンシパルの追加します。

Azure 多要素認証のクライアントとの通信に AD FS サーバーを有効にするためには、Azure 多要素認証のクライアントのサービス プリンシパルの資格情報を追加する必要があります。 使用して生成された証明書、`New-AdfsAzureMFaTenantCertificate`コマンドレットは、これらの資格情報として使用されます。 次の操作に Azure 多要素認証クライアント サービス プリンシパルを追加するには、新しい資格情報を PowerShell を使用します。  

> [!NOTE]
> この手順を完了するためには、Connect-msolservice を使用して PowerShell を使用した Azure AD のインスタンスに接続する必要があります。  次の手順では、PowerShell を使用して既に接続するいると仮定します。  については、次を参照してください。 [Connect-msolservice します。](https://msdn.microsoft.com/library/dn194123.aspx)  

**Azure 多要素認証のクライアントに対して、新しい資格情報として証明書を設定します。**  

`New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type asymmetric -Usage verify -Value $certBase64`

> [!IMPORTANT]
> このコマンドは、すべてのファームで AD FS サーバーで実行する必要があります。  Azure AD MFA は、Azure 多要素認証のクライアントに対して、新しい資格情報として設定される証明書がないサーバーで失敗します。

> [!NOTE]  
> 981f26a1-7f43-403b-a875-f8b09b8cd720 は、Azure 多要素認証のクライアントの GUID です。  
  
## <a name="configure-the-ad-fs-farm"></a>AD FS ファームを構成します。  
  
各 AD FS サーバーで、前のセクションを完了すると、実行する必要があります、`Set-AdfsAzureMfaTenant`コマンドレット。  
  
このコマンドレットは、AD FS ファームに 1 回だけ実行する必要があります。  PowerShell を使用して、この手順を完了します。
  
> [!NOTE]  
> これらの変更を有効にする前に、ファーム内の各サーバーで AD FS サービスを再起動する必要があります。  
  
    Set-AdfsAzureMfaTenant -TenantId <tenant ID> -ClientId 981f26a1-7f43-403b-a875-f8b09b8cd720  

![AD FS と MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA5.png)  
  
その後、Azure MFA はイントラネットとエクストラネットの使用のためのプライマリ認証方法として使用できることがわかります。    
  
![AD FS と MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA6.png)  

## <a name="renew-and-manage-ad-fs-azure-mfa-certificates"></a>更新して、AD FS の Azure 管理証明書の MFA

次のガイダンスでは、AD FS サーバー上の Azure MFA 証明書を管理する方法について説明します。
既定では、Azure MFA と AD FS を構成するときに新規 AdfsAzureMfaTenantCertificate PowerShell コマンドレットを使用して生成された証明書は有効な 2 年間です。  近い方法を決定する有効期限、証明書を更新して新しい証明書をインストールし、次の手順を使用します。

### <a name="assess-ad-fs-azure-mfa-certificate-expiration-date"></a>AD FS の Azure MFA 証明書の有効期限日を評価します。

ローカル コンピューターで、各 AD FS サーバーで、My ストアに自己署名証明書があります&#34;OU = Microsoft AD FS の Azure MFA&#34;発行者とサブジェクトで。  これは、Azure MFA 証明書です。  有効期限を決定するには、各 AD FS サーバーでこの証明書の有効期間を確認します。  

### <a name="create-new-ad-fs-azure-mfa-certificate-on-each-ad-fs-server"></a>各 AD FS サーバーで新しい AD FS の Azure MFA 証明を作成します。

場合は、証明書の有効期間には、その終了が近づいている、各 AD FS サーバーで、新しい Azure MFA 証明書を生成することによって、更新手続きを開始します。 Powershell コマンド ウィンドウで、次のコマンドレットを使用して各 AD FS サーバーで新しい証明書を生成します。

```
PS C:\> $newcert = New-AdfsAzureMfaTenantCertificate -TenantId <tenant id such as contoso.onmicrosoft.com> -Renew $true
```

このコマンドレットでは、結果として、2 日 + 2 年に 2 日後から有効な新しい証明書が生成されます。  AD FS と Azure MFA の操作はこのコマンドレットまたは新しい証明書を受けません。 (注: 2 日間の遅延が意図的なものし、AD FS が Azure MFA の使用を開始する前に、テナントで新しい証明書を構成する次の手順を実行する時刻を提供します)。

### <a name="configure-each-new-ad-fs-azure-mfa-certificate-in-the-azure-ad-tenant"></a>Azure AD テナントで新しい AD FS の Azure MFA の各証明書を構成します。

次のように Azure AD テナントの設定を更新する (各 AD FS サーバー上)、新しい各証明書、Azure AD PowerShell モジュールを使用して (注: Connect-msolservice を使用して、次のコマンドを実行してテナントに初めて接続する必要があります)。

```
PS C:/> New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type Asymmetric -Usage Verify -Value $newcert
```

$certbase64 は、新しい証明書です。  Base64 でエンコードされた証明書を DER エンコード ファイルと、Notepad.exe で開き、PSH セッションにコピー/貼り付けられると certbase64 $ 変数に割り当てることとして、(秘密キー) を含まない証明書をエクスポートすることによって取得できます。

### <a name="verify-that-the-new-certificates-will-be-used-for-azure-mfa"></a>Azure MFA の新しい証明書が使用されることを確認します。

新しい証明書が有効になると AD FS がピックアップして、1 日に数時間以内に Azure MFA のそれぞれの各証明書の使用を開始します。  これが発生した場合、各サーバーで表示されます、次の情報を AD FS 管理者イベント ログに記録されたイベント。ログ名:    AD FS/管理者ソース:      AD FS 日:        2018 年 2 月 27 日午後 7時 33分: 31 イベント ID:    547 タスク カテゴリ:None レベルします。       情報のキーワード:    AD FS のユーザー:        DOMAIN\adfssvc コンピューター:    ADFS.domain.contoso.com 説明:Azure mfa テナント証明書が更新されました。  

TenantId: contoso.onmicrosoft.com です。
古い拇印:7CC103D60967318A11D8C51C289EF85214D9FC63.
古い期限:9/15/2019 9時 43分: 17 PM。
新しい拇印:8110D7415744C9D4D5A4A6309499F7B48B5F3CCF.
新しい有効期限:2020 27/2/2時 16分: 07 AM。

## <a name="customize-the-ad-fs-web-page-to-guide-users-to-register-mfa-verification-methods"></a>MFA の確認方法を登録するユーザーをガイドする AD FS web ページをカスタマイズします。

次の例を検証しましたがないユーザーの AD FS web ページをカスタマイズする (構成の検証については MFA) を使用します。

### <a name="find-the-error"></a>エラーを検索します。

最初に、いくつかのさまざまなエラー メッセージをユーザーが認証情報を持っていない場合は、AD FS が返されます。
プライマリ認証と Azure MFA を使用する場合、校正しました。 されていないユーザーは、次のメッセージを格納している AD FS エラー ページに表示されます。
```
    <div id="errorArea">
        <div id="openingMessage" class="groupMargin bigText">
            An error occurred
        </div>
        <div id="errorMessage" class="groupMargin">
            Authentication attempt failed. Select a different sign in option or close the web browser and sign in again. Contact your administrator for more information.
        </div>
```
追加の認証としての Azure AD が試行されていない校正済みのユーザーに、次のメッセージを格納している AD FS エラー ページが表示されます。
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

### <a name="catch-the-error-and-update-the-page-text"></a>エラーをキャッチし、ページのテキストを更新

エラーをキャッチし、ユーザーに表示するには、カスタム ガイダンスは単に AD FS web テーマの一部である onload.js ファイルの末尾に、javascript を追加します。  これにより、次の操作を行います。
 - 特定のエラー文字列の検索
 - カスタムの web コンテンツを提供します。  

(Onload.js ファイルをカスタマイズする方法の一般的なガイダンスについては、この記事を参照してください[Advanced Customization of AD FS サインイン ページ](advanced-customization-of-ad-fs-sign-in-pages.md)。)。

簡単な例を次に示しますを拡張したい場合があります。

1. プライマリ AD FS サーバーで Windows PowerShell を開き、次のコマンドを実行して、新しい AD FS Web テーマを作成します。
    
    ``` PowerShell
        New-AdfsWebTheme –Name ProofUp –SourceName default
    ``` 
2. 次に、既定の AD FS Web テーマをエクスポートします。

    ``` PowerShell
       Export-AdfsWebTheme –Name default –DirectoryPath c:\Theme
    ```
3. テキスト エディターで C:\Theme\script\onload.js ファイルを開く
4. Onload.js ファイルの末尾に次のコードを追加します。
    
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

    //End Customize MFA Exception
    //End Custom Code
    ```
    > [!IMPORTANT]
    > "YOUR_DOMAIN_NAME_HERE < >"; を変更する必要があります。ドメイン名を使用します。 たとえば次のようになります。`var domain_hint = "contoso.com";`
    
5. Onload.js ファイルを保存します。
6. 次の Windows PowerShell コマンドを入力して、カスタム テーマに onload.js ファイルをインポートします。
    
    ``` PowerShell
    Set-AdfsWebTheme -TargetName ProofUp -AdditionalFileResource @{Uri=’/adfs/portal/script/onload.js’;path="c:\theme\script\onload.js"}
    ```
7. 最後に、次の Windows PowerShell コマンドを入力して、カスタムの AD FS Web テーマが適用されます。
    
    ``` PowerShell
    Set-AdfsWebConfig -ActiveThemeName
    ```

## <a name="next-steps"></a>次のステップ

[TLS と SSL プロトコルと AD FS と Azure MFA で使用される暗号スイートを管理します。](manage-ssl-protocols-in-ad-fs.md)
