---
ms.assetid: b734cbcb-342c-4a28-8ab5-b9cd990bb1c2
title: 承認要求規則を使用するタイミング
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 2e8be891a8f09e38809503c40469e21a7e99687a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853765"
---
# <a name="when-to-use-an-authorization-claim-rule"></a>承認要求規則を使用するタイミング
この規則は、入力方向の要求の種類を取得する必要があり、規則で指定された値に基づいてユーザーがアクセスを許可または拒否するかどうかを決定するアクションを適用する場合に、Active Directory フェデレーションサービス (AD FS)\) AD FS \(で使用できます。 この規則を使用する場合、次の規則ロジックと一致する要求を、規則で構成するオプションに基づいてパススルーまたは変換します。  
  
|規則のオプション|規則のロジック|  
|---------------|--------------|  
|すべてのユーザーを許可|入力方向の要求の種類が *[すべての要求の種類]* に等しく、値が *[すべての値]* に等しい場合、値が *[許可]* に等しい要求が発行されます。|  
|この入力方向の要求を行ったユーザーのアクセスを許可|入力方向の要求の種類が *[指定された要求の種類]* に等しく、値が *[指定された要求の値]* に等しい場合は、値が *[許可]* に等しい要求が発行されます。|  
|この入力方向の要求を行ったユーザーのアクセスを拒否|入力方向の要求の種類が *[指定された要求の種類]* に等しく、値が *[指定された要求の値]* に等しい場合は、値が *[拒否]* に等しい要求が発行されます。|  
  
次のセクションでは、要求規則の概要と、その規則を使用するタイミングについて詳しく説明します。  
  
## <a name="about-claim-rules"></a>要求規則について  
要求規則は、入力方向の要求を受け取り、それに条件を適用するビジネスロジックのインスタンスを表します。この場合 \(x\) y の場合は、条件パラメーターに基づいて出力方向の要求を生成します。 次の一覧に、このトピックを読む前に理解しておく必要のある、要求規則に関する重要なヒントを示します。  
  
-   の AD FS 管理スナップ\-では、要求規則テンプレートを使用してのみ要求規則を作成できます。  
  
-   要求規則は、入力方向の要求を、Active Directory や別の\) フェデレーションサービスなどの要求プロバイダー \(から直接、または要求プロバイダー信頼の受け入れ変換規則の出力から処理します。  
  
-   要求規則は、要求発行エンジンによって、特定の規則セット内で時系列に従って処理されます。 規則に優先順位を設定すると、特定の規則セット内の先行する規則で生成された要求をさらに調整またはフィルター処理できます。  
  
-   要求規則テンプレートでは、常に入力方向の要求の種類を指定する必要があります。 ただし、1 つの規則を使用して、要求の種類が同じ複数の要求の値を処理できます。  
  
要求規則と要求規則セットの詳細については、「[要求規則の役割](The-Role-of-Claim-Rules.md)」を参照してください。 規則の処理方法の詳細については、「[要求エンジンの役割](The-Role-of-the-Claims-Engine.md)」を参照してください。 要求規則セットの処理方法の詳細については、「[要求パイプラインの役割](The-Role-of-the-Claims-Pipeline.md)」を参照してください。  
  
## <a name="permit-all-users"></a>すべてのユーザーを許可  
"すべてのユーザーを許可" 規則テンプレートを使用すると、すべてのユーザーが、証明書利用者にアクセスできます。 ただし、追加の承認規則を使用すると、アクセスを制限できます。 証明書利用者へのユーザーのアクセスを許可する規則と、拒否する規則が存在する場合は、拒否の結果が許可の結果よりも優先され、ユーザーのアクセスは拒否されます。  
  
ユーザーは、フェデレーション サービスから証明書利用者へのアクセスが許可されても、証明書利用者によってサービスが拒否される場合があります。  
  
## <a name="permit-access-to-users-with-this-incoming-claim"></a>この入力方向の要求を行ったユーザーのアクセスを許可  
"入力方向の要求に基づくユーザーの許可または拒否" 規則テンプレートを使用して規則を作成し、許可する条件を設定すると、入力方向の要求の種類と値に基づいて、証明書利用者への特定のユーザーのアクセスを許可することができます。 たとえば、この規則テンプレートを使用して、Domain Admins という値が含まれるグループ要求を持つユーザーのみを許可する規則を作成できます。 証明書利用者へのユーザーのアクセスを許可する規則と、拒否する規則が存在する場合は、拒否の結果が許可の結果よりも優先され、ユーザーのアクセスは拒否されます。  
  
ユーザーは、フェデレーション サービスから証明書利用者へのアクセスが許可されても、証明書利用者によってサービスが拒否される場合があります。 証明書利用者へのすべてのユーザーのアクセスを許可する場合は、"すべてのユーザーを許可" 規則テンプレートを使用します。  
  
## <a name="deny-access-to-users-with-this-incoming-claim"></a>この入力方向の要求を行ったユーザーのアクセスを拒否  
"入力方向の要求に基づくユーザーの許可または拒否" 規則テンプレートを使用して規則を作成し、条件を [拒否] に設定すると、入力方向の要求の種類と値に基づいて、証明書利用者へのユーザーのアクセスを拒否することができます。 たとえば、この規則テンプレートを使用して、Domain Users という値が含まれるグループ要求を持つすべてのユーザーを拒否する規則を作成できます。  
  
拒否の条件を使用しながら、特定のユーザーが証明書利用者にアクセスできるようにする場合は、許可の条件が指定された承認規則を後で明示的に追加して、そのユーザーが証明書利用者にアクセスできるようにする必要があります。  
  
要求発行エンジンが規則セットを処理するときに、ユーザーがアクセスを拒否された場合、さらに規則の処理がシャットダウンし、AD FS はユーザーの要求に "アクセスが拒否されました" というエラーを返します。  
  
## <a name="authorizing-users"></a>ユーザーの承認  
AD FS では、承認規則を使用して許可要求または拒否要求を発行し、\) 使用される要求の種類によって \(ユーザーまたはユーザーグループが特定の証明書利用者の Web\-ベースのリソースにアクセスできるかどうかを判断します。 承認規則は証明書利用者信頼を基づいてのみ設定できます。  
  
### <a name="authorization-rule-sets"></a>承認規則セット  
構成する必要がある許可操作または拒否操作に応じて、さまざまな承認規則セットがあります。 たとえば、次のような規則セットがあります。  
  
-   **発行承認規則**: この規則により、ユーザーが証明書利用者の要求を受信できるかどうか、つまり、その証明書利用者にアクセスできるかどうかが決まります。  
  
-   **委任承認規則**: この規則により、ユーザーが証明書利用者に対して別のユーザーとして動作できるかどうかが決まります。 ユーザーが別のユーザーとして動作しているとき、要求元のユーザーに関する要求はまだトークンにあります。  
  
-   **偽装承認規則**: この規則により、ユーザーが証明書利用者に対して別のユーザーを完全に偽装できるかどうかが決まります。 ユーザーが偽装されていることは証明書利用者に認識されないため、他のユーザーを偽装するこの機能は非常に強力です。  
  
承認規則プロセスが要求発行パイプラインにどのように適合するかの詳細については、要求発行エンジンの役割に関するトピックを参照してください。  
  
### <a name="supported-claim-types"></a>サポートされている要求の種類  
AD FS は、ユーザーが許可されるか拒否されるかを決定するために使用される2つの要求の種類を定義します。 これらの要求の種類の Uniform Resource identifier \(Uri\) は次のようになります。  
  
1.  **許可**: http:\/\/schemas.microsoft.com\/承認\/要求\/許可  
  
2.  **拒否**: http:\/\/schemas.microsoft.com\/承認\/要求\/拒否  
  
## <a name="how-to-create-this-rule"></a>この規則の作成方法  
両方の承認規則を作成するには、要求規則言語を使用するか、[**すべてのユーザーを許可**する] 規則テンプレートを使用するか、またはの AD FS 管理スナップ\-インで、[**入力方向の要求に基づいてユーザーを許可または拒否**する] 規則テンプレートを使用します。 "すべてのユーザーを許可" 規則テンプレートには、構成オプションは用意されていませんが、 "入力方向の要求に基づくユーザーの許可または拒否" 規則テンプレートには、次の構成オプションがあります。  
  
-   要求規則名を指定する  
  
-   入力方向の要求の種類を指定  
  
-   入力方向の要求値を入力  
  
-   この入力方向の要求を行ったユーザーのアクセスを許可  
  
-   この入力方向の要求を行ったユーザーのアクセスを拒否  
  
このテンプレートを作成する方法の詳細については、「AD FS 展開ガイド」の「[すべてのユーザーを許可する、](https://technet.microsoft.com/library/ee913577.aspx)または[入力方向の要求に基づいてユーザーを許可または拒否する規則](https://technet.microsoft.com/library/ee913594.aspx)を作成する」を参照してください。  
  
## <a name="using-the-claim-rule-language"></a>要求規則言語の使用  
要求値がカスタム パターンに一致する場合にのみ要求を送信する場合は、カスタム規則を使用する必要があります。 詳細については、「 [When to Use a Custom Claim Rule](When-to-Use-a-Custom-Claim-Rule.md)」を参照してください。  
  
### <a name="example-of-how-to-create-an-authorization-rule-based-on-multiple-claims"></a>複数の要求に基づいて承認規則を作成する方法の例  
要求規則言語の構文を使用して要求を承認する場合は、ユーザーの元の要求に複数の要求が存在するかどうかに基づいて要求を発行することもできます。 次の規則は、ユーザーが Editor グループのメンバーで、認証に Windows 認証を使用している場合にのみ承認要求を発行します。  
  
```  
[type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/authenticationmethod",   
value == "urn:federation:authentication:windows" ]  
&& [type == "http://schemas.xmlsoap.org/claims/Group ", value == "editors"]   
=> issue(type = "http://schemas.xmlsoap.org/claims/authZ", value = "Granted");  
```  
  
### <a name="example-of-how-to-create-authorization-rules-that-will-delegate-who-can-create-or-remove-federation-server-proxy-trusts"></a>フェデレーション サーバー プロキシ信頼の作成または削除を委任する承認規則を作成する例  
フェデレーション サービスでフェデレーション サーバー プロキシを使用してクライアント要求をリダイレクトする前に、まず、フェデレーション サービスとフェデレーション サーバー プロキシ コンピューターの間で信頼関係を確立する必要があります。 既定では、AD FS フェデレーション サーバー プロキシ構成ウィザードで次のいずれかの資格情報が適切に指定されたときに、プロキシの信頼が確立されます。  
  
-   フェデレーション サービスによって使用され、プロキシによって保護されるサービス アカウント  
  
-   フェデレーション サーバー ファーム内のフェデレーション サーバーすべてのローカル Administrators グループのメンバーである Active Directory ドメイン アカウント  
  
指定されたフェデレーション サービスに対するプロキシ信頼を作成できるユーザーを指定するには、次の委任方法のいずれかを使用します。 この一連の方法は、最も安全で問題の少ない委任方法に関する AD FS 製品チームの推奨事項に基づいて、優先順位が設定されています。 組織のニーズに応じて、必ずいずれか 1 つの方法のみを使用してください。  
  
1.  Active Directory \(でドメインセキュリティグループを作成します。たとえば、FSProxyTrustCreators\)、ファーム内の各フェデレーションサーバーのローカル Administrators グループにこのグループを追加し、この権限を新しいグループに委任するユーザーアカウントのみを追加します。 この方法を使用することをお勧めします。  
  
2.  ユーザーのドメインアカウントを、ファーム内の各フェデレーションサーバーの administrator グループに追加します。  
  
3.  何らかの理由で、どちらの方法も使用できない場合は、この目的で承認規則を作成することもできます。 正しく規則を記述しないと複雑になる可能性があるため、推奨できませんが、カスタム承認規則を使用して、Active Directory ドメイン ユーザー アカウントに、指定されたフェデレーション サービスに関連付けられているすべてのフェデレーション サーバー プロキシ間の信頼関係の作成または削除を委任することができます。  
  
    方法3を選択した場合は、次の規則構文を使用して、指定されたユーザー \(を許可する承認要求を発行できます。この場合、contoso\\frankm\) は、1つまたは複数のフェデレーションサーバープロキシの信頼をフェデレーションサービスに作成します。 この規則は、Windows PowerShell コマンド**セット\-Set-adfsproperties AddProxyAuthorizationRules**を使用して適用する必要があります。  
  
    ```  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", issuer=~"^AD AUTHORITY$" value == "contoso\frankm" ] => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true")  
  
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-544", Issuer =~ "^AD AUTHORITY$"])   
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", Issuer =~ "^AD AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustManagerSid({0})", param= c.Value );  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/proxytrustid", Issuer =~ "^SELF AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustProvisioned({0})", param=c.Value );  
    ```  
  
    後で、ユーザーがプロキシ信頼を作成できないようにユーザーを削除する必要がある場合は、既定のプロキシ信頼の承認規則に戻してユーザーの権限を削除し、フェデレーション サービスのプロキシ信頼を作成できます。 また、Windows PowerShell コマンド**セット\-Set-adfsproperties AddProxyAuthorizationRules**を使用して、この規則を適用する必要があります。  
  
    ```  
    exists([Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", Value == "S-1-5-32-544", Issuer =~ "^AD AUTHORITY$"])   
    => issue(Type = "https://schemas.microsoft.com/authorization/claims/permit", Value = "true");  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", Issuer =~ "^AD AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustManagerSid({0})", param= c.Value );  
  
    c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/proxytrustid", Issuer =~ "^SELF AUTHORITY$" ] => issue(store="_ProxyCredentialStore",types=("https://schemas.microsoft.com/authorization/claims/permit"),query="isProxyTrustProvisioned({0})", param=c.Value );  
    ```  
  
要求規則言語の使用方法の詳細については、「[要求規則言語の役割](The-Role-of-the-Claim-Rule-Language.md)」を参照してください。  
  

