---
ms.assetid: 8e7015bc-c489-4ec7-8b6e-3ece90f72317
title: 認証ポリシーを構成する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 2215f172128a533e0e0d4e10b72be53ad455a262
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444963"
---
# <a name="configure-authentication-policies"></a>認証ポリシーを構成する

Windows Server 2012 R2 での AD FS で両方のアクセス制御と認証メカニズムに強化され、ユーザー、デバイス、場所、および認証データを含む複数の要素。 これらの拡張機能を有効にするには、ユーザー インターフェイスまたは AD FS にアクセス許可の付与のリスクを管理する、Windows PowerShell のいずれか\-マルチ経由でアプリケーションをセキュリティで保護された\-要素アクセス制御とマルチ\-要素認証にユーザー id またはグループのメンバーシップ、ネットワークの場所、デバイスのデータが職場に基づく\-参加している場合、認証状態とマルチ\-authentication \(MFA\)実行されました。  

MFA と複数の詳細については\-Active Directory フェデレーション サービスでのアクセス制御を考慮\(AD FS\)で Windows Server 2012 R2 では、次のトピックを参照してください。  


-   [SSO およびシームレスな第 2 の任意のデバイスから社内への参加要素用アプリケーション間での認証](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)

-   [条件付きアクセス制御によってリスクを管理する](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md)

-   [機密性の高いアプリケーションの追加の多要素認証によるリスクを管理します。](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

## <a name="configure-authentication-policies-via-the-ad-fs-management-snap-in"></a>AD FS 管理スナップインを使用して認証ポリシーを構成する\-で  
これらの手順を実行するには、ローカル コンピューターの **Administrators** グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   

Windows Server 2012 R2 での AD FS では、すべてのアプリケーションや AD FS によって保護されているサービスに適用されるグローバル スコープで認証ポリシーを指定できます。 特定のアプリケーションとサービスを信頼に依存しており、AD FS によって保護された認証ポリシーを設定することもできます。 証明書利用者ごとの特定のアプリケーションの認証ポリシーを指定する信頼がグローバル認証ポリシーをオーバーライドしません。 グローバルまたは証明書利用者ごとの場合、ユーザーが、この証明書利用者信頼に対して認証しようとしています。 信頼認証ポリシーには、MFA、MFA が必要ですがトリガーされます。 グローバル認証ポリシーは、アプリケーションと特定の構成された認証ポリシーがないサービスの証明書利用者信頼のフォールバックです。 

## <a name="to-configure-primary-authentication-globally-in-windows-server-2012-r2"></a>Windows Server 2012 R2 でグローバル プライマリ認証を構成するには 

1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  

2.  AD FS でスナップ\-で、クリックして**認証ポリシー**します。  

3.  **プライマリ認証**セクションで、**編集**横に**グローバル設定**します。 右することもできます\-クリックして**認証ポリシー**を選択し、**グローバル プライマリ認証の編集**、または 、**アクション**ウィンドウ、 **グローバル プライマリ認証の編集**します。  
![認証ポリシー](media/Configure-Authentication-Policies/authpolicy1.png)

4.  **グローバル認証ポリシーの編集**ウィンドウの**プライマリ**] タブの [グローバル認証ポリシーの一部として、次の設定を構成することができます。  

    -   プライマリ認証に使用する認証方法。 使用できる認証方法を選択することができます、**エクストラネット**と**イントラネット**します。  

    -   デバイス認証を使用して、**デバイス認証を有効にする**チェック ボックスをオンします。 詳細については、「 [任意のデバイスからの職場への参加による業務用アプリケーション間の SSO とシームレスな 2 要素認証](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)」を参照してください。  
![認証ポリシー](media/Configure-Authentication-Policies/authpolicy2.png)  

## <a name="to-configure-primary-authentication-per-relying-party-trust"></a>証明書利用者ごとのプライマリ認証を構成するパーティの信頼  

1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  

2.  AD FS でスナップ\-で、クリックして**認証ポリシー**\\**証明書利用者信頼ごと**、証明書利用者信頼の認証を構成する をクリックポリシー。  

3.  右側か\-認証ポリシーを構成し、選択する証明書利用者のパーティの信頼をクリックします**カスタム プライマリ認証の編集**、または、下、**アクション**ウィンドウで、。選択**カスタム プライマリ認証の編集**します。  
![認証ポリシー](media/Configure-Authentication-Policies/authpolicy5.png)   

4.  **の認証ポリシーの編集 < 証明書利用者\_パーティ\_信頼\_名 >** ウィンドウで、**プライマリ** タブで、次の設定を構成します。一部として、**あたり Relying Party Trust**認証ポリシー。  

    -   ユーザーはサインインのたびに資格情報を入力する必要かどうか\-でを使用して、**ユーザー サインインのたびに資格情報を入力する必要が\-で**チェック ボックスをオンします。  
![認証ポリシー](media/Configure-Authentication-Policies/authpolicy6.png) 

## <a name="to-configure-multi-factor-authentication-globally"></a>多要素認証をグローバルに構成するには  

1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  

2.  AD FS でスナップ\-で、クリックして**認証ポリシー**します。  

3.  **マルチ\-要素認証**セクションで、**編集**横に**グローバル設定**します。 右することもできます\-クリックして**認証ポリシー**を選択し、**グローバル マルチの編集\-要素認証**、または 、**アクション**ペインで、**編集グローバル マルチ\-要素認証**します。  
![認証ポリシー](media/Configure-Authentication-Policies/authpolicy8.png)   

4.  **グローバル認証ポリシーの編集**ウィンドウで、**マルチ\-要素** タブで、グローバルの複数の一部として、次の設定を構成する\-要素認証ポリシー:  

    -   設定または mfa の条件下で使用可能なオプションを使用して、**ユーザー\/グループ**、**デバイス**、および**場所**セクション。  

    -   これらの設定のいずれかに対して MFA を有効にするには、少なくとも 1 つの追加の認証方法を選択してください。 **証明書の認証**は既定の使用可能なオプションです。 他のカスタムの追加認証方法、たとえば、Windows Azure Active Authentication を構成することもできます。 詳細については、次を参照してください。[チュートリアル ガイド。機密性の高いアプリケーションの追加の多要素認証によるリスク管理](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)します。  

> [!WARNING]  
> 追加の認証方法をグローバルにのみ構成できます。  
![認証ポリシー](media/Configure-Authentication-Policies/authpolicy9.png)  

## <a name="to-configure-multi-factor-authentication-per-relying-party-trust"></a>複数を構成する\-証明書利用者ごとの要素認証の信頼  

1.  サーバー マネージャーで、**ツール**、し、 **AD FS 管理**します。  

2.  AD FS でスナップ\-で、クリックして**認証ポリシー**\\**証明書利用者信頼ごと**MFA を構成する利用者を順にクリックします。  

3.  右側か\-、MFA を構成し、選択する証明書利用者のパーティの信頼をクリックします**編集カスタム マルチ\-要素認証**、または 、**アクション**ウィンドウで、。選択**編集カスタム マルチ\-要素認証**します。  

4.  **の認証ポリシーの編集 < 証明書利用者\_パーティ\_信頼\_名 >** ウィンドウで、**マルチ\-係数**ことができます タブで、一部として、次の設定を構成、あたり\-証明書利用者信頼の認証ポリシー。  

    -   設定または mfa の条件下で使用可能なオプションを使用して、**ユーザー\/グループ**、**デバイス**、および**場所**セクション。  

## <a name="configure-authentication-policies-via-windows-powershell"></a>Windows PowerShell を使用して認証ポリシーを構成します。  
Windows PowerShell により、アクセス制御のさまざまな要因を使用して、柔軟性とするに必要な認証ポリシーと承認を構成する Windows Server 2012 R2 で AD FS で使用できる認証メカニズムのルールAD FS の場合は true。 条件付きアクセスを実装\-リソースをセキュリティで保護します。  

管理者、またはローカル コンピューター上のそれと同等のメンバーシップは、これらの手順を実行する最小要件です。  適切なアカウントの使用に関する詳細を確認し、グループ メンバーシップ[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.microsoft.com\/fwlink\/でしょうか。LinkId\=83477\)します。   

### <a name="to-configure-an-additional-authentication-method-via-windows-powershell"></a>Windows PowerShell を使用して、追加の認証方法を構成するには  

1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  


~~~
`Set-AdfsGlobalAuthenticationPolicy –AdditionalAuthenticationProvider CertificateAuthentication  `
~~~


> [!WARNING]  
> このコマンドが正常に実行されたことを確認するには、 `Get-AdfsGlobalAuthenticationPolicy` コマンドを実行できます。  

### <a name="to-configure-mfa-per-relying-party-trust-that-is-based-on-a-users-group-membership-data"></a>ごとの MFA を構成する\-ユーザーのグループ メンバーシップ データに基づく証明書利用者の信頼  

1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  


~~~
`$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust`  
~~~


> [!WARNING]  
> 置換することを確認 *< 証明書利用者\_パーティ\_信頼 >* 証明書利用者信頼の名前に置き換えます。  

2. 同じ Windows PowerShell コマンド ウィンドウで、次のコマンドを実行します。  


~~~
$MfaClaimRule = “c:[Type == ‘“https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid’”, Value =~ ‘“^(?i) <group_SID>$’”] => issue(Type = ‘“https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod’”, Value ‘“https://schemas.microsoft.com/claims/multipleauthn’”);” 

Set-AdfsRelyingPartyTrust –TargetRelyingParty $rp –AdditionalAuthenticationRules $MfaClaimRule
~~~


> [!NOTE]  
> 置換することを確認 < グループ\_SID > セキュリティ識別子の値を持つ\(SID\) Active Directory の\(AD\)グループ。  

### <a name="to-configure-mfa-globally-based-on-users-group-membership-data"></a>グローバルにユーザーのグループ メンバーシップ データに基づく MFA を構成するには  

1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  


~~~
$MfaClaimRule = “c:[Type == ‘" https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid’", Value == ‘"group_SID’"]  
 => issue(Type = ‘"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod’", Value = ‘"https://schemas.microsoft.com/claims/multipleauthn’");”  

Set-AdfsAdditionalAuthenticationRule $MfaClaimRule  
~~~


> [!NOTE]  
> 置換することを確認 *< グループ\_SID >* AD グループの SID の値。  

### <a name="to-configure-mfa-globally-based-on-users-location"></a>ユーザーの場所にグローバルに基づく MFA を構成するには  

1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  


~~~
$MfaClaimRule = “c:[Type == ‘" https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork’", Value == ‘"true_or_false’"]  
 => issue(Type = ‘"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod’", Value = ‘"https://schemas.microsoft.com/claims/multipleauthn’");”  

Set-AdfsAdditionalAuthenticationRule $MfaClaimRule  
~~~



> [!NOTE]  
> 置換することを確認 *< true\_または\_false >* いずれかで`true`または`false`します。 値は、エクストラネットまたはイントラネットからのアクセス要求を受信するかどうかに基づいている、特定の規則の条件によって異なります。  

### <a name="to-configure-mfa-globally-based-on-users-device-data"></a>グローバルにユーザーのデバイス データに基づく MFA を構成するには  

1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  


~~~
$MfaClaimRule = "c:[Type == ‘" https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser’", Value == ‘"true_or_false"']  
 => issue(Type = ‘"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod’", Value = ‘"https://schemas.microsoft.com/claims/multipleauthn’");"  

Set-AdfsAdditionalAuthenticationRule $MfaClaimRule  
~~~


> [!NOTE]  
> 置換することを確認 *< true\_または\_false >* いずれかで`true`または`false`します。 値は、デバイスが社内でかどうかに基づいている、特定の規則の条件によって異なります。\-参加済みか。  

### <a name="to-configure-mfa-globally-if-the-access-request-comes-from-the-extranet-and-from-a-non-workplace-joined-device"></a>アクセス要求がエクストラネットと以外からの場合、グローバルに MFA を構成する\-ワークプ レース\-参加しているデバイス  

1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  


~~~
`Set-AdfsAdditionalAuthenticationRule "c:[Type == '"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser'", Value == '"true_or_false'"] && c2:[Type == '"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork'", Value == '" true_or_false '"] => issue(Type = '"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", Value ='"https://schemas.microsoft.com/claims/multipleauthn'");" ` 
~~~


> [!NOTE]  
> 両方のインスタンスを置換することを確認 *< true\_または\_false >* いずれかで`true`または`false`、特定のルール条件によって決まります。 ルールの条件が、デバイスが社内でかどうかに基づいて\-参加しているか、エクストラネットからアクセス要求を受信しないとするかどうか、またはイントラネットです。  

### <a name="to-configure-mfa-globally-if-access-comes-from-an-extranet-user-that-belongs-to-a-certain-group"></a>特定のグループに属しているユーザーがエクストラネットからのアクセスの場合、グローバルに MFA を構成するには  

1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  


~~~
Set-AdfsAdditionalAuthenticationRule "c:[Type == `"https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid`", Value == `"group_SID`"] && c2:[Type == `"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`", Value== `"true_or_false`"] => issue(Type = `"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod`", Value =`"https://schemas.microsoft.com/claims/
~~~

> [!NOTE]  
> 置換することを確認 *< グループ\_SID >* グループ SID の値を持つと *< true\_または\_false >* いずれかで`true`または`false`、エクストラネットからのアクセス要求を受信するかどうかに基づいている、特定のルール条件に依存する、またはイントラネットです。  

### <a name="to-grant-access-to-an-application-based-on-user-data-via-windows-powershell"></a>Windows PowerShell を使用してユーザー データに基づくアプリケーションへのアクセスを許可するには  

1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  

    ```  
    $rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust  

    ```  

> [!NOTE]  
> 置換することを確認 *< 証明書利用者\_パーティ\_信頼 >* 証明書利用者信頼の値。  

2. 同じ Windows PowerShell コマンド ウィンドウで、次のコマンドを実行します。  

   ```  

     $GroupAuthzRule = "@RuleTemplate = `“Authorization`” @RuleName = `"Foo`" c:[Type == `"https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid`", Value =~ `"^(?i)<group_SID>$`"] =>issue(Type = `"https://schemas.microsoft.com/authorization/claims/deny`", Value = `"DenyUsersWithClaim`");"  
   Set-AdfsRelyingPartyTrust –TargetRelyingParty $rp –IssuanceAuthorizationRules $GroupAuthzRule  
   ```  

> [!NOTE]  
> > 置換することを確認 *< グループ\_SID >* AD グループの SID の値。  

### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-this-users-identity-was-validated-with-mfa"></a>MFA で検証されたユーザーの場合にのみ、AD FS で保護されているアプリケーションへのアクセスを許可するには  

1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  


~~~
`$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust ` 
~~~


> [!NOTE]  
> 置換することを確認 *< 証明書利用者\_パーティ\_信頼 >* 証明書利用者信頼の値。  

2. 同じ Windows PowerShell コマンド ウィンドウで、次のコマンドを実行します。  

   ```  
   $GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
   @RuleName = `"PermitAccessWithMFA`"  
   c:[Type == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Value =~ `"^(?i)https://schemas\.microsoft\.com/claims/multipleauthn$`"] => issue(Type = `"https://schemas.microsoft.com/authorization/claims/permit`", Value = ‘“PermitUsersWithClaim’");"  

   ```  

### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-the-access-request-comes-from-a-workplace-joined-device-that-is-registered-to-the-user"></a>職場からアクセスする場合にのみ、AD FS で保護されているアプリケーションへのアクセスを許可する要求を受け取った\-参加しているデバイスをユーザーに登録されています。  

1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  

    ```  
    $rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust  

    ```  

> [!NOTE]  
> 置換することを確認 *< 証明書利用者\_パーティ\_信頼 >* 証明書利用者信頼の値。  

2. 同じ Windows PowerShell コマンド ウィンドウで、次のコマンドを実行します。  


~~~
$GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
@RuleName = `"PermitAccessFromRegisteredWorkplaceJoinedDevice`"  
c:[Type == `"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser`", Value =~ `"^(?i)true$`"] => issue(Type = `"https://schemas.microsoft.com/authorization/claims/permit`", Value = `"PermitUsersWithClaim`");  
~~~



### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-the-access-request-comes-from-a-workplace-joined-device-that-is-registered-to-a-user-whose-identity-has-been-validated-with-mfa"></a>職場からアクセスする場合にのみ、AD FS で保護されているアプリケーションへのアクセスを許可する要求を受け取った\-id が MFA で検証済みユーザーに登録されているが参加しているデバイス  

1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  


~~~
`$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust ` 
~~~


> [!NOTE]  
> 置換することを確認 *< 証明書利用者\_パーティ\_信頼 >* 証明書利用者信頼の値。  

2. 同じ Windows PowerShell コマンド ウィンドウで、次のコマンドを実行します。  

   ```  
   $GroupAuthzRule = ‘@RuleTemplate = “Authorization”  
   @RuleName = “RequireMFAOnRegisteredWorkplaceJoinedDevice”  
   c1:[Type == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Value =~ `"^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$`"] &&  
   c2:[Type == `"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser`", Value =~ `"^(?i)true$”] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit`", Value = `"PermitUsersWithClaim`");"  

   ```  

### <a name="to-grant-extranet-access-to-an-application-secured-by-ad-fs-only-if-the-access-request-comes-from-a-user-whose-identity-has-been-validated-with-mfa"></a>Id が MFA で検証済みのユーザーからアクセス要求を受け取った場合にのみ、AD FS によって保護されたアプリケーションへのエクストラネット アクセスを許可するには  

1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  


~~~
`$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust`  
~~~


> [!NOTE]  
> 置換することを確認 *< 証明書利用者\_パーティ\_信頼 >* 証明書利用者信頼の値。  

2. 同じ Windows PowerShell コマンド ウィンドウで、次のコマンドを実行します。  


~~~
$GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
@RuleName = `"RequireMFAForExtranetAccess`"  
c1:[Type == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Value =~ `"^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$`"] &&  
c2:[Type == `"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`", Value =~ `"^(?i)false$`"] => issue(Type = `"https://schemas.microsoft.com/authorization/claims/permit`", Value = `"PermitUsersWithClaim`");"  
~~~

## <a name="additional-references"></a>その他の参照情報  

[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md)
