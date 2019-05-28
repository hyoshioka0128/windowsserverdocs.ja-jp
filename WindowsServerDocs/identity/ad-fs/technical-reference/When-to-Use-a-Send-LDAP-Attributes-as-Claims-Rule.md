---
ms.assetid: 606f4196-b579-4806-a462-3abd4d93e87c
title: "\"LDAP 属性を要求として送信\" 規則を使用するタイミング"
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5af00db05c572a45811eea49b832a054a9e0e492
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188252"
---
# <a name="when-to-use-a-send-ldap-attributes-as-claims-rule"></a>"LDAP 属性を要求として送信" 規則を使用するタイミング
この規則を使用するには Active Directory フェデレーション サービスで\(AD FS\)実際のライトウェイト ディレクトリ アクセス プロトコルを含む出力方向の要求を発行するときに\(LDAP\)属性値内に存在します。属性は、格納し、各 LDAP 属性の要求の種類を関連付けます。 属性ストアの詳細については、次を参照してください。 [The Role of Attribute Stores](The-Role-of-Attribute-Stores.md)します。  
  
この規則を使用すると、次の表で説明するように、指定した各 LDAP 属性に対して、規則のロジックに一致する場合に要求が発行されます。  
  
|規則のオプション|規則のロジック|  
|---------------|--------------|  
|出力方向の要求の種類に LDAP 属性をマップする|属性ストアが*指定した属性ストア*と等しく、LDAP 属性が*指定した値*と等しい場合、その LDAP 属性値を*指定した出力方向の要求*の種類にマップし、要求を発行します。|  
  
以下のセクションでは、要求規則の基本的な概要を説明します。 "LDAP 属性を要求として送信" 規則を使用するタイミングについても詳しく説明します。  
  
## <a name="about-claim-rules"></a>要求規則について  
要求規則が入力方向の要求を実行を条件を適用するビジネス ロジックのインスタンスを表します\(x、y if\)条件パラメーターに基づいて出力方向の要求を生成します。 次の一覧に、このトピックを読む前に理解しておく必要のある、要求規則に関する重要なヒントを示します。  
  
-   AD FS 管理スナップインで\-要求規則テンプレートを使用してルールを作成することができますのみを要求  
  
-   要求規則プロセスが受信要求の要求プロバイダーから直接、 \(Active Directory または別のフェデレーション サービスなど\)または変換要求プロバイダー信頼規則、受け入れの出力から。  
  
-   要求規則は、要求発行エンジンによって、特定の規則セット内で時系列に従って処理されます。 規則に優先順位を設定すると、特定の規則セット内の先行する規則で生成された要求をさらに調整またはフィルター処理できます。  
  
-   要求規則テンプレートでは、常に入力方向の要求の種類を指定する必要があります。 ただし、1 つの規則を使用して、要求の種類が同じ複数の要求の値を処理できます。  
  
詳細については、要求規則および要求規則セットについてを参照してください。 [、要求規則の役割](The-Role-of-Claim-Rules.md)します。 ルールの処理方法の詳細については、次を参照してください。[要求エンジンの役割](The-Role-of-the-Claims-Engine.md)します。 要求規則セットを処理する方法の詳細については、次を参照してください。[要求パイプラインの役割](The-Role-of-the-Claims-Pipeline.md)します。  
  
## <a name="mapping-of-ldap-attributes-to-outgoing-claim-types"></a>出力方向の要求の種類に LDAP 属性をマップする  
Active Directory または Active Directory Domain Services などの LDAP 属性ストアから属性を選択するには、要求規則テンプレートとして送信 LDAP 属性を使用するときに\(AD DS\)証明書利用者に要求としてそれらの値を送信するには. これにより、実質的に、ユーザーが定義した属性ストアから、承認に使用できる出力方向の要求のセットに各 LDAP 属性がマップされます。  
  
このテンプレートを使用することにより、単一の規則で、複数の属性を追加して複数の要求として送信できます。 たとえば、この規則テンプレートを使用して、**会社**および**部署**の Active Directory 属性から認証済みユーザーの属性値を検索し、それらの値を 2 つの異なる出力方向の要求として送信する規則を作成できます。  
  
また、この規則を使用して、すべてのユーザーのグループ メンバーシップを送信することもできます。 個々のグループのメンバーシップのみを送信する場合は、"グループ メンバーシップを要求として送信" 規則テンプレートを使用します。 詳細については、「 [When to Use a Send Group Membership as a Claim Rule](When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md)」を参照してください。  
  
## <a name="how-to-create-this-rule"></a>この規則の作成方法  
要求規則言語を使用してこの規則を作成したり、AD FS 管理での要求規則テンプレートとして送信 LDAP 属性を使用してスナップ\-でします。 この規則テンプレートには、次の構成オプションがあります。  
  
-   要求規則名を指定する  
  
-   LDAP 属性の抽出元の属性ストアを選択する  
  
-   出力方向の要求の種類に LDAP 属性をマップする  
  
このルールを作成する方法の詳細については、次を参照してください。[要求として LDAP 属性を送信するルールを作成](https://technet.microsoft.com/library/dd807115.aspx)です。  
  
## <a name="using-the-claim-rule-language"></a>要求規則言語の使用  
場合に、Active Directory、AD DS、または Active Directory ライトウェイト ディレクトリ サービス クエリ\(AD LDS\)以外の LDAP 属性と比較する必要があります**samAccountname**、代わりにカスタム規則を使用する必要があります。 また、入力セットに Windows アカウント名要求がない場合も、AD DS または AD LDS のクエリに使用する要求を指定するためにカスタム規則を使用する必要があります。  
  
以下に示す例は、属性ストア内のデータにクエリを実行して抽出するために、要求規則言語を使用してカスタム規則を作成するさまざまな方法を理解するのに役立ちます。  
  
### <a name="example-how-to-query-an-adlds-attribute-store-and-return-a-specified-value"></a>以下に例を示します。AD LDS 属性ストアのクエリを実行し、指定した値を返す方法  
パラメーターは、セミコロンで区切る必要があります。 最初のパラメーターは、LDAP フィルターです。 後続のパラメーターは、一致するすべてのオブジェクトを返すための属性です。  
  
次の例でユーザーを検索する方法を示しています、 **sAMAccountName**属性し、発行、e\-ユーザーの mail 属性の値を使用して、メール アドレスを要求します。  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]  
=> issue(store = "AD LDS", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"), query = "sAMAccountName={0};mail", param = regexreplace(c.Value, "(?<domain>[^\\]+)\\(?<user>.+)", "${user}"));  
  
```  
  
次の例は、**mail** 属性でユーザーを検索し、ユーザーの **title** 属性および **displayname** 属性の値を使用して役職と表示名の要求を発行する方法を示しています。  
  
```  
c:[Type == " http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress ", Issuer == "AD AUTHORITY"]  
=> issue(store = "AD LDS ", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/title","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/displayname"), query = "mail={0};title;displayname", param = c.Value);  
```  
  
次の例は、mail と title でユーザーを検索し、ユーザーの **displayname** 属性を使用して表示名の要求を発行する方法を示しています。  
  
```  
c1:[Type == " http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"] && c2:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/title"]  
=> issue(store = "AD LDS ", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/displayname"), query = "(&(mail={0})(title={1}));displayname", param = c1.Value, param = c2.Value);  
```  
  
### <a name="example-how-to-query-an-activedirectory-attribute-store-and-return-a-specified-value"></a>以下に例を示します。Active Directory 属性ストアのクエリを実行し、指定した値を返す方法  
Active Directory のクエリは、ユーザーの名前を含める必要があります\(ドメイン名を持つ\)最後のパラメーター、Active Directory 属性を格納できるようにできますクエリとして適切なドメイン。 それ以外は、上記と同じ構文がサポートされます。  
  
次の例は、該当ユーザーのドメイン内で **sAMAccountName** 属性でユーザーを検索し、**mail** 属性を返す方法を示しています。  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]  
=> issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"), query = "sAMAccountName={0};mail;{1}", param = regexreplace(c.Value, "(?<domain>[^\\]+)\\(?<user>.+)", "${user}"), param = c.Value);  
```  
  
### <a name="example-how-to-query-an-activedirectory-attribute-store-based-on-the-value-of-an-incoming-claim"></a>以下に例を示します。入力方向の要求の値に基づいて Active Directory 属性ストアのクエリを実行する方法  
  
```  
c:[Type == "http://test/name"]  
  
   => issue(store = "Enterprise AD Attribute Store",  
  
         types = ("http://test/email"),  
  
         query = ";mail;{0}",  
  
         param = c.Value)  
  
```  
  
上記のクエリは、次の 3 つの部分で構成されています。  
  
-   LDAP フィルター - クエリのこの部分を指定することで、属性のクエリを実行する対象のオブジェクトを取得します。 有効な LDAP クエリに関する一般的な情報については、RFC 2254 を参照してください。 Active Directory 属性ストアのクエリを実行して、samAccountName、LDAP フィルターを指定しない\={0}クエリと見なされ、Active Directory 属性ストアの値をフィードできるパラメーターが必要ですが{0}. 設定できない場合、クエリはエラーになります。 Active Directory 以外の LDAP 属性ストアの場合、クエリの LDAP フィルターの部分は省略できません。省略すると、クエリはエラーになります。  
  
-   属性の指定: 属性を指定するクエリの 2 番目の部分で\(コンマは\-区切り、複数の属性値を使用する場合\)をフィルター処理されたオブジェクトから取得します。 指定する属性の数は、クエリで定義する要求の種類の数と一致する必要があります。  
  
-   Active Directory ドメイン - 属性ストアが Active Directory である場合にのみ、クエリのこの最後の部分を指定します。 \(その他の属性ストアを照会する際に必要はありません。\)クエリのこの部分がフォーム ドメインでユーザー アカウントを指定するために使用が\\名。 Active Directory 属性ストアではドメインの部分を使用して、接続先として適切なドメイン コントローラーを判断し、クエリを実行して属性を要求します。  
  
### <a name="example-how-to-use-two-custom-rules-to-extract-the-manager-e-mail-from-an-attribute-in-activedirectory"></a>以下に例を示します。2 つのカスタム規則を使用して、マネージャーの電子メールを抽出する方法\-Active Directory 内の属性からのメール  
2 つカスタムの規則を次に示す順序で一緒に使用する場合は Active Directory のクエリ、 **manager**のユーザー アカウント属性\(ルール 1\)し、その属性を使用して、ユーザーのクエリ管理者のアカウント、**メール**属性\(ルール 2\)します。 最後に、**mail** 属性を "ManagerEmail" の要求として発行します。 要約すると、ルール 1 は Active Directory クエリし、Rule 2 は、マネージャーの電子メールを抽出し、クエリの結果に渡します\-メールの値。  
  
たとえば、これらの規則の実行が完了時に要求が発行マネージャーの電子メールを含む\-メール、corp.fabrikam.com ドメイン内のユーザーのアドレス。  
  
**ルール 1**  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]  
=> add(store = "Active Directory", types = ("http://schemas.xmlsoap.org/claims/ManagerDistinguishedName"), query = "sAMAccountName=  
{0};mail,userPrincipalName,extensionAttribute5,manager,department,extensionAttribute2,cn;{1}", param = regexreplace(c.Value, "(?  
<domain>[^\\]+)\\(?<user>.+)", "${user}"), param = c.Value);  
```  
  
**Rule 2**  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]  
&& c1:[Type == "http://schemas.xmlsoap.org/claims/ManagerDistinguishedName"]  
=> issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/claims/ManagerEmail"), query = "distinguishedName={0};mail;{1}", param = c1.Value,   
param = regexreplace(c1.Value, ".*DC=(?<domain>.+),DC=corp,DC=fabrikam,DC=com", "${domain}\username"));  
```  
  
> [!NOTE]  
> これらのルール機能、ユーザーのマネージャーが、ユーザーと同じドメイン内にある場合にのみ\(この例では corp.fabrikam.com\)します。  
  
## <a name="additional-references"></a>その他の参照情報  
[要求として LDAP 属性を送信するルールを作成します。](https://technet.microsoft.com/library/dd807115.aspx)  
  

