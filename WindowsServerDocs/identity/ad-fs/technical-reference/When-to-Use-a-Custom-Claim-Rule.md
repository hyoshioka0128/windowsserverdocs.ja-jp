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
ms.openlocfilehash: e566de4df2895dfa2ed1104f85c1429881ff5bbf
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188286"
---
# <a name="when-to-use-a-custom-claim-rule"></a>カスタム要求規則を使用する状況
Active Directory フェデレーション サービスでカスタム要求規則を記述する\(AD FS\) framework 要求発行エンジンを使用してプログラムで生成するには、要求規則言語を使用して変換、パススルー、およびフィルター処理要求。 カスタム規則を使用することで、標準的な規則テンプレートよりもさらに複雑なロジックを持つ規則を作成できます。 次の状況に該当する場合に、カスタム規則の使用を検討してください。  
  
-   構造化照会言語から抽出された値に基づいて要求を送信\(SQL\)属性ストアです。  
  
-   ライトウェイト ディレクトリ アクセス プロトコルから抽出された値に基づいて要求を送信\(LDAP\)属性ストアのカスタム LDAP フィルターを使用します。  
  
-   カスタム属性ストアから抽出された値に基づいて要求を送信する場合。  
  
-   2 つ以上の入力方向の要求が存在する場合にのみ要求を送信する必要がある場合。  
  
-   入力方向の要求の値が複雑なパターンに一致する場合にのみ要求を送信する場合。  
  
-   複雑な変更のある要求を、入力方向の要求の値に送信する場合。  
  
-   実際に要求を送らずに、後続の規則でのみ使用するための要求を作成する場合。  
  
-   1 つ以上の入力方向の要求のコンテンツから出力方向の要求を作成する場合。  
  
出力方向の要求の値が、入力方向の要求の値に基づく必要がある場合で、その他のコンテンツも含める必要がある場合もカスタム規則を使用できます。  
  
要求規則言語は、規則ベースの言語で、 条件部分と実行部分があります。 要求規則言語の構文を使用して、組織のニーズに合わせて要求を列挙、追加、削除、または変更できます。 動作をどのようにこれらの各部分についての詳細については、次を参照してください。[要求規則言語の役割](The-Role-of-the-Claim-Rule-Language.md)します。  
  
以下のセクションでは、要求規則の基本的な概要を説明します。 どのような場合にカスタム要求規則を使用するかにについても記載しています。  
  
## <a name="about-claim-rules"></a>要求規則について  
要求規則を表す入力方向の要求は、ビジネス ロジックのインスタンス、それに条件を適用\(x, y し場合\)条件パラメーターに基づいて出力方向の要求を生成します。  
  
> [!IMPORTANT]  
> -   AD FS 管理スナップインで\-での要求のみ要求規則テンプレートを使用してルールを作成することができます  
> -   要求規則プロセスが受信要求の要求プロバイダーから直接、 \(Active Directory または別のフェデレーション サービスなど\)または変換要求プロバイダー信頼規則、受け入れの出力から。  
> -   要求規則は、要求発行エンジンによって、特定の規則セット内で時系列に従って処理されます。 規則に優先順位を設定すると、特定の規則セット内の先行する規則で生成された要求をさらに調整またはフィルター処理できます。  
> -   要求規則テンプレートでは、常に入力方向の要求の種類を指定する必要があります。 ただし、1 つの規則を使用して、要求の種類が同じ複数の要求の値を処理できます。  
  
詳細については、要求規則および要求規則セットについてを参照してください。 [、要求規則の役割](The-Role-of-Claim-Rules.md)します。 ルールの処理方法の詳細については、次を参照してください。[要求エンジンの役割](The-Role-of-the-Claims-Engine.md)します。 要求規則セットを処理する方法の詳細については、次を参照してください。[要求パイプラインの役割](The-Role-of-the-Claims-Pipeline.md)します。  
  
## <a name="how-to-create-this-rule"></a>この規則の作成方法  
このルールを使用して要求送信で、結果をテキスト ボックスは、要求規則言語と、貼り付けを使用して、操作が提供する必要がある構文を最初に作成することによりテンプレートを作成するカスタム ルールをクレーム プロバイダーのいずれかのプロパティの trAD FS 管理スナップインで ust または証明書利用者の信頼\-でします。  
  
この規則テンプレートには、次のオプションがあります。  
  
-   要求規則名を指定する  
  
-   1 つを入力するか、要求規則言語のオプションの複数の条件と AD FS を使用して、発行ステートメント  
  
このテンプレートを使用して、カスタム ルールを作成する詳細手順については、次を参照してください。[送信要求を使用するルールをカスタム ルールを作成](https://technet.microsoft.com/library/dd807049.aspx)AD FS Deployment guide の「します。  
  
について理解を深めるの要求規則言語のしくみ、既に存在する他の規則の要求規則言語構文を表示、スナップインで\-でをクリックして、**規則言語の表示**ルールのプロパティ タブ。 このセクションの情報とこのタブの構文情報を使用すると、独自のカスタム規則を作成する方法を把握できます。  
  
要求規則言語を使用する方法の詳細については、次を参照してください。[要求規則言語の役割](The-Role-of-the-Claim-Rule-Language.md)します。  
  
## <a name="using-the-claim-rule-language"></a>要求規則言語の使用  
  
### <a name="example-how-to-combine-first-and-last-names-based-on-a-users-name-attribute-values"></a>以下に例を示します。ユーザーの名前属性の値に基づいて姓と名を結合する方法  
次の規則の構文は、特定の属性ストアの属性値からの姓と名を結合します。 ポリシー エンジンは、各条件の一致結果のデカルト積を形成します。 たとえば、名 {“Frank”, “Alan”} と姓 {“Miller”, “Shen”} の出力は、{“Frank Miller”, “Frank Shen”, “Alan Miller”, “Alan Shen”}: となります。  
  
```  
c1:[type == "http://exampleschema/firstname" ]  
&&  c2:[type == "http://exampleschema/lastname",]   
=> issue(type = "http://exampleschema/name", value = c1.value + “  “ + c2.value);  
```  
  
### <a name="example-how-to-issue-a-manager-claim-based-on-whether-users-have-direct-reports"></a>以下に例を示します。ユーザーに直属の部下があるかどうかに基づいてマネージャー要求をを発行する方法  
次の規則は、ユーザーに直属の部下がいる場合にのみマネージャー要求を発行します。  
  
```  
c:[type == "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name"] => add(store = "SQL Store", types = ("http://schemas.xmlsoap.org/claims/Reports"), query = "SELECT Reports FROM dbo.DirectReports WHERE UserName = {0}", param = c.value );  
count([type == “http://schemas.xmlsoap.org/claims/Reports“] ) > 0 => issue(= "http://schemas.xmlsoap.org/claims/ismanager", value = "true");  
```  
  
### <a name="example-how-to-issue-a-ppid-claim-based-on-an-ldap-attribute"></a>以下に例を示します。LDAP 属性に基づいて PPID 要求を発行する方法  
次の規則は、プライベートの個人識別子を発行\(PPID\)クレームに基づいて、 **windowsaccountname**と**originalissuer** LDAP 属性内のユーザーの属性ストア:  
  
```  
c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]  
 => issue(store = "_OpaqueIdStore", types = ("http://schemas.xmlsoap.org/ws/2005/05/identity/claims/privatepersonalidentifier"), query = "{0};{1};{2}", param = "ppid", param = c.Value, param = c.OriginalIssuer);  
```  
  
このクエリのユーザーを一意に識別するために使用できる一般的な属性には次のようなものがあります。  
  
-   **ユーザーの SID**  
  
-   **windowsaccountname**  
  
-   **samaccountname**  
  

