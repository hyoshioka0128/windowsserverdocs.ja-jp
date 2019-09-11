---
ms.assetid: 20d183f0-ef94-44bb-9dfc-ed93799dd1a6
title: カスタム要求規則を使用する状況
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1a3f3e711d8e8443eb80109245eef42c668353d9
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70869292"
---
# <a name="when-to-use-a-custom-claim-rule"></a>カスタム要求規則を使用する状況
要求規則言語を使用して Active Directory フェデレーションサービス (AD FS) \(AD FS\)でカスタム要求規則を記述します。要求規則言語は、クレーム発行エンジンがプログラムによる生成、変換、パススルー、およびフィルター処理に使用するフレームワークです。保険. カスタム規則を使用することで、標準的な規則テンプレートよりもさらに複雑なロジックを持つ規則を作成できます。 次の状況に該当する場合に、カスタム規則の使用を検討してください。  
  
-   構造化照会言語\(SQL\)属性ストアから抽出された値に基づいて要求を送信します。  
  
-   カスタム ldap フィルターを使用して、ライトウェイトディレクトリアクセスプロトコル\(LDAP\)属性ストアから抽出された値に基づいて要求を送信します。  
  
-   カスタム属性ストアから抽出された値に基づいて要求を送信する場合。  
  
-   2 つ以上の入力方向の要求が存在する場合にのみ要求を送信する必要がある場合。  
  
-   入力方向の要求の値が複雑なパターンに一致する場合にのみ要求を送信する場合。  
  
-   複雑な変更のある要求を、入力方向の要求の値に送信する場合。  
  
-   実際に要求を送らずに、後続の規則でのみ使用するための要求を作成する場合。  
  
-   1 つ以上の入力方向の要求のコンテンツから出力方向の要求を作成する場合。  
  
出力方向の要求の値が、入力方向の要求の値に基づく必要がある場合で、その他のコンテンツも含める必要がある場合もカスタム規則を使用できます。  
  
要求規則言語は、規則ベースの言語で、 条件部分と実行部分があります。 要求規則言語の構文を使用して、組織のニーズに合わせて要求を列挙、追加、削除、または変更できます。 これらの各部分の動作の詳細については、「[要求規則言語の役割](The-Role-of-the-Claim-Rule-Language.md)」を参照してください。  
  
以下のセクションでは、要求規則の基本的な概要を説明します。 どのような場合にカスタム要求規則を使用するかにについても記載しています。  
  
## <a name="about-claim-rules"></a>要求規則について  
要求規則は、入力方向の要求を受け取るビジネスロジックのインスタンスを表します。 \(\)また、x の場合は条件を適用し、その後、条件パラメーターに基づいて出力方向の要求を生成します。  
  
> [!IMPORTANT]  
> -   AD FS 管理スナップイン\-では、要求規則テンプレートを使用してのみ要求規則を作成できます。  
> -   要求規則は、フェデレーションサービス\(\) Active Directory などの要求プロバイダーから直接、または要求プロバイダー信頼の受け入れ変換規則の出力から、入力方向の要求を処理します。  
> -   要求規則は、要求発行エンジンによって、特定の規則セット内で時系列に従って処理されます。 規則に優先順位を設定すると、特定の規則セット内の先行する規則で生成された要求をさらに調整またはフィルター処理できます。  
> -   要求規則テンプレートでは、常に入力方向の要求の種類を指定する必要があります。 ただし、1 つの規則を使用して、要求の種類が同じ複数の要求の値を処理できます。  
  
要求規則と要求規則セットの詳細については、「[要求規則の役割](The-Role-of-Claim-Rules.md)」を参照してください。 規則の処理方法の詳細については、「[要求エンジンの役割](The-Role-of-the-Claims-Engine.md)」を参照してください。 要求規則セットの処理方法の詳細については、「[要求パイプラインの役割](The-Role-of-the-Claims-Pipeline.md)」を参照してください。  
  
## <a name="how-to-create-this-rule"></a>この規則の作成方法  
この規則を作成するには、最初に要求規則言語を使用して操作に必要な構文を作成し、次に、要求プロバイダー tr のプロパティの [カスタム規則を使用して要求を送信] テンプレートに表示されるテキストボックスに結果を貼り付けます。AD FS 管理スナップイン\-での ust または証明書利用者の信頼。  
  
この規則テンプレートには、次のオプションがあります。  
  
-   要求規則名を指定する  
  
-   AD FS 要求規則言語を使用して、1つまたは複数のオプションの条件と発行ステートメントを入力します  
  
このテンプレートを使用してカスタムルールを作成する方法の詳細については、「AD FS 展開ガイド」の「[カスタムルールを使用して要求を送信するためのルールを作成する](https://technet.microsoft.com/library/dd807049.aspx)」を参照してください。  
  
要求規則言語のしくみについて理解を深めるには、その規則のプロパティの **[規則言語の表示]** タブを\-クリックして、スナップインに既に存在する他の規則の要求規則言語の構文を確認します。 このセクションの情報とこのタブの構文情報を使用すると、独自のカスタム規則を作成する方法を把握できます。  
  
要求規則言語の使用方法の詳細については、「[要求規則言語の役割](The-Role-of-the-Claim-Rule-Language.md)」を参照してください。  
  
## <a name="using-the-claim-rule-language"></a>要求規則言語の使用  
  
### <a name="example-how-to-combine-first-and-last-names-based-on-a-users-name-attribute-values"></a>例:ユーザーの名前属性値に基づいて姓と名を結合する方法  
次の規則の構文は、特定の属性ストアの属性値からの姓と名を結合します。 ポリシー エンジンは、各条件の一致結果のデカルト積を形成します。 たとえば、名 {“Frank”, “Alan”} と姓 {“Miller”, “Shen”} の出力は、{“Frank Miller”, “Frank Shen”, “Alan Miller”, “Alan Shen”}: となります。  
  
```  
c1:[type == "http://exampleschema/firstname" ]  
&&  c2:[type == "http://exampleschema/lastname",]   
=> issue(type = "http://exampleschema/name", value = c1.value + “  “ + c2.value);  
```  
  
### <a name="example-how-to-issue-a-manager-claim-based-on-whether-users-have-direct-reports"></a>例:ユーザーに直属の部下があるかどうかに基づいてマネージャー要求をを発行する方法  
次の規則は、ユーザーに直属の部下がいる場合にのみマネージャー要求を発行します。  
  
```  
c:[type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name"] => add(store = "SQL Store", types = ("http://schemas.xmlsoap.org/claims/Reports"), query = "SELECT Reports FROM dbo.DirectReports WHERE UserName = {0}", param = c.value );  
count([type == “http://schemas.xmlsoap.org/claims/Reports“] ) > 0 => issue(= "http://schemas.xmlsoap.org/claims/ismanager", value = "true");  
```  
  
### <a name="example-how-to-issue-a-ppid-claim-based-on-an-ldap-attribute"></a>例:LDAP 属性に基づいて PPID 要求を発行する方法  
次の規則は、LDAP 属性ストア\(の\)ユーザーの**windowsaccountname**および**originalissuer**属性に基づいて、プライベート個人識別子の PPID 要求を発行します。  
  
```  
c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]  
 => issue(store = "_OpaqueIdStore", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier"), query = "{0};{1};{2}", param = "ppid", param = c.Value, param = c.OriginalIssuer);  
```  
  
このクエリのユーザーを一意に識別するために使用できる一般的な属性には次のようなものがあります。  
  
-   **ユーザー SID**  
  
-   **windowsaccountname**  
  
-   **samaccountname**  
  

