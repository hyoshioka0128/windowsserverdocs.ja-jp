---
ms.assetid: 8a3cf2ae-2511-4eea-afd5-a43179a78613
title: ディレクトリ サービス コンポーネントの更新
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: cde839feda47d55415b2b6cc1026a7a3e6515a44
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823095"
---
# <a name="directory-services-component-updates"></a>ディレクトリ サービス コンポーネントの更新

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

**Author**: Justin 書籍、シニアサポートエスカレーションエンジニア (Windows グループ)  
  
> [!NOTE]  
> この内容は Microsoft カスタマー サポート エンジニアによって作成され、TechNet が通常提供しているトピックよりも詳細な Windows Server 2012 R2 の機能やソリューションの技術的説明を求めている、経験豊かな管理者とシステム設計者を対象としています。 ただし、TechNet と同様の編集過程は実施されていないため、言語によっては通常より洗練されていない文章が見られる場合があります。  
  
このレッスンでは、Windows Server 2012 R2 のディレクトリサービスコンポーネントの更新について説明します。  
  
## <a name="what-you-will-learn"></a>学習する内容  
次の新しいディレクトリサービスコンポーネントの更新について説明します。  
  
-   次の新しいディレクトリサービスコンポーネントの更新について説明します。  
  
    -   [ドメインとフォレストの機能レベル](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_FL)  
  
    -   [NTFRS の廃止](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_NTFRS)  
  
    -   [LDAP クエリ オプティマイザーの変更点](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_LDAPQuery)  
  
    -   [1644 イベントの改善](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_1644)  
  
    -   [Active Directory レプリケーション スループットの向上](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_ADRepl)  
  
## <a name="domain-and-forest-functional-levels"></a><a name="BKMK_FL"></a>ドメインとフォレストの機能レベル  
  
### <a name="overview"></a>概要  
このセクションでは、ドメインとフォレストの機能レベルの変更について簡単に説明します。  
  
### <a name="new-dfl-and-ffl"></a>新しい DFL と FFL  
リリースでは、新しいドメインとフォレストの機能レベルがあります。  
  
-   フォレストの機能レベル: Windows Server 2012 R2  
  
-   ドメインの機能レベル: Windows Server 2012 R2  
  
### <a name="the-windows-server-2012-r2-domain-functional-level-enables-support-for-the-following"></a>Windows Server 2012 R2 ドメインの機能レベルにより、次のサポートが有効になります。  
  
1.  *保護されたユーザー*の DC 側の保護  
  
    *保護されたユーザー*が Windows Server 2012 R2 ドメインに対する認証を行うことができ**なくなり**ます。  
  
    -   NTLM 認証で認証を行う  
  
    -   Kerberos の事前認証で DES または RC4 の暗号スイートを使用する  
  
    -   制約なしの委任または制約付き委任を使用して委任される  
  
    -   最初の 4 時間の有効期間を超えてユーザー チケット (TGT) を更新する  
  
2.  認証ポリシー  
  
    新しいフォレストベースの Active Directory ポリシーでは、Windows Server 2012 R2 ドメインのアカウントに適用して、アカウントがサインオンできるホストを制御し、アカウントとして実行されているサービスに認証のアクセス制御条件を適用することができます。  
  
3.  Authentication Policy Silos  
  
    新しいフォレストベースの Active Directory オブジェクト。認証ポリシーまたは認証の分離のためにアカウントを分類するために使用される、ユーザー、管理されたサービス、およびコンピューターアカウントの間にリレーションシップを作成できます。  
  
詳細については、「保護されたアカウントの構成方法」を参照してください。  
  
Windows Server 2012 R2 のドメイン機能レベルでは、上記の機能に加えて、ドメイン内のすべてのドメインコントローラーで Windows Server 2012 R2 が実行されるようになります。  
Windows Server 2012 R2 フォレストの機能レベルでは新しい機能は提供されませんが、フォレスト内に作成された新しいドメインは、Windows Server 2012 R2 ドメインの機能レベルで自動的に動作するようになります。  
  
### <a name="minimum-dfl-enforced-on-new-domain-creation"></a>新しいドメインの作成時に最小 DFL が適用される  
Windows Server 2008 DFL は、新しいドメインの作成でサポートされる最小限の機能レベルです。  
  
> [!NOTE]  
> FRS の廃止は、Windows Server 2008 より低いドメインの機能レベルを持つ新しいドメインをインストールする機能を、サーバーマネージャーまたは Windows PowerShell を使用して削除することで実現できます。  
  
### <a name="lowering-the-forest-and-domain-functional-levels"></a>フォレストおよびドメインの機能レベルを下げる  
フォレストおよびドメインの機能レベルは、新しいドメインと新しいフォレストの作成時に既定で Windows Server 2012 R2 に設定されますが、Windows PowerShell を使用して下げることができます。  
  
Windows PowerShell を使用してフォレストの機能レベルを上げたり下げたりするには、 **set-adforestmode**コマンドレットを使用します。  
  
**Contoso.com FFL を Windows Server 2008 モードに設定するには、次のようにします。**  
  
```sql  
Set-ADForestMode -ForestMode Windows2008Forest -Identity contoso.com  
```  
  
Windows PowerShell を使用してドメインの機能レベルを上げたり下げたりするには、Set ADDomainMode コマンドレットを使用します。  
  
**Contoso.com DFL を Windows Server 2008 モードに設定するには、次のようにします。**  
  
```powershell  
Set-ADDomainMode -DomainMode Windows2008Domain -Identity contoso.com  
```  
  
Windows Server 2012 R2 を実行している DC を、2003 DFL を実行している既存のドメインに追加のレプリカとして昇格する機能が動作します。  
  
既存のフォレストでの新しいドメインの作成  
  
![ディレクトリサービスの更新](media/Directory-Services-component-updates/GTR_ADDS_FFL.gif)  
  
### <a name="adprep"></a>ADPREP  
このリリースでは、新しいフォレストまたはドメインの操作はありません。  
  
これらの .ldf ファイルには、**デバイス登録サービス**のスキーマ変更が含まれています。  
  
1.  Sch59  
  
2.  Sch61  
  
3.  Sch62  
  
4.  Sch63  
  
5.  Sch64  
  
6.  Sch65  
  
7.  Sch67  
  
**ワークフォルダー:**  
  
1.  Sch66  
  
**MSODS**  
  
1.  Sch60  
  
**認証ポリシーとサイロ**  
  
1.  Sch68  
  
2.  Sch69  
  
## <a name="deprecation-of-ntfrs"></a><a name="BKMK_NTFRS"></a>NTFRS の非推奨  
  
### <a name="overview"></a>概要  
FRS は、Windows Server 2012 R2 で非推奨とされます。  FRS の廃止は、Windows Server 2008 の最小ドメイン機能レベル (DFL) を適用することで実現されます。  この強制は、サーバーマネージャーまたは Windows PowerShell を使用して新しいドメインが作成された場合にのみ存在します。  
  
ドメインの機能レベルを指定するには、-DomainMode パラメーターを Install-ADDSForest または Install-Addsforest コマンドレットと共に使用します。  このパラメーターでサポートされる値は、有効な整数または対応する列挙文字列値のいずれかです。 たとえば、ドメインモードレベルを Windows Server 2008 R2 に設定するには、値として4または "Win2008R2" を指定します。  これらのコマンドレットをサーバー 2012 R2 から実行する場合、有効な値には、windows server 2008 (3、Win2008) windows server 2008 R2 (4、Win2008R2) windows server 2012 (5、Win2012) および Windows Server 2012 R2 (6、Win2012R2) が含まれます。 ドメインの機能レベルは、フォレストの機能レベルより低くすることはできませんが、それより高くすることはできます。  このリリースでは FRS が非推奨とされているため、windows server 2012 R2 から実行すると、Windows Server 2003 (2, Win2003) はこれらのコマンドレットで認識されるパラメーターではなくなりました。  
  
![ディレクトリサービスの更新](media/Directory-Services-component-updates/GTR_ADDS_PS_Install2003DFL.gif)  
  
![ディレクトリサービスの更新](media/Directory-Services-component-updates/GTR_ADDS_PS_InstallDFL2.gif)  
  
## <a name="ldap-query-optimizer-changes"></a><a name="BKMK_LDAPQuery"></a>LDAP クエリオプティマイザーの変更  
  
### <a name="overview"></a>概要  
LDAP クエリオプティマイザーアルゴリズムが再評価され、さらに最適化されました。  その結果、LDAP search の効率と複雑なクエリの LDAP 検索時間のパフォーマンスが向上します。  
  
> [!NOTE]
> <strong>開発者から:</strong>LDAP クエリから ESE クエリへのマッピングの機能強化により、検索のパフォーマンスが向上しました。  特定レベルの複雑さを超える LDAP フィルターでは、インデックスの選択が最適化されないため、パフォーマンスが大幅に低下します (1000x 以上)。 この変更により、この問題を回避するために、LDAP クエリのインデックスを選択する方法が変更されます。  
> 
> [!NOTE]
> LDAP クエリオプティマイザーアルゴリズムの完全な見直し。結果は次のようになります。  
> 
> -   検索時間の短縮  
> -   効率の向上により、Dc はより多くのことを行うことができます  
> -   AD のパフォーマンスの問題に関するサポート呼び出しが少ない  
> -   Windows Server 2008 R2 に移植される (KB 2862304)  
  
### <a name="background"></a>背景  
Active Directory を検索する機能は、ドメインコントローラーによって提供されるコアサービスです。  その他のサービスや基幹業務アプリケーションは、Active Directory の検索に依存しています。  この機能が使用できない場合は、ビジネス操作が中止されることがあります。  コアと使用率の高いサービスとして、ドメインコントローラーは LDAP 検索トラフィックを効率的に処理することが不可欠です。  Ldap クエリオプティマイザーアルゴリズムでは、ldap 検索フィルターを、データベース内に既にインデックスが作成されているレコードを使用して満たすことのできる結果セットにマッピングすることにより、ldap 検索を可能な限り効率的にすることを試みます。  このアルゴリズムは再評価され、さらに最適化されました。  その結果、LDAP search の効率と複雑なクエリの LDAP 検索時間のパフォーマンスが向上します。  
  
### <a name="details-of-change"></a>変更の詳細  
LDAP 検索には次のものが含まれます。  
  
-   検索を開始する階層内の場所 (NC ヘッド、OU、オブジェクト)  
  
-   検索フィルター  
  
-   返される属性の一覧  
  
検索プロセスは次のようにまとめることができます。  
  
1.  可能であれば、検索フィルターを単純化します。  
  
2.  対象となる最小セットを返す一連のインデックスキーを選択します。  
  
3.  インデックスキーの1つまたは複数の交差部分を実行して、カバーされるセットを減らします。  
  
4.  対象セット内の各レコードについて、フィルター式およびセキュリティを評価します。 フィルターが TRUE と評価され、アクセス権が付与されている場合は、このレコードをクライアントに返します。  
  
LDAP クエリの最適化作業では、手順 2. と 3. を変更して、対象セットのサイズを小さくします。 具体的には、現在の実装では、重複するインデックスキーを選択し、重複する交差部分を実行します。  
  
### <a name="comparison-between-old-and-new-algorithm"></a>古いアルゴリズムと新しいアルゴリズムの比較  
この例では、非効率的な LDAP 検索の対象は、Windows Server 2012 のドメインコントローラーです。  より効率的なインデックスを見つけることができなかったため、検索は約44秒で完了します。  
  
```  
adfind -b dc=blue,dc=contoso,dc=com -f "(| (& (|(cn=justintu) (postalcode=80304) (userprincipalname=justintu@blue.contoso.com)) (|(objectclass=person) (cn=justintu)) ) (&(cn=justintu)(objectclass=person)))" -stats >>adfind.txt  
  
Using server: WINSRV-DC1.blue.contoso.com:389  
  
<removed search results>  
  
Statistics  
=====  
Elapsed Time: 44640 (ms)  
Returned 324 entries of 553896 visited - (0.06%)  
  
Used Filter:  
 ( |  ( &  ( |  (cn=justintu)  (postalCode=80304)  (userPrincipalName=justintu@blue.contoso.com) )  ( |  (objectClass=person)  (cn=justintu) ) )  ( &  (cn=justintu)  (objectClass=person) ) )   
  
Used Indices:  
 DNT_index:516615:N  
  
Pages Referenced          : 4619650  
Pages Read From Disk      : 973  
Pages Pre-read From Disk  : 180898  
Pages Dirtied             : 0  
Pages Re-Dirtied          : 0  
Log Records Generated     : 0  
Log Record Bytes Generated: 0  
```  
  
### <a name="sample-results-using-the-new-algorithm"></a>新しいアルゴリズムを使用したサンプル結果  
この例では、上記とまったく同じ検索を繰り返しますが、Windows Server 2012 R2 ドメインコントローラーを対象としています。  LDAP クエリオプティマイザーアルゴリズムが改善されたため、同じ検索が1秒未満で完了します。  
  
```  
adfind -b dc=blue,dc=contoso,dc=com -f "(| (& (|(cn=justintu) (postalcode=80304) (userprincipalname=dhunt@blue.contoso.com)) (|(objectclass=person) (cn=justintu)) ) (&(cn=justintu)(objectclass=person)))" -stats >>adfindBLUE.txt  
  
Using server: winblueDC1.blue.contoso.com:389  
  
.<removed search results>  
  
Statistics  
=====  
Elapsed Time: 672 (ms)  
Returned 324 entries of 648 visited - (50.00%)  
  
Used Filter:  
 ( |  ( &  ( |  (cn=justintu)  (postalCode=80304)  (userPrincipalName=justintu@blue.contoso.com) )  ( |  (objectClass=person)  (cn=justintu) ) )  ( &  (cn=justintu)  (objectClass=person) ) )   
  
Used Indices:  
 idx_userPrincipalName:648:N  
 idx_postalCode:323:N  
 idx_cn:1:N  
  
Pages Referenced          : 15350  
Pages Read From Disk      : 176  
Pages Pre-read From Disk  : 2  
Pages Dirtied             : 0  
Pages Re-Dirtied          : 0  
Log Records Generated     : 0  
Log Record Bytes Generated: 0  
```  
  
-   ツリーを最適化できない場合は、次のようになります。  
  
    -   例: ツリー内の式が、インデックスを設定されていない列を超えていた  
  
    -   最適化を妨げるインデックスの一覧を記録する  
  
    -   ETW トレースとイベント ID 1644 を介して公開されます。  
  
        ![ディレクトリサービスの更新](media/Directory-Services-component-updates/GTR_ADDS_Event1644.gif)  
  
### <a name="to-enable-the-stats-control-in-ldp"></a><a name="BKMK_EnableStats"></a>LDP で Stats コントロールを有効にするには  
  
1.  LDP.EXE を開き、ドメインコントローラーに接続してバインドします。  
  
2.  **[オプション]** メニューの **[コントロール]** をクリックします。  
  
3.  コントロール ダイアログボックスで、**事前定義済み** プルダウンメニューを展開し、**検索統計** をクリックして、**OK** をクリックします。  
  
    ![ディレクトリサービスの更新](media/Directory-Services-component-updates/GTR_ADDS_Controls.gif)  
  
4.  **[参照]** メニューの **[検索]** をクリックします。  
  
5.  検索 ダイアログボックスで、**オプション** ボタンを選択します。  
  
6.  検索オプション ダイアログボックスの **拡張** チェックボックスがオンになっていることを確認し、 **OK**を選択します。  
  
    ![ディレクトリサービスの更新](media/Directory-Services-component-updates/GTR_ADDS_SearchOptions.gif)  
  
### <a name="try-this-use-ldp-to-return-query-statistics"></a>試してみる: LDP を使用してクエリの統計情報を返す  
ドメインコントローラー、または AD DS ツールがインストールされているドメインに参加しているクライアントまたはサーバーで、次の操作を実行します。  Windows Server 2012 DC と Windows Server 2012 R2 DC を対象として、次の手順を繰り返します。  
  
1.  [「より効率的な MICROSOFT AD 対応アプリケーションの作成」](https://msdn.microsoft.com/library/ms808539.aspx)の記事を確認し、必要に応じて参照してください。  
  
2.  LDP を使用して、検索統計を有効にします ( [ldp で Stats コントロールを有効にするに](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_EnableStats)はこちらを参照してください)。  
  
3.  複数の LDAP 検索を実行し、結果の上部にある統計情報を観察します。  他のアクティビティでも同じ検索を繰り返し、メモ帳のテキストファイルに記述します。  
  
4.  属性インデックスのためにクエリオプティマイザーで最適化できる LDAP 検索を実行する  
  
5.  完了までに長い時間がかかる検索を作成しようとしています (検索がタイムアウトにならないように、 **[制限時間]** オプションを長くすることもできます)。  
  
### <a name="additional-resources"></a>その他のリソース  
[Active Directory 検索とは何ですか。](https://technet.microsoft.com/library/cc783845(v=ws.10).aspx)  
  
[Active Directory 検索のしくみ](https://technet.microsoft.com/library/cc755809(v=WS.10).aspx)  
  
[より効率的な Microsoft Active Directory 対応アプリケーションの作成](https://msdn.microsoft.com/library/ms808539.aspx)  
  
[951581](https://support.microsoft.com/kb/951581) AD または LDS/ADAM ディレクトリサービスでの LDAP クエリの実行速度が予想よりも遅く、イベント ID 1644 がログに記録されることがある  
  
## <a name="1644-event-improvements"></a><a name="BKMK_1644"></a>1644イベントの改善  
  
### <a name="overview"></a>概要  
この更新により、トラブルシューティングのために、LDAP 検索結果の統計がイベント ID 1644 に追加されます。  また、新しいレジストリ値を使用して、時間ベースのしきい値でログ記録を有効にすることもできます。  これらの機能強化は、Windows server 2012 および Windows Server 2008 R2 SP1 で、KB [2800945](https://support.microsoft.com/kb/2800945)を使用して提供され、windows SERVER 2008 SP2 で使用できるようになりました。  
  
> [!NOTE]  
> -   非効率的または高価な LDAP 検索のトラブルシューティングを支援するために、追加の LDAP 検索統計情報がイベント ID 1644 に追加されます。  
> -   検索時間のしきい値を指定できるようになりました (例 高コストで非効率的な検索結果のしきい値を指定する代わりに、100ミリ秒よりも長い時間がかかっている検索のイベント1644をログに記録します。  
  
### <a name="background"></a>背景  
パフォーマンスの問題のトラブルシューティング Active Directory、LDAP 検索アクティビティが問題に寄与している可能性があることが明らかになります。  ドメインコントローラーによって処理される高価または非効率的な LDAP クエリを確認できるように、ログ記録を有効にすることを決定しました。  ログ記録を有効にするには、フィールドエンジニアリング診断の値を設定し、必要に応じて、高価または非効率的な検索結果のしきい値を指定できます。  フィールドエンジニアリングのログ記録レベルを5にすると、これらの条件を満たす検索は、イベント ID 1644 のディレクトリサービスイベントログに記録されます。  
  
イベントには次のものが含まれます。  
  
-   クライアント IP とポート  
  
-   開始ノード  
  
-   フィルター  
  
-   ［検索範囲］  
  
-   属性の選択  
  
-   サーバーコントロール  
  
-   閲覧したエントリ  
  
-   返されたエントリ  
  
ただし、検索操作にかかった時間や、インデックスが使用された (存在する場合) などのイベントには、キーデータがありません。  
  
#### <a name="additional-search-statistics-added-to-event-1644"></a>イベント1644に追加された追加の検索統計  
  
-   使用されたインデックス  
  
-   参照されたページ  
  
-   ディスクから読み取られるページ  
  
-   ディスクから preread ページ  
  
-   変更されたページの消去  
  
-   ダーティページが変更されました  
  
-   検索時間  
  
-   最適化を妨げる属性  
  
#### <a name="new-time-based-threshold-registry-value-for-event-1644-logging"></a>イベント1644ログの新しい時間ベースのしきい値レジストリ値  
高価で非効率的な検索結果のしきい値を指定する代わりに、検索時間のしきい値を指定できます。  50ミリ秒以上かかったすべての検索結果をログに記録する場合は、50 decimal/32 hex (フィールドエンジニアリング値の設定に加えて) を指定します。  
  
```  
Windows Registry Editor Version 5.00  
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters]  
"Search Time Threshold (msecs)"=dword:00000032  
```  
  
#### <a name="comparison-of-the-old-and-new-event-id-1644"></a>新旧のイベント ID 1644 の比較  
まで  
  
![ディレクトリサービスの更新](media/Directory-Services-component-updates/GTR_ADDS_Event1644_2012.gif)  
  
NEW  
  
![ディレクトリサービスの更新](media/Directory-Services-component-updates/GTR_ADDS_Event1644_2012R2.gif)  
  
#### <a name="try-this-use-the-event-log-to-return-query-statistics"></a>試してみよう: イベントログを使用してクエリの統計情報を返す  
  
1.  Windows Server 2012 DC と Windows Server 2012 R2 DC を対象として、次の手順を繰り返します。 各検索の後に、両方の Dc でイベント ID 1644s を確認します。  
  
2.  Regedit を使用して、Windows Server 2012 R2 DC では時間ベースのしきい値を使用し、Windows Server 2012 DC では古いメソッドを使用して、イベント ID 1644 のログ記録を有効にします。  
  
3.  しきい値を超える LDAP 検索をいくつか実行し、結果の上部にある統計情報を観察します。  前の手順で説明した LDAP クエリを使用して、同じ検索を繰り返します。  
  
4.  1つまたは複数の属性のインデックスが作成されていないため、クエリオプティマイザーで最適化できない LDAP 検索を実行します。  
  
## <a name="active-directory-replication-throughput-improvement"></a><a name="BKMK_ADRepl"></a>Active Directory レプリケーションのスループットの向上  
  
### <a name="overview"></a>概要  
AD レプリケーションでは、レプリケーショントランスポートに RPC を使用します。 既定では、RPC は8K の送信バッファーと5K パケットサイズを使用します。 これにより、送信側インスタンスが3つのパケット (約15,000 分のデータ) を送信し、さらに送信する前にネットワークラウンドトリップを待機する必要があるという、実質的な効果があります。 3ミリ秒の往復時間が想定されている場合、スループットは、1 gbps または 10 Gbps のネットワークであっても、最大で 40 mbps になります。  
  
> [!NOTE]  
> -   この更新プログラムは、AD レプリケーションの最大スループットを 40 Mbps から約 600 Mbps に調整します。  
>   
>     -   RPC 送信バッファーのサイズが増加し、ネットワークラウンドトリップの数が減少します。  
> -   この効果は、高速で待機時間の長いネットワークで最も顕著になります。  
  
この更新では、RPC 送信バッファーサイズを8K から 256 KB に変更することで、最大スループットが約 600 Mbps に増加します。  この変更により、TCP ウィンドウサイズは8K を超えて拡張され、ネットワークラウンドトリップの数が減ります。  
  
> [!NOTE]  
> この動作を変更するための構成可能な設定はありません。  
  
### <a name="additional-resources"></a>その他のリソース  
[Active Directory レプリケーションモデルのしくみ](https://technet.microsoft.com/library/cc772726(v=WS.10).aspx)  
  


