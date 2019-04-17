---
ms.assetid: 20d183f0-ef94-44bb-9dfc-ed93799dd1a6
title: "カスタム要求規則を使用する場合"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: f5398f0b10d9e62548145fdde0354a3d047eb0ae
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

# <a name="when-to-use-a-custom-claim-rule"></a>カスタム要求規則を使用する場合
要求発行エンジンを使用してプログラムで生成、変換、パススルーするフレームワークでは、要求規則言語を使用して Active Directory フェデレーション サービス \(AD FS\) でカスタム要求規則を作成し、要求をフィルター処理します。 カスタム規則を使用すると、標準的な規則テンプレートよりもさらに複雑なロジックを持つルールを作成することができます。 場合にカスタム規則の使用を検討してください。  
  
-   構造化照会言語 \(SQL\) 属性ストアから抽出された値に基づいて要求を送信します。  
  
-   カスタム LDAP フィルターを使用して、Lightweight Directory Access Protocol \(LDAP\) 属性ストアから抽出された値に基づいて要求を送信します。  
  
-   カスタム属性ストアから抽出された値に基づいて要求を送信します。  
  
-   2 つ以上の入力方向の要求がある場合にのみ要求を送信します。  
  
-   入力方向の要求の値と一致する複雑なパターン場合にのみ要求を送信します。  
  
-   入力方向に複雑な変更で信頼性情報の要求の値を送信します。  
  
-   実際に要求を送信せず、後続の規則でのみ使用するための信頼性情報を作成します。  
  
-   1 つ以上の入力方向の要求のコンテンツから出力方向の要求を作成します。  
  
出力方向の要求の要求の値は、入力方向の要求の値に基づく必要がありますが、その他のコンテンツを含める必要がありますも、カスタム規則を使用できます。  
  
信頼性情報規則言語は、規則ベース 条件部分と実行部分があります。 要求規則言語構文を使用して、列挙、追加、削除、またはを組織のニーズを満たすために信頼性情報を変更できます。 動作をこれらの各部分方法の詳細については、次を参照してください。[要求規則言語の役割](The-Role-of-the-Claim-Rule-Language.md)します。  
  
次のセクションでは、要求規則の概要を提供します。 詳細については、カスタム要求規則を使用する場合もあります。  
  
## <a name="about-claim-rules"></a>要求規則について  
要求規則は、入力方向の要求は、ビジネス ロジックのインスタンスを表す、条件を適用 \ (し y\ x の場合)、条件のパラメーターに基づいて出力方向の要求を生成します。  
  
> [!IMPORTANT]  
> -   AD FS の管理スナップインには、要求のみ要求規則テンプレートを使用して規則を作成することができます。  
> -   入力方向の要求規則プロセスを要求するか、要求プロバイダーから直接 \ (など、Active Directory または別のフェデレーション \) または受付の出力から、要求プロバイダー信頼規則を変換します。  
> -   要求規則は、特定の規則セット内で時系列要求発行エンジンによって処理されます。 規則に優先順位を設定、さらに調整したり、特定の規則セット内の先行する規則で生成された要求をフィルター処理できます。  
> -   常に要求規則テンプレートでは、入力方向の要求の種類を指定する必要があります。 ただし、1 つの規則を使用して要求の種類が同じで複数の要求の値を処理することができます。  
  
詳細については、要求規則および要求規則セットを参照してください。[、要求規則の役割](The-Role-of-Claim-Rules.md)します。 規則が処理される方法の詳細については、次を参照してください。[The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md)します。 要求規則セットを処理する方法の詳細については、次を参照してください。[要求パイプラインの役割](The-Role-of-the-Claims-Pipeline.md)します。  
  
## <a name="how-to-create-this-rule"></a>このルールを作成する方法  
このルールを作成するには、最初に、構文こと要求規則言語を使用して操作を行う必要があるとし、信頼要求プロバイダーのプロパティの [カスタム規則テンプレートを使用して信頼性情報、送信で提供されるテキスト ボックスに、結果を貼り付けるかの AD FS 管理スナップインで証明書利用者の信頼を作成します。  
  
この規則テンプレートは、次のオプションを提供します。  
  
-   要求規則名を指定します。  
  
-   いずれかを入力するか、要求規則言語のオプションの複数の条件と AD FS を使用して、発行ステートメント  
  
このテンプレートを使用してカスタム規則を作成するための詳細については、次を参照してください。[規則を作成する信頼性情報の送信を使用して、カスタム ルール](https://technet.microsoft.com/library/dd807049.aspx)AD FS 展開ガイドにします。  
  
さらに詳しく理解の要求規則言語のしくみ、既に存在するその他の規則の要求規則言語構文、スナップインでをクリックして表示、**[規則言語の**] タブで、その規則のプロパティ。 このタブのこのセクションの情報との構文情報を使用して、独自のカスタム規則を作成する方法に関する洞察を提供できます。  
  
要求規則言語を使用する方法の詳細については、次を参照してください。[要求規則言語の役割](The-Role-of-the-Claim-Rule-Language.md)します。  
  
## <a name="using-the-claim-rule-language"></a>要求規則言語を使用します。  
  
### <a name="example-how-to-combine-first-and-last-names-based-on-a-users-name-attribute-values"></a>例: ユーザーの名前属性の値に基づいて姓と名を結合する方法  
次の規則の構文は、属性の値で指定した属性ストアからの姓と名を結合します。 ポリシー エンジンは、各条件の一致のデカルト積を形成します。 たとえば、名 {"Frank","Alan"} と姓 {"Miller","Shen"} の出力は、{"Frank Miller","Frank Shen"、"Alan Miller","Alan Shen"} です。  
  
```  
c1:[type == "http://exampleschema/firstname" ]  
&&  c2:[type == "http://exampleschema/lastname",]   
=> issue(type = "http://exampleschema/name", value = c1.value + “  “ + c2.value);  
```  
  
### <a name="example-how-to-issue-a-manager-claim-based-on-whether-users-have-direct-reports"></a>例: ユーザーに直属の部下があるかどうかに基づいてマネージャー要求を発行する方法  
次の規則は、ユーザーに直属の部下がある場合にのみマネージャー要求を発行します。  
  
```  
c:[type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name"] => add(store = "SQL Store", types = ("http://schemas.xmlsoap.org/claims/Reports"), query = "SELECT Reports FROM dbo.DirectReports WHERE UserName = {0}", param = c.value );  
count([type == “http://schemas.xmlsoap.org/claims/Reports“] ) > 0 => issue(= "http://schemas.xmlsoap.org/claims/ismanager", value = "true");  
```  
  
### <a name="example-how-to-issue-a-ppid-claim-based-on-an-ldap-attribute"></a>例: LDAP 属性に基づいて PPID 要求を発行する方法  
次の規則に基づいて Private Personal 識別子 \(PPID\) 要求の発行、**windowsaccountname**と**originalissuer** LDAP 属性ストア内のユーザーの属性。  
  
```  
c:[Type == "https://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]  
 => issue(store = "_OpaqueIdStore", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier"), query = "{0};{1};{2}", param = "ppid", param = c.Value, param = c.OriginalIssuer);  
```  
  
このクエリのユーザーを一意に識別するために使用される共通の属性は次のとおりです。  
  
-   **ユーザーの SID**  
  
-   **windowsaccountname**  
  
-   **Sam アカウント名**  
  

