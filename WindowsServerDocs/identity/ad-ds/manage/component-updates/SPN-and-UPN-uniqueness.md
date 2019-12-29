---
ms.assetid: 40bc24b1-2e7d-4e77-bd0f-794743250888
title: SPN と UPN の一意性
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: ded707276471fccd28f0ec17afef0a24015ff32f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390030"
---
# <a name="spn-and-upn-uniqueness"></a>SPN と UPN の一意性

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

**Author**: Justin 書籍、シニアサポートエスカレーションエンジニア (Windows グループ)  
  
> [!NOTE]  
> この内容は Microsoft カスタマー サポート エンジニアによって作成され、TechNet が通常提供しているトピックよりも詳細な Windows Server 2012 R2 の機能やソリューションの技術的説明を求めている、経験豊かな管理者とシステム設計者を対象としています。 ただし、TechNet と同様の編集過程は実施されていないため、言語によっては通常より洗練されていない文章が見られる場合があります。  
  
## <a name="overview"></a>概要  
Windows Server 2012 R2 のブロックの作成を実行しているドメイン コント ローラーには、サービス プリンシパル名 (SPN) とユーザー プリンシパル名 (UPN) が重複しています。 これには、復元または削除されたオブジェクトの復元またはオブジェクトの名前の変更の結果と重複してになる場合が含まれます。  
  
### <a name="background"></a>背景  
重複するサービス プリンシパル名 (SPN) がよく発生し認証エラーが発生し、LSASS の CPU 使用率が過剰につながる可能性があります。 重複する SPN または UPN の追加をブロックするインボックス メソッドはありません。 *  
  
重複する UPN の値は、内部設置型の間で同期を中断 AD および Office 365 です。  
  
*Setspn.exe では、一般的に新しい Spn を作成するために使用し、重複の確認を追加する Windows Server 2008 と共にリリースされたバージョンに組み込まれていた機能します。  
  
**テーブル SEQ テーブル \\\* アラビア 1: UPN と SPN の一意性**  
  
|機能|Comment|  
|-----------|-----------|  
|UPN の一意性|重複する Upn 中断同期の内部設置型 Windows Azure AD ベースのサービスと Office 365 などの AD アカウントです。|  
|SPN の一意性|Kerberos では、相互認証用の Spn が必要です。  Spn が重複すると、認証エラーが発生します。|  
  
Upn と Spn の一意性の要件の詳細については、次を参照してください。 [一意性制約](https://msdn.microsoft.com/library/dn392337.aspx)します。  
  
## <a name="symptoms"></a>現象  
8467 または 8468 のエラー コードのシンボリック 16 進数、または同等の文字列に記録されます様々 な画面に表示されるダイアログ ボックスとディレクトリ サービス イベント ログでイベント ID 2974 にします。 次の状況でのみが、重複する UPN または SPN を作成しようとすると、ブロックされます。  
  
-   書き込みは、Windows Server 2012 R2 の DC によって処理されます。  
  
**テーブル SEQ テーブル \\\* アラビア 2: UPN と SPN の一意性のエラーコード**  
  
|10 進数|16 進数|シンボル|String|  
|-----------|-------|------------|----------|  
|8467|21C 7|ERROR_DS_SPN_VALUE_NOT_UNIQUE_IN_FOREST|追加/変更するために提供される SPN 値が一意なフォレスト全体ではないため、操作が失敗しました。|  
|8648|21C 8|ERROR_DS_UPN_VALUE_NOT_UNIQUE_IN_FOREST|追加/変更するための UPN 値が一意なフォレスト全体ではないため、操作が失敗しました。|  
  
## <a name="new-user-creation-fails-if-upn-is-not-unique"></a>UPN が一意でない場合、新しいユーザーの作成が失敗しました。  
  
### <a name="dsamsc"></a>DSA.msc  
選択したユーザーのログオン名は既にこのエンタープライズで使用されています。 別のログオン名を選択してからやり直してください。  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig01_DupUPN.gif)  
  
既存のアカウントを変更します。  
  
指定したユーザーのログオン名は、企業で既に存在します。 プレフィックスを変更するか、一覧から別のサフィックスを選択するか、新しいものを指定します。  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig02_DupUPNMod.gif)  
  
### <a name="active-directory-administrative-center-dsacexe"></a>Active Directory 管理センター (DSAC.exe)  
既に存在している UPN を持つ Active Directory 管理センターに新しいユーザーを作成しようとすると、次のエラーが生成されます。  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig03_DupUPNADAC.gif)  
  
**図 SEQ 図 \\新しいユーザーの作成が UPN の重複によって失敗したときに、AD 管理センターに表示されるアラビア語1のエラー \***  
  
### <a name="event-2974-source-activedirectory_domainservice"></a>イベント 2974 ソース: ActiveDirectory_DomainService  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig04_Event2974.gif)  
  
**図 SEQ 図 \\\* アラビア語2イベント ID 2974 とエラー8648**  
  
イベント 2974 では、ブロックされていた値とその値がまだ含まれている (最大 10) 1 つまたは複数のオブジェクトの一覧を示します。  次の図では、他の4つのオブジェクトに **<em>dhunt@blue.contoso.com</em>** UPN 属性値が既に存在していることがわかります。  これが Windows Server 2012 R2 の新機能であるため、ダウンレベルのドメイン コント ローラーの書き込み試行の処理時に混在環境で重複する UPN と Spn の偶発的な作成がまだ発生します。  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig05_Event2974ShowAllDups.gif)  
  
**図 SEQ 図 \\\* アラビア語3イベント2974で重複する UPN を含むすべてのオブジェクトを表示する**  
  
> [!TIP]  
> イベント ID 2974s を定期的に確認してください。  
>   
> -   重複する UPN または Spn を作成する試行を識別します。  
> -   既にが重複しているオブジェクトを識別します。  
  
8648 =「操作の追加および変更の UPN 値が一意なフォレスト全体ではないために失敗しました」。  
  
### <a name="setspn"></a>SetSPN:  
使用する場合、Setspn.exe は、Windows Server 2008 のリリース以降に組み込み重複データの SPN の検出には、 **"-S"** オプション。  SPN の重複の検出をバイパスするにを使用して、 **"-A"** ただしオプションします。  SetSPN を使用するには、オプションを使用して Windows Server 2012 R2 DC を対象とする場合、重複する SPN の作成がブロックされます。  表示されるエラー メッセージが表示されている、-s オプションを使用する場合と同じ:"Duplicate SPN 見つかると、操作を中止しています"。  
  
### <a name="adsiedit"></a>ADSIEDIT:  
  
```  
Operation failed. Error code: 0x21c8  
The operation failed because UPN value provided for addition/modification is not unique forest-wide.  
000021C8: AtrErr: DSID-03200BBA, #1: 0: 000021C8: DSID-03200BBA, problem 1005 (CONSTRAINT_ATT_TYPE), data 0, Att 90290 (userPrincipalName)  
```  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig06_ADSI21c8.gif)  
  
**図 SEQ 図 \\\* 重複する UPN の追加がブロックされたときに ADSIEdit に表示されるアラビア語4のエラーメッセージ**  
  
### <a name="windows-powershell"></a>Windows PowerShell  
Windows Server 2012 R2  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig07_SetADUser2012.gif)  
  
PS Server 2012 の Windows Server 2012 R2 の DC を対象とするから実行しています。  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig08_SetADUser2012R2.gif)  
  
Windows Server 2012 R2 の DC を対象とする Windows Server 2012 で実行されている DSAC.exe:  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig09_UserCreateError.gif)  
  
**図 SEQ 図 \\Windows server 2012 R2 DC を対象としているときに、Windows Server 2012 R2 以外で \* アラビア語 5 DSAC ユーザー作成エラーが発生する**  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig10_UserModError.gif)  
  
**図 SEQ 図 \\Windows server 2012 R2 DC を対象としているときに、Windows Server 2012 R2 以外でアラビア語 6 DSAC ユーザー変更エラーが発生した \***  
  
### <a name="restore-of-an-object-that-would-result-in-a-duplicate-upn-fails"></a>重複する UPN になるオブジェクトの復元が失敗します。  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig11_RestoreDupUPN.gif)  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig12_RestoreDupUPNError.gif)  
  
オブジェクトが重複する UPN のため復元に失敗した場合にイベントは記録されません/SPN。  
  
オブジェクトの UPN は、復元するために一意である必要があります。  
  
1.  ごみ箱内のオブジェクト上に存在する UPN を識別します。  
  
2.  同じ値を持つすべてのオブジェクトを識別します。  
  
3.  重複する UPN(s) を削除します。  
  
### <a name="identify-the-conflicting-upn-on-the-deleted-objectusing-repadminexe"></a>削除された objectUsing repadmin.exe に競合する UPN を識別します。  
  
```  
Repadmin /showattr DCName "DN of deleted objects container" /subtree /filter:"(msDS-LastKnownRDN=<NAME>)" /deleted /atts:userprincipalname  
```  
  
```  
repadmin /showattr DCName "CN=Deleted Objects,DC=blue,DC=contoso,DC=com" /subtree /filter:"(msDS-LastKnownRDN=Dianne Hunt2)" /deleted /atts:userprincipalname  
  
C:\>repadmin /showattr winbluedc1 "cn=deleted objects,dc=blue,dc=contoso,dc=com" /subtree /filter:"(msds-lastknownrdn=Dianne Hunt2)" /deleted /atts:userprincipalname  
DN: CN=Dianne Hunt2\0ADEL:dd3ab8a4-3005-4f2f-814f-d6fc54a1a1c0,CN=Deleted Object  
s,DC=blue,DC=contoso,DC=com  
    1> userPrincipalName: dhunt@blue.contoso.com  
```  
  
### <a name="to-identify-all-objects-with-the-same-upnusing-repadminexe"></a>同じ UPN を持つすべてのオブジェクトを識別するために: を使用して Repadmin.exe  
  
```  
repadmin /showattr WinBlueDC1 "DC=blue,DC=contoso,DC=com" /subtree /filter:"(userPrincipalName=dhunt@blue.contoso.com)" /deleted /atts:DN  
  
C:\>repadmin /showattr winbluedc1 "dc=blue,dc=contoso,dc=com" /subtree /filter:"(userPrincipalName=dhunt@blue.contoso.com)" /deleted /atts:DN  
DN: CN=Administrator,CN=Users,DC=blue,DC=contoso,DC=com  
DN: CN=xouser1,CN=Users,DC=blue,DC=contoso,DC=com  
DN: CN=xouser10,CN=Users,DC=blue,DC=contoso,DC=com  
DN: CN=xouser100,CN=Users,DC=blue,DC=contoso,DC=com  
DN: CN=Dianne Hunt,OU=Marketing,DC=blue,DC=contoso,DC=com  
DN: CN=Dianne Hunt2\0ADEL:dd3ab8a4-3005-4f2f-814f-d6fc54a1a1c0,CN=Deleted Objects,DC=blue,DC=contoso,DC=com  
```  
  
> [!TIP]  
> 以前ドキュメントに未記載 **削除/** に削除されたオブジェクトを結果セットに含める repadmin.exe でパラメーターを使用  
  
### <a name="using-global-search"></a>グローバル検索を使用してください。  
  
-   開いて Active Directory 管理センターに移動して **グローバル検索**  
  
-   選択、 **LDAP に変換** オプション ボタン  
  
-   型 **(userPrincipalName =*競合*** している upn)  
  
    -   置換 ***ConflictingUPN*** 競合している実際の UPN を持つ  
  
-   選択 **適用**  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig13_GlobalSearch.gif)  
  
### <a name="using-windows-powershell"></a>Windows PowerShell を使用する  
  
```  
Get-ADObject -LdapFilter "(userPrincipalName=dhunt@blue.contoso.com)" -IncludeDeletedObjects -SearchBase "DC=blue,DC=Contoso,DC=com" -SearchScope Subtree -Server winbluedc1.blue.contoso.com  
```  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig13_GlobalSearchPS.gif)  
  
オブジェクトを復元する場合は、他のオブジェクトから重複する Upn を削除する必要があるされます。  1 つのオブジェクトには、ADSIEdit を使用して、重複を削除する簡単なです。  重複部分のオブジェクトが複数の場合は、Windows PowerShell はより優れたツールを使用するにする可能性があります。  
  
Windows PowerShell を使用する UserPrincipalName 属性を null。  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig15_NullUPN.gif)  
  
> [!NOTE]  
> UserPrincipalName 属性は単一値属性は、この手順は、重複する UPN だけを削除です。  
  
### <a name="duplicate-spn"></a>重複する SPN  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig16_DupSPN.gif)  
  
**図 SEQ 図 \\重複する SPN の追加がブロックされると、ADSIEdit に表示されるアラビア語8のエラーメッセージ \***  
  
ディレクトリ サービス イベント ログに記録する **ActiveDirectory_DomainService** イベント ID **2974**します。  
  
```  
Operation failed. Error code: 0x21c7  
The operation failed   
The attribute value provided is not unique in the forest or partition. Attribute:  
servicePrincipalName Value=<SPN>  
<Object DN> Winerror: 8467  
```  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig17_DupSPN2974.gif)  
  
**図 SEQ 図 \\\* 重複する SPN の作成がブロックされたときに、アラビア語9のエラーが記録される**  
  
### <a name="workflow"></a>ワークフロー  
  
-   **場合 DC = = GC**  
  
    -   Offbox 呼び出しは必要ありません、クエリはローカルで満たすことができます。  
  
    -   ***UPN ケース***  
  
        -   クエリ ローカル フォレスト全体の UPN インデックスの指定した UPN (*userPrincipalName はグローバル インデックス*)  
  
            -   エントリが返される場合は = = 0 が書き込み処理を ->  
  
            -   エントリが返される場合は! = 0] の [書き込みが失敗します。  
  
                -   イベントのログ記録  
  
                -   また拡張エラーが返されます。  
  
                    -   **8648:**  
  
                        *ERROR_DS_UPN_VALUE_NOT_UNIQUE_IN_FOREST*  
  
    -   ***SPN のケース***  
  
        -   クエリ ローカル フォレスト全体の SPN インデックス指定された SPN に (*サービス プリンシパル名はグローバル インデックス*)  
  
            -   エントリが返される場合は = = 0 が書き込み処理を ->  
  
            -   エントリが返される場合は! = 0] の [書き込みが失敗します。  
  
                -   イベントのログ記録  
  
                -   また拡張エラーが返されます。  
  
                    -   **8647:**  
  
                        **ERROR_DS_SPN_VALUE_NOT_UNIQUE_IN_FOREST**  
  
-   **If DC! = GC**  
  
    -   Offbox 呼び出し **望ましい** が、重要でない、つまりこれはベスト エフォート一意性の確認  
  
        -   GC を検出できない場合にのみローカル DIT に対してチェックを実行します。  
  
        -   このようなを示すために記録されたイベント  
  
    -   ***UPN ケース***  
  
        -   最も近い GC に対して LDAP クエリを送信するにはありますか。 指定した UPN のクエリの GC のフォレスト全体に関わる UPN インデックス (*userPrincipalName はグローバル インデックス*)  
  
            -   エントリが返される場合は = = 0 が書き込み処理を ->  
  
            -   エントリが返される場合は! = 0] の [書き込みが失敗します。  
  
                -   イベントのログ記録  
  
                -   また拡張エラーが返されます。  
  
                    -   **8648:**  
  
                        *ERROR_DS_UPN_VALUE_NOT_UNIQUE_IN_FOREST*  
  
    -   ***SPN のケース***  
  
        -   最も近い GC に対して LDAP クエリを送信するにはありますか。 指定された SPN にクエリ GC のフォレスト全体に関わる SPN インデックス (*サービス プリンシパル名はグローバル インデックス*)  
  
            -   エントリが返される場合は = = 0 が書き込み処理を ->  
  
            -   エントリが返される場合は! = 0] の [書き込みが失敗します。  
  
                -   イベントのログ記録  
  
                -   また拡張エラーが返されます。  
  
                    -   **8647:**  
  
                        *ERROR_DS_SPN_VALUE_NOT_UNIQUE_IN_FOREST*  
  
削除されたオブジェクトが再アニメーション化されたときは、一意性 SPN または UPN 値の存在が確認されます。 重複が見つかった場合、要求は失敗します。  
  
-   DNS ホスト名、SAM アカウントの名前などのような特定の属性変更の変更が行われたときに Spn も更新されます。 プロセスでは、古い Spn を削除し、新しい Spn が構築され、データベースに追加します。 このパスをトリガーする対象となる必須の属性の変更は次のとおりです。  
  
    -   ATT_DNS_HOST_NAME  
  
    -   ATT_MS_DS_ADDITIONAL_DNS_HOST_NAME  
  
    -   ATT_SAM_ACCOUNT_NAME  
  
    -   ATT_MS_DS_ADDITIONAL_SAM_ACCOUNT_NAME  
  
    -   ATT_SERVER_REFERENCE_BL  
  
    -   ATT_USER_ACCOUNT_CONTROL  
  
重複する SPN の新しい値のいずれかの場合は、変更が失敗します。 上記の一覧の重要な属性は、ATT_DNS_HOST_NAME (コンピューター名) と ATT_SAM_ACCOUNT_NAME (SAM アカウント名) です。  
  
### <a name="try-this-exploring-spn-and-upn-uniqueness"></a>SPN と UPN の一意性の表示にしてください。  
これは、最初のいくつかの"**実際に使ってみる**"、モジュール内の活動です。  このモジュールの別のラボ ガイドではありません。  **実際に使ってみる** アクティビティは、本質的に自由に使用できるアクティビティがラボ環境のレッスンの内容を表示します。  次のプロンプトまたはスクリプトのオプションを独自のアクティビティを思い付くなりません。  
  
> [!NOTE]  
> -   これは、最初のいくつかの"**実際に使ってみる**"アクティビティ。  
> -   このモジュールの別のラボ ガイドではありません。  
> -   **実際に使ってみる** アクティビティは、本質的に自由に使用できるアクティビティがラボ環境のレッスンの内容を表示します。  
> -   次のプロンプトまたはスクリプトのオプションを独自のアクティビティを思い付くなりません。  
> -   すべてのセクションではありますが、 **実際に使ってみる** プロンプトで、適切な場所は、演習のレッスンの内容を調査が推奨されます。  
  
SPN と UPN の一意性をテストします。  これらの指示に従ってか、独自に完了します。  
  
1.  UPN を持つ新しいユーザーを作成します。  
  
2.  アカウントの Spn を作成します。  
  
3.  既に以前に定義された UPN を持つ新しいユーザーを作成するか、既存のアカウントの UPN を変更します。  別のアカウントの SPN に同じ操作を行います  
  
    1.  既に使用されている UPN を持つ既存のユーザー アカウントを設定します。  
  
        1.  PowerShell、ADSIEDIT、または Active Directory 管理センター (DSAC.exe) を使用します。  
  
    2.  既存のアカウントで既に使用されている SPN を設定します。  
  
        1.  Windows PowerShell、ADSIEDIT をまたは SetSPN  
  
4.  エラーを確認します。  
  
**オプション**  
  
1.  クラスルーム講師であることを確認を有効にしても問題ありません、 *[AD のごみ箱](https://technet.microsoft.com/library/jj574144.aspx#BKMK_EnableRecycleBin)* で Active Directory 管理センターです。  その場合は、次の手順に移動します。  
  
2.  ユーザー アカウントの UPN を設定します。  
  
3.  アカウントを削除します。  
  
4.  削除されたアカウントとして同じ UPN を持つ別のアカウントを設定します。  
  
5.  ごみ箱 GUI を使用して、アカウントを復元しようとしてください。  
  
6.  前の手順で表示するエラー メッセージに表示されるだけは想像してみてください。  (および実行するステップの履歴はありません)目標は、アカウントの復元を完了します。  ブックの例の手順を参照してください。  
  


