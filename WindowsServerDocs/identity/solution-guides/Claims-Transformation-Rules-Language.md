---
ms.assetid: e831f781-3c45-4d44-b411-160d121d1324
title: 要求変換規則言語
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 200d592bc68562856bbdee623e70d73d41457c15
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357582"
---
# <a name="claims-transformation-rules-language"></a>要求変換規則言語

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

フォレスト間の要求変換機能を使用すると、フォレスト間の信頼に対して要求変換ポリシーを設定することによって、フォレストの境界を越えて動的 Access Control の要求をブリッジできます。 すべてのポリシーの主要なコンポーネントは、要求変換ルール言語で記述されたルールです。 このトピックでは、この言語について詳しく説明し、要求変換規則の作成に関するガイダンスを提供します。  
  
フォレスト全体の信頼に対する変換ポリシーの Windows PowerShell コマンドレットには、一般的なシナリオで必要な単純なポリシーを設定するためのオプションがあります。 これらのコマンドレットは、要求変換規則言語のポリシーと規則にユーザー入力を変換し、指定された形式で Active Directory に格納します。 要求変換のコマンドレットの詳細については、「[動的 Access Control 用の AD DS コマンドレット](https://go.microsoft.com/fwlink/?LinkId=243150)」を参照してください。  
  
要求の構成と Active Directory フォレスト内のフォレスト全体の信頼に対する要件によっては、要求の変換ポリシーが、Windows PowerShell コマンドレットでサポートされている Active のポリシーより複雑になることがあります。名簿. このようなポリシーを効果的に作成するには、要求変換規則言語の構文とセマンティクスを理解しておくことが不可欠です。 Active Directory のこの要求変換規則言語 ("言語") は、類似した目的で[Active Directory フェデレーションサービス (AD FS)](https://go.microsoft.com/fwlink/?LinkId=243982)によって使用される言語のサブセットであり、構文とセマンティクスが非常によく似ています。 ただし、許可される操作の数は減り、Active Directory バージョンの言語では追加の構文制限が適用されます。  
  
このトピックでは、Active Directory の要求変換規則言語の構文とセマンティクス、およびポリシーを作成するときに行う考慮事項について簡単に説明します。 これには、開始するためのいくつかのサンプルルールのセットと、不適切な構文の例と生成されるメッセージの例が用意されており、ルールの作成時にエラーメッセージを解読するのに役立ちます。  
  
## <a name="tools-for-authoring-claims-transformation-policies"></a>要求変換ポリシーを作成するためのツール  
**Active Directory 用の Windows PowerShell コマンドレット**: 要求変換ポリシーを作成および設定するための推奨される方法です。 これらのコマンドレットは、単純なポリシーのスイッチを提供し、より複雑なポリシーに設定されている規則を検証します。  
  
**Ldap**: ライトウェイトディレクトリアクセスプロトコル (ldap) を使用して Active Directory で要求変換ポリシーを編集できます。 ただし、これは推奨されません。ポリシーには複雑なコンポーネントがいくつかあり、使用するツールがポリシーを検証せずに Active Directory に書き込むことができるためです。 その後、問題を診断するためにかなりの時間が必要になることがあります。  
  
## <a name="active-directory-claims-transformation-rules-language"></a>Active Directory 要求変換ルール言語  
  
### <a name="syntax-overview"></a>構文の概要  
言語の構文とセマンティクスの概要を次に示します。  
  
-   要求変換規則セットは、0個以上の規則で構成されています。 各ルールには、**条件リスト**と**ルールアクション**の選択という2つのアクティブな部分があります。 **[条件の選択] の一覧**が TRUE と評価された場合、対応するルールアクションが実行されます。  
  
-   **Select 条件の一覧**には、0個以上の**select 条件**があります。 Select**条件リスト**が true と評価されるためには、すべての**選択条件**が true と評価される必要があります。  
  
-   各**Select 条件**には、0個以上の**一致条件**のセットがあります。 Select 条件が TRUE と評価されるためには、すべての**一致条件**が true と評価される必要があります。 これらのすべての条件は、1つのクレームに対して評価されます。 **Select 条件**に一致するクレームは、**識別子**でタグ付けし、**ルールアクション**で参照できます。  
  
-   **一致条件**ごとに、異なる**条件演算子**と**文字列リテラル**を使用して、クレームの**型**または**値**または**ValueType**と一致する条件を指定します。  
  
    -   **値**に**一致条件**を指定する場合は、特定の**ValueType**に**一致条件**を指定し、その逆も指定する必要があります。 これらの条件は、構文内で相互に隣接している必要があります。  
  
    -   **Valuetype**一致条件では、特定の**valuetype**リテラルのみを使用する必要があります。  
  
-   **ルールアクション**では、**識別子**を使用してタグ付けされた1つの要求をコピーすることも、識別子や指定された文字列リテラルを使用してタグ付けされた要求に基づいて1つの要求を発行することもできます。  
  
**ルールの例**  
  
次の例では、2つのフォレスト間で要求の種類を変換するために使用できる規則を示しています。これは、同じ要求 ValueTypes を使用し、この型の要求値に対して同じ解釈を持つ場合に使用します。 ルールには1つの一致条件と、文字列リテラルと一致する要求参照を使用する Issue ステートメントがあります。  
  
```  
C1: [TYPE=="EmployeeType"]    
                 => ISSUE (TYPE= "EmpType", VALUE = C1.VALUE, VALUETYPE = C1.VALUETYPE);  
[TYPE=="EmployeeType"] == Select Condition List with one Matching Condition for claims Type.  
ISSUE (TYPE= "EmpType", VALUE = C1.VALUE, VALUETYPE = C1.VALUETYPE) == Rule Action that issues a claims using string literal and matching claim referred with the Identifier.  
  
```  
  
### <a name="runtime-operation"></a>ランタイム操作  
ルールを効果的に作成するには、要求変換のランタイム操作を理解することが重要です。 ランタイム操作では、次の3つのクレームセットが使用されます。  
  
1.  **入力要求セット**: 要求変換操作に対して指定されるクレームの入力セット。  
  
2.  **Working claim set**: 要求変換中に読み取りおよび書き込みを行う中間要求。  
  
3.  **出力要求セット**: 要求変換操作の出力。  
  
ランタイム要求変換操作の簡単な概要を次に示します。  
  
1.  要求変換の入力要求は、作業中の要求セットを初期化するために使用されます。  
  
    1.  各ルールを処理するときに、入力要求に対して作業中の要求セットが使用されます。  
  
    2.  ルール内の選択条件リストは、作業中の要求セットから得られるすべての要求セットと照合されます。  
  
    3.  一致する要求の各セットを使用して、そのルールでアクションを実行します。  
  
    4.  ルールアクションを実行すると、1つの要求が生成されます。これは、出力要求セットと作業要求セットに追加されます。 したがって、規則の出力は、規則セット内の後続の規則の入力として使用されます。  
  
2.  規則セット内の規則は、最初の規則から順番に処理されます。  
  
3.  ルールセット全体が処理されると、出力要求セットが処理され、重複する要求とその他のセキュリティの問題が削除されます。結果として得られる要求は、要求変換プロセスの出力です。  
  
前の実行時の動作に基づいて、複雑な要求変換を作成することができます。  
  
**例: ランタイム操作**  
  
次の例では、2つの規則を使用する要求変換のランタイム操作を示します。  
  
```  
  
     C1:[Type=="EmpType", Value=="FullTime",ValueType=="string"] =>  
                Issue(Type=="EmployeeType", Value=="FullTime",ValueType=="string");  
     [Type=="EmployeeType"] =>   
               Issue(Type=="AccessType", Value=="Privileged", ValueType=="string");  
Input claims and Initial Evaluation Context:  
  {(Type= "EmpType"),(Value="FullTime"),(ValueType="String")}  
{(Type= "Organization"),(Value="Marketing"),(ValueType="String")}  
After Processing Rule 1:  
 Evaluation Context:  
  {(Type= "EmpType"),(Value="FullTime"),(ValueType="String")}  
{(Type= "Organization"), (Value="Marketing"),(ValueType="String")}  
  {(Type= "EmployeeType"),(Value="FullTime"),(ValueType="String")}  
Output Context:  
  {(Type= "EmployeeType"),(Value="FullTime"),(ValueType="String")}  
  
After Processing Rule 2:  
Evaluation Context:  
  {(Type= "EmpType"),(Value="FullTime"),(ValueType="String")}  
{(Type= "Organization"),(Value="Marketing"),(ValueType="String")}  
  {(Type= "EmployeeType"),(Value="FullTime"),(ValueType="String")}  
  {(Type= "AccessType"),(Value="Privileged"),(ValueType="String")}  
Output Context:  
  {(Type= "EmployeeType"),(Value="FullTime"),(ValueType="String")}  
  {(Type= "AccessType"),(Value="Privileged"),(ValueType="String")}  
  
Final Output:  
  {(Type= "EmployeeType"),(Value="FullTime"),(ValueType="String")}  
  {(Type= "AccessType"),(Value="Privileged"),(ValueType="String")}  
  
```  
  
### <a name="special-rules-semantics"></a>特別な規則のセマンティクス  
ルールには、次のような特殊な構文があります。  
  
1.  空の規則セット = = 出力要求なし  
  
2.  空の Select 条件リスト = = すべての要求が条件一覧に一致します  
  
    **例: 空の選択条件一覧**  
  
    次の規則は、ワーキングセット内のすべてのクレームに一致します。  
  
    ```  
    => Issue (Type = "UserType", Value = "External", ValueType = "string")  
    ```  
  
3.  空選択一致リスト = = すべての要求が条件一覧と一致します  
  
    **例: 空の一致条件**  
  
    次の規則は、ワーキングセット内のすべてのクレームに一致します。 これは、単独で使用される場合の基本的な "すべて許可" 規則です。  
  
    ```  
    C1:[] => Issule (claim = C1);  
    ```  
  
## <a name="security-considerations"></a>セキュリティの考慮事項  
**フォレストに入る要求**  
  
フォレストに着信するプリンシパルによって提示される要求は、正しい要求だけを許可または発行するように十分に検査する必要があります。 不適切な要求を行うと、フォレストのセキュリティが損なわれる可能性があります。これは、フォレストに入る要求の変換ポリシーを作成するときに考慮する必要があります。  
  
Active Directory には、フォレストに入る要求の構成の誤りを防ぐための次の機能があります。  
  
-   フォレストの信頼に、フォレストに入る要求に対して要求変換ポリシーが設定されていない場合、セキュリティ上の理由から、Active Directory は、フォレストに入るすべてのプリンシパル要求を削除します。  
  
-   フォレストに入る要求に対して規則セットを実行すると、フォレストで定義されていない要求が発生した場合に、未定義の要求が出力要求から削除されます。  
  
**フォレストを離れる要求**  
  
フォレストに参加している要求は、フォレストに入ってくる要求よりも、フォレストに対するセキュリティ上の懸念が低いことを示します。 対応する要求変換ポリシーが適用されていない場合でも、要求はフォレストをそのままにすることができます。 フォレストにある要求の変換の一部として、フォレストに定義されていない要求を発行することもできます。 これは、要求を使用してフォレスト間の信頼を簡単に設定するためのものです。 管理者は、フォレストに入る要求を変換する必要があるかどうかを判断し、適切なポリシーを設定できます。 たとえば、情報の漏えいを防ぐために要求を非表示にする必要がある場合に、管理者がポリシーを設定できます。  
  
**要求変換規則の構文エラー**  
  
特定の要求変換ポリシーの構文が正しくない規則セットがある場合、またはその他の構文や記憶域の問題がある場合、ポリシーは無効と見なされます。 これは、前に説明した既定の条件とは異なる方法で扱われます。  
  
Active Directory は、この場合の目的を特定できず、フェールセーフモードになります。このモードでは、その信頼とトラバーサルの方向に対して出力要求が生成されません。 この問題を解決するには、管理者の介入が必要です。 これは、要求変換ポリシーを編集するために LDAP が使用されている場合に発生する可能性があります。 Active Directory 用の Windows PowerShell コマンドレットでは、構文の問題があるポリシーを記述しないように検証が行われます。  
  
## <a name="other-language-considerations"></a>その他の言語に関する考慮事項  
  
1.  この言語 (ターミナルと呼ばれます) には、いくつかの重要な単語や文字があります。 これらは、このトピックで後述する[言語ターミナル](Claims-Transformation-Rules-Language.md#BKMK_LT)の表に記載されています。 エラーメッセージは、あいまいさを解消するために、これらの端末にタグを使用します。  
  
2.  端末は文字列リテラルとして使用することもできます。 ただし、このような使用方法は、言語定義と競合したり、意図しない結果になる場合があります。 この種類の使用は推奨されません。  
  
3.  ルールアクションでは、要求値に対して任意の型変換を実行できません。また、ルールアクションを含むルールセットは無効と見なされます。 これにより、ランタイムエラーが発生し、出力要求は生成されません。  
  
4.  ルールのアクションが、ルールの選択条件の一覧の部分で使用されていない識別子を参照している場合は、無効な使用法です。 これにより、構文エラーが発生します。  
  
    **例: 間違った識別子の参照**  
    次のルールは、ルールアクションで使用される間違った識別子を示しています。  
  
    ```  
    C1:[] => Issue (claim = C2);  
    ```  
  
## <a name="sample-transformation-rules"></a>変換規則のサンプル  
  
-   **特定の種類の要求をすべて許可する**  
  
    正確な型  
  
    ```  
    C1:[type=="XYZ"] => Issue (claim = C1);  
    ```  
  
    Regex の使用  
  
    ```  
    C1: [type =~ "XYZ*"] => Issue (claim = C1);  
    ```  
  
-   **特定の要求の種類を許可しない**  
    正確な型  
  
    ```  
    C1:[type != "XYZ"] => Issue (claim=C1);  
    ```  
  
    Regex の使用  
  
    ```  
    C1:[Type !~ "XYZ?"] => Issue (claim=C1);  
    ```  
  
## <a name="examples-of-rules-parser-errors"></a>ルールパーサーエラーの例  
要求変換ルールは、構文エラーをチェックするために、カスタムパーサーによって解析されます。 このパーサーは、Active Directory に規則を格納する前に、関連する Windows PowerShell コマンドレットによって実行されます。 構文エラーを含む規則の解析でエラーが発生すると、コンソールに出力されます。 また、ドメインコントローラーは、要求を変換するための規則を使用する前にパーサーを実行し、イベントログにエラーを記録します (イベントログ番号を追加します)。  
  
このセクションでは、不適切な構文を使用して記述されたルールの例と、パーサーによって生成される対応する構文エラーについて説明します。  
  
1. 以下に例を示します。  
  
   ```  
   c1;[]=>Issue(claim=c1);  
   ```  
  
   この例では、コロンの代わりに誤ってセミコロンを使用しています。   
   **エラー メッセージ:**  
   *POLICY0002: ポリシーデータを解析できませんでした。*  
   *行番号: 1、列番号: 2、エラートークン:;。行: ' c1;[] = > 問題 (要求 = c1); '。*  
   *パーサーエラー: ' POLICY0030: 構文エラーが発生し、予期しない '; ' が発生します。次のいずれかが必要です: ': '。 '*  
  
2. 以下に例を示します。  
  
   ```  
   c1:[]=>Issue(claim=c2);  
   ```  
  
   この例では、コピー発行ステートメントの Identifier タグは定義されていません。   
   **エラーメッセージ**:   
   *POLICY0011: CopyIssuanceStatement: ' c2 ' に指定された条件タグと一致する条件が要求規則にありません。*  
  
3. 以下に例を示します。  
  
   ```  
   c1:[type=="x1", value=="1", valuetype=="bool"]=>Issue(claim=c1)  
   ```  
  
   "bool" は言語のターミナルではなく、有効な ValueType ではありません。 有効なターミナルは、次のエラーメッセージに一覧表示されます。   
   **エラー メッセージ:**  
   *POLICY0002: ポリシーデータを解析できませんでした。*  
   行番号: 1、列番号:39、エラートークン: "bool"。 行: ' c1: [type = = "x1", value = = "1", valuetype = = "bool"] = > Issue (claim = c1); '。   
   *パーサーエラー: ' POLICY0030: 構文エラーが発生し、予期しない ' STRING ' が指定されています: ' INT64_TYPE ' ' UINT64_TYPE ' ' STRING_TYPE ' ' BOOLEAN_TYPE ' ' IDENTIFIER '*  
  
4. 以下に例を示します。  
  
   ```  
   c1:[type=="x1", value==1, valuetype=="boolean"]=>Issue(claim=c1);  
   ```  
  
   この例の数字**1**は、言語の有効なトークンではありません。このような使用方法は、一致条件では許可されていません。 文字列にするには、二重引用符で囲む必要があります。   
   **エラー メッセージ:**  
   *POLICY0002: ポリシーデータを解析できませんでした。*  
   *行番号: 1、列番号:23、エラートークン: 1。行: ' c1: [type = = "x1"、value = = 1、valuetype = = "bool"] = > Issue (claim = c1); '。* <em>パーサーエラー: ' POLICY0029: 予期しない入力です。</em>  
  
5. 以下に例を示します。  
  
   ```  
   c1:[type == "x1", value == "1", valuetype == "boolean"] =>   
  
        Issue(type = c1.type, value="0", valuetype == "boolean");  
   ```  
  
   この例では、単一の等号 (=) ではなく、2つの等号 (= =) を使用しています。   
   **エラー メッセージ:**  
   *POLICY0002: ポリシーデータを解析できませんでした。*  
   *行番号: 1、列番号:91、エラートークン: = =。行: ' c1: [type = = "x1", value = = "1",*  
   *valuetype = = "boolean"] = > Issue (type = c1. type, value = "0", valuetype = = "boolean"); '。*  
   *パーサーエラー: ' POLICY0030: 構文エラーです。予期しない ' = = ' が想定されています。次のいずれかが必要です: ' = '*  
  
6. 以下に例を示します。  
  
   ```  
   c1:[type=="x1", value=="boolean", valuetype=="string"] =>   
  
         Issue(type=c1.type, value=c1.value, valuetype = "string");  
   ```  
  
   この例は構文的で、意味は正しいです。 ただし、文字列値として "boolean" を使用すると、混乱を招く可能性があるため、回避する必要があります。 既に説明したように、可能な限り、言語端末を要求値として使用することは避けてください。  
  
## <a name="BKMK_LT"></a>言語ターミナル  
次の表に、すべてのターミナル文字列と、要求変換ルール言語で使用される関連言語ターミナルの一覧を示します。 これらの定義では、大文字と小文字を区別しない UTF-16 文字列を使用します。  
  
|String|ターミナル|  
|----------|------------|  
|"= >"|意味|  
|";"|セミコロン|  
|":"|:)|  
|","|傍点|  
|"."|.DOT|  
|"["|O_SQ_BRACKET|  
|"]"|C_SQ_BRACKET|  
|"("|O_BRACKET|  
|")"|C_BRACKET|  
|"=="|EQ|  
|"!="|NEQ|  
|"=~"|REGEXP_MATCH|  
|"!~"|REGEXP_NOT_MATCH|  
|"="|割り当てる|  
|"& &"|および|  
|関する|問題|  
|各種|TYPE|  
|数値|Value|  
|valuetype|VALUE_TYPE|  
|言う|言う|  
|"[_A-Za] [_A-a-za-z0-9] *"|識別子|  
|"\\" [^\\"\n] *\\" "|STRING|  
|uint64|UINT64_TYPE|  
|int64|INT64_TYPE|  
|文字列|STRING_TYPE|  
|演算|BOOLEAN_TYPE|  
  
## <a name="language-syntax"></a>言語の構文  
次の要求変換規則言語が ABNF form で指定されています。 この定義では、ここで定義されている ABNF の生産に加えて、前の表で指定されている端末を使用します。 規則は UTF-16 でエンコードする必要があり、文字列比較は大文字と小文字を区別しないものとして扱う必要があります。  
  
```  
Rule_set        = ;/*Empty*/  
             / Rules  
Rules         = Rule  
             / Rule Rules  
Rule          = Rule_body  
Rule_body       = (Conditions IMPLY Rule_action SEMICOLON)  
Conditions       = ;/*Empty*/  
             / Sel_condition_list  
Sel_condition_list   = Sel_condition  
             / (Sel_condition_list AND Sel_condition)  
Sel_condition     = Sel_condition_body  
             / (IDENTIFIER COLON Sel_condition_body)  
Sel_condition_body   = O_SQ_BRACKET Opt_cond_list C_SQ_BRACKET  
Opt_cond_list     = /*Empty*/  
             / Cond_list  
Cond_list       = Cond  
             / (Cond_list COMMA Cond)  
Cond          = Value_cond  
             / Type_cond  
Type_cond       = TYPE Cond_oper Literal_expr  
Value_cond       = (Val_cond COMMA Val_type_cond)  
             /(Val_type_cond COMMA Val_cond)  
Val_cond        = VALUE Cond_oper Literal_expr  
Val_type_cond     = VALUE_TYPE Cond_oper Value_type_literal  
claim_prop       = TYPE  
             / VALUE  
Cond_oper       = EQ  
             / NEQ  
             / REGEXP_MATCH  
             / REGEXP_NOT_MATCH  
Literal_expr      = Literal  
             / Value_type_literal  
  
Expr          = Literal  
             / Value_type_expr  
             / (IDENTIFIER DOT claim_prop)  
Value_type_expr    = Value_type_literal  
             /(IDENTIFIER DOT VALUE_TYPE)  
Value_type_literal   = INT64_TYPE  
             / UINT64_TYPE  
             / STRING_TYPE  
             / BOOLEAN_TYPE  
Literal        = STRING  
Rule_action      = ISSUE O_BRACKET Issue_params C_BRACKET  
Issue_params      = claim_copy  
             / claim_new  
claim_copy       = CLAIM ASSIGN IDENTIFIER  
claim_new       = claim_prop_assign_list  
claim_prop_assign_list = (claim_value_assign COMMA claim_type_assign)  
             /(claim_type_assign COMMA claim_value_assign)  
claim_value_assign   = (claim_val_assign COMMA claim_val_type_assign)  
             /(claim_val_type_assign COMMA claim_val_assign)  
claim_val_assign    = VALUE ASSIGN Expr  
claim_val_type_assign = VALUE_TYPE ASSIGN Value_type_expr  
Claim_type_assign   = TYPE ASSIGN Expr  
  
```  
  


