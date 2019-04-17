---
ms.assetid: 40bc24b1-2e7d-4e77-bd0f-794743250888
title: "SPN と UPN の一意性"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 81d686c81082ad29384585d541c1304d654e1924
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="spn-and-upn-uniqueness"></a>SPN と UPN の一意性

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

**作成者**: Windows グループに Justin チューナー シニア サポート エスカレーション エンジニア  
  
> [!NOTE]  
> このコンテンツが、Microsoft カスタマー サポート エンジニアによって書き込まれるあり、経験豊富な管理者と TechNet の通常のトピックよりも機能と Windows Server 2012 R2 で解決策の詳細な技術的説明を求めているシステム アーキテクトです。 ただし、実施されていません、同様の編集過程のため、TechNet の「新機能が見つかった通常より洗練されて、言語によってように見える場合があります。  
  
## <a name="overview"></a>概要  
Windows Server 2012 R2 のブロックの作成を実行しているドメイン コントローラーには、サービス プリンシパル名 (SPN) とユーザー プリンシパル名 (UPN) が重複しています。 これには、復元または削除されたオブジェクトの復元またはオブジェクトの名前の変更の結果と重複になる場合が含まれます。  
  
### <a name="background"></a>バック グラウンド  
重複するサービス プリンシパル名 (SPN) でよく発生し認証エラーが発生し、LSASS の CPU 使用率が過剰につながる可能性があります。 重複する SPN または UPN の追加をブロックするインボックス メソッドはありません。 *  
  
重複する UPN 値が内部設置型の間で同期を中断 AD および Office 365 します。  
  
*Setspn.exe では、一般的に新しい SPN を作成するために使用し、重複の確認を追加する Windows Server 2008 と共にリリースされたバージョンに組み込まれていた機能を提供します。  
  
**SEQ テーブル \\\ * ARABIC 1: UPN と SPN の一意性**  
  
|機能|コメント|  
|-----------|-----------|  
|UPN の一意性|重複する Upn 中断同期の内部設置型 Windows Azure AD ベースのサービス Office 365 などの AD アカウントです。|  
|SPN の一意性|Kerberos では、相互認証用の SPN が必要です。  重複する SPN は、認証エラーが発生します。|  
  
Upn と SPN の一意性の要件の詳細については、次を参照してください。[一意性制約](https://msdn.microsoft.com/library/dn392337.aspx)します。  
  
## <a name="symptoms"></a>問題の症状  
8467 または 8468 のエラー コードのシンボリック 16 進数または同等の文字列に記録されます様々 な画面に表示されるダイアログ ボックスとディレクトリ サービス イベント ログでイベント ID 2974 にします。 重複する UPN または SPN を作成する試みは次の状況でのみブロックされます。  
  
-   Windows Server 2012 R2 の DC で、書き込みが処理されます。  
  
**SEQ テーブル \\\ * ARABIC 2: UPN と SPN の一意性エラー コード**  
  
|10 進数|16 進数|シンボリック|文字列|  
|-----------|-------|------------|----------|  
|8467|21C 7|ERROR_DS_SPN_VALUE_NOT_UNIQUE_IN_FOREST|追加/変更するために提供される SPN 値が一意なフォレスト全体ではないために、操作に失敗しました。|  
|8648|21C 8|ERROR_DS_UPN_VALUE_NOT_UNIQUE_IN_FOREST|追加/変更の UPN 値が一意なフォレスト全体ではないために、操作に失敗しました。|  
  
## <a name="new-user-creation-fails-if-upn-is-not-unique"></a>UPN が一意でない場合、新しいユーザーの作成が失敗します。  
  
### <a name="dsamsc"></a>DSA.msc  
選択したユーザーのログオン名は、既にこのエンタープライズで使用されています。 別のログオン名を選択して、もう一度やり直してください。  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig01_DupUPN.gif)  
  
既存のアカウントを変更します。  
  
指定したユーザーのログオン名は、企業で既に存在します。 いずれかのプレフィックスを変更するか、一覧から別のサフィックスを選択すると、新しいものを指定します。  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig02_DupUPNMod.gif)  
  
### <a name="active-directory-administrative-center-dsacexe"></a>Active Directory 管理センターの (DSAC.exe)  
既に存在する UPN を持つ Active Directory 管理センターで新しいユーザーを作成しようとすると、次のエラーが生成されます。  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig03_DupUPNADAC.gif)  
  
**図 SEQ Figure \\\ * アラビア語の 1 エラーが重複する UPN のために新しいユーザーの作成が失敗したときに、AD 管理センターで表示されます。**  
  
### <a name="event-2974-source-activedirectorydomainservice"></a>イベント 2974 ソース: ActiveDirectory_DomainService  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig04_Event2974.gif)  
  
**図 SEQ Figure \\\ * エラー 8648 アラビア語の 2 イベント ID 2974**  
  
イベント 2974 では、ブロックされていた値とその値が既に含まれている (最大 10) 1 つまたは複数のオブジェクトの一覧を示します。  次の図では、その UPN 属性の値を確認できます***dhunt@blue.contoso.com***既に他の 4 つのオブジェクト上に存在します。  これは、Windows Server 2012 R2 の新機能であるため、ダウンレベルのドメイン コントローラー書き込み試行の処理時に混在環境で重複する UPN と SPN の偶発的な作成が引き続き発生します。  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig05_Event2974ShowAllDups.gif)  
  
**図 SEQ Figure \\\ * アラビア 3 イベント 2974 が重複する UPN を含むすべてのオブジェクトを表示します。**  
  
> [!TIP]  
> イベント ID 2974 を定期的に確認します。  
>   
> -   重複する UPN または SPN を作成する試行を識別します  
> -   既にが重複しているオブジェクトを識別します。  
  
8648 =「操作追加/変更の UPN 値が一意なフォレスト全体ではないために失敗しました。」  
  
### <a name="setspn"></a>SetSPN:  
Setspn.exe で数が、Windows Server 2008 のリリース以降に組み込み重複する SPN の検出を使用する場合、**"-S"**オプションです。  使用して重複する SPN の検出をバイパスできる、**"-A"**ただしオプションします。  SetSPN を使用するには、オプションで Windows Server 2012 R2 DC を対象とする場合、重複する SPN の作成がブロックされます。  エラー メッセージが表示される、-s オプションを使用する場合に表示されているのと同じ:"Duplicate SPN 見つかると、操作を中止!"  
  
### <a name="adsiedit"></a>ADSIEDIT:  
  
```  
Operation failed. Error code: 0x21c8  
The operation failed because UPN value provided for addition/modification is not unique forest-wide.  
000021C8: AtrErr: DSID-03200BBA, #1: 0: 000021C8: DSID-03200BBA, problem 1005 (CONSTRAINT_ATT_TYPE), data 0, Att 90290 (userPrincipalName)  
```  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig06_ADSI21c8.gif)  
  
**図 SEQ Figure \\\ * アラビア語の 4 エラー メッセージが重複する UPN の追加がブロックされたときに ADSIEdit の表示**  
  
### <a name="windows-powershell"></a>Windows PowerShell  
Windows Server 2012 R2 の場合:  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig07_SetADUser2012.gif)  
  
PS Server 2012、Windows Server 2012 R2 DC を対象とするから実行しています。  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig08_SetADUser2012R2.gif)  
  
Windows Server 2012 R2 の DC を対象とする Windows Server 2012 で実行されている DSAC.exe:  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig09_UserCreateError.gif)  
  
**図 SEQ Figure \\\ * ARABIC 5 DSAC ユーザー作成エラーの非-Windows Server 2012 R2 Windows Server 2012 R2 DC を対象とするときに**  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig10_UserModError.gif)  
  
**図 SEQ Figure \\\ * アラビア語の 6 DSAC ユーザー変更エラーの非-Windows Server 2012 R2 Windows Server 2012 R2 DC を対象とするときに**  
  
### <a name="restore-of-an-object-that-would-result-in-a-duplicate-upn-fails"></a>重複する UPN になるオブジェクトの復元に失敗します。  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig11_RestoreDupUPN.gif)  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig12_RestoreDupUPNError.gif)  
  
オブジェクトが重複する UPN のため復元に失敗したときにイベントは記録されません/SPN します。  
  
オブジェクトの UPN は、復元するために一意である必要があります。  
  
1.  ごみ箱内のオブジェクト上に存在する UPN を識別します。  
  
2.  同じ値を持つすべてのオブジェクトを識別します。  
  
3.  重複する Upn を削除します。  
  
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
  
### <a name="to-identify-all-objects-with-the-same-upnusing-repadminexe"></a>同じ UPN を持つすべてのオブジェクトを識別する: Repadmin.exe を使用します。  
  
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
> 以前ドキュメントに未記載**削除/** repadmin.exe でパラメーターを使用して、削除されたオブジェクトを結果セットに含める  
  
### <a name="using-global-search"></a>グローバル検索を使用してください。  
  
-   開いて Active Directory 管理センターに移動**グローバル検索**  
  
-   選択、**LDAP に変換**ラジオ ボタン  
  
-   種類**(userPrincipalName =*ConflictingUPN*) * *  
  
    -   置換***ConflictingUPN***と競合している実際の UPN  
  
-   選択**適用**  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig13_GlobalSearch.gif)  
  
### <a name="using-windows-powershell"></a>Windows PowerShell を使用します。  
  
```  
Get-ADObject -LdapFilter "(userPrincipalName=dhunt@blue.contoso.com)" -IncludeDeletedObjects -SearchBase "DC=blue,DC=Contoso,DC=com" -SearchScope Subtree -Server winbluedc1.blue.contoso.com  
```  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig13_GlobalSearchPS.gif)  
  
オブジェクトは、復元する必要がある場合、その他のオブジェクトから重複する Upn を削除する必要があるされます。  1 つのオブジェクトは ADSIEdit を使用して、重複を削除する簡単なです。  重複のオブジェクトが複数ある場合は、Windows PowerShell はより優れたツールを使用するをする可能性があります。  
  
Windows PowerShell を使用する UserPrincipalName 属性は null。  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig15_NullUPN.gif)  
  
> [!NOTE]  
> UserPrincipalName 属性は単一値属性はため、この手順は、重複する UPN だけを削除します。  
  
### <a name="duplicate-spn"></a>重複する SPN  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig16_DupSPN.gif)  
  
**図 SEQ Figure \\\ * アラビア語の 8 エラー メッセージが重複する SPN の追加がブロックされたときに、ADSIEdit の表示**  
  
ディレクトリ サービス イベント ログに記録、**ActiveDirectory_DomainService**イベント ID **2974**します。  
  
```  
Operation failed. Error code: 0x21c7  
The operation failed   
The attribute value provided is not unique in the forest or partition. Attribute:  
servicePrincipalName Value=<SPN>  
<Object DN> Winerror: 8467  
```  
  
![SPN と UPN の一意性](media/SPN-and-UPN-uniqueness/GTR_ADDS_Fig17_DupSPN2974.gif)  
  
**図 SEQ Figure \\\ * アラビア語の 9 エラーが重複する SPN の作成がブロックされたときにログに記録**  
  
### <a name="workflow"></a>ワークフロー  
  
-   **場合 DC = GC**  
  
    -   Offbox 呼び出しは必要ありません、クエリをローカルで満たすことができます。  
  
    -   ***Upn***  
  
        -   クエリ ローカル フォレスト全体に関わる UPN インデックス指定した UPN (*userPrincipalName はグローバル インデックス*)  
  
            -   エントリが返される場合は = = 0 が書き込み処理を ->  
  
            -   エントリが返される場合は! = 0 の手順 -> 書き込みが失敗します。  
  
                -   イベント ログに記録  
  
                -   また拡張エラーが返されます。  
  
                    -   **8648:**  
  
                        *ERROR_DS_UPN_VALUE_NOT_UNIQUE_IN_FOREST*  
  
    -   ***SPN の場合***  
  
        -   クエリ ローカル フォレスト全体に関わる SPN インデックス指定された SPN (*サービス プリンシパル名はグローバル インデックス*)  
  
            -   エントリが返される場合は = = 0 が書き込み処理を ->  
  
            -   エントリが返される場合は! = 0 の手順 -> 書き込みが失敗します。  
  
                -   イベント ログに記録  
  
                -   また拡張エラーが返されます。  
  
                    -   **8647:**  
  
                        **ERROR_DS_SPN_VALUE_NOT_UNIQUE_IN_FOREST**  
  
-   **場合 DC! = GC**  
  
    -   Offbox 呼び出し**望ましい**が重要でない、つまりこれはベスト エフォート一意性の確認  
  
        -   GC を検出できない場合にのみローカル DIT に対してチェックを実行します  
  
        -   このようなを示すために記録されたイベント  
  
    -   ***Upn***  
  
        -   最も近い GC に対して LDAP クエリを送信しますか。 指定した UPN のクエリの GC のフォレスト全体に関わる UPN インデックス (*userPrincipalName はグローバル インデックス*)  
  
            -   エントリが返される場合は = = 0 が書き込み処理を ->  
  
            -   エントリが返される場合は! = 0 の手順 -> 書き込みが失敗します。  
  
                -   イベント ログに記録  
  
                -   また拡張エラーが返されます。  
  
                    -   **8648:**  
  
                        *ERROR_DS_UPN_VALUE_NOT_UNIQUE_IN_FOREST*  
  
    -   ***SPN の場合***  
  
        -   最も近い GC に対して LDAP クエリを送信しますか。 指定された spn のクエリの GC のフォレスト全体の SPN インデックス (*サービス プリンシパル名はグローバル インデックス*)  
  
            -   エントリが返される場合は = = 0 が書き込み処理を ->  
  
            -   エントリが返される場合は! = 0 の手順 -> 書き込みが失敗します。  
  
                -   イベント ログに記録  
  
                -   また拡張エラーが返されます。  
  
                    -   **8647:**  
  
                        *ERROR_DS_SPN_VALUE_NOT_UNIQUE_IN_FOREST*  
  
削除されたオブジェクトが再アニメーション化、一意性 SPN または UPN 値の存在がチェックされます。 重複が見つかった場合、要求は失敗します。  
  
-   DNS ホスト名、SAM アカウントの名前などのような特定の属性変更の変更が行われたときに SPN も更新されます。 プロセスで、古い SPN を削除し、新しい SPN が構築され、データベースに追加します。 このパスをトリガーする対象となる必須の属性の変更は次のとおりです。  
  
    -   ATT_DNS_HOST_NAME  
  
    -   ATT_MS_DS_ADDITIONAL_DNS_HOST_NAME  
  
    -   ATT_SAM_ACCOUNT_NAME  
  
    -   ATT_MS_DS_ADDITIONAL_SAM_ACCOUNT_NAME  
  
    -   ATT_SERVER_REFERENCE_BL  
  
    -   ATT_USER_ACCOUNT_CONTROL  
  
重複する SPN の新しい値のいずれかの場合は、変更が失敗します。 上記の一覧の重要な属性は、ATT_DNS_HOST_NAME (コンピューター名) と ATT_SAM_ACCOUNT_NAME (SAM アカウント名) です。  
  
### <a name="try-this-exploring-spn-and-upn-uniqueness"></a>SPN と UPN の一意性を検討してください。  
これは、最初のいくつか"**実際に使ってみる**"、モジュール内のアクティビティ。  このモジュールの別のラボ ガイドではありません。  **実際に使ってみる**活動は、ラボ環境のレッスンの表示を許可する自由形式活動本質的にします。  独自のアクティビティを思い付くし、次のプロンプトまたはスクリプトのオプションがあります。  
  
> [!NOTE]  
> -   これは、最初のいくつか"**実際に使ってみる**"アクティビティ。  
> -   このモジュールの別のラボ ガイドではありません。  
> -   **実際に使ってみる**活動は、ラボ環境のレッスンの表示を許可する自由形式活動本質的にします。  
> -   独自のアクティビティを思い付くし、次のプロンプトまたはスクリプトのオプションがあります。  
> -   すべてのセクションであるときに、**実際に使ってみる**プロンプトで、必要に応じて、演習のレッスンの内容を見て回るが推奨されます。  
  
SPN と UPN の一意性を試してください。  これらの指示に従って操作または、独自に完了します。  
  
1.  UPN を持つ新しいユーザーを作成します。  
  
2.  アカウントを SPN を作成します。  
  
3.  既に以前に定義されている UPN を持つ新しいユーザーを作成するか、既存のアカウントの UPN を変更します。  他のアカウントの SPN の同じ操作を行います  
  
    1.  既に使用されている UPN を持つ既存のユーザー アカウントを設定します  
  
        1.  PowerShell、ADSIEDIT、または Active Directory 管理センター (DSAC.exe) を使用します。  
  
    2.  既に使用されている SPN を既存のアカウントを設定します  
  
        1.  Windows PowerShell、ADSIEDIT をまたは SetSPN  
  
4.  エラーを確認します。  
  
**必要に応じて**  
  
1.  クラスルーム講師であることを確認 [OK] を有効にする、*[AD のごみ箱](https://technet.microsoft.com/library/jj574144.aspx#BKMK_EnableRecycleBin)* Active Directory 管理センターでします。  その場合は、次の手順に移動します。  
  
2.  UPN ユーザー アカウントを設定します  
  
3.  アカウントを削除します  
  
4.  削除されたアカウントとして同じ UPN を持つ別のアカウントを設定します  
  
5.  ごみ箱 GUI を使用して、アカウントを復元しようとしてください。  
  
6.  前の手順で表示するエラーに表示されるだけを想像してみてください。  (および実行した手順の履歴はありません)目標は、アカウントの復元を完了します。  ブックの例の手順を参照してください。  
  


