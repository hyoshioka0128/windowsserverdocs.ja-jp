---
ms.assetid: 8a3cf2ae-2511-4eea-afd5-a43179a78613
title: ディレクトリ サービス コンポーネントの更新
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: fe27b61abe196a2148ced18806be904ebd555fcc
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442892"
---
# <a name="directory-services-component-updates"></a>ディレクトリ サービス コンポーネントの更新

>適用先:Windows Server 2016 では、Windows Server 2012 R2、Windows Server 2012

**作成者**:Justin Turner、シニア サポート エスカレーション エンジニア、Windows グループ  
  
> [!NOTE]  
> この内容は Microsoft カスタマー サポート エンジニアによって作成され、TechNet が通常提供しているトピックよりも詳細な Windows Server 2012 R2 の機能やソリューションの技術的説明を求めている、経験豊かな管理者とシステム設計者を対象としています。 ただし、TechNet と同様の編集過程は実施されていないため、言語によっては通常より洗練されていない文章が見られる場合があります。  
  
このレッスンでは、Windows Server 2012 R2 でのディレクトリ サービス コンポーネントの更新について説明します。  
  
## <a name="what-you-will-learn"></a>学習する内容  
次のディレクトリ サービス コンポーネントの新しい更新をについて説明します。  
  
-   次のディレクトリ サービス コンポーネントの新しい更新をについて説明します。  
  
    -   [ドメインとフォレストの機能レベル](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_FL)  
  
    -   [NTFRS の廃止](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_NTFRS)  
  
    -   [LDAP クエリ オプティマイザーの変更点](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_LDAPQuery)  
  
    -   [1644 イベントの改善](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_1644)  
  
    -   [Active Directory レプリケーション スループットの向上](../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_ADRepl)  
  
## <a name="BKMK_FL"></a>ドメインとフォレストの機能レベル  
  
### <a name="overview"></a>概要  
ドメインとフォレストの機能レベル変更の概要を説明します。  
  
### <a name="new-dfl-and-ffl"></a>新しい DFL と FFL  
リリースでは、新しいドメインとフォレストの機能レベルがあります。  
  
-   フォレストの機能レベル:Windows Server 2012 R2  
  
-   ドメイン機能レベル:Windows Server 2012 R2  
  
### <a name="the-windows-server-2012-r2-domain-functional-level-enables-support-for-the-following"></a>Windows Server 2012 R2 ドメインの機能レベルは、次のサポートを有効にします。  
  
1.  DC 側の保護の*Protected Users*  
  
    *保護されたユーザー*できる Windows Server 2012 R2 のドメインへの認証**されなく**:  
  
    -   NTLM 認証を使用します。  
  
    -   Kerberos 事前認証で DES または RC4 暗号スイートを使用します。  
  
    -   委任を使用して制約なし/制約付き委任  
  
    -   最初の 4 時間以内の有効期間を超えてユーザー チケット (Tgt) を更新します。  
  
2.  Authentication Policies  
  
    新しいフォレストに基づいた Active Directory ポリシーのうちでホストを管理する Windows Server 2012 R2 のドメインのアカウントに適用できるアカウントできますからシングル サインオンとアカウントとして実行されているサービスに認証のアクセス制御条件を適用  
  
3.  Authentication Policy Silos  
  
    新しいフォレストに基づいた Active Directory オブジェクト アカウントの認証ポリシーまたは認証を分離するための分類に使用するには、ユーザー、管理されたサービスおよびコンピューター アカウント間のリレーションシップを作成することができます。  
  
参照してください詳細については保護されたアカウントを構成する方法。  
  
上記の機能に加え、Windows Server 2012 R2 のドメイン機能レベルにより、ドメイン内の任意のドメイン コント ローラーが Windows Server 2012 R2 を実行します。  
Windows Server 2012 R2 のフォレストの機能レベルは、新機能を提供しませんが、フォレスト内に作成、新しいドメインを Windows Server 2012 R2 のドメイン機能レベルで自動的に動作するようになります。  
  
### <a name="minimum-dfl-enforced-on-new-domain-creation"></a>新しいドメインの作成に適用されている最小 DFL  
Windows Server 2008 DFL では、新しいドメインの作成でサポートされている最小限の機能レベルです。  
  
> [!NOTE]  
> FRS の廃止は、ドメイン機能レベルが Windows Server 2008 サーバー マネージャーまたは Windows PowerShell を使用してより新しいドメインをインストールする機能を削除することによって実現されます。  
  
### <a name="lowering-the-forest-and-domain-functional-levels"></a>フォレストおよびドメインの機能レベルを下げる  
フォレストおよびドメインの機能レベルでは、新しいドメインと新しいフォレストの作成時に既定で Windows Server 2012 R2 に設定されますが、Windows PowerShell を使用して下げることができます。  
  
Windows PowerShell を使用してフォレストの機能レベルを上げたり下げたりを使用して、 **Set-adforestmode**コマンドレット。  
  
**Contoso.com FFL を Windows Server 2008 モードに設定します。**  
  
```sql  
Set-ADForestMode -ForestMode Windows2008Forest -Identity contoso.com  
```  
  
Windows PowerShell を使用して、ドメイン機能レベルを上げたり下げたりするには、Set-addomainmode コマンドレットを使用します。  
  
**Contoso.com DFL を Windows Server 2008 モードに設定します。**  
  
```powershell  
Set-ADDomainMode -DomainMode Windows2008Domain -Identity contoso.com  
```  
  
2003 DFL を実行している既存のドメインに追加のレプリカとして Windows Server 2012 R2 を実行している DC の昇格は機能します。  
  
既存のフォレストに新しいドメインの作成  
  
![ディレクトリ サービスの更新プログラム](media/Directory-Services-component-updates/GTR_ADDS_FFL.gif)  
  
### <a name="adprep"></a>ADPREP  
新しいフォレストまたはドメインの操作をこのリリースではありません。  
  
これらの .ldf ファイルにはスキーマ変更が含まれて、 **Device Registration Service**します。  
  
1.  Sch59  
  
2.  Sch61  
  
3.  Sch62  
  
4.  Sch63  
  
5.  Sch64  
  
6.  Sch65  
  
7.  Sch67  
  
**ワーク フォルダー:**  
  
1.  Sch66  
  
**MSODS:**  
  
1.  Sch60  
  
**認証ポリシーとサイロ**  
  
1.  Sch68  
  
2.  Sch69  
  
## <a name="BKMK_NTFRS"></a>NTFRS の廃止  
  
### <a name="overview"></a>概要  
FRS は、Windows Server 2012 R2 で非推奨とされます。  FRS の廃止は、Windows Server 2008 の最低限のドメイン機能レベル (DFL) に適用することによって実現されます。  この強制は、サーバー マネージャーまたは Windows PowerShell を使用して、新しいドメインを作成する場合にのみ存在します。  
  
ドメインの機能レベルを指定するのにには、Install-addsforest または Install-addsdomain コマンドレットで、DomainMode - パラメーターを使用します。  このパラメーターのサポートされている値は有効な整数または対応する列挙された文字列値のいずれかにできます。 たとえば、ドメイン モードのレベルを Windows Server 2008 R2 を設定する、4 の値または"Win2008R2"のいずれかを指定できます。  Windows Server 2008 (3、Win2008) の値は、Server 2012 R2 の有効なからこれらのコマンドレットを実行するときに Windows Server 2008 R2 (4、Win2008R2) Windows Server 2012 (5、Win2012) および Windows Server 2012 R2 (6、Win2012R2)。 ドメインの機能レベルは、フォレストの機能レベルより低くすることはできませんが、それより高くすることはできます。  このリリースでは、Windows Server 2003 (2, Win2003) で FRS が非推奨とされますので認識されている Windows Server 2012 R2 から実行すると、これらのコマンドレットとパラメーターではありません。  
  
![ディレクトリ サービスの更新プログラム](media/Directory-Services-component-updates/GTR_ADDS_PS_Install2003DFL.gif)  
  
![ディレクトリ サービスの更新プログラム](media/Directory-Services-component-updates/GTR_ADDS_PS_InstallDFL2.gif)  
  
## <a name="BKMK_LDAPQuery"></a>LDAP クエリ オプティマイザーの変更  
  
### <a name="overview"></a>概要  
LDAP クエリ オプティマイザーのアルゴリズムが再評価され、さらに最適化します。  結果は、LDAP 検索効率および複雑なクエリの LDAP search time のパフォーマンスの向上です。  
  
> [!NOTE]
> <strong>開発者:</strong>LDAP からのマッピングの向上によって検索のパフォーマンスの向上 ESE クエリにクエリを実行します。  複雑さの特定のレベルの LDAP フィルターを防ぐのパフォーマンスを大幅に低下 (1000 x 以上)、最適化されたインデックスを選択します。 この変更は、この問題を回避するために LDAP クエリのインデックスを選択する方法を変更します。  
> 
> [!NOTE]
> その結果、LDAP クエリ オプティマイザーのアルゴリズムの完全なオーバー ホール:  
> 
> -   検索時間の短縮  
> -   効率を向上させるより多くの Dc を許可します。  
> -   電話サポートよりに関する AD パフォーマンス上の問題します。  
> -   Windows Server 2008 R2 (KB 2862304) に移植バック  
  
### <a name="background"></a>背景  
Active Directory を検索する機能は、ドメイン コント ローラーによって提供されるコア サービスです。  他のサービスや基幹業務アプリケーションは、Active Directory の検索に依存します。  ビジネス操作はこの機能が利用できない場合、停止しなくなります。  コアと使用頻度の高いサービスでは、としては、ドメイン コント ローラーが効率的に LDAP 検索のトラフィックを処理することが不可欠です。  LDAP クエリ オプティマイザーのアルゴリズムは、既にデータベースにインデックスを作成するレコードを使用して満たすことができる結果セットに LDAP 検索フィルターをマップすることによって LDAP 検索を可能な限り効率的にしようとします。  このアルゴリズムが再評価され、さらに最適化します。  結果は、LDAP 検索効率および複雑なクエリの LDAP search time のパフォーマンスの向上です。  
  
### <a name="details-of-change"></a>変更の詳細  
LDAP 検索が含まれます。  
  
-   検索を開始する階層内の場所 (NC ヘッド、OU、オブジェクト)  
  
-   検索フィルター  
  
-   返す属性の一覧  
  
検索のプロセスに関するものです。  
  
1.  可能であれば、検索フィルターを簡略化します。  
  
2.  管理対象の最小セットを返すインデックス キーのセットを選択します。  
  
3.  対象セットを削減する、インデックス キーの 1 つまたは複数の交差部分を実行します。  
  
4.  対象セット内の各レコードに対して、セキュリティだけでなく、フィルター式を評価します。 フィルターが TRUE に評価され、アクセスが許可される場合、は、クライアントにこのレコードを返します。  
  
LDAP クエリの最適化作業は、手順 2. および 3. は、対象セットのサイズを小さくを変更します。 具体的には、現在の実装では、重複するインデックス キーを選択し、冗長の交差部分を実行します。  
  
### <a name="comparison-between-old-and-new-algorithm"></a>古いマスター_キーと新しいアルゴリズムとの間の比較  
この例では非効率的な LDAP 検索の対象では、Windows Server 2012 ドメイン コント ローラーです。  検索より効率的なインデックスの検索に失敗する結果として、約 44 秒で完了します。  
  
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
  
### <a name="sample-results-using-the-new-algorithm"></a>新しいアルゴリズムを使用してサンプルの結果  
この例では、上記と同じ検索を繰り返しますが、Windows Server 2012 R2 ドメイン コント ローラーを対象とします。  同じ検索は、LDAP クエリ オプティマイザーのアルゴリズムが改善されたのため 1 秒未満で完了します。  
  
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
  
-   場合、ツリーを最適化することができません。  
  
    -   例: ツリー内の式がないインデックス付き列を超えました  
  
    -   記録の最適化がインデックスの一覧  
  
    -   ETW トレースとイベント ID 1644 経由で公開  
  
        ![ディレクトリ サービスの更新プログラム](media/Directory-Services-component-updates/GTR_ADDS_Event1644.gif)  
  
### <a name="BKMK_EnableStats"></a>LDP の統計情報のコントロールを有効にするには  
  
1.  LDP.exe を開き、接続、およびドメイン コント ローラーにバインドします。  
  
2.  **オプション** メニューのをクリックして**コントロール**します。  
  
3.  コントロール ダイアログ ボックスで、展開、**定義済みの負荷**プルダウンで表示 メニューのをクリックして**検索 Stats**順にクリックします**ok**。  
  
    ![ディレクトリ サービスの更新プログラム](media/Directory-Services-component-updates/GTR_ADDS_Controls.gif)  
  
4.  **参照** メニューのをクリックして**検索**  
  
5.  検索ダイアログ ボックスで、選択、**オプション**ボタンをクリックします。  
  
6.  確認、**拡張**検索オプション ダイアログ ボックスを選択します チェック ボックスをオン**OK**します。  
  
    ![ディレクトリ サービスの更新プログラム](media/Directory-Services-component-updates/GTR_ADDS_SearchOptions.gif)  
  
### <a name="try-this-use-ldp-to-return-query-statistics"></a>これを試してください。LDP を使用して、クエリの統計情報を返す  
ドメイン コント ローラーで、またはドメインに参加しているクライアントまたは AD DS ツールがインストールされているサーバーは、次を実行します。  次を繰り返して、Windows Server 2012 DC と Windows Server 2012 R2 の DC を対象とします。  
  
1.  レビュー、 [「を作成するより効率的な Microsoft AD 対応アプリケーション」](https://msdn.microsoft.com/library/ms808539.aspx)記事を参照して、必要に応じてに戻っています。  
  
2.  LDP を使用して、検索の統計情報を有効にする (を参照してください[LDP で統計の管理を有効に](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_EnableStats))  
  
3.  いくつかの LDAP 検索を実行し、結果の上部にある統計情報を確認します。  その他で同じ検索を繰り返すことがアクティビティ ドキュメントので、メモ帳テキスト ファイルにします。  
  
4.  クエリ オプティマイザーは、属性のインデックスのために最適化できるようにする LDAP 検索を実行します。  
  
5.  所要時間がかかる検索を作成しようとしています (を増やしたい場合があります、**制限時間**オプション、検索がタイムアウトしないように) します。  
  
### <a name="additional-resources"></a>その他のリソース  
[Active Directory の検索とは](https://technet.microsoft.com/library/cc783845(v=ws.10).aspx)  
  
[Active Directory の作業の検索方法](https://technet.microsoft.com/library/cc755809(v=WS.10).aspx)  
  
[効率の高い Microsoft Active Directory 対応のアプリケーションを作成します。](https://msdn.microsoft.com/library/ms808539.aspx)  
  
[951581](https://support.microsoft.com/kb/951581)広告に予想よりも遅くの LDAP クエリの実行または LDS と ADAM ディレクトリ サービスとイベント ID 1644 を記録する可能性があります  
  
## <a name="BKMK_1644"></a>1644 イベントの改善  
  
### <a name="overview"></a>概要  
この更新プログラムは、トラブルシューティングの目的で支援するためにイベント ID 1644 に追加 LDAP 検索結果の統計情報を追加します。  さらに、時間ベースのしきい値にログを有効に使用できる新しいレジストリ値があります。  これらの機能強化は Windows Server 2012 および Windows Server 2008 R2 SP1 KB 経由で入手可能になった[2800945](https://support.microsoft.com/kb/2800945)が利用できる Windows Server 2008 sp2 とします。  
  
> [!NOTE]  
> -   イベント ID 1644 非効率的なまたは高コストの LDAP 検索のトラブルシューティングを支援するその他の LDAP 検索の統計情報が追加されます。  
> -   検索時間のしきい値 (例: を指定できるようになりました 検索以上 100 ミリ秒かかってログのイベント 1644)、高コストと効率低下を招く検索結果のしきい値の値を指定する代わりに  
  
### <a name="background"></a>背景  
Active Directory のパフォーマンスの問題をトラブルシューティングの際に LDAP 検索の利用状況を問題に貢献する可能性があることが明らかになります。  ドメイン コント ローラーによって処理コストがかかったり、非効率的なの LDAP クエリを表示することをログ記録を有効にすること。  ログ記録を有効にするためには、フィールド エンジニア リングの診断の値を設定する必要があり、必要に応じて、高価な/非効率的な検索結果のしきい値の値を指定できます。  フィールド エンジニアで 5 の値をログ記録レベルを有効にするのには、これらの条件を満たす任意の検索は、イベント ID 1644 にディレクトリ サービス イベント ログに記録されます。  
  
イベントが含まれます。  
  
-   クライアント IP とポート  
  
-   開始ノード  
  
-   フィルター  
  
-   ［検索範囲］  
  
-   属性の選択  
  
-   サーバー コントロール  
  
-   アクセスしたエントリ  
  
-   返されるエントリ  
  
ただし、キーのデータは、イベントから不足しているインデックスが使用された (存在する場合)、検索操作との時間が費やされたなど。  
  
#### <a name="additional-search-statistics-added-to-event-1644"></a>追加の検索の統計情報のイベント 1644 に追加  
  
-   使用中のインデックス  
  
-   参照するページ  
  
-   ディスクから読み取られたページ  
  
-   ディスクから preread ページ  
  
-   クリーンなページの変更  
  
-   変更のダーティ ページ  
  
-   検索時間  
  
-   属性の最適化を防ぐ  
  
#### <a name="new-time-based-threshold-registry-value-for-event-1644-logging"></a>1644 イベントのログ記録用の新しいしきい値の時間に基づくレジストリ値  
高コストと効率低下を招く検索結果のしきい値値を指定するには、代わりに、検索時間のしきい値を指定できます。  かどうかに 50 ミリ秒を要したすべての検索結果を記録するか、大きい、する指定 50 の 10 進数 (フィールド エンジニア リングの値の設定) に加えて 16 進数の 32/。  
  
```  
Windows Registry Editor Version 5.00  
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters]  
"Search Time Threshold (msecs)"=dword:00000032  
```  
  
#### <a name="comparison-of-the-old-and-new-event-id-1644"></a>新旧のイベント ID 1644 の比較  
古い  
  
![ディレクトリ サービスの更新プログラム](media/Directory-Services-component-updates/GTR_ADDS_Event1644_2012.gif)  
  
新規  
  
![ディレクトリ サービスの更新プログラム](media/Directory-Services-component-updates/GTR_ADDS_Event1644_2012R2.gif)  
  
#### <a name="try-this-use-the-event-log-to-return-query-statistics"></a>これを試してください。イベント ログを使用して、クエリの統計情報を返す  
  
1.  次を繰り返して、Windows Server 2012 DC と Windows Server 2012 R2 の DC を対象とします。 各検索後に 2 つの Dc では、イベント ID 1644s を確認します。  
  
2.  Regedit を使用して、時間ベースのしきい値を使用して、Windows Server 2012 R2 の DC と Windows Server 2012 DC の古いメソッドでイベント ID 1644 ログ記録が有効にします。  
  
3.  しきい値を超えるし、結果の上部にある統計情報を確認するいくつかの LDAP 検索を実行します。  先ほど手順で指定した LDAP クエリを使用し、同じ検索を繰り返します。  
  
4.  クエリ オプティマイザーで 1 つまたは複数の属性のインデックス化されていないため、最適化することは、LDAP の検索を実行します。  
  
## <a name="BKMK_ADRepl"></a>Active Directory レプリケーション スループットの向上  
  
### <a name="overview"></a>概要  
AD レプリケーションでは、そのレプリケーション トランスポートに RPC を使用します。 既定では、RPC は、8 K の送信バッファーとパケット サイズを 5 K を使用します。 これは、場所、送信元のインスタンスが (約 15 K 分のデータ) の 3 つのパケットを送信し、詳細を送信する前にラウンド トリップ ネットワークの待機するには、実質的な効果です。 ミリ秒と仮定するとラウンドト リップ時間、最高のスループットは、40 mbps、1 gbps または 10 Gbps のネットワーク上でもの周囲には。  
  
> [!NOTE]  
> -   この更新プログラムでは、最大の AD レプリケーションのスループットが 40 mbps から約 600 Mbps に調整されます。  
>   
>     -   ネットワークの数が減少する RPC 送信バッファーのサイズを増加しているラウンド トリップ  
> -   影響があるに高速で最も顕著な待機時間の長いネットワーク。  
  
この更新プログラムは、256 KB に 8 K から RPC 送信バッファーのサイズを変更することで、約 600 Mbps に最大のスループットを向上します。  この変更により、TCP ウィンドウ サイズ 8 K、を超えて増加するラウンド トリップのネットワークの数を減らします。  
  
> [!NOTE]  
> この動作を変更する構成可能な設定はありません。  
  
### <a name="additional-resources"></a>その他のリソース  
[Active Directory レプリケーション モデルのしくみ](https://technet.microsoft.com/library/cc772726(v=WS.10).aspx)  
  


