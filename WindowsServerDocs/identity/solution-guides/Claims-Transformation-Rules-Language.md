---
ms.assetid: e831f781-3c45-4d44-b411-160d121d1324
title: Claims Transformation Rules Language
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4a6b378bc4aef180ebedd260008febaa2f2a76ae
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="claims-transformation-rules-language"></a>Claims Transformation Rules Language

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

フォレスト間での要求にフォレストをまたいだ信頼で信頼性情報変換ポリシーを設定してフォレスト境界全体でダイナミック アクセス制御の要求をブリッジする変換機能を使用します。 すべてのポリシーの主要なコンポーネントは、信頼性情報変換規則言語で記述されているルールです。 このトピックでは、この言語の詳細を提供し、信頼性情報変換規則の作成に関するガイダンスを提供します。  
  
フォレスト間で情報変換ポリシー用の Windows PowerShell コマンドレットがオプションは、単純なポリシーを設定するために必要な共通のシナリオを信頼します。 これらのコマンドレットは、ユーザーが入力信頼性情報の変換規則言語でポリシーとルールに変換し、所定の形式で Active Directory に格納します。 要求変換用のコマンドレットの詳細については、次を参照してください。、[ダイナミック アクセス制御の AD DS コマンドレット](https://go.microsoft.com/fwlink/?LinkId=243150)します。  
  
要求の構成と、Active Directory フォレストのフォレストをまたいだ信頼上に配置要件に応じて、信頼性情報変換ポリシーは、Active Directory 用 Windows PowerShell コマンドレットでサポートされているポリシーよりも複雑にする必要があります。 このようなポリシーを効果的に作成するには、信頼性情報変換規則言語の構文とセマンティクスを理解する必要があります。 これは、要求変換規則言語 ("、") Active Directory で使用される言語のサブセット[Active Directory フェデレーション サービス](https://go.microsoft.com/fwlink/?LinkId=243982)類似した目的とそれが非常に同様の構文とセマンティクスします。 ただし、少ない操作が許可されている場合、あるされ、構文が追加の制限は、Active Directory のバージョンの言語で配置されます。  
  
このトピックでは、構文とセマンティクスでは、Active Directory との考慮事項は、ポリシーを作成するときに行われる要求変換規則言語の画面が一時的に説明します。 いくつかの一連のように、例の規則と正しくない構文と、規則を作成するときにエラー メッセージを解読するために、生成したメッセージの例を提供します。  
  
## <a name="tools-for-authoring-claims-transformation-policies"></a>信頼性情報変換ポリシーを作成するためのツール  
**Active Directory 用 Windows PowerShell コマンドレット**: これは、作成し、信頼性情報変換ポリシーの設定を優先と推奨される方法です。 これらのコマンドレットは、スイッチは、単純なポリシーより複雑なポリシーに設定されているルールを確認します。  
  
**LDAP**: Active Directory ライトウェイト ディレクトリ アクセス プロトコル (LDAP) 経由で信頼性情報変換ポリシーを編集することができます。 ただし、これは推奨されませんので、ポリシーがあるいくつかの複雑なコンポーネントとツールを使用する Active Directory に書き込む前に、ポリシーを検証しない可能性があります。 その後かなりの問題を診断する時間が必要です。  
  
## <a name="active-directory-claims-transformation-rules-language"></a>Active Directory の要求規則言語の変換  
  
### <a name="syntax-overview"></a>構文の概要  
構文の簡単な概要と言語のセマンティクスを次に示します。  
  
-   要求変換規則セットは、0 個以上の規則で構成されます。 各ルールには 2 つのアクティブな部分:**選択条件の一覧**と**ルール Action**します。 場合、**選択条件の一覧**の評価が true の場合、対応する、規則の操作を実行します。  
  
-   **選択条件の一覧で**0 個以上を持つ**選択条件**します。 すべての**選択条件**プロパティを TRUE に評価する必要があります、**選択条件の一覧**を TRUE に評価します。  
  
-   各**選択条件**の 0 個以上のセットを持つ**一致条件**します。 すべての**一致条件**評価が TRUE に評価する選択条件を TRUE にする必要があります。 すべての条件が 1 つの要求に対して評価されます。 一致する要求、**選択条件**タグ付けされたことができます、**識別子**で参照されると、**ルール Action**します。  
  
-   各**マッチング条件**と一致する条件を指定します、**種類**または**値**または**ValueType**異なるを使用して、要求の**条件演算子**と**文字列リテラル**します。  
  
    -   指定すると、**マッチング条件**の**値**も指定する必要があります、**マッチング条件**、特定の**ValueType**およびその逆方向。 これらの条件は、互いの横にある、構文でなければなりません。  
  
    -   **ValueType**条件に一致する必要がありますを使用して特定**ValueType**リテラルのみです。  
  
-   A**ルール Action**タグが付けられている 1 つの要求をコピーすることができます、**識別子**または識別子にタグ付けされた要求に基づくやリテラル文字列を指定された 1 つの要求を発行します。  
  
**規則の例**  
  
この例は、同じ要求 Valuetype を使用してこの種類の値の信頼性情報の同じ意味を指定することは、2 つのフォレスト間で信頼性情報の種類を変換するのに使用できる規則を示します。 ルールは、1 つに一致する状態とリテラル文字列と一致する信頼性情報の参照を使用する Issue ステートメントがします。  
  
```  
C1: [TYPE=="EmployeeType"]    
                 => ISSUE (TYPE= "EmpType", VALUE = C1.VALUE, VALUETYPE = C1.VALUETYPE);  
[TYPE=="EmployeeType"] == Select Condition List with one Matching Condition for claims Type.  
ISSUE (TYPE= "EmpType", VALUE = C1.VALUE, VALUETYPE = C1.VALUETYPE) == Rule Action that issues a claims using string literal and matching claim referred with the Identifier.  
  
```  
  
### <a name="runtime-operation"></a>ランタイム操作  
ことが重要効果的に規則を作成する信頼性情報変換のランタイム操作を理解します。 ランタイム操作は、3 つの信頼性情報のセットを使用します。  
  
1.  **入力要求セット**: 入力信頼性情報変換操作に指定されている要求のセットです。  
  
2.  **ワーキング セットの要求**: 中間からの読み取りおよびの信頼性情報変換中に書き込まれるを要求します。  
  
3.  **出力要求セット**: 信頼性情報変換操作の出力します。  
  
実行時の信頼性情報変換操作の概要を次に示します。  
  
1.  要求変換の入力信頼性情報は、作業のクレーム セットの初期化に使用されます。  
  
    1.  各規則を処理するには、入力信頼性情報、作業の信頼性情報のセットが使用されます。  
  
    2.  規則の選択条件の一覧は、作業の信頼性情報のセットからのクレームのすべての可能なセットと照合されます。  
  
    3.  信頼性情報に一致するのには、各セットを使用すると、その規則でアクションを実行します。  
  
    4.  ルールを実行するアクションの結果の 1 つの要求は、出力が追加されているセットと作業の信頼性情報のセットに要求します。 したがって、規則からの出力は、規則セット内の後続の規則の入力として使用されます。  
  
2.  規則セット内のルールは、以降の最初のルールでは、順番に処理されます。  
  
3.  重複する信頼性情報を削除する出力要求セットが処理される規則セット全体が処理されるときに、その他のセキュリティ issues.The 結果として得られるクレームは、信頼性情報変換プロセスの出力です。  
  
以前の実行時の動作に基づいて、複雑なクレームの変換を記述することが勧めします。  
  
**例: のランタイム操作**  
  
この例では、2 つの規則を使用する信頼性情報変換のランタイム操作を示します。  
  
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
  
### <a name="special-rules-semantics"></a>特別な規則セマンティクス  
ルールの特別な構文を次に示します。  
  
1.  空の規則セットの出力の信頼性情報 = = なし  
  
2.  選択条件の一覧を空にすべての要求と一致する選択条件の一覧を = =  
  
    **例: 空の選択条件の一覧**  
  
    次の規則では、ワーキング セット内のすべての要求と一致します。  
  
    ```  
    => Issue (Type = "UserType", Value = "External", ValueType = "string")  
    ```  
  
3.  選択に一致する] の一覧を空にすべての要求は、選択条件の一覧と一致する = =  
  
    **例: 空の条件に一致します。**  
  
    次の規則では、ワーキング セット内のすべての要求と一致します。 これは、単独で使用されている場合は、基本的な"許可"ルールです。  
  
    ```  
    C1:[] => Issule (claim = C1);  
    ```  
  
## <a name="security-considerations"></a>セキュリティの考慮事項  
**フォレストの入力信頼性情報**  
  
フォレストへの入力方向であるプリンシパルによって提示される信頼性情報は、十分に検査を許可するか、適切な要求のみを発行したことを確認する必要があります。 不適切な信頼性情報には、フォレストのセキュリティが損なわれる可能性があり、必要があります上重要な考慮事項、フォレストが入力信頼性情報変換ポリシーを作成するときにあります。  
  
Active Directory フォレストが入力信頼性情報の構成の誤りを防ぐために、次の機能があります。  
  
-   フォレストの信頼に信頼性情報変換ポリシーの設定、セキュリティのため、フォレストが入力信頼性情報があるない場合、Active Directory はすべて、プリンシパルの信頼性情報、フォレストが入力するを削除します。  
  
-   フォレストの結果が入力したフォレストで定義されていない要求に規則の信頼性情報にセットを実行している場合は、未定義の信頼性情報が出力要求から削除されます。  
  
**信頼性情報、フォレストのままにします。**  
  
信頼性情報、フォレストのままにするには、フォレストのフォレストが入力信頼性情報よりも小さいセキュリティの問題が表示されます。 フォレストをそのまま使用する要求が許可されている-でもがない場合に対応する信頼性情報変換ポリシーでは、します。 フォレストをそのまま使用する要求を変換することの一部として、フォレストで定義されていない要求を発行することもできます。 これは、信頼性情報を含むフォレストをまたいだ信頼を簡単に設定します。 管理者は、フォレストが入力信頼性情報変換、および適切なポリシーを設定する必要がある場合に指定できます。 たとえばの管理者は、情報漏洩の防止への要求を非表示にする必要がある場合などに、ポリシーを設定します。  
  
**要求変換規則の構文エラー**  
  
特定の信頼性情報変換ポリシーが正しくない構文が規則セットがある場合、またはその他の構文または記憶域の問題がある場合は、ポリシーが無効と見なされます。 これは、既定の条件の前に説明したものとは異なる扱われます。  
  
Active Directory をここで、目的を判断できないし、出力の信頼性情報が生成されない信頼 + トラバーサルの方向にフェイル セーフ モードに入ります。 問題を修正するには、管理者の介入が必要です。 これは、LDAP を使用して信頼性情報変換ポリシーを編集する場合に発生する可能性があります。 Active Directory 用 Windows PowerShell コマンドレットでは、構文上の問題のポリシーの書き込みを防止するために検証があります。  
  
## <a name="other-language-considerations"></a>その他の言語に関する考慮事項  
  
1.  いくつかの主要な単語または (端末と呼ばれる) この言語で特殊文字があります。 掲載して、[言語端末](Claims-Transformation-Rules-Language.md#BKMK_LT)表はこのトピックで後述します。 エラー メッセージは、これらの端末不明瞭解消のタグを使用します。  
  
2.  端末は、リテラル文字列としても使用できます。 ただし、その使用量が言語の定義と競合する可能性がありますまたはが予想外の結果。 このような使用法は推奨されません。  
  
3.  規則の動作で任意の型の変換は実行できません要求の値、および規則セットを含むこのような規則の動作は無効と見なされます。 これが原因で、ランタイム エラーが発生し、信頼性情報の出力は生成されません。  
  
4.  ルール action を指す場合、規則の選択条件の一覧の部分に使用されなかった識別子は使用が無効です。 これにより、構文エラーが原因です。  
  
    **例: 誤った識別子のリファレンス**  
    次の規則は、規則の操作で使用されている不適切な識別子を示しています。  
  
    ```  
    C1:[] => Issue (claim = C2);  
    ```  
  
## <a name="sample-transformation-rules"></a>変換規則のサンプル  
  
-   **特定の種類のすべての要求を許可します。**  
  
    正確な型  
  
    ```  
    C1:[type=="XYZ"] => Issue (claim = C1);  
    ```  
  
    正規表現を使用します。  
  
    ```  
    C1: [type =~ "XYZ*"] => Issue (claim = C1);  
    ```  
  
-   **特定の要求の種類を禁止します。**  
    正確な型  
  
    ```  
    C1:[type != "XYZ"] => Issue (claim=C1);  
    ```  
  
    正規表現を使用します。  
  
    ```  
    C1:[Type !~ "XYZ?"] => Issue (claim=C1);  
    ```  
  
## <a name="examples-of-rules-parser-errors"></a>ルールのパーサー エラーの例  
要求変換規則は、構文エラーをチェックするカスタムのパーサーによって解析されます。 このパーサーは、Active Directory 内の規則を保存する前に、関連する Windows PowerShell コマンドレットによって実行されます。 コンソールで、構文エラーを含む、ルールを解析中にエラーが印刷されます。 また、ドメイン コントローラーは信頼性情報、変換するための規則を使用する前に、パーサーを実行し、イベント ログにエラーを記録する (イベント ログの番号の追加) します。  
  
このセクションでは、パーサーによって生成されたエラーを正しくない構文と対応する構文で記述されている規則の例をいくつかを示しています。  
  
1.  例:  
  
    ```  
    c1;[]=>Issue(claim=c1);  
    ```  
  
    この例にあるコロンの代わりに正しく使用のセミコロンします。   
    **エラー メッセージ:**  
    *POLICY0002: ポリシー データを解析できませんでした。*  
    *行番号: 1 の場合、列番号: 2、エラー トークン:; します。 行: ' c1 です。= > Issue(claim=c1);' です。*  
    *パーサー エラー: ' POLICY0030: 構文エラー、予期しない「;」、次の予想 1: ':'.'*  
  
2.  例:  
  
    ```  
    c1:[]=>Issue(claim=c2);  
    ```  
  
    この例では、コピーの発行ステートメントの識別子のタグは、定義されていません。   
    **エラー メッセージ**:   
    *POLICY0011: 要求規則の条件に一致するありません、CopyIssuanceStatement で指定された条件のタグ: 'c2' です。*  
  
3.  例:  
  
    ```  
    c1:[type=="x1", value=="1", valuetype=="bool"]=>Issue(claim=c1)  
    ```  
  
    "bool"しない言語では、ターミナル、有効な ValueType はありません。 有効な端末は、次のエラー メッセージに表示されます。   
    **エラー メッセージ:**  
    *POLICY0002: ポリシー データを解析できませんでした。*  
    行番号: 1 の場合、列番号: 39、エラー トークン:"bool"です。 行: ' c1: [種類"x1"、値を = =「1」、valuetype = ="bool"= =] = > Issue(claim=c1);' です。   
    *パーサー エラー: ' POLICY0030: 構文エラー、予期しない '文字列'、次のいずれかを指定して: 'INT64_TYPE' 'UINT64_TYPE' 'STRING_TYPE' 'BOOLEAN_TYPE' '識別子'*  
  
4.  例:  
  
    ```  
    c1:[type=="x1", value==1, valuetype=="boolean"]=>Issue(claim=c1);  
    ```  
  
    数字**1**この例では、いない言語では、有効なトークンと一致する状態でその使用量は許可されません。 文字列を二重引用符で囲む必要があります。   
    **エラー メッセージ:**  
    *POLICY0002: ポリシー データを解析できませんでした。*  
    *行番号: 1 の場合、列番号: 23、エラー トークン: 1。行: ' c1: [種類"x1"、値を = = 1、valuetype = ="bool"= =] = > Issue(claim=c1);'。**パーサー エラー: ' POLICY0029: 予期しない入力します。*  
  
5.  例:  
  
    ```  
    c1:[type == "x1", value == "1", valuetype == "boolean"] =>   
  
         Issue(type = c1.type, value="0", valuetype == "boolean");  
    ```  
  
    この例では、1 つの等号 (=) ではなく、二重に等号 (= =) を使用します。   
    **エラー メッセージ:**  
    *POLICY0002: ポリシー データを解析できませんでした。*  
    *行番号: 1 の場合、列番号: 91、エラー トークン: = = します。 行: ' c1: [種類"x1"、値を = =「1」= =*  
    *valuetype「ブール値」= =] = > 問題 (type=c1.type、値「0」、valuetype =「ブール値」= =);"です。*  
    *パーサー エラー: ' POLICY0030: 構文エラー、予期しない '= ='、次のいずれかを指定して: '='*  
  
6.  例:  
  
    ```  
    c1:[type=="x1", value=="boolean", valuetype=="string"] =>   
  
          Issue(type=c1.type, value=c1.value, valuetype = "string");  
    ```  
  
    この例は、正しい構文とセマンティクスがあります。 ただし、「ブール値」を使用して文字列値が、混乱の原因にバインドされているし、避ける必要があります。 既に触れましたが、言語端末を使用して信頼性情報の値は、可能な限り避ける必要があります。  
  
## <a name="BKMK_LT"></a>端末の言語  
次の表は、ターミナル文字列と要求変換規則言語で使用されている関連する言語端末の完全なセットを示します。 これらの定義は、大文字 UTF-16 文字列を使用します。  
  
|文字列|ターミナル|  
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
|"&&"|そして|  
|"issue"|問題|  
|"type"|種類|  
|"value"|値|  
|"valuetype"|VALUE_TYPE|  
|「クレーム」|要求|  
|"[_A-Za-z][_A-Za-z0-9]*"|識別子|  
|"\\"[^\\"\n]*\\""|文字列|  
|"uint64"|UINT64_TYPE|  
|"int64"|INT64_TYPE|  
|「文字列」|STRING_TYPE|  
|「ブール値」|BOOLEAN_TYPE|  
  
## <a name="language-syntax"></a>言語の構文  
次の要求変換規則言語は ABNF 形式で指定します。 この定義は、ここで定義された ABNF 生産だけでなく、前の表で指定されている端末を使用します。 Utf-16 で規則をエンコードする必要があり、文字列比較が大文字と小文字として扱う必要があります。  
  
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
  


