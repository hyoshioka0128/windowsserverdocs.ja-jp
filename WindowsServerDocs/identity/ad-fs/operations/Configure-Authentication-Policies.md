---
ms.assetid: 8e7015bc-c489-4ec7-8b6e-3ece90f72317
title: "認証ポリシーを構成します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 7faffb7ccbb4b0ea3c65329d18f915d7dafcd46f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="configure-authentication-policies"></a>認証ポリシーを構成します。

>Windows Server 2012 R2 の適用対象:

Windows Server 2012 R2 での AD FS で両方のアクセス制御と認証メカニズムに強化され、ユーザー、デバイス、場所、および認証データを含む複数の要因です。 これらの拡張機能を有効にする、ユーザー インターフェイス、またはマルチ要素アクセス制御やはユーザーの id またはグループのメンバーシップ、ネットワークの場所、workplace\ に参加しているはデバイスのデータに基づいているため、複数要素認証を介した広告 FS\ で保護されたアプリケーションへのアクセス許可を付与するリスクを管理する、Windows PowerShell とマルチ要素認証 \(MFA\) されたときに、認証状態を通じて実行されます。  
  
Windows Server 2012 R2 で Active Directory フェデレーション サービス \(AD FS\) での MFA およびマルチ要素のアクセス制御の詳細については、次のトピックを参照してください。  


-   [Join to Workplace from 任意のデバイス用の SSO とシームレスな 2 要素認証を企業アプリケーション間で](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)

-   [条件付きアクセス制御によるリスクを管理します。](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md)

-   [追加の多要素認証による個人情報アプリケーションのリスクを管理します。](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

## <a name="configure-authentication-policies-via-the-ad-fs-management-snap-in"></a>AD FS 管理スナップインを使用して認証ポリシーを構成します。  
メンバーシップ**管理者**、または相当するもので、ローカル コンピューターが最小要件を次の手順を完了します。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   
  
Windows Server 2012 R2 での AD FS では、すべてのアプリケーションや AD FS によって保護されたサービスに適用されるグローバル スコープで認証ポリシーを指定できます。 特定のアプリケーションとサービスを信頼に基づいており、AD FS によって保護された認証ポリシーを設定することもできます。 証明書利用者ごとの特定のアプリケーションの認証ポリシーの指定の信頼では、グローバル認証ポリシーは上書きされません。 グローバルまたは証明書利用者ごとの場合、ユーザーがこの証明書利用者信頼に対して認証するときに、[信頼の認証ポリシーには、MFA、MFA が必要ですがトリガーされます。 グローバル認証ポリシーは、代替の証明書利用者信頼のアプリケーションとサービスが構成されている特定の認証ポリシーがないです。 

## <a name="to-configure-primary-authentication-globally-in-windows-server-2012-r2"></a>Windows Server 2012 R2 でグローバル プライマリ認証を構成するには 
  
1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  AD FS スナップイン、] をクリックして**認証ポリシー**します。  
  
3.  **プライマリ認証**セクションで、をクリックして**編集**] の横に**グローバル設定**します。 右クリックすることも**認証ポリシー**、] を選択して**グローバル プライマリ認証の編集**、または下にある、**アクション**ウィンドウで、**グローバル プライマリ認証の編集**します。  
![認証ポリシー](media/Configure-Authentication-Policies/authpolicy1.png)
  
4.  **グローバル認証ポリシーの編集**ウィンドウ] の [、**プライマリ**] タブの [グローバル認証ポリシーの一部として、次の設定を構成することができます。  
  
    -   プライマリ認証に使用する認証方法です。 [使用できる認証方法を選択することができます、**エクストラネット**と**イントラネット**します。  
  
    -   デバイス認証を使用して、**デバイス認証を有効にする**チェック ボックスをオンします。 詳細については、次を参照してください。[任意のデバイスからの SSO とシームレスな 2 つ目 Factor Authentication Across Company Applications 職場への参加](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)します。  
![認証ポリシー](media/Configure-Authentication-Policies/authpolicy2.png)  

## <a name="to-configure-primary-authentication-per-relying-party-trust"></a>証明書利用者ごとのプライマリ認証を構成するパーティの信頼  
  
1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  AD FS スナップイン、] をクリックして**認証ポリシー**\\**あたり証明書利用者信頼**、証明書利用者信頼の認証ポリシーを構成する] をクリックします。  
  
3.  いずれか右クリック、証明書利用者信頼を認証ポリシーを構成し、を選択する**カスタム プライマリ認証の編集**、または下にある、**アクション**ウィンドウで、**カスタム プライマリ認証の編集**します。  
![認証ポリシー](media/Configure-Authentication-Policies/authpolicy5.png)   

4.  **< Relying\_party\_trust\_name > の認証ポリシーの編集**ウィンドウ下で、**プライマリ**] タブの一部として、次の設定を構成することができます、**あたり Relying Party Trust**認証ポリシー。  
  
    -   ユーザーがサインインに毎回自分の資格情報を提供するために必要かどうかによって、**ユーザーがサインインに毎回自分の資格情報を提供する必要が**チェック ボックスをオンします。  
![認証ポリシー](media/Configure-Authentication-Policies/authpolicy6.png) 

## <a name="to-configure-multi-factor-authentication-globally"></a>グローバルに multi-factor authentication を構成するには  
  
1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  AD FS スナップイン、] をクリックして**認証ポリシー**します。  
  
3.  **マルチ要素認証**セクションで、をクリックして**編集**] の横に**グローバル設定**します。 右クリックすることも**認証ポリシー**、] を選択し、**グローバル編集のマルチ要素認証**、または下にある、**アクション**ウィンドウで、**マルチ要素認証の編集グローバル**します。  
![認証ポリシー](media/Configure-Authentication-Policies/authpolicy8.png)   

4.  **グローバル認証ポリシーの編集**ウィンドウ下で、**マルチ要素**] タブで、マルチ要素のグローバル認証ポリシーの一部として、次の設定を構成することができます。  
  
    -   設定または [利用可能なオプションを使用して MFA の条件、 **Users\/グループ**、**デバイス**、および**場所**セクションです。  
  
    -   これらの設定のいずれかに対して MFA を有効にするには、少なくとも 1 つの追加の認証方法を選択してください。 **証明書の認証**既定の利用可能なオプションです。 たとえば、Windows Azure Active Authentication、他のカスタムの追加の認証方法を構成することもできます。 詳細については、次を参照してください。[チュートリアル ガイド: 追加の多要素認証による個人情報アプリケーションのリスク管理](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)します。  
  
> [!WARNING]  
> 追加の認証方法をグローバルにのみ構成できます。  
![認証ポリシー](media/Configure-Authentication-Policies/authpolicy9.png)  

## <a name="to-configure-multi-factor-authentication-per-relying-party-trust"></a>証明書利用者ごとのマルチ要素認証を構成するパーティの信頼  
  
1.  サーバー マネージャーで、クリックして**ツール**、し、[ **AD FS 管理**します。  
  
2.  AD FS スナップイン、] をクリックして**認証ポリシー**\\**あたり証明書利用者信頼**、証明書利用者信頼 MFA を構成する] をクリックします。  
  
3.  か右クリック、証明書利用者の信頼、MFA を構成して、を選択する**マルチ要素認証のユーザー設定の編集**、または下にある、**アクション**ウィンドウで、**マルチ要素認証のユーザー設定の編集**します。  
  
4.  **< Relying\_party\_trust\_name > の認証ポリシーの編集**ウィンドウ下で、**マルチ要素**] タブの一部として、次の設定を構成することができます、ごとに証明書利用者信頼の認証ポリシー。  
  
    -   設定または [利用可能なオプションを使用して MFA の条件、 **Users\/グループ**、**デバイス**、および**場所**セクションです。  

## <a name="configure-authentication-policies-via-windows-powershell"></a>Windows PowerShell を使用して認証ポリシーを構成します。  
Windows PowerShell はより柔軟なアクセス制御のさまざまな要因を使用してを有効にして認証ポリシーと認証を構成する Windows Server 2012 R2 の AD FS で使用できる認証メカニズム ルールが true の条件付きアクセスの AD FS \-secured リソースを実装する必要があります。  
  
管理者、またはそれと同等のローカル コンピューター上、メンバーシップは、これらの手順を完了する最低限必要です。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)\ (http:///\/go.microsoft.com\/fwlink\/ですか?LinkId\ = 83477\)。   
  
### <a name="to-configure-an-additional-authentication-method-via-windows-powershell"></a>Windows PowerShell を使用して、追加の認証方法を構成するには  
  
1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  
  

    `Set-AdfsGlobalAuthenticationPolicy –AdditionalAuthenticationProvider CertificateAuthentication  `

  
> [!WARNING]  
> このコマンドが正常に実行された、実行できることを確認する、`Get-AdfsGlobalAuthenticationPolicy`コマンド。  
  
### <a name="to-configure-mfa-per-relying-party-trust-that-is-based-on-a-users-group-membership-data"></a>MFA ごとに証明書利用者を構成するのには、ユーザーのグループ メンバーシップ データに基づいているパーティーの信頼  
  
1.  フェデレーション サーバーで Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  
  

    `$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust`  
  
  
> [!WARNING]  
> 置き換えることを確認して*< relying\_party\_trust >* 、証明書利用者信頼の名前にします。  
  
2.  同じ Windows PowerShell コマンド ウィンドウで、次のコマンドを実行します。  
  
 
    $MfaClaimRule ="c: [型 = = '"https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid'"、値 = ~ '"^(?i) < group_SID >$ '"] = > 問題 (型 = '"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'"、値 '"https://schemas.microsoft.com/claims/multipleauthn'")"。 
    
    セット AdfsRelyingPartyTrust – TargetRelyingParty $rp – AdditionalAuthenticationRules $MfaClaimRule
  
  
> [!NOTE]  
> セキュリティ識別子の値を < group\_SID > を置き換えることを確認して、Active Directory \(AD\) グループの \(SID\) します。  
  
### <a name="to-configure-mfa-globally-based-on-users-group-membership-data"></a>グローバル ユーザーのグループ メンバーシップ データに基づく MFA を構成するには  
  
1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  
  

    $MfaClaimRule ="c: [型 = = '"https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid'"、値 = = '"group_SID'"]  
     = > 問題 (型 = '"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'"、値 = '"https://schemas.microsoft.com/claims/multipleauthn'")"。  
      
    セット AdfsAdditionalAuthenticationRule $MfaClaimRule  

  
> [!NOTE]  
> 置き換えることを確認して*< group\_SID >* AD グループの SID の値。  
  
### <a name="to-configure-mfa-globally-based-on-users-location"></a>グローバル ユーザーの位置情報に基づく MFA を構成するには  
  
1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  
  
 
    $MfaClaimRule ="c: [型 = = '"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork'"、値 = = '"true_or_false'"]  
     = > 問題 (型 = '"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'"、値 = '"https://schemas.microsoft.com/claims/multipleauthn'")"。  
  
    セット AdfsAdditionalAuthenticationRule $MfaClaimRule  
  

  
> [!NOTE]  
> 置き換えることを確認して*< true\_or\_false >*いずれかで`true`または`false`します。 値は、エクストラネットまたはイントラネットからアクセス要求を送信するかどうかに基づいて、特定の規則の条件によって異なります。  
  
### <a name="to-configure-mfa-globally-based-on-users-device-data"></a>グローバル ユーザーのデバイスのデータに基づく MFA を構成するには  
  
1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  
  

    $MfaClaimRule ="c: [型 = = '"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser'"、値"true_or_false"= =]  
     = > 問題 (型 = '"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'"、値 = '"https://schemas.microsoft.com/claims/multipleauthn'")"。  
  
    セット AdfsAdditionalAuthenticationRule $MfaClaimRule  

  
> [!NOTE]  
> 置き換えることを確認して*< true\_or\_false >*いずれかで`true`または`false`します。 値は、かどうか、デバイスが workplace\ に参加しているかどうかに基づいて、特定の規則の条件によって異なります。  
  
### <a name="to-configure-mfa-globally-if-the-access-request-comes-from-the-extranet-and-from-a-non-workplace-joined-device"></a>エクストラネットおよび以外に workplace\ 参加しているデバイスから、アクセス要求が送られた場合、グローバルに MFA を構成するには  
  
1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  
  
 
    `Set-AdfsAdditionalAuthenticationRule "c:[Type == '"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser'", Value == '"true_or_false'"] && c2:[Type == '"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork'", Value == '" true_or_false '"] => issue(Type = '"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", Value ='"https://schemas.microsoft.com/claims/multipleauthn'");" ` 
 
  
> [!NOTE]  
> 2 つのインスタンスを置き換えることを確認*< true\_or\_false >*いずれかで`true`または`false`、これは、特定の規則の条件に依存します。 ルールの条件に基づいてかどうか、デバイスが workplace\ に参加しているかどうか、アクセス要求がエクストラネットから取得するかどうか、またはイントラネットします。  
  
### <a name="to-configure-mfa-globally-if-access-comes-from-an-extranet-user-that-belongs-to-a-certain-group"></a>特定のグループに属しているエクストラネットのユーザーからのアクセスの場合、グローバル一意識 MFA を構成するには  
  
1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  
  

    Set-AdfsAdditionalAuthenticationRule"c: [型 = = `"https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid`"、値 = = `"group_SID`"] & & c2: [型 = = `"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`"、値 = = `"true_or_false`"] = > 問題 (型 = `"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod`"、値 ='"https://schemas.microsoft.com/claims/
      
> [!NOTE]  
> 置き換えることを確認して*< group\_SID >*グループ SID の値と*< true\_or\_false >*いずれかで`true`または`false`、アクセス要求がエクストラネットから取得するかどうかに基づいて、特定の規則の条件によってはまたはイントラネットします。  
  
### <a name="to-grant-access-to-an-application-based-on-user-data-via-windows-powershell"></a>Windows PowerShell を使用してユーザー データに基づくアプリケーションへのアクセスを付与するには  
  
1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  
  
    ```  
    $rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust  
  
    ```  
  
> [!NOTE]  
> 置き換えることを確認して*< relying\_party\_trust >* 、証明書利用者信頼の値。  
  
2.  同じ Windows PowerShell コマンド ウィンドウで、次のコマンドを実行します。  
  
    ```  
  
      $GroupAuthzRule = "@RuleTemplate = `“Authorization`” @RuleName = `"Foo`" c:[Type == `"https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid`", Value =~ `"^(?i)<group_SID>$`"] =>issue(Type = `"https://schemas.microsoft.com/authorization/claims/deny`", Value = `"DenyUsersWithClaim`");"  
    Set-AdfsRelyingPartyTrust –TargetRelyingParty $rp –IssuanceAuthorizationRules $GroupAuthzRule  
    ```  
  
> [!NOTE]  
> > 置き換えることを確認して*< group\_SID >* AD グループの SID の値。  
  
### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-this-users-identity-was-validated-with-mfa"></a>ユーザーの場合にのみ、AD FS で保護されているアプリケーションへのアクセスを付与するには、が MFA で検証されました。  
  
1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  
  

    `$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust ` 
 
  
> [!NOTE]  
> 置き換えることを確認して*< relying\_party\_trust >* 、証明書利用者信頼の値。  
  
2.  同じ Windows PowerShell コマンド ウィンドウで、次のコマンドを実行します。  
  
    ```  
    $GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
    @RuleName = `"PermitAccessWithMFA`"  
    c:[Type == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Value =~ `"^(?i)https://schemas\.microsoft\.com/claims/multipleauthn$`"] => issue(Type = `"https://schemas.microsoft.com/authorization/claims/permit`", Value = ‘“PermitUsersWithClaim’");"  
  
    ```  
  
### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-the-access-request-comes-from-a-workplace-joined-device-that-is-registered-to-the-user"></a>ユーザーに登録されている workplace\ に参加しているデバイスからアクセス要求が取得かどうかのみに AD FS によって保護されているアプリケーションへのアクセスを付与するには  
  
1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  
  
    ```  
    $rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust  
  
    ```  
  
> [!NOTE]  
> 置き換えることを確認して*< relying\_party\_trust >* 、証明書利用者信頼の値。  
  
2.  同じ Windows PowerShell コマンド ウィンドウで、次のコマンドを実行します。  
  

    $GroupAuthzRule ="@RuleTemplate = `"Authorization`"  
    @RuleName = `"PermitAccessFromRegisteredWorkplaceJoinedDevice`"  
    c: [型 = = `"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser`"、値 = ~ `"^(?i)true$`"] = > 問題 (型 = `"https://schemas.microsoft.com/authorization/claims/permit`"、値 = `"PermitUsersWithClaim`")。  
  

  
### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-the-access-request-comes-from-a-workplace-joined-device-that-is-registered-to-a-user-whose-identity-has-been-validated-with-mfa"></a>Id が MFA で検証済みのユーザーに登録されている workplace\ に参加しているデバイスからアクセス要求が取得かどうかのみに AD FS によって保護されているアプリケーションへのアクセスを付与するには  
  
1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  
  
 
    `$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust ` 
 
  
> [!NOTE]  
> 置き換えることを確認して*< relying\_party\_trust >* 、証明書利用者信頼の値。  
  
2.  同じ Windows PowerShell コマンド ウィンドウで、次のコマンドを実行します。  
  
    ```  
    $GroupAuthzRule = ‘@RuleTemplate = “Authorization”  
    @RuleName = “RequireMFAOnRegisteredWorkplaceJoinedDevice”  
    c1:[Type == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Value =~ `"^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$`"] &&  
    c2:[Type == `"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser`", Value =~ `"^(?i)true$”] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit`", Value = `"PermitUsersWithClaim`");"  
  
    ```  
  
### <a name="to-grant-extranet-access-to-an-application-secured-by-ad-fs-only-if-the-access-request-comes-from-a-user-whose-identity-has-been-validated-with-mfa"></a>Id が MFA で検証済みのユーザーからアクセス要求を受け取った場合にのみ、AD FS によって保護されたアプリケーションへのエクストラネット アクセスを付与するには  
  
1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  
  
 
    `$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust`  

  
> [!NOTE]  
> 置き換えることを確認して*< relying\_party\_trust >* 、証明書利用者信頼の値。  
  
2.  同じ Windows PowerShell コマンド ウィンドウで、次のコマンドを実行します。  
  

    $GroupAuthzRule ="@RuleTemplate = `"Authorization`"  
    @RuleName = `"RequireMFAForExtranetAccess`"  
    c1: [型 = = `"https://schemas.microsoft.com/claims/authnmethodsreferences`"、値 = 約`"^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$`"] (& a) (& a)  
    c2: [型 = = `"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`"、値 = ~ `"^(?i)false$`"] = > 問題 (型 = `"https://schemas.microsoft.com/authorization/claims/permit`"、値 = `"PermitUsersWithClaim`")"。  

## <a name="additional-references"></a>その他の参照  

[AD FS の操作](../../ad-fs/AD-FS-2016-Operations.md)
