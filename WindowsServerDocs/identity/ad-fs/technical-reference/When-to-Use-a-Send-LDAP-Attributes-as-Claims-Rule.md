---
ms.assetid: 606f4196-b579-4806-a462-3abd4d93e87c
title: "\"LDAP 属性を要求として送信\" 規則を使用するタイミング"
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: bc7b98a5d65bf03eb11ed57a8a5f9a0ea696df19
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853775"
---
# <a name="when-to-use-a-send-ldap-attributes-as-claims-rule"></a>"LDAP 属性を要求として送信" 規則を使用するタイミング
この規則は、実際のライトウェイトディレクトリアクセスプロトコル \(属性ストアに存在する LDAP\) 属性値を含む出力方向の要求を発行した後、要求の種類を各 LDAP 属性に関連付ける場合に Active Directory フェデレーションサービス (AD FS) \(AD FS\) で使用できます。 属性ストアの詳細については、「[属性ストアの役割](The-Role-of-Attribute-Stores.md)」を参照してください。  
  
この規則を使用すると、次の表で説明するように、指定した各 LDAP 属性に対して、規則のロジックに一致する場合に要求が発行されます。  
  
|規則のオプション|規則のロジック|  
|---------------|--------------|  
|出力方向の要求の種類に LDAP 属性をマップする|属性ストアが*指定した属性ストア*と等しく、LDAP 属性が*指定した値*と等しい場合、その LDAP 属性値を*指定した出力方向の要求*の種類にマップし、要求を発行します。|  
  
以下のセクションでは、要求規則の基本的な概要を説明します。 "LDAP 属性を要求として送信" 規則を使用するタイミングについても詳しく説明します。  
  
## <a name="about-claim-rules"></a>要求規則について  
要求規則は、入力方向の要求を受け取り、それに条件を適用するビジネスロジックのインスタンスを表します。この場合 \(x\) y の場合は、条件パラメーターに基づいて出力方向の要求を生成します。 次の一覧に、このトピックを読む前に理解しておく必要のある、要求規則に関する重要なヒントを示します。  
  
-   の AD FS 管理スナップ\-では、要求規則テンプレートを使用してのみ要求規則を作成できます。  
  
-   要求規則は、入力方向の要求を、Active Directory や別の\) フェデレーションサービスなどの要求プロバイダー \(から直接、または要求プロバイダー信頼の受け入れ変換規則の出力から処理します。  
  
-   要求規則は、要求発行エンジンによって、特定の規則セット内で時系列に従って処理されます。 規則に優先順位を設定すると、特定の規則セット内の先行する規則で生成された要求をさらに調整またはフィルター処理できます。  
  
-   要求規則テンプレートでは、常に入力方向の要求の種類を指定する必要があります。 ただし、1 つの規則を使用して、要求の種類が同じ複数の要求の値を処理できます。  
  
要求規則と要求規則セットの詳細については、「[要求規則の役割](The-Role-of-Claim-Rules.md)」を参照してください。 規則の処理方法の詳細については、「[要求エンジンの役割](The-Role-of-the-Claims-Engine.md)」を参照してください。 要求規則セットの処理方法の詳細については、「[要求パイプラインの役割](The-Role-of-the-Claims-Pipeline.md)」を参照してください。  
  
## <a name="mapping-of-ldap-attributes-to-outgoing-claim-types"></a>出力方向の要求の種類に LDAP 属性をマップする  
"LDAP 属性を要求として送信" 規則テンプレートを使用する場合は、Active Directory や Active Directory Domain Services \(AD DS\) などの LDAP 属性ストアから属性を選択して、証明書利用者に要求として値を送信することができます。 これにより、実質的に、ユーザーが定義した属性ストアから、承認に使用できる出力方向の要求のセットに各 LDAP 属性がマップされます。  
  
このテンプレートを使用することにより、単一の規則で、複数の属性を追加して複数の要求として送信できます。 たとえば、この規則テンプレートを使用して、**会社**および**部署**の Active Directory 属性から認証済みユーザーの属性値を検索し、それらの値を 2 つの異なる出力方向の要求として送信する規則を作成できます。  
  
この規則を使用して、すべてのユーザーのグループメンバーシップを送信することもできます。 個々のグループのメンバーシップのみを送信する場合は、"グループ メンバーシップを要求として送信" 規則テンプレートを使用します。 詳細については、「 [When to Use a Send Group Membership as a Claim Rule](When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md)」を参照してください。  
  
## <a name="how-to-create-this-rule"></a>この規則の作成方法  
この規則を作成するには、要求規則言語を使用するか、の AD FS 管理スナップ\-で [LDAP 属性を要求として送信] 規則テンプレートを使用します。 この規則テンプレートには、次の構成オプションがあります。  
  
-   要求規則名を指定する  
  
-   LDAP 属性の抽出元の属性ストアを選択する  
  
-   出力方向の要求の種類に LDAP 属性をマップする  
  
このルールを作成する方法の詳細については、「 [LDAP 属性を要求として送信するルールを作成](https://technet.microsoft.com/library/dd807115.aspx)する」を参照してください。  
  
## <a name="using-the-claim-rule-language"></a>要求規則言語の使用  
Active Directory、AD DS、または AD LDS \(Active Directory ライトウェイトディレクトリサービスに対するクエリを、 **samAccountname**以外の LDAP 属性と比較する必要がある場合は、代わりにカスタム規則を使用する必要があります。\) また、入力セットに Windows アカウント名要求がない場合も、AD DS または AD LDS のクエリに使用する要求を指定するためにカスタム規則を使用する必要があります。  
  
以下に示す例は、属性ストア内のデータにクエリを実行して抽出するために、要求規則言語を使用してカスタム規則を作成するさまざまな方法を理解するのに役立ちます。  
  
### <a name="example-how-to-query-an-adlds-attribute-store-and-return-a-specified-value"></a>例: AD LDS 属性ストアのクエリを実行し、指定した値を返す方法  
パラメーターは、セミコロンで区切る必要があります。 最初のパラメーターは、LDAP フィルターです。 後続のパラメーターは、一致するすべてのオブジェクトを返すための属性です。  
  
次の例では、 **sAMAccountName**属性でユーザーを検索し、ユーザーの mail 属性の値を使用して電子\-メールアドレス要求を発行する方法を示します。  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]  
=> issue(store = "AD LDS", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"), query = "sAMAccountName={0};mail", param = regexreplace(c.Value, "(?<domain>[^\\]+)\\(?<user>.+)", "${user}"));  
  
```  
  
次の例では、 **mail**属性でユーザーを検索し、ユーザーの**title**属性および**displayname**属性の値を使用して、タイトルと表示名の要求を発行する方法を示します。  
  
```  
c:[Type == " http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress ", Issuer == "AD AUTHORITY"]  
=> issue(store = "AD LDS ", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/title","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/displayname"), query = "mail={0};title;displayname", param = c.Value);  
```  
  
次の例は、メールとタイトルでユーザーを検索し、ユーザーの**displayname**属性を使用して表示名要求を発行する方法を示しています。  
  
```  
c1:[Type == " http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"] && c2:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/title"]  
=> issue(store = "AD LDS ", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/displayname"), query = "(&(mail={0})(title={1}));displayname", param = c1.Value, param = c2.Value);  
```  
  
### <a name="example-how-to-query-an-activedirectory-attribute-store-and-return-a-specified-value"></a>例: Active Directory 属性ストアのクエリを実行し、指定した値を返す方法  
Active Directory 属性ストアで正しいドメインを照会できるようにするには、Active Directory クエリには、ドメイン名\) を最後のパラメーターとして \(ユーザーの名前を含める必要があります。 それ以外は、上記と同じ構文がサポートされます。  
  
次の例は、該当ユーザーのドメイン内で **sAMAccountName** 属性でユーザーを検索し、**mail** 属性を返す方法を示しています。  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]  
=> issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"), query = "sAMAccountName={0};mail;{1}", param = regexreplace(c.Value, "(?<domain>[^\\]+)\\(?<user>.+)", "${user}"), param = c.Value);  
```  
  
### <a name="example-how-to-query-an-activedirectory-attribute-store-based-on-the-value-of-an-incoming-claim"></a>例: 入力方向の要求の値に基づいて Active Directory 属性ストアのクエリを実行する方法  
  
```  
c:[Type == "http://test/name"]  
  
   => issue(store = "Enterprise AD Attribute Store",  
  
         types = ("http://test/email"),  
  
         query = ";mail;{0}",  
  
         param = c.Value)  
  
```  
  
上記のクエリは、次の 3 つの部分で構成されています。  
  
-   LDAP フィルター - クエリのこの部分を指定することで、属性のクエリを実行する対象のオブジェクトを取得します。 有効な LDAP クエリに関する一般的な情報については、RFC 2254 を参照してください。 Active Directory 属性ストアに対してクエリを実行しているときに LDAP フィルターを指定していない場合は、samAccountName\={0} クエリと見なされ、Active Directory 属性ストアは {0}の値をフィードできるパラメーターを想定します。 設定できない場合、クエリはエラーになります。 Active Directory 以外の LDAP 属性ストアの場合、クエリの LDAP フィルターの部分は省略できません。省略すると、クエリはエラーになります。  
  
-   属性の指定-クエリのこの2番目の部分では、フィルター処理されたオブジェクトから除外する\) 複数の属性値を使用する場合に、コンマ\-区切り \(属性を指定します。 指定する属性の数は、クエリで定義する要求の種類の数と一致する必要があります。  
  
-   Active Directory ドメイン - 属性ストアが Active Directory である場合にのみ、クエリのこの最後の部分を指定します。 \(他の属性ストアに対してクエリを実行する場合は必要ありません。\) クエリのこの部分を使用して、ドメイン\\名の形式でユーザーアカウントを指定します。 Active Directory 属性ストアではドメインの部分を使用して、接続先として適切なドメイン コントローラーを判断し、クエリを実行して属性を要求します。  
  
### <a name="example-how-to-use-two-custom-rules-to-extract-the-manager-e-mail-from-an-attribute-in-activedirectory"></a>例: 2 つのカスタムルールを使用して、Active Directory の属性からマネージャー e\-メールを抽出する方法  
次の2つのカスタムルールを次に示す順序で使用した場合は、ユーザーアカウントの**manager**属性 \(ルール 1\) に対してクエリ Active Directory を実行し、その属性を使用して、 **Mail**属性 \(Rule 2\)のマネージャーのユーザーアカウントを照会します。 最後に、 **mail**属性は "manageremail" 要求として発行されます。 要約すると、ルール1は Active Directory を照会し、クエリの結果をルール2に渡します。これにより、manager e\-mail 値が抽出されます。  
  
たとえば、これらのルールの実行が完了すると、corp.fabrikam.com ドメイン内のユーザーに対応するマネージャーの\-電子メールアドレスを含む要求が発行されます。  
  
**ルール1**  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]  
=> add(store = "Active Directory", types = ("http://schemas.xmlsoap.org/claims/ManagerDistinguishedName"), query = "sAMAccountName=  
{0};mail,userPrincipalName,extensionAttribute5,manager,department,extensionAttribute2,cn;{1}", param = regexreplace(c.Value, "(?  
<domain>[^\\]+)\\(?<user>.+)", "${user}"), param = c.Value);  
```  
  
**規則2**  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]  
&& c1:[Type == "http://schemas.xmlsoap.org/claims/ManagerDistinguishedName"]  
=> issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/claims/ManagerEmail"), query = "distinguishedName={0};mail;{1}", param = c1.Value,   
param = regexreplace(c1.Value, ".*DC=(?<domain>.+),DC=corp,DC=fabrikam,DC=com", "${domain}\username"));  
```  
  
> [!NOTE]  
> これらの規則は、ユーザーのマネージャーがユーザー \(と同じドメインにある場合にのみ機能します。この例では、\)を corp.fabrikam.com します。  
  
## <a name="additional-references"></a>その他の参照情報  
[LDAP 属性を要求として送信するルールを作成する](https://technet.microsoft.com/library/dd807115.aspx)  
  

