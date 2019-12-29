---
ms.assetid: 8e7015bc-c489-4ec7-8b6e-3ece90f72317
title: 認証ポリシーを構成する
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: ef38b0280a5753b0995e85d0809de6b632fa3afc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358121"
---
# <a name="configure-authentication-policies"></a>認証ポリシーを構成する

AD FS の Windows Server 2012 R2 では、アクセス制御と認証メカニズムの両方が、ユーザー、デバイス、場所、および認証データを含む複数の要因によって強化されています。 これらの拡張機能により、ユーザーインターフェイスまたは Windows PowerShell を使用して、セキュリティで保護されたアプリケーション\-を多\-要素アクセス制御と複数\-のADFSにアクセス許可を付与するリスクを管理できます。ユーザー id またはグループメンバーシップ、ネットワークの場所、ワークプレース\-に参加しているデバイスデータ、multi-factor\-authentication \(の MFAの認証状態に基づいて認証を行います。\)が実行されました。  

Windows Server 2012 R2 の Active Directory フェデレーションサービス (AD FS)\- \(AD FS\)での MFA と多要素アクセス制御の詳細については、次のトピックを参照してください。  


-   [任意のデバイスからの職場への参加による業務用アプリケーション間の SSO とシームレスな 2 要素認証](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)

-   [条件付きアクセス制御によってリスクを管理する](../../ad-fs/operations/Manage-Risk-with-Conditional-Access-Control.md)

-   [追加の多要素認証による個人情報アプリケーションのリスク管理](../../ad-fs/operations/Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)

## <a name="configure-authentication-policies-via-the-ad-fs-management-snap-in"></a>AD FS 管理スナップイン\-を使用して認証ポリシーを構成する  
これらの手順を実行するには、ローカル コンピューターの **Administrators** グループのメンバーシップか、それと同等のメンバーシップが最低限必要です。  適切なアカウントの使用方法の詳細を確認し、グループ メンバーシップ [ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477)します。   

AD FS の Windows Server 2012 R2 では、AD FS によって保護されているすべてのアプリケーションとサービスに適用されるグローバルスコープで認証ポリシーを指定できます。 パーティの信頼に依存し、AD FS によって保護されている特定のアプリケーションとサービスに対して、認証ポリシーを設定することもできます。 証明書利用者信頼ごとに特定のアプリケーションの認証ポリシーを指定しても、グローバル認証ポリシーは上書きされません。 グローバルまたは証明書利用者信頼ごとの認証ポリシーに MFA が必要な場合、ユーザーがこの証明書利用者信頼に対して認証を試みると、MFA がトリガーされます。 グローバル認証ポリシーは、特定の認証ポリシーが構成されていないアプリケーションやサービスに対する証明書利用者信頼のフォールバックです。 

## <a name="to-configure-primary-authentication-globally-in-windows-server-2012-r2"></a>Windows Server 2012 R2 でプライマリ認証をグローバルに構成するには 

1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  

2.  AD FS スナップイン\- で、**認証ポリシー** をクリックします。  

3.  **[プライマリ認証]** セクションで、 **[グローバル設定]** の横にある **[編集]** をクリックします。 \-また、 **[認証ポリシー]** を右クリックし、 **[グローバルプライマリ認証の編集]** を選択するか、 **[操作]** ウィンドウで **[グローバルプライマリ認証の編集]** を選択します。  
![認証ポリシー](media/Configure-Authentication-Policies/authpolicy1.png)

4.  **[グローバル認証ポリシーの編集]** ウィンドウの **[プライマリ]** タブで、グローバル認証ポリシーの一部として次の設定を構成できます。  

    -   プライマリ認証に使用する認証方法。 **エクストラネット**と**イントラネット**で使用可能な認証方法を選択できます。  

    -   **[デバイス認証を有効にする]** チェックボックスを使用したデバイス認証。 詳細については、「 [任意のデバイスからの職場への参加による業務用アプリケーション間の SSO とシームレスな 2 要素認証](../../ad-fs/operations/Join-to-Workplace-from-Any-Device-for-SSO-and-Seamless-Second-Factor-Authentication-Across-Company-Applications.md)」を参照してください。  
![認証ポリシー](media/Configure-Authentication-Policies/authpolicy2.png)  

## <a name="to-configure-primary-authentication-per-relying-party-trust"></a>証明書利用者信頼ごとにプライマリ認証を構成するには  

1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  

2.  AD FS スナップイン\- で、**証明書利用者信頼ごと**の**認証ポリシー**\\ をクリックし、認証ポリシーを構成する証明書利用者信頼をクリックします。  

3.  認証ポリシー\-を構成する証明書利用者信頼を右クリックし、**カスタムプライマリ認証の編集** を選択するか、**操作** ウィンドウで カスタムプライマリの編集 を選択します。 **認証**。  
![認証ポリシー](media/Configure-Authentication-Policies/authpolicy5.png)   

4.  [ **< 証明書\_\_利用者信頼\_名 > の認証ポリシーの編集**] ウィンドウの **[プライマリ]** タブで、**証明書利用者信頼ごと**に次の設定を構成できます。認証ポリシー:  

    -   ユーザーが\- **サインイン\-** するたびに資格情報を入力するようにユーザーに要求するかどうかを指定します。  
![認証ポリシー](media/Configure-Authentication-Policies/authpolicy6.png) 

## <a name="to-configure-multi-factor-authentication-globally"></a>Multi-factor authentication をグローバルに構成するには  

1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  

2.  AD FS スナップイン\- で、**認証ポリシー** をクリックします。  

3.  [ **Multi-factor\-authentication** ] セクションで、 **[グローバル設定]** の横にある **[編集]** をクリックします。 **[認証ポリシー]** \-を右クリックし、[**グローバルな multi-factor\-authentication の編集**] を選択するか、 **[操作]** ウィンドウで [**グローバル\-multi-factor authentication の編集] を選択します。** .  
![認証ポリシー](media/Configure-Authentication-Policies/authpolicy8.png)   

4.  **[グローバル認証ポリシーの編集]** ウィンドウの [**多\-要素**] タブで、グローバル多\-要素認証ポリシーの一部として次の設定を構成できます。  

    -   [**ユーザー\/のグループ**]、 **[デバイス]** 、および **[場所]** セクションで利用可能なオプションを使用した MFA の設定または条件。  

    -   これらの設定のいずれかに対して MFA を有効にするには、追加の認証方法を少なくとも1つ選択する必要があります。 **証明書認証**は、既定で使用可能なオプションです。 また、Windows Azure Active Authentication など、その他のカスタムの認証方法を構成することもできます。 詳細については[、「チュートリアルガイド:機密アプリケーション](../../ad-fs/operations/Walkthrough-Guide--Manage-Risk-with-Additional-Multi-Factor-Authentication-for-Sensitive-Applications.md)の追加 Multi-Factor Authentication によってリスクを管理します。  

> [!WARNING]  
> 追加の認証方法はグローバルにのみ構成できます。  
![認証ポリシー](media/Configure-Authentication-Policies/authpolicy9.png)  

## <a name="to-configure-multi-factor-authentication-per-relying-party-trust"></a>証明書利用者\-信頼ごとに多要素認証を構成するには  

1.  サーバーマネージャーで、 **[ツール]** をクリックし、 **[AD FS の管理]** を選択します。  

2.  AD FS スナップイン\- で、**証明書利用者信頼ごと**の**認証ポリシー**\\ をクリックし、MFA を構成する証明書利用者の信頼をクリックします。  

3.  MFA を\-構成する証明書利用者の信頼を右クリックし、[**カスタム多\-要素認証の編集**] を選択するか、 **[操作]** ウィンドウで [**カスタムマルチ\-ポイントの編集] を選択します。要素認証**。  

4.  [ **< 証明書\_\_利用者信頼\_名 > の認証ポリシーの編集**] ウィンドウの [**多\-要素**] タブで、の一部\-として次の設定を構成できます。証明書利用者信頼の認証ポリシー:  

    -   [**ユーザー\/のグループ**]、 **[デバイス]** 、および **[場所]** セクションで利用可能なオプションを使用した MFA の設定または条件。  

## <a name="configure-authentication-policies-via-windows-powershell"></a>Windows PowerShell を使用して認証ポリシーを構成する  
Windows PowerShell では、アクセス制御のさまざまな要素をより柔軟に使用できます。また、Windows Server 2012 R2 の AD FS で使用できる認証メカニズムを使用して、認証ポリシーと承認規則を構成して、AD FS \-のセキュリティで保護されたリソースに対して true の条件付きアクセスを実装します。  

これらの手順を完了するには、ローカルコンピューターの Administrators、またはそれと同等のメンバーシップが最低限必要です。  適切なアカウントおよびグループメンバーシップの使用に関する詳細については、「[ローカルおよびドメインの既定のグループ](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.microsoft.com\/fwlink\/?」を参照してください。LinkId\=83477\)。   

### <a name="to-configure-an-additional-authentication-method-via-windows-powershell"></a>Windows PowerShell を使用して追加の認証方法を構成するには  

1.  フェデレーションサーバーで、Windows PowerShell コマンドウィンドウを開き、次のコマンドを実行します。  


~~~
`Set-AdfsGlobalAuthenticationPolicy –AdditionalAuthenticationProvider CertificateAuthentication  `
~~~


> [!WARNING]  
> このコマンドが正常に実行されたことを確認するには、 `Get-AdfsGlobalAuthenticationPolicy` コマンドを実行できます。  

### <a name="to-configure-mfa-per-relying-party-trust-that-is-based-on-a-users-group-membership-data"></a>ユーザーのグループメンバーシップ\-データに基づく証明書利用者信頼ごとに MFA を構成するには  

1.  フェデレーション サーバーで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  


~~~
`$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust`  
~~~


> [!WARNING]  
> *< 証明書\_\_利用者信頼の >* を、証明書利用者信頼の名前に置き換えるようにしてください。  

2. 同じ Windows PowerShell コマンドウィンドウで、次のコマンドを実行します。  


~~~
$MfaClaimRule = “c:[Type == ‘“https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid'”, Value =~ ‘“^(?i) <group_SID>$'”] => issue(Type = ‘“https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'”, Value ‘“https://schemas.microsoft.com/claims/multipleauthn'”);” 

Set-AdfsRelyingPartyTrust –TargetRelyingParty $rp –AdditionalAuthenticationRules $MfaClaimRule
~~~


> [!NOTE]  
> < グループ\_SID > を Active Directory \(\) \(ADグループのセキュリティ識別子SIDの値に置き換えてください。\)  

### <a name="to-configure-mfa-globally-based-on-users-group-membership-data"></a>ユーザーのグループメンバーシップデータに基づいて MFA をグローバルに構成するには  

1.  フェデレーションサーバーで、Windows PowerShell コマンドウィンドウを開き、次のコマンドを実行します。  


~~~
$MfaClaimRule = “c:[Type == ‘" https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid'", Value == ‘"group_SID'"]  
 => issue(Type = ‘"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", Value = ‘"https://schemas.microsoft.com/claims/multipleauthn'");”  

Set-AdfsAdditionalAuthenticationRule $MfaClaimRule  
~~~


> [!NOTE]  
> *< グループ\_sid >* を AD グループの sid の値に置き換えてください。  

### <a name="to-configure-mfa-globally-based-on-users-location"></a>ユーザーの場所に基づいて MFA をグローバルに構成するには  

1.  フェデレーションサーバーで、Windows PowerShell コマンドウィンドウを開き、次のコマンドを実行します。  


~~~
$MfaClaimRule = “c:[Type == ‘" https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork'", Value == ‘"true_or_false'"]  
 => issue(Type = ‘"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", Value = ‘"https://schemas.microsoft.com/claims/multipleauthn'");”  

Set-AdfsAdditionalAuthenticationRule $MfaClaimRule  
~~~



> [!NOTE]  
> *< True\_また\_は false >* をまたは`false`の`true`どちらかに置き換えるようにしてください。 この値は、アクセス要求がエクストラネットまたはイントラネットのどちらからのものであるかに基づいて、特定の規則条件によって異なります。  

### <a name="to-configure-mfa-globally-based-on-users-device-data"></a>ユーザーのデバイスデータに基づいて MFA をグローバルに構成するには  

1.  フェデレーションサーバーで、Windows PowerShell コマンドウィンドウを開き、次のコマンドを実行します。  


~~~
$MfaClaimRule = "c:[Type == ‘" https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser'", Value == ‘"true_or_false"']  
 => issue(Type = ‘"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", Value = ‘"https://schemas.microsoft.com/claims/multipleauthn'");"  

Set-AdfsAdditionalAuthenticationRule $MfaClaimRule  
~~~


> [!NOTE]  
> *< True\_また\_は false >* をまたは`false`の`true`どちらかに置き換えるようにしてください。 値は、デバイスが社内\-参加しているかどうかに基づいて、特定のルール条件によって異なります。  

### <a name="to-configure-mfa-globally-if-the-access-request-comes-from-the-extranet-and-from-a-non-workplace-joined-device"></a>アクセス要求がエクストラネットと職場\-\-に参加していないデバイスからのものである場合に、MFA をグローバルに構成するには  

1.  フェデレーションサーバーで、Windows PowerShell コマンドウィンドウを開き、次のコマンドを実行します。  


~~~
`Set-AdfsAdditionalAuthenticationRule "c:[Type == '"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser'", Value == '"true_or_false'"] && c2:[Type == '"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork'", Value == '" true_or_false '"] => issue(Type = '"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod'", Value ='"https://schemas.microsoft.com/claims/multipleauthn'");" ` 
~~~


> [!NOTE]  
> *< True\_また\_は false >* の両方のインスタンスを、特定の`false`規則条件に応じてまたはのどちらか`true`に置き換えるようにしてください。 ルール条件は、デバイスが社内\-参加しているかどうか、およびアクセス要求がエクストラネットまたはイントラネットのどちらであるかに基づいています。  

### <a name="to-configure-mfa-globally-if-access-comes-from-an-extranet-user-that-belongs-to-a-certain-group"></a>特定のグループに属するエクストラネットユーザーからのアクセスがある場合に MFA をグローバルに構成するには  

1.  フェデレーションサーバーで、Windows PowerShell コマンドウィンドウを開き、次のコマンドを実行します。  


~~~
Set-AdfsAdditionalAuthenticationRule "c:[Type == `"https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid`", Value == `"group_SID`"] && c2:[Type == `"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`", Value== `"true_or_false`"] => issue(Type = `"https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod`", Value =`"https://schemas.microsoft.com/claims/
~~~

> [!NOTE]  
> *< グループ\_sid >* をグループ sid の値に、 *< true\_また\_は false >* `true`をまたは`false`で置き換えてください。これは、特定のルール条件によって異なります。は、アクセス要求がエクストラネットとイントラネットのどちらからのものであるかに基づいています。  

### <a name="to-grant-access-to-an-application-based-on-user-data-via-windows-powershell"></a>Windows PowerShell を使用してユーザーデータに基づいてアプリケーションへのアクセスを許可するには  

1.  フェデレーションサーバーで、Windows PowerShell コマンドウィンドウを開き、次のコマンドを実行します。  

    ```  
    $rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust  

    ```  

> [!NOTE]  
> *< 証明書\_\_利用者信頼の >* を、証明書利用者信頼の値に置き換えてください。  

2. 同じ Windows PowerShell コマンドウィンドウで、次のコマンドを実行します。  

   ```  

     $GroupAuthzRule = "@RuleTemplate = `“Authorization`” @RuleName = `"Foo`" c:[Type == `"https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid`", Value =~ `"^(?i)<group_SID>$`"] =>issue(Type = `"https://schemas.microsoft.com/authorization/claims/deny`", Value = `"DenyUsersWithClaim`");"  
   Set-AdfsRelyingPartyTrust –TargetRelyingParty $rp –IssuanceAuthorizationRules $GroupAuthzRule  
   ```  

> [!NOTE]  
> > *< グループ\_sid >* を AD グループの sid の値に置き換えてください。  

### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-this-users-identity-was-validated-with-mfa"></a>このユーザーの id が MFA で検証された場合にのみ AD FS によって保護されているアプリケーションへのアクセスを許可するには  

1.  フェデレーションサーバーで、Windows PowerShell コマンドウィンドウを開き、次のコマンドを実行します。  


~~~
`$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust ` 
~~~


> [!NOTE]  
> *< 証明書\_\_利用者信頼の >* を、証明書利用者信頼の値に置き換えてください。  

2. 同じ Windows PowerShell コマンドウィンドウで、次のコマンドを実行します。  

   ```  
   $GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
   @RuleName = `"PermitAccessWithMFA`"  
   c:[Type == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Value =~ `"^(?i)https://schemas\.microsoft\.com/claims/multipleauthn$`"] => issue(Type = `"https://schemas.microsoft.com/authorization/claims/permit`", Value = ‘“PermitUsersWithClaim'");"  

   ```  

### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-the-access-request-comes-from-a-workplace-joined-device-that-is-registered-to-the-user"></a>AD FS によって保護されているアプリケーションへのアクセスを許可するには、ユーザー\-に登録されている社内参加デバイスからアクセス要求が送られた場合にのみ  

1.  フェデレーションサーバーで、Windows PowerShell コマンドウィンドウを開き、次のコマンドを実行します。  

    ```  
    $rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust  

    ```  

> [!NOTE]  
> *< 証明書\_\_利用者信頼の >* を、証明書利用者信頼の値に置き換えてください。  

2. 同じ Windows PowerShell コマンドウィンドウで、次のコマンドを実行します。  


~~~
$GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
@RuleName = `"PermitAccessFromRegisteredWorkplaceJoinedDevice`"  
c:[Type == `"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser`", Value =~ `"^(?i)true$`"] => issue(Type = `"https://schemas.microsoft.com/authorization/claims/permit`", Value = `"PermitUsersWithClaim`");  
~~~



### <a name="to-grant-access-to-an-application-that-is-secured-by-ad-fs-only-if-the-access-request-comes-from-a-workplace-joined-device-that-is-registered-to-a-user-whose-identity-has-been-validated-with-mfa"></a>Id が MFA で検証済みのユーザーに登録されている社内\-参加デバイスからアクセス要求が送られた場合にのみ AD FS によって保護されているアプリケーションへのアクセスを許可するには  

1.  フェデレーションサーバーで、Windows PowerShell コマンドウィンドウを開き、次のコマンドを実行します。  


~~~
`$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust ` 
~~~


> [!NOTE]  
> *< 証明書\_\_利用者信頼の >* を、証明書利用者信頼の値に置き換えてください。  

2. 同じ Windows PowerShell コマンドウィンドウで、次のコマンドを実行します。  

   ```  
   $GroupAuthzRule = ‘@RuleTemplate = “Authorization”  
   @RuleName = “RequireMFAOnRegisteredWorkplaceJoinedDevice”  
   c1:[Type == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Value =~ `"^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$`"] &&  
   c2:[Type == `"https://schemas.microsoft.com/2012/01/devicecontext/claims/isregistereduser`", Value =~ `"^(?i)true$”] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit`", Value = `"PermitUsersWithClaim`");"  

   ```  

### <a name="to-grant-extranet-access-to-an-application-secured-by-ad-fs-only-if-the-access-request-comes-from-a-user-whose-identity-has-been-validated-with-mfa"></a>Id が MFA で検証済みのユーザーからアクセス要求が送られた場合にのみ、AD FS によって保護されたアプリケーションへのエクストラネットアクセスを許可するには  

1.  フェデレーションサーバーで、Windows PowerShell コマンドウィンドウを開き、次のコマンドを実行します。  


~~~
`$rp = Get-AdfsRelyingPartyTrust –Name relying_party_trust`  
~~~


> [!NOTE]  
> *< 証明書\_\_利用者信頼の >* を、証明書利用者信頼の値に置き換えてください。  

2. 同じ Windows PowerShell コマンドウィンドウで、次のコマンドを実行します。  


~~~
$GroupAuthzRule = "@RuleTemplate = `"Authorization`"  
@RuleName = `"RequireMFAForExtranetAccess`"  
c1:[Type == `"https://schemas.microsoft.com/claims/authnmethodsreferences`", Value =~ `"^(?i)http://schemas\.microsoft\.com/claims/multipleauthn$`"] &&  
c2:[Type == `"https://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork`", Value =~ `"^(?i)false$`"] => issue(Type = `"https://schemas.microsoft.com/authorization/claims/permit`", Value = `"PermitUsersWithClaim`");"  
~~~

## <a name="additional-references"></a>その他の参照情報  

[AD FS の運用](../../ad-fs/AD-FS-2016-Operations.md)
