---
ms.assetid: e831f781-3c45-4d44-b411-160d121d1324
title: 要求変換規則言語
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4a6b378bc4aef180ebedd260008febaa2f2a76ae
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856213"
---
# <a name="claims-transformation-rules-language"></a>要求変換規則言語

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

フォレスト間での要求にフォレストをまたいだ信頼に信頼性情報変換ポリシーを設定してフォレストの境界を越えてダイナミック アクセス制御の要求ブリッジする変換機能を使用します。 すべてのポリシーの主要なコンポーネントには、クレーム変換規則言語で記述されている規則です。 このトピックでは、この言語について詳しく説明し、クレーム変換規則を作成する方法のガイダンスを提供します。  
  
フォレスト間での変換ポリシー用の Windows PowerShell コマンドレットでは、オプションは、単純なポリシーを設定する必要が共通のシナリオを信頼します。 これらのコマンドレットは、ユーザーが入力クレームの変換規則言語でポリシーとルールに変換し、し、所定の形式で Active Directory に保存します。 クレームの変換用のコマンドレットの詳細については、次を参照してください。、[ダイナミック アクセス制御の AD DS コマンドレット](https://go.microsoft.com/fwlink/?LinkId=243150)します。  
  
要求の構成と、Active Directory フォレストのフォレストにまたがって信頼上に配置要件に応じて、信頼性情報変換ポリシーがアクティブの Windows PowerShell コマンドレットでサポートされているポリシーよりも複雑にする必要があります。ディレクトリ。 このようなポリシーを効果的に作成するには、クレーム変換規則言語構文とセマンティクスを理解する必要があります。 Active Directory での変換規則言語 (「言語」) で使用される言語のサブセットは、このクレーム[Active Directory フェデレーション サービス](https://go.microsoft.com/fwlink/?LinkId=243982)のような目的で、およびそれが構文とセマンティクスとよく似ています。 ただし、許可されている場合、以下の操作がある、追加の構文の制限は、Active Directory のバージョンの言語に配置されます。  
  
このトピックでは、構文とポリシーを作成する際に、Active Directory と考慮事項でクレーム変換規則言語のセマンティクスについて簡単に説明します。 を開始するための例の規則と不適切な構文と規則を作成するときにエラー メッセージを解読するため、生成したメッセージの例のいくつかのセットを提供します。  
  
## <a name="tools-for-authoring-claims-transformation-policies"></a>信頼性情報変換ポリシーを作成するためのツール  
**Active Directory 用 Windows PowerShell コマンドレット**:これは、作成、および信頼性情報変換ポリシーを設定する優先および推奨される方法です。 これらのコマンドレットは、単純なポリシーのスイッチを指定しより複雑なポリシーに設定されている規則を確認します。  
  
**LDAP**:Active Directory ライトウェイト ディレクトリ アクセス プロトコル (LDAP) 経由では、信頼性情報変換ポリシーを編集できます。 ただし、これは推奨されませんので、ポリシーがあるいくつかの複雑なコンポーネントとツールを使用する Active Directory に書き込む前にポリシーを検証しない可能性があります。 問題を診断する時間の非常に長い時間が、その後必要です。  
  
## <a name="active-directory-claims-transformation-rules-language"></a>Active Directory の要求規則言語の変換  
  
### <a name="syntax-overview"></a>構文の概要  
構文の概要と、言語のセマンティクスを次に示します。  
  
-   クレーム変換規則セットは、0 個以上の規則で構成されます。 各ルールでは、2 つのアクティブな部分があります。**条件の一覧を選択します。** と**ルール アクション**します。 場合、**選択条件の一覧**を TRUE に評価される、対応する規則の操作を実行します。  
  
-   **条件の一覧を選択します。** が 0 個以上**選択条件**します。 すべての**選択条件**プロパティを TRUE に評価する必要があります、**選択条件一覧**を TRUE に評価します。  
  
-   各**条件の選択**0 個以上のセットを持つ**一致条件**します。 すべての**一致条件**を TRUE に評価する選択条件を TRUE に評価される必要があります。 1 つの要求に対しては、すべての条件が評価されます。 一致する要求を**条件の選択**でタグ付けすることができます、**識別子**で参照されると、**ルール アクション**します。  
  
-   各**一致条件**と一致する条件を指定します、**型**または**値**または**ValueType**異なるを使用して、クレームの**条件演算子**と**文字列リテラル**します。  
  
    -   指定すると、**一致条件**の**値**も指定する必要があります、**一致条件**、特定の**ValueType**とその逆にします。 これらの条件は、互いの横にある構文である必要があります。  
  
    -   **ValueType**特定使用条件に一致する必要があります**ValueType**リテラルのみです。  
  
-   A**ルール アクション**タグ付けされている 1 つの要求をコピーすることができます、**識別子**識別子のタグ付けされている要求に基づくや文字列リテラルを指定された 1 つの要求を発行またはします。  
  
**ルールの例**  
  
この例では、同じ要求の Valuetype を使用して、この種類のクレーム値の解釈が同じであること、2 つのフォレスト間で信頼性情報の種類を変換するのに使用できる規則を使用します。 ルールは、1 つの一致条件とリテラル文字列と一致するクレームのリファレンスを使用した問題ステートメントにします。  
  
```  
C1: [TYPE=="EmployeeType"]    
                 => ISSUE (TYPE= "EmpType", VALUE = C1.VALUE, VALUETYPE = C1.VALUETYPE);  
[TYPE=="EmployeeType"] == Select Condition List with one Matching Condition for claims Type.  
ISSUE (TYPE= "EmpType", VALUE = C1.VALUE, VALUETYPE = C1.VALUETYPE) == Rule Action that issues a claims using string literal and matching claim referred with the Identifier.  
  
```  
  
### <a name="runtime-operation"></a>ランタイム操作  
効果的に規則を作成する要求変換の実行時の操作を理解しておく必要があります。 ランタイム操作は、3 つのクレーム セットを使用します。  
  
1.  **入力要求セット**:クレームの変換操作に指定されている要求の入力セット。  
  
2.  **ワーキング セットをクレーム**:中間の要求から読み取られても、クレームの変換中に書き込まれます。  
  
3.  **出力要求セット**:クレームの変換操作の出力。  
  
ランタイムの信頼性情報変換操作の概要を次に示します。  
  
1.  クレームの変換の入力方向の要求は、作業のクレーム セットを初期化するために使用されます。  
  
    1.  各ルールを処理するには、入力要求の作業のクレーム セットが使用されます。  
  
    2.  ルールの選択条件の一覧は、作業のクレーム セットからの要求のすべての可能なセットと照合されます。  
  
    3.  要求に一致するのには、各セットは、その規則でアクションを実行に使用されます。  
  
    4.  ルールを実行するアクションの結果では 1 つの要求では、出力に追加するセットと作業のクレーム セットに要求します。 そのため、ルールからの出力は、規則セット内の後続の規則の入力として使用されます。  
  
2.  規則セット内のルールは、以降では、最初の規則は順番に処理されます。  
  
3.  出力要求セットが重複する要求を削除する処理規則セット全体が処理されるときに、他のセキュリティの問題。結果として得られる要求は、クレームの変換プロセスの出力です。  
  
前の実行時の動作に基づいて、複雑なクレームの変換を記述することになります。  
  
**例:ランタイム操作**  
  
この例では、2 つの規則を使用するクレームの変換の実行時の操作を示します。  
  
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
次に、ルールの特別な構文を示します。  
  
1.  空の規則セット出力要求を = = なし  
  
2.  選択条件の一覧を空にすべての要求と一致する条件の選択リストを = =  
  
    **例:空の条件の選択 の一覧**  
  
    次の規則では、ワーキング セット内のすべての要求と一致します。  
  
    ```  
    => Issue (Type = "UserType", Value = "External", ValueType = "string")  
    ```  
  
3.  一致するリストの選択を空にすべての要求は、選択条件の一覧と一致する = =  
  
    **例:空の一致条件**  
  
    次の規則では、ワーキング セット内のすべての要求と一致します。 これは、単独で使用されている場合は、基本的な"許可"ルールです。  
  
    ```  
    C1:[] => Issule (claim = C1);  
    ```  
  
## <a name="security-considerations"></a>セキュリティの考慮事項  
**フォレストの入力要求**  
  
受信のフォレストにあるプリンシパルによって提示されるクレームを徹底的に検査を許可するか、適切な要求のみを発行したことを確認する必要があります。 不適切な要求には、フォレストのセキュリティが損なわれる可能性が、フォレストの入力信頼性情報変換ポリシーを作成するときの最上位の考慮事項があります。  
  
Active Directory には、フォレストの入力要求の構成の誤りを防ぐために、次の機能があります。  
  
-   フォレストの信頼は、セキュリティのため、フォレストの入力要求セット信頼性情報変換ポリシーを持たない場合、Active Directory は、フォレストを入力します。 すべてのプリンシパル クレームを削除します。  
  
-   要求で設定が、フォレストで定義されていない要求にフォレストの結果を入力するルールを実行している場合は、未定義の要求が出力要求から削除されます。  
  
**フォレストのままにする要求**  
  
フォレストのままにする要求は、フォレストのフォレストの入力要求よりも少ないセキュリティの問題を提示します。 フォレストのままにする要求が許可されているのがない場合でも対応する信頼性情報変換ポリシーでは、します。 フォレスト、フォレストのままにクレームを変換の一部として定義されていない要求を発行することもできます。 これは、簡単にクレームを含むフォレストをまたいだ信頼を設定します。 管理者は、フォレストの入力クレームの変換、および適切なポリシーを設定する必要がある場合を判断できます。 たとえばの管理者は、情報の漏えいを防ぐために要求を非表示にする必要がある場合などに、ポリシーを設定します。  
  
**クレーム変換規則で構文エラー**  
  
指定したクレームの変換ポリシーに構文が正しくないルール セットがある場合、またはその他の構文またはストレージの問題がある場合は、ポリシーは無効と見なされます。 これは、前に説明した既定の条件とは異なる処理されます。  
  
Active Directory では、ここでは意味を判断するようになってし、出力方向の要求は生成されませんその信頼 + のトラバーサル方向は、緊急時モードに。 問題を解決するには、管理者の介入が必要です。 これは、LDAP を使用して信頼性情報変換ポリシーを編集する場合に発生する可能性があります。 Active Directory 用 Windows PowerShell コマンドレットでは、構文の問題のポリシーの作成を防止するために検証があります。  
  
## <a name="other-language-considerations"></a>その他の言語に関する注意点  
  
1.  いくつかのキーワードまたは (端末と呼ばれます)、この言語で特別な文字があります。 これらが表示されます、[言語端末](Claims-Transformation-Rules-Language.md#BKMK_LT)テーブルでは、このトピックで後述します。 エラー メッセージは、あいまいさ排除のこれらの端末のタグを使用します。  
  
2.  端末は、文字列リテラルとしても使用できます。 ただし、このような使用状況は、言語定義と競合するが予期しない結果。 この種の使用は推奨されません。  
  
3.  規則の操作ですべての型変換を実行できません要求値、および、このようなルールのアクションを含む規則セットは無効と見なされます。 これが原因で、実行時エラーと、出力方向の要求は生成されません。  
  
4.  識別子をルールの条件の一覧の選択部分で使用されませんでしたが、ルールのアクションが参照されている場合は、使い方が無効です。 これにより、構文エラーが原因。  
  
    **例:識別子の参照が正しくありません。**  
    次の規則は、規則の操作で使用が正しくない識別子を示しています。  
  
    ```  
    C1:[] => Issue (claim = C2);  
    ```  
  
## <a name="sample-transformation-rules"></a>サンプルの変換ルール  
  
-   **特定の種類のすべての要求を許可します。**  
  
    正確な型  
  
    ```  
    C1:[type=="XYZ"] => Issue (claim = C1);  
    ```  
  
    正規表現を使用します。  
  
    ```  
    C1: [type =~ "XYZ*"] => Issue (claim = C1);  
    ```  
  
-   **特定の要求の種類を許可しません。**  
    正確な型  
  
    ```  
    C1:[type != "XYZ"] => Issue (claim=C1);  
    ```  
  
    正規表現を使用します。  
  
    ```  
    C1:[Type !~ "XYZ?"] => Issue (claim=C1);  
    ```  
  
## <a name="examples-of-rules-parser-errors"></a>パーサー エラーのルールの例  
クレーム変換規則は、構文エラーをチェックするカスタム パーサーによって解析されます。 このパーサーは、Active Directory の規則を保存する前に、関連する Windows PowerShell コマンドレットによって実行されます。 構文エラーなど、ルールを解析中にエラーがコンソールに出力されます。 ドメイン コント ローラーが、要求を変換するための規則を使用する前にも、パーサーを実行し、イベント ログにエラーを記録する (イベントのログ番号の追加) します。  
  
このセクションでは、パーサーによって生成されるエラーに不適切な構文と対応する構文で記述されているルールの例をいくつか示しています。  
  
1.  以下に例を示します。  
  
    ```  
    c1;[]=>Issue(claim=c1);  
    ```  
  
    この例では、コロンの代わりに、不適切に使用されるセミコロンがあります。   
    **エラー メッセージ:**  
    *POLICY0002:ポリシー データを解析できませんでした。*  
    *行番号:1、列番号:エラー トークンが、2:;。コマンドライン: ' c1;= > Issue(claim=c1);'。*  
    *パーサー エラー:' POLICY0030:予期しない構文エラーです ';' で、次のいずれかのが必要です: ':'。 '。*  
  
2.  以下に例を示します。  
  
    ```  
    c1:[]=>Issue(claim=c2);  
    ```  
  
    この例では、コピーの発行ステートメントの識別子のタグは定義されません。   
    **エラー メッセージ**:   
    *POLICY0011:CopyIssuanceStatement で指定された条件タグに一致する要求規則の条件がありません: 'c2'。*  
  
3.  以下に例を示します。  
  
    ```  
    c1:[type=="x1", value=="1", valuetype=="bool"]=>Issue(claim=c1)  
    ```  
  
    "bool"言語では、ターミナルでないし、有効な値型ではありません。 有効な端末は、次のエラー メッセージに表示されます。   
    **エラー メッセージ:**  
    *POLICY0002:ポリシー データを解析できませんでした。*  
    行番号:1、列番号:エラー トークンが、39:"bool"。 コマンドライン: ' c1: [型の値である"x1"= =「1」、valuetype = ="bool"= =] = > Issue(claim=c1);'。   
    *パーサー エラー:' POLICY0030:構文エラー: 予期しない 'STRING' で、次のいずれかを指定してください:'INT64_TYPE' 'UINT64_TYPE' 'STRING_TYPE' 'BOOLEAN_TYPE' 'IDENTIFIER'*  
  
4.  以下に例を示します。  
  
    ```  
    c1:[type=="x1", value==1, valuetype=="boolean"]=>Issue(claim=c1);  
    ```  
  
    数字の**1**言語では、有効なトークンのないこの例では、このような使用状況は、一致条件では許可されません。 文字列を二重引用符で囲む必要があります。   
    **エラー メッセージ:**  
    *POLICY0002:ポリシー データを解析できませんでした。*  
    *行番号:1、列番号:23 のエラー トークン:1. コマンドライン: ' c1: [型の値である"x1"= = 1、valuetype = ="bool"= =] = > Issue(claim=c1);'。* * パーサー エラー:' POLICY0029:入力が間違っています。*  
  
5.  以下に例を示します。  
  
    ```  
    c1:[type == "x1", value == "1", valuetype == "boolean"] =>   
  
         Issue(type = c1.type, value="0", valuetype == "boolean");  
    ```  
  
    この例では、1 つの等号 (=) ではなく、2 つの等号 (= =) を使用します。   
    **エラー メッセージ:**  
    *POLICY0002:ポリシー データを解析できませんでした。*  
    *行番号:1、列番号:エラー トークンが、91: = =。コマンドライン: ' c1: [型の値である"x1"= =「1」を = =*  
    *valuetype=="boolean"]=>Issue(type=c1.type, value="0", valuetype=="boolean");'.*  
    *パーサー エラー:' POLICY0030:構文エラー、予期しない '= ='、次のいずれかを指定してください: '='*  
  
6.  以下に例を示します。  
  
    ```  
    c1:[type=="x1", value=="boolean", valuetype=="string"] =>   
  
          Issue(type=c1.type, value=c1.value, valuetype = "string");  
    ```  
  
    この例は、正しい構文的および意味的があります。 ただし、"boolean"を使用して、文字列値は、混乱が生じるにバインドされ、避ける必要があります。 既に触れましたが、言語の端末を使用して要求の値は、可能な限り避ける必要があります。  
  
## <a name="BKMK_LT"></a>言語終端要素  
次の表では、ターミナルの文字列と、要求変換規則言語で使用される、関連する言語端末の完全なセットを示します。 これらの定義は、utf-16 文字列の大文字を使用します。  
  
|String|ターミナル|  
|----------|------------|  
|"=>"|意味|  
|";"|セミコロン|  
|":"|コロン|  
|","|コンマ|  
|"."|ドット|  
|"["|O_SQ_BRACKET|  
|"]"|C_SQ_BRACKET|  
|"("|O_BRACKET|  
|")"|C_BRACKET|  
|"=="|EQ|  
|"!="|NEQ|  
|"=~"|REGEXP_MATCH|  
|"!~"|REGEXP_NOT_MATCH|  
|"="|割り当てる|  
|"&&"|および|  
|「問題」|問題|  
|"type"|TYPE|  
|"value"|Value|  
|"valuetype"|VALUE_TYPE|  
|「要求」|要求|  
|"[_A-Za-z][_A-Za-z0-9]*"|識別子|  
|"\\"[^\\"\n]*\\""|STRING|  
|"uint64"|UINT64_TYPE|  
|"int64"|INT64_TYPE|  
|"string"|STRING_TYPE|  
|"boolean"|BOOLEAN_TYPE|  
  
## <a name="language-syntax"></a>言語の構文  
次のクレーム変換規則言語は、ABNF 形式で指定されます。 この定義は、ここで定義された ABNF 生産だけでなく、前の表で指定されているターミナルを使用します。 ルールは、utf-16 でエンコードする必要があり、文字列比較が小文字扱う必要があります。  
  
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
  


