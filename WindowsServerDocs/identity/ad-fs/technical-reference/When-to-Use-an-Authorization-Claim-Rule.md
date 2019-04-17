---
ms.assetid: b734cbcb-342c-4a28-8ab5-b9cd990bb1c2
title: When to Use an Authorization Claim Rule
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 144e382692e8f2a6732f8c7c5b8a1dd6049192cb
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

# <a name="when-to-use-an-authorization-claim-rule"></a>When to Use an Authorization Claim Rule
入力方向の要求の種類を取得し、ユーザーを許可するか、規則で指定した値に基づいたのアクセスを拒否するかどうかを決定するアクションを適用する必要がある場合、Active Directory フェデレーション サービス \(AD FS\) でこの規則を使用することができます。 この規則を使用するときにパススルーまたは規則に構成するオプションのいずれかに基づいて、次の規則ロジックと一致する要求を変換します。  
  
|規則のオプション|規則のロジック|  
|---------------|--------------|  
|すべてのユーザーを許可します。|入力方向の要求の種類と等しい場合*いずれかの要求の種類*等しく、値*任意の値*、要求値が発行されます*許可*|  
|この入力方向の要求を持つユーザーにアクセスを許可します。|入力方向の要求の種類と等しい場合*要求の種類を指定した*等しく、値*指定した要求値*、要求値が発行されます*許可*|  
|この入力方向の要求を持つユーザーにアクセス権を拒否します。|入力方向の要求の種類と等しい場合*要求の種類を指定した*等しく、値*指定した要求値*、要求値が発行されます*拒否*|  
  
次のセクションでは、要求規則およびをこの規則を使用するタイミングについて詳しく説明するための基本的な概要を提供します。  
  
## <a name="about-claim-rules"></a>要求規則について  
要求規則は、入力方向の要求を行う、条件を適用するビジネス ロジックのインスタンスを表します \ (し y\ x の場合)、条件のパラメーターに基づいて出力方向の要求を生成します。 輪郭について知っておくべきヒントの要求規則を読む前に重要な一覧を次にこのトピックの「します。  
  
-   AD FS の管理スナップインには、要求規則でのみ作成できます要求規則テンプレートを使用します。  
  
-   入力方向の要求規則プロセスを要求するか、要求プロバイダーから直接 \ (など、Active Directory または別のフェデレーション \) または受付の出力から、要求プロバイダー信頼規則を変換します。  
  
-   要求規則は、特定の規則セット内で時系列要求発行エンジンによって処理されます。 規則に対する優先順位を設定、さらに調整したり、特定の規則セット内の先行する規則で生成された要求をフィルター処理できます。  
  
-   要求規則テンプレートを使用して、入力方向の要求の種類を指定する必要が常にします。 ただし、1 つの規則を使用して要求の種類が同じで、複数の要求の値を処理することができます。  
  
詳細については、要求規則および要求規則セットを参照してください。[、要求規則の役割](The-Role-of-Claim-Rules.md)します。 規則が処理される方法の詳細については、次を参照してください。[The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md)します。 要求規則セットを処理する方法の詳細については、次を参照してください。[要求パイプラインの役割](The-Role-of-the-Claims-Pipeline.md)します。  
  
## <a name="permit-all-users"></a>すべてのユーザーを許可します。  
すべてのユーザーを許可規則テンプレートを使用すると、すべてのユーザーは、証明書利用者へのアクセスがあります。 ただし、追加の承認規則を使用して、さらにアクセスを制限することができます。 1 つのルールは、証明書利用者にアクセスするユーザーを許可し、別のルールを証明書利用者のパーティーにユーザーのアクセスを拒否する場合は、拒否の結果が許可結果を上書きし、ユーザーがアクセスを拒否します。  
  
フェデレーション サービスから証明書利用者へのアクセスを許可するユーザーを可能性がありますもによって拒否されるサービス証明書利用者のパーティします。  
  
## <a name="permit-access-to-users-with-this-incoming-claim"></a>この入力方向の要求を持つユーザーにアクセスを許可します。  
使用すると、基づく許可または拒否ユーザー入力方向の要求規則テンプレートに規則を作成することを許可する条件を設定して、種類と、入力方向の要求の値に基づいて証明書利用者に特定のユーザーのアクセスを許可することができます。 たとえば、この規則テンプレートを使用して、含まれるグループ要求の Domain Admins という値を持つユーザーのみを許可する規則を作成することができます。 1 つのルールは、証明書利用者にアクセスするユーザーを許可し、別のルールを証明書利用者のパーティーにユーザーのアクセスを拒否する場合は、拒否の結果が許可結果を上書きし、ユーザーがアクセスを拒否します。  
  
ユーザーは、フェデレーション サービスから証明書利用者にアクセスする許可されている可能性がありますもによって拒否されるサービス証明書利用者のパーティします。 証明書利用者にアクセスするすべてのユーザーを許可する場合は、すべてのユーザーを許可規則テンプレートを使用します。  
  
## <a name="deny-access-to-users-with-this-incoming-claim"></a>この入力方向の要求を持つユーザーにアクセス権を拒否します。  
使用すると、基づく許可または拒否ユーザー入力方向の要求規則テンプレートに規則を作成し、拒否する条件を設定する、種類と、入力方向の要求の値に基づいて証明書利用者にユーザーのアクセスを拒否できます。 たとえば、この規則テンプレートを使用して、ドメイン ユーザーの値を持つグループのすべてのユーザーが要求を拒否する規則を作成することができます。  
  
拒否の条件を使用して、まだも特定のユーザーの証明書利用者へのアクセスを有効にする場合は、後で明示的に許可の条件をそのユーザー証明書利用者へのアクセスを有効にすると、承認規則を追加する必要があります。  
  
場合は、ユーザーがアクセスを拒否される、要求発行エンジンが規則セットを処理するときは、さらに規則の処理がシャット ダウンし、AD FS では、ユーザーの要求に「アクセス拒否」エラーを返します。  
  
## <a name="authorizing-users"></a>ユーザーの承認  
は、AD FS の承認規則を使用して、許可または拒否要求をユーザーまたはユーザーのグループかどうかを決定するして \ もよりますが、要求の種類 used\) ができるかどうか、指定された証明書利用者の Web ベースのリソースにアクセスします。 承認規則は、証明書利用者信頼にのみ設定できます。  
  
### <a name="authorization-rule-sets"></a>承認規則セット  
別の承認規則セット許可の種類に応じて存在操作または拒否操作を構成する必要があります。 これらの規則セットは、次のとおりです。  
  
-   **発行承認規則**: これらの規則はかどうかユーザー証明書利用者の要求を受信して、そのため、証明書利用者へのアクセスを決定します。  
  
-   **委任承認規則**: これらのルールは、ユーザーが証明書利用者に対して別のユーザーとして動作できるかどうかを決定します。 ユーザーが別のユーザーとして動作しているときに、要求元ユーザーに関する要求まだトークンに配置されます。  
  
-   **偽装承認規則**: これらの規則では、ユーザーが証明書利用者に対して別のユーザーを完全に偽装するかどうかを決定します。 証明書利用者は、ユーザーが偽装されていることを把握していないため、非常に強力な機能は別のユーザーを偽装します。  
  
承認規則プロセスが要求発行パイプラインにどのように適合する方法の詳細については、要求発行エンジンの役割を参照してください。  
  
### <a name="supported-claim-types"></a>サポートされている要求の種類  
AD FSdefines 2 つの要求の種類を使用して、ユーザーが許可または拒否するかどうかを決定します。 これらの要求の種類 Uniform Resource Identifier が \(URIs\) は次のようにします。  
  
1.  **許可**: http:///\/schemas.microsoft.com\/authorization\/claims\/permit  
  
2.  **拒否**: http:///\/schemas.microsoft.com\/authorization\/claims\/deny  
  
## <a name="how-to-create-this-rule"></a>このルールを作成する方法  
要求規則言語を使用して、またはを使用して両方の承認規則を作成することができます、**すべてのユーザーを許可**規則テンプレートまたは**の許可または拒否に基づいてユーザー入力方向の要求**規則テンプレートの AD FS 管理スナップインでします。 すべてのユーザーを許可規則テンプレートは、すべての構成オプションを提供しません。 ただし、許可または拒否する入力方向の要求規則テンプレートに基づくユーザーは、次の構成オプションを提供します。  
  
-   要求規則名を指定します。  
  
-   入力方向の要求の種類を指定します。  
  
-   入力方向の要求の値を入力します。  
  
-   この入力方向の要求を持つユーザーにアクセスを許可します。  
  
-   この入力方向の要求を持つユーザーにアクセス権を拒否します。  
  
このテンプレートを作成する方法の詳細については、次を参照してください。[すべてのユーザーを許可する規則を作成する](https://technet.microsoft.com/library/ee913577.aspx)または[入力方向の要求に基づく許可または拒否のユーザーにルールを作成](https://technet.microsoft.com/library/ee913594.aspx)AD FS 展開ガイドにします。  
  
## <a name="using-the-claim-rule-language"></a>要求規則言語を使用します。  
要求の値がカスタム パターンに一致する場合にのみ、要求を送信する必要があります、カスタム規則を使用する必要があります。 詳細については、次を参照してください。[When to Use a Custom Claim Rule](When-to-Use-a-Custom-Claim-Rule.md)します。  
  
### <a name="example-of-how-to-create-an-authorization-rule-based-on-multiple-claims"></a>複数の要求に基づいて承認規則を作成する方法の例  
要求規則言語構文を使用して要求を承認するために場合、ユーザーの元の要求で複数の要求の有無に基づいて、信頼性情報も発行することができます。 次の規則は、ユーザーが Editor グループのメンバーであるし、Windows 認証を使用して認証している場合にのみ承認要求を発行します。  
  
```  
[type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod",   
value == "urn:federation:authentication:windows" ]  
&& [type == "http://schemas.xmlsoap.org/claims/Group ", value == “editors”]   
=> issue(type = "http://schemas.xmlsoap.org/claims/authZ", value = "Granted");  
```  
  
### <a name="example-of-how-to-create-authorization-rules-that-will-delegate-who-can-create-or-remove-federation-server-proxy-trusts"></a>承認を作成する方法の例の規則を委任を作成したり、フェデレーション サーバー プロキシ信頼を削除します。  
フェデレーション サービスは、フェデレーション サーバー プロキシを使用して、クライアント要求をリダイレクトが、前に、信頼まず、フェデレーション サービスとフェデレーション サーバー プロキシ コンピューター間で確立する必要があります。 既定では、プロキシ信頼が確立されているときに次の資格情報のいずれかで提供されているが正常に AD FS フェデレーション サーバー プロキシ構成ウィザード。  
  
-   プロキシによって保護されるフェデレーション サービスによって使用される、サービス アカウント  
  
-   フェデレーション サーバー ファーム内のすべてのフェデレーション サーバーのローカルの Administrators グループのメンバーある Active Directory ドメイン アカウント  
  
指定されたフェデレーション サービスのプロキシ信頼を作成できるユーザーまたはユーザーを指定する場合は、次の委任方法のいずれかを使用できます。 このメソッドの一覧では、優先順位に従って、委任の少なくとも問題がある最も安全な方法の AD FS 製品チームの推奨事項に基づくです。 組織のニーズに応じて、これらのメソッドの 1 つだけを使用する必要があります。  
  
1.  Active Directory にドメイン セキュリティ グループを作成 \ (たとえば、FSProxyTrustCreators\) には、それぞれ、ファーム内のフェデレーション サーバーのローカルの Administrators グループにこのグループを追加し、新しいグループには、この権限を委任するユーザー アカウントのみを追加します。 これは、推奨される方法です。  
  
2.  各ファーム内のフェデレーション サーバーの管理者グループにユーザーのドメイン アカウントを追加します。  
  
3.  何らかの理由でこれらのメソッドのいずれかを使用することはできない場合、は、この目的の承認規則を作成することもできます。 お勧めできませんが — このルールが正しく記述されていない場合に発生する可能性があります可能な複雑な問題のため — どの Active Directory ドメイン ユーザー アカウントもを作成したりも指定されたフェデレーション サービスに関連付けられているすべてのフェデレーション サーバー プロキシ間の信頼関係を削除を委任するカスタム承認規則を使用することができます。  
  
    指定したユーザーを許可する承認要求を発行する、次の規則の構文を使用するには 3 の方法を選択した場合 \ (ここでは、contoso\\frankm\) フェデレーション サービスのプロキシ サーバーの 1 つまたは複数のフェデレーションの信頼を作成します。 Windows PowerShell コマンドを使用してこの規則を適用する必要があります**になって ADFSProperties AddProxyAuthorizationRules**します。  
  
    ```  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", issuer=~"^AD AUTHORITY$" value == "contoso\frankm" ] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true")  
  
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-544", Issuer =~ "^AD AUTHORITY$"])   
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", Issuer =~ "^AD AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustManagerSid({0})", param= c.Value );  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/proxytrustid", Issuer =~ "^SELF AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustProvisioned({0})", param=c.Value );  
    ```  
  
    後で、ユーザーが不要になったプロキシ信頼を作成するために、ユーザーを削除する場合は、フェデレーション サービスのプロキシ信頼を作成するユーザーの権利を削除する既定のプロキシ信頼の承認規則を戻すことができます。 Windows PowerShell コマンドを使用してこの規則を適用する必要がありますも**になって ADFSProperties AddProxyAuthorizationRules**します。  
  
    ```  
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-544", Issuer =~ "^AD AUTHORITY$"])   
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", Issuer =~ "^AD AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustManagerSid({0})", param= c.Value );  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/proxytrustid", Issuer =~ "^SELF AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustProvisioned({0})", param=c.Value );  
    ```  
  
要求規則言語を使用する方法の詳細については、次を参照してください。[要求規則言語の役割](The-Role-of-the-Claim-Rule-Language.md)します。  
  

