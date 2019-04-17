---
ms.assetid: 606f4196-b579-4806-a462-3abd4d93e87c
title: "As Claims Rule Send LDAP 属性を使用する場合"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 05a2dd88057b64675bbc3bd30724d1eda0880c44
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

# <a name="when-to-use-a-send-ldap-attributes-as-claims-rule"></a>As Claims Rule Send LDAP 属性を使用する場合
実際のライトウェイト ディレクトリ アクセス プロトコル \(LDAP\) 属性値の属性ストアに存在し、各 LDAP 属性信頼性情報の種類を関連付けるを含む出力方向の要求を発行するときに、Active Directory フェデレーション サービス \(AD FS\) でこの規則を使用することができます。 属性ストアの詳細については、次を参照してください。[、属性ストアの役割](The-Role-of-Attribute-Stores.md)します。  
  
この規則を使用するときに指定した各 LDAP 属性に対して要求を発行して、規則のロジックに一致するように、次の表で説明します。  
  
|規則のオプション|規則のロジック|  
|---------------|--------------|  
|LDAP 属性と出力方向の要求の種類のマッピング|属性ストアが等しい場合*指定した属性ストア*LDAP 属性に等しいと*値が指定されている*、LDAP 属性値をマップし、*指定した出力方向の要求*を入力し、要求を発行します。|  
  
次のセクションでは、要求規則の概要を提供します。 詳細については、信頼性情報規則として LDAP 属性の送信を使用する場合もあります。  
  
## <a name="about-claim-rules"></a>要求規則について  
要求規則は、入力方向の要求を行う、条件を適用するビジネス ロジックのインスタンスを表します \ (し y\ x の場合)、条件のパラメーターに基づいて出力方向の要求を生成します。 輪郭について知っておくべきヒントの要求規則を読む前に重要な一覧を次にこのトピックの「します。  
  
-   AD FS の管理スナップインには、要求規則でのみ作成できます要求規則テンプレートを使用します。  
  
-   入力方向の要求規則プロセスを要求するか、要求プロバイダーから直接 \ (など、Active Directory または別のフェデレーション \) または受付の出力から、要求プロバイダー信頼規則を変換します。  
  
-   要求規則は、特定の規則セット内で時系列要求発行エンジンによって処理されます。 規則に対する優先順位を設定、さらに調整したり、特定の規則セット内の先行する規則で生成された要求をフィルター処理できます。  
  
-   要求規則テンプレートを使用して、入力方向の要求の種類を指定する必要が常にします。 ただし、1 つの規則を使用して要求の種類が同じで、複数の要求の値を処理することができます。  
  
詳細については、要求規則および要求規則セットを参照してください。[、要求規則の役割](The-Role-of-Claim-Rules.md)します。 規則が処理される方法の詳細については、次を参照してください。[The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md)します。 要求規則セットを処理する方法の詳細については、次を参照してください。[要求パイプラインの役割](The-Role-of-the-Claims-Pipeline.md)します。  
  
## <a name="mapping-of-ldap-attributes-to-outgoing-claim-types"></a>LDAP 属性と出力方向の要求の種類のマッピング  
要求規則テンプレートとして LDAP 属性の送信を使用する場合は、その値を証明書利用者に要求として送信する Active Directory または Active Directory ドメイン サービスの \(AD DS\) などの LDAP 属性ストアから属性を選択できます。 これにより、承認のために使用できる出力方向の要求のセットに定義した属性ストアから特定の LDAP 属性が本質的にマップされます。  
  
このテンプレートを使用すると、1 つの規則から複数の要求として送信される、複数の属性を追加できます。 たとえば、この規則テンプレートを使用してから認証済みユーザーの属性値を検索する規則を作成することができます、**会社**と**部門**Active Directory 属性し、これらの値を 2 つの異なる出力方向の要求として送信します。  
  
すべてのユーザーのグループ メンバーシップを送信するのにこの規則を使用することもできます。 個々 のグループのメンバーシップのみを送信する場合は、要求規則テンプレートとグループ メンバーシップの送信を使用します。 詳細については、次を参照してください。[要求規則として a Send Group Membership を使用するときに](When-to-Use-a-Send-Group-Membership-as-a-Claim-Rule.md)します。  
  
## <a name="how-to-create-this-rule"></a>このルールを作成する方法  
要求として LDAP 属性の送信を使用して、AD FS の管理スナップインでテンプレートをルールまたは要求規則言語を使用して、この規則を作成できます。 この規則テンプレートは、次の構成オプションを提供します。  
  
-   要求規則名を指定します。  
  
-   LDAP 属性の抽出元の属性ストアを選択します。  
  
-   LDAP 属性と出力方向の要求の種類のマッピング  
  
このルールを作成する方法の詳細については、次を参照してください。[LDAP 属性を要求として送信する規則を作成する](https://technet.microsoft.com/library/dd807115.aspx)します。  
  
## <a name="using-the-claim-rule-language"></a>要求規則言語を使用します。  
Active Directory、AD DS、または Active Directory ライトウェイト ディレクトリ サービスの \(AD LDS\) にクエリが以外の LDAP 属性と比較する必要がある場合**samAccountname**、代わりにカスタム規則を使用する必要があります。 入力セット内の Windows アカウント名要求がない場合は、AD DS または AD LDS のクエリに使用する要求を指定するもカスタム規則を使用する必要があります。  
  
次の例は、いくつかの属性ストアのクエリおよび抽出のデータへの要求規則言語を使用してカスタム規則を作成するさまざまな方法を理解するのに役立つが提供されます。  
  
### <a name="example-how-to-query-an-ad-lds-attribute-store-and-return-a-specified-value"></a>例: する AD LDS 属性ストアを照会し、指定した値を返す方法  
パラメーターは、セミコロンで区切る必要があります。 最初のパラメーターは、LDAP フィルターです。 後続のパラメーターは、一致するオブジェクトを返す属性です。  
  
次の例は、ユーザーを検索する方法を示しています、**sAMAccountName**属性および e\ メール アドレス、ユーザーの mail 属性の値を使用しての要求を発行するには。  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]  
=> issue(store = "AD LDS", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"), query = "sAMAccountName={0};mail", param = regexreplace(c.Value, "(?<domain>[^\\]+)\\(?<user>.+)", "${user}"));  
  
```  
  
次の例は、ユーザーを検索する方法を示しています、**メール**属性およびユーザーの値を使用して役職と表示名の要求を発行する**タイトル**と**displayname**属性。  
  
```  
c:[Type == " http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress ", Issuer == "AD AUTHORITY"]  
=> issue(store = "AD LDS ", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/title","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/displayname"), query = "mail={0};title;displayname", param = c.Value);  
```  
  
次の例は、mail と title でユーザーを検索し、使用、ユーザーの表示名の要求を発行する方法を示しています。**displayname**属性。  
  
```  
c1:[Type == " http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"] && c2:[Type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/title"]  
=> issue(store = "AD LDS ", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/displayname"), query = "(&(mail={0})(title={1}));displayname", param = c1.Value, param = c2.Value);  
```  
  
### <a name="example-how-to-query-an-active-directory-attribute-store-and-return-a-specified-value"></a>例: Active Directory 属性ストアを照会し、指定した値を返す方法  
Active Directory のクエリは、ユーザーの名前を含める必要があります \ (、ドメイン名前 \/) と最後のパラメーターできるように、Active Directory 属性ストアをクエリとして正しいドメインです。 それ以外の場合、同じ構文はサポートされます。  
  
次の例は、ユーザーを検索する方法を示しています、**sAMAccountName**属性または自分のドメインに戻ると、**メール**属性。  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", Issuer == "AD AUTHORITY"]  
=> issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/emailaddress"), query = "sAMAccountName={0};mail;{1}", param = regexreplace(c.Value, "(?<domain>[^\\]+)\\(?<user>.+)", "${user}"), param = c.Value);  
```  
  
### <a name="example-how-to-query-an-active-directory-attribute-store-based-on-the-value-of-an-incoming-claim"></a>例: 入力方向の要求の値に基づいて Active Directory 属性ストアを照会する方法  
  
```  
c:[Type == "http://test/name"]  
  
   => issue(store = "Enterprise AD Attribute Store",  
  
         types = ("http://test/email"),  
  
         query = ";mail;{0}",  
  
         param = c.Value)  
  
```  
  
前のクエリは、次の 3 つの部分で構成されています。  
  
-   LDAP フィルター-属性をクエリするオブジェクトを取得するクエリのこの部分を指定します。 有効な LDAP クエリの詳細については、RFC 2254 を参照してください。 Active Directory 属性ストアのクエリを実行して、samAccountName\、LDAP フィルターを指定しない = {0} と見なされますクエリと Active Directory 属性ストアが {0} の値は、できるパラメーターを想定します。 それ以外の場合、クエリはエラーになります。 Active Directory 以外の LDAP 属性ストア、クエリの LDAP フィルターの部分を省略することはできませんか、クエリはエラーになります。  
  
-   属性の指定-クエリの 2 番目の部分では、属性を指定 \ (これは、複数の属性 values\ を使用する場合のコンマ区切り) をフィルター処理されたオブジェクトから場合します。 指定した属性の数は、クエリに定義する要求の種類の数に一致する必要があります。  
  
-   Active Directory ドメイン-属性ストアが Active Directory の場合にのみ、クエリの最後の部分を指定します。 \ (その他の属性ストア。クエリする場合は必要ありません \)、クエリのこの部分はフォーム domain\\name でユーザー アカウントを指定するために使用します。 Active Directory 属性ストアでは、ドメインの部分を使用して、適切なドメイン コントローラーに接続して、クエリを実行して、属性を要求を調べます。  
  
### <a name="example-how-to-use-two-custom-rules-to-extract-the-manager-e-mail-from-an-attribute-in-active-directory"></a>例: 2 つのカスタム規則を使用して、Active Directory 内の属性からマネージャー e\ メールを抽出する方法  
次 2 つカスタムの規則を次に示す順序で一緒に使用するときは Active Directory のクエリ、**manager** \(Rule 1\) のアカウントとしてクエリの管理者のユーザー アカウントをその属性を使用してユーザーの属性、**メール**\(Rule 2\) の属性です。 最後に、**メール**属性を"ManagerEmail"の要求としてに発行します。 要約すると、規則 1 は Active Directory のクエリを実行し、e\ メール値のクエリの結果をマネージャーを抽出し、規則 2 に渡します。  
  
たとえば、これらの規則が実行を終了時に要求が発行される corp.fabrikam.com ドメイン内のユーザーのマネージャーの e\ メール アドレスを含みます。  
  
**規則 1**  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]  
=> add(store = "Active Directory", types = ("http://schemas.xmlsoap.org/claims/ManagerDistinguishedName"), query = "sAMAccountName=  
{0};mail,userPrincipalName,extensionAttribute5,manager,department,extensionAttribute2,cn;{1}", param = regexreplace(c.Value, "(?  
<domain>[^\\]+)\\(?<user>.+)", "${user}"), param = c.Value);  
```  
  
**ルール 2**  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]  
&& c1:[Type == "http://schemas.xmlsoap.org/claims/ManagerDistinguishedName"]  
=> issue(store = "Active Directory", types = ("http://schemas.xmlsoap.org/claims/ManagerEmail"), query = "distinguishedName={0};mail;{1}", param = c1.Value,   
param = regexreplace(c1.Value, ".*DC=(?<domain>.+),DC=corp,DC=fabrikam,DC=com", "${domain}\username"));  
```  
  
> [!NOTE]  
> ユーザーのマネージャーが、ユーザーと同じドメイン内にある場合にのみこれらの規則が動作 \ (この example\ で corp.fabrikam.com)。  
  
## <a name="additional-references"></a>その他の参照  
[LDAP 属性を要求として送信する規則を作成します。](https://technet.microsoft.com/library/dd807115.aspx)  
  

