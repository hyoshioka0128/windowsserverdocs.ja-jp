---
ms.assetid: 24c4b9bb-928a-4118-acf1-5eb06c6b08e5
title: "AD FS 2016 と Azure MFA を構成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 11/01/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: be8e88ae36f344f1265fb76e66c19e0ac8aeb533
ms.sourcegitcommit: ffdfbb76c7f775e20d089d3f662d4f9a7d642f1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2018
---
# <a name="configure-ad-fs-2016-and-azure-mfa"></a>AD FS 2016 と Azure MFA を構成します。

>Windows Server 2016 の適用対象:

組織は Azure AD とフェデレーションされた場合、は、セキュリティで保護された AD FS リソース、オンプレミスとクラウドに Azure Multi-factor Authentication を使用できます。 Azure MFA を使用すると、パスワードを排除しより安全な認証方法を提供できます。  Windows Server 2016 以降では、プライマリ認証に Azure MFA を構成することができますようになりました。 
  
異なり Windows Server 2012 R2 で AD FS と AD FS 2016 Azure MFA アダプターは Azure AD と直接統合し、オンプレミス Azure MFA のサーバーには必要ありません。   Azure MFA アダプターが、Windows Server 2016 に組み込まれているし、追加のインストールの必要はありません。

## <a name="registering-users-for-azure-mfa-with-ad-fs-2016"></a>Registering users for Azure MFA with AD FS 2016
AD FS は、インライン「実証を」、または Azure MFA のセキュリティ確認情報など、電話番号またはモバイル アプリの登録をサポートしていません。 つまり、ユーザーを AD FS のアプリケーションへの認証に Azure MFA を使用する前に https://account.activedirectory.windowsazure.com/Proofup.aspx にアクセス可能なを取得する必要があります。 ときに、ユーザーがいないまだわたってを AD FS での Azure MFA を使用して認証する Azure AD の試行で、AD FS エラーが表示されます。  AD FS 管理者は、proofup ページの代わりに、ユーザー ガイドには、このエラー エクスペリエンスをカスタマイズできます。  AD FS ページ内にエラー メッセージ文字列を検出し、新しい https://aka.ms/mfasetup にアクセスするユーザーを案内メッセージを表示する onload.js カスタマイズを使ってこれを実行し、再認証を試行できます。 詳細なガイダンスを参照してください「カスタマイズ、AD FS Web ページの検証の MFA 方法を登録するユーザーのガイドに」の下の「します。

>[!NOTE]
> 以前は、ユーザー (訪問 https://account.activedirectory.windowsazure.com/Proofup.aspx、ショートカット aka.ms/mfasetup 経由など) の登録の MFA で認証する必要があります。  MFA の検証の詳細についてはまだ登録していない AD FS ユーザーを使用して Azure AD にアクセスできるようになりましたのショートカット aka.ms/mfasetup を介して proofup ページなどを使用してのみプライマリ認証 (Windows 統合認証またはユーザー名とパスワードを AD FS を介したは Web ページ).  構成の検証方法、ユーザーがいない場合は、Azure AD は、ユーザーにメッセージが表示されるインライン登録「、管理者が必要な追加のセキュリティ確認のためには、このアカウントを設定する」、ユーザーを選択して、"これを設定するようになりました」。
> 構成されている少なくとも 1 つの MFA の検証方法を既に持っているユーザーは引き続き proofup ページにアクセスしたときに MFA を提供するように求められます。

### <a name="recommended-deployment-topologies"></a>推奨される展開トポロジ

#### <a name="azure-mfa-as-primary-authentication"></a>プライマリ認証と azure MFA
これには、いくつかのプライマリ認証に AD FS と Azure MFA を使用する大きな理由があります。
 - Office 365 やその他の AD FS のアプリを Azure AD にサインインにパスワードを回避するには
 - パスワードを保護してベースのサインインにパスワードの前に確認コードなどの他の要素を要求することで

AD FS でのプライマリ認証方法として、これらのメリットを実現するために Azure MFA を使用する場合、条件付き Azure AD を使用する機能を維持することも必要"true MFA"を求めることでその他の要因の AD fs を含むアクセスします。

これをオンプレミス (を $True に設定"SupportsMfa") で MFA を行うには、Azure AD ドメインの設定を構成することによって今すぐ実行できます。  この構成では、それを必要とする条件付きアクセス シナリオの追加の認証または"場合は true。MFA"を実行する、Azure AD によって、AD FS を求められます。  

前述のように、AD FS 持つユーザーは登録されている (構成されている MFA 検証情報) はカスタマイズされた AD FS のエラー ページを使用して、検証の情報を構成する aka.ms/mfasetup を参照してくださいするように求められます必要がありますいないし、再度試みます AD FS ログインします。  
初期構成のユーザーは、その他の要素を管理または Azure AD での検証の情報を更新するか、MFA を必要とするその他のリソースにアクセスを提供する必要があります後、プライマリとして Azure MFA は、1 つの要因と見なされます。


#### <a name="azure-mfa-as-additional-authentication-to-office-365"></a>Office 365 に追加の認証として azure MFA
以前は、希望する場合は、Azure MFA と AD FS での Office 365 やその他の証明書利用者、最適なオプションの追加の認証方法をオンプレミスの AD FS で MFA をプライマリ認証が実行される、MFA を複合は Azure AD を構成するのには trAzure AD によって iggered します。 これで、ドメイン SupportsMfa 設定が $True に設定されている場合は、AD FS で追加の認証として Azure MFA を使用できます。  

前述のように、AD FS 持つユーザーは登録されている (構成されている MFA 検証情報) はカスタマイズされた AD FS のエラー ページを使用して、検証の情報を構成する aka.ms/mfasetup を参照してくださいするように求められます必要がありますいないし、再度試みます AD FS ログインします。  


## <a name="pre-requisites"></a>前提条件  
Azure MFA を AD FS での認証を使用する場合、次の前提条件が必要です。  
  
- [Azure Active Directory と Azure サブスクリプションを](https://azure.microsoft.com/pricing/free-trial/)します。  
- [Azure 多要素認証](https://azure.microsoft.com/documentation/articles/multi-factor-authentication/)  

>[!NOTE]   
> Azure AD と Azure MFA は、Azure AD Premium と Enterprise Mobility Suite (EMS) に含まれています。  これらのいずれかがある場合、個々 のサブスクリプションは必要ありません。   
- Windows Server 2016 の AD FS 内部設置型の環境です。  
- オンプレミス環境で[Azure AD と統合します。](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#configuring-federation-with-ad-fs)  
- [Windows Azure Active Directory Module for Windows PowerShell](https://go.microsoft.com/fwlink/p/?linkid=236297).  
- グローバル管理者のアクセス許可で Azure AD のインスタンスを Azure AD PowerShell を使用して構成します。  
- エンタープライズ管理者の資格情報を Azure MFA の AD FS ファームを構成します。  
  
  
## <a name="configure-the-ad-fs-servers"></a>AD FS サーバーを構成します。  
Azure MFA の AD FS の構成を完了するためには、説明されている手順を使用して各 AD FS サーバーを構成する必要があります。 

>[!NOTE]
>これらの手順を実行することを確認**すべて**ファーム内の AD FS サーバー。 複数の AD FS サーバーがある場合は、ファームで、Azure AD Powershell を使用してリモートで必要な構成を実行できます。  
  
  
  
### <a name="step-1-generate-a-certificate-for-azure-mfa-on-each-ad-fs-server-using-the-new-adfsazuremfatenantcertificate-cmdlet"></a>手順 1: Azure MFA の各 AD FS を使用してサーバーに証明書を生成する、`New-AdfsAzureMfaTenantCertificate`コマンドレット。   
最初に行う必要がありますが、Azure MFA を使用するための証明書を生成します。  これを行う PowerShell を使用します。  生成された証明書は、ローカル コンピューターの証明書ストアのあり、Azure AD ディレクトリを TenantID が含まれているサブジェクト名が付いています。    
  
![AD FS と MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA3.png)  
  
TenantID の Azure AD でのディレクトリの名前ことに注意してください。  次の PowerShell コマンドレットを使用して、新しい証明書を生成します。  
    `$certbase64 = New-AdfsAzureMfaTenantCertificate -TenantID <tenantID>`  
      
![AD FS と MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA1.PNG)  
  
### <a name="step-2-add-the-new-credentials-to-azure-multi-factor-auth-client-spn"></a>手順 2: Azure 多要素認証クライアント SPN に新しい資格情報を追加します。   
Azure の Multi-factor Auth クライアントと通信するための AD FS サーバーを有効にするためには、SPN に Azure の Multi-factor Auth クライアント用の資格情報を追加する必要があります。 証明書を使用して生成、`New-AdfsAzureMFaTenantCertificate`コマンドレットは、これらの資格情報として機能します。 次の操作 PowerShell を使用して、Azure の Multi-factor Auth クライアント SPN に新しい資格情報を追加します。  

>[!NOTE]   
>この手順を完了するためには、powershell Connect-MsolService で Azure AD のインスタンスに接続する必要があります。  次の手順では、PowerShell を使用して既に接続するいると仮定します。  詳細については、次を参照してください。[Connect-msolservice します。](https://msdn.microsoft.com/library/dn194123.aspx)  
     
  
2. **Azure の Multi-factor Auth クライアントに対して新しい資格情報として、証明書を設定します。**  
    
    `New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type asymmetric -Usage verify -Value $certBase64 `

>[!IMPORTANT]
>  This command needs to be run on all of the AD FS servers in your farm.  Azure AD MFA will fail on servers that have not have the certificate set as the new credential against the Azure Multi-Factor Auth Client. 

>[!NOTE]  
> 981f26a1-7f43-403b-a875-f8b09b8cd720 は、Azure の Multi-factor Auth クライアントの guid です。  
  
## <a name="configure-the-ad-fs-farm"></a>AD FS ファームを構成します。  
  
各 AD FS サーバーで、前のセクションを完了するを実行する必要があります、`Set-AdfsAzureMfaTenant`コマンドレット。  
  
このコマンドレットは、AD FS ファーム用に 1 回だけ実行する必要があります。  この手順を完了するのにには、PowerShell を使用します。    
  
>[!NOTE]  
>これらの変更を有効にする前に、ファーム内の各サーバーに AD FS サービスを再起動する必要があります。  
  
    Set-AdfsAzureMfaTenant -TenantId <tenant ID> -ClientId 981f26a1-7f43-403b-a875-f8b09b8cd720  
      
![AD FS と MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA5.png)  
  
その後、Azure MFA が使用可能にイントラネットとエクストラネットのプライマリ認証方法として表示されます。    
  
![AD FS と MFA](media/Configure-AD-FS-2016-and-Azure-MFA/ADFS_AzureMFA6.png)  

## <a name="renew-and-manage-ad-fs-azure-mfa-certificates"></a>更新し、AD FS の Azure 管理証明書の MFA
次のガイダンスでは、AD FS サーバー上の Azure MFA 証明書を管理する方法を見ていきます。
既定では、Azure MFA を使用して AD FS を構成するときに、New-AdfsAzureMfaTenantCertificate PowerShell コマンドレットによって生成された証明書は有効 2 年間です。  閉じるに方法を決定する有効期限、証明書は、更新を新しい証明書のインストールは、次の手順を使用しています。

### <a name="assess-ad-fs-azure-mfa-certificate-expiration-date"></a>AD FS Azure MFA の証明書の有効期限の日付を評価します。
各 AD FS サーバーで、ローカル コンピューターの My ストアに自己署名証明書がある"OU = Microsoft AD FS Azure MFA"」サブジェクトと発行者にします。  これは、Azure MFA の証明書です。  この証明書の有効期限日を確認するには、各 AD FS サーバーの有効期間を確認します。  

### <a name="create-new-ad-fs-azure-mfa-certificate-on-each-ad-fs-server"></a>各 AD FS サーバーで新しい AD FS Azure MFA 証明を作成します。
証明書の有効期間の最後に近づいています場合、は、各 AD FS サーバーで新しい Azure MFA の証明書を生成することによって更新処理を開始します。 Powershell のコマンド ウィンドウで、次のコマンドレットを使用して AD FS サーバーごとに新しい証明書を生成します。

```
PS C:\> $newcert = New-AdfsAzureMfaTenantCertificate -TenantId <tenant id such as contoso.onmicrosoft.com> -Renew $true
```

このコマンドレットの結果として、2 日 + 2 年に 2 日間、今後から有効な新しい証明書が生成されます。  AD FS と Azure MFA の操作は、このコマンドレットで新しい証明書は影響しません。 (注: 2 日の延期が意図的なものと AD FS では、Azure MFA を使用することが始まる前に、テナントで新しい証明書を構成するには、次の手順を実行する時刻を提供します)。


### <a name="configure-each-new-ad-fs-azure-mfa-certificate-in-the-azure-ad-tenant"></a>Azure AD テナントで新しい AD FS Azure MFA の各証明書を構成します。
次のようには、Azure AD テナントの設定の更新プログラム (サーバーごとに AD FS) の新しい証明書をごとに、Azure AD PowerShell モジュールを使用して (注: 最初 Connect-MsolService 次のコマンドを実行する)。

```
PS C:/> New-MsolServicePrincipalCredential -AppPrincipalId 981f26a1-7f43-403b-a875-f8b09b8cd720 -Type Asymmetric -Usage Verify -Value $certbase64
```
    Where $certbase64 is the new certificate.  The base64 encoded certificate can be obtained by exporting the certificate (without the private key) as a DER encoded file and opening in Notepad.exe, then copy/pasting to the PSH session and assigning to the variable $certbase64

### <a name="verify-that-the-new-certificates-will-be-used-for-azure-mfa"></a>Azure MFA に対して新しい証明書を使用することを確認します。
1 回、新しい証明書有効になります、AD FS はそれらを選択および Azure MFA に対して 1 日には数時間内で各それぞれの証明書の使用を開始します。  この問題が発生すると、各サーバーで表示されます、次の情報を AD FS 管理者イベント ログに記録イベント: ログ名: AD Fs/admin] ソース: AD FS の日付: 2/27/2018 午後 7時 33分: 31 イベント ID: 547 タスク カテゴリ: None レベル: 情報キーワード: AD FS のユーザー: DOMAIN\adfssvc コンピューター: ADFS.domain.contoso.com 説明: Azure MFA のテナントの証明書が更新されています。  

TenantId: contoso.onmicrosoft.com します。古い拇印: 7CC103D60967318A11D8C51C289EF85214D9FC63 します。 有効期限の日付以前: 2019/9/15 午後 9時 43分: 17 します。 新しい拇印: 8110D7415744C9D4D5A4A6309499F7B48B5F3CCF します。 新しい有効期限: 2/27/2020 2時 16分: 07 します。

## <a name="customize-the-ad-fs-web-page-to-guide-users-to-register-mfa-verification-methods"></a>ユーザー登録の検証の MFA 方法を説明する AD FS Web ページをカスタマイズします。

次の例を可能ながないユーザーのため、AD FS Web ページをカスタマイズする (構成されている MFA 検証情報) を使用します。

### <a name="find-the-error"></a>エラーを検索します。
最初は、いくつかのさまざまなエラー メッセージがユーザーに確認情報が持っていない場合は、AD FS が返されます。
プライマリ認証として Azure MFA を使用している、校正したされていないユーザーは、次のメッセージが含まれている AD FS のエラー ページに表示されます。
```
    <div id="errorArea"> 
        <div id="openingMessage" class="groupMargin bigText">
            An error occurred 
        </div> 
        <div id="errorMessage" class="groupMargin">
            Authentication attempt failed. Select a different sign in option or close the web browser and sign in again. Contact your administrator for more information. 
        </div>
```
Azure AD と追加の認証が試行されているときに校正したされていないユーザーには、次のメッセージが含まれている AD FS のエラー ページが表示されます。
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

### <a name="catch-the-error-and-update-the-page-text"></a>エラーを検出し、ページのテキストを更新
エラーをキャッチの表示とユーザー カスタムのガイダンスは、javascript を AD FS の一部である onload.js ファイルの末尾に追加の問題 Web テーマを (1) 検索エラー文字列を識別し、(2) ユーザー設定を提供します。Web コンテンツです。  (Onload.js ファイルをカスタマイズする方法に関する一般的なガイダンスについては、記事を参照してください[ここ](https://docs.microsoft.com/en-us/windows-server/identity/ad-fs/operations/advanced-customization-of-ad-fs-sign-in-pages)。)。

