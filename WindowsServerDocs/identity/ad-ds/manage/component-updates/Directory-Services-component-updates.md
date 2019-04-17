---
ms.assetid: 8a3cf2ae-2511-4eea-afd5-a43179a78613
title: "ディレクトリ サービス コンポーネントの更新"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ac42591450038240ced273555fb01e66b1ff5546
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="directory-services-component-updates"></a>ディレクトリ サービス コンポーネントの更新

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

**作成者**: Windows グループに Justin チューナー シニア サポート エスカレーション エンジニア  
  
> [!NOTE]  
> このコンテンツが、Microsoft カスタマー サポート エンジニアによって書き込まれるあり、経験豊富な管理者と TechNet の通常のトピックよりも機能と Windows Server 2012 R2 で解決策の詳細な技術的説明を求めているシステム アーキテクトです。 ただし、実施されていません、同様の編集過程のため、TechNet の「新機能が見つかった通常より洗練されて、言語によってように見える場合があります。  
  
ここでは、Windows Server 2012 R2 でのディレクトリ サービス コンポーネントの更新について説明します。  
  
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
リリースは、新しいドメインとフォレストの機能レベルがあります。  
  
-   Windows Server 2012 R2 のフォレストの機能レベル:  
  
-   Windows Server 2012 R2 のドメインの機能レベル:  
  
### <a name="the-windows-server-2012-r2-domain-functional-level-enables-support-for-the-following"></a>Windows Server 2012 R2 ドメインの機能レベルは、次のサポートを有効にします。  
  
1.  DC 側の保護の*Protected Users*  
  
    *ユーザーが保護されている*Windows Server 2012 R2 のドメインに対して認証を行うことができます**不要になった**:  
  
    -   NTLM 認証を使用します。  
  
    -   Kerberos 事前認証で DES または RC4 暗号スイートを使用してください。  
  
    -   制約なし/制約付き委任を使用して委任します。  
  
    -   最初の 4 時間の有効期間を超えるユーザー チケット (Tgt) を更新します。  
  
2.  認証ポリシー  
  
    ホストを管理する Windows Server 2012 R2 のドメインにアカウントに適用できますを新しいフォレストに基づいた Active Directory ポリシーできますからサインオンおよびアカウントのアカウントとして実行されているサービスに認証のアクセス制御条件を適用  
  
3.  認証ポリシー サイロ  
  
    新しいフォレストに基づいた Active Directory オブジェクトのアカウントの認証ポリシーまたは認証の分離のための分類に使用するには、ユーザー、管理されたサービスおよびコンピューター アカウント間の関係を作成することができます。  
  
表示の詳細については保護されるアカウントを構成する方法。  
  
上記の機能に加え、Windows Server 2012 R2 のドメイン機能レベルは、ドメイン内の任意のドメイン コントローラーが Windows Server 2012 R2 が実行されることを確認します。  
Windows Server 2012 R2 フォレストの機能レベルが任意の新機能を提供していないが、フォレスト内に作成の任意の新しいドメインを Windows Server 2012 R2 のドメイン機能レベルで自動的に動作するようになります。  
  
### <a name="minimum-dfl-enforced-on-new-domain-creation"></a>新しいドメインの作成に適用される最小 DFL  
Windows Server 2008 DFL では、新しいドメインの作成でサポートされている最小機能レベルです。  
  
> [!NOTE]  
> FRS の廃止については、サーバー マネージャーまたは Windows PowerShell を使用して、Windows Server 2008 よりも低いドメイン機能レベルを持つ新しいドメインをインストールする機能を削除することで実現します。  
  
### <a name="lowering-the-forest-and-domain-functional-levels"></a>フォレストおよびドメインの機能レベルを下げる  
フォレストおよびドメインの機能レベルは、新しいドメインと新しいフォレストの作成時に既定で Windows Server 2012 R2 に設定されますが、Windows PowerShell を使用して下げることができます。  
  
昇格または Windows PowerShell を使用してフォレストの機能レベルを下げるを使用して、**Set-adforestmode**コマンドレット。  
  
**Windows Server 2008 モードに contoso.com FFL を設定します。**  
  
```sql  
Set-ADForestMode -ForestMode Windows2008Forest -Identity contoso.com  
```  
  
上げるまたは Windows PowerShell を使用してドメインの機能レベルを下げる Set-ADDomainMode コマンドレットを使用します。  
  
**Windows Server 2008 モードを contoso.com DFL を設定します。**  
  
```powershell  
Set-ADDomainMode -DomainMode Windows2008Domain -Identity contoso.com  
```  
  
2003 DFL を実行している既存のドメインに追加のレプリカとして Windows Server 2012 R2 を実行している DC の昇格は次のとおり動作します。  
  
既存のフォレストに新しいドメインの作成  
  
![ディレクトリ サービスの更新プログラム](media/Directory-Services-component-updates/GTR_ADDS_FFL.gif)  
  
### <a name="adprep"></a>ADPREP  
新しいフォレストやドメインの操作をこのリリースではありません。  
  
これらの .ldf ファイルのスキーマ変更が含まれている、**デバイス登録サービス**します。  
  
1.  Sch59  
  
2.  Sch61  
  
3.  Sch62  
  
4.  Sch63  
  
5.  Sch64  
  
6.  Sch65  
  
7.  Sch67  
  
**ワーク フォルダーの場合:**  
  
1.  Sch66  
  
**MSODS:**  
  
1.  Sch60  
  
**認証ポリシーとサイロ**  
  
1.  Sch68  
  
2.  Sch69  
  
## <a name="BKMK_NTFRS"></a>NTFRS の廃止  
  
### <a name="overview"></a>概要  
FRS は、Windows Server 2012 R2 で推奨されなくなりました。  FRS の廃止については、Windows Server 2008 の最小のドメイン機能レベル (DFL) に適用することで実現します。  この強制は、サーバー マネージャーまたは Windows PowerShell を使用して、新しいドメインが作成された場合にのみ存在します。  
  
Install-ADDSForest または Install-ADDSDomain コマンドレットで - DomainMode パラメーターを使用するドメインの機能レベルを指定します。  このパラメーターの値がサポートされている有効な整数または対応する列挙型の文字列値のいずれかを使用できます。 たとえば、ドメイン モードのレベルを Windows Server 2008 R2 を設定する、4 の値または"Win2008R2"のいずれかを指定できます。  Windows Server 2008 (3 Win2008) の値にはサーバー 2012 R2 の有効なからこれらのコマンドレットを実行するときに Windows Server 2008 R2 (4 Win2008R2) Windows Server 2012 (5、Win2012) および Windows Server 2012 R2 (6、Win2012R2)。 ドメインの機能レベルは、フォレストの機能レベルよりも低いすることはできませんより高いことができます。  このリリースでは、Windows Server 2003 (2, Win2003) で推奨されなくなった FRS から Windows Server 2012 R2 から実行すると、これらのコマンドレットで認識されているパラメータではありません。  
  
![ディレクトリ サービスの更新プログラム](media/Directory-Services-component-updates/GTR_ADDS_PS_Install2003DFL.gif)  
  
![ディレクトリ サービスの更新プログラム](media/Directory-Services-component-updates/GTR_ADDS_PS_InstallDFL2.gif)  
  
## <a name="BKMK_LDAPQuery"></a>LDAP クエリ オプティマイザーの変更点  
  
### <a name="overview"></a>概要  
LDAP クエリ オプティマイザー アルゴリズムが再評価し、さらに最適化します。  結果は、LDAP 検索効率および複雑なクエリの LDAP 検索時間において、パフォーマンスが向上します。  
  
> [!NOTE]  
> **開発者から:**ESE クエリを LDAP からのマッピングの向上によって検索のパフォーマンスの向上を照会します。  特定のレベルの複雑さの LDAP フィルターでは、インデックスを最適化された選択した場合、結果として (x 1000 以上) のパフォーマンスの大幅に低下しないようにします。 この変更は、LDAP クエリは、この問題を回避するインデックスを選択する方法を変更します。  
  
> [!NOTE]  
> 結果として、LDAP クエリ オプティマイザー アルゴリズムの完全なオーバー ホール:  
>   
> -   高速な検索時間  
> -   効率を向上させるより多くの Dc を許可します。  
> -   サポートへの問い合わせが少なくに関する広告パフォーマンス上の問題します。  
> -   Windows Server 2008 R2 (KB 2862304) に移植戻る  
  
### <a name="background"></a>バック グラウンド  
Active Directory を検索する機能は、ドメイン コントローラーによって提供されるコア サービスです。  他のサービスや基幹業務アプリケーションは、Active Directory の検索に依存します。  業務はこの機能が利用できない場合に停止しなくなります。  コア使用頻度の高いサービスと、ドメイン コントローラーが効率的に LDAP 検索のトラフィックを処理することが不可欠です。  LDAP クエリ オプティマイザー アルゴリズムは、既にデータベースでインデックスが作成レコード経由で満たされる結果セットへの LDAP 検索フィルターのマッピングを LDAP 検索をできるだけ効率を高めるため試行します。  このアルゴリズムが再評価し、さらに最適化します。  結果は、LDAP 検索効率および複雑なクエリの LDAP 検索時間において、パフォーマンスが向上します。  
  
### <a name="details-of-change"></a>変更の詳細  
LDAP 検索が含まれています。  
  
-   検索を開始する階層内の場所 (NC の一番上、OU、オブジェクト)  
  
-   検索フィルター  
  
-   返す属性の一覧  
  
検索プロセスようにまとめることができます。  
  
1.  可能であれば、検索フィルターを簡略化します。  
  
2.  カバーされている最小のセットを返すインデックス キーのセットを選択します。  
  
3.  管理対象のセットを減らすために、インデックスのキーの交差が 1 つまたは複数を実行します。  
  
4.  管理対象のセット内の各レコードのセキュリティと同様に、フィルター式を評価します。 このレコードをフィルターの評価が TRUE アクセスが許可される場合は、クライアントに戻ります。  
  
LDAP クエリの最適化作業では、手順 2 および 3 は、管理対象のセットのサイズを小さくを変更します。 具体的には、現在の実装では、重複するインデックスのキーを選択し、冗長の交差を実行します。  
  
### <a name="comparison-between-old-and-new-algorithm"></a>古いと新しいアルゴリズムの比較  
この例では、非効率的な LDAP 検索の対象は、Windows Server 2012 ドメイン コントローラーです。  検索をより効率的なインデックスの検索に失敗した結果としては約 44 秒で完了します。  
  
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
  
### <a name="sample-results-using-the-new-algorithm"></a>新しいアルゴリズムを使用して結果の例  
この例では、上記と同じ検索を繰り返しますが、Windows Server 2012 R2 ドメイン コントローラーを対象とします。  同じ検索は、LDAP クエリ オプティマイザー アルゴリズムの機能強化のため 1 秒未満で完了します。  
  
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
  
-   ツリーを最適化するためにできない場合は。  
  
    -   例: ツリー内の式が付いていない列経由  
  
    -   最適化ができないようにするインデックスの一覧を記録します。  
  
    -   ETW トレースは、イベント ID 1644 経由で公開されています。  
  
        ![ディレクトリ サービスの更新プログラム](media/Directory-Services-component-updates/GTR_ADDS_Event1644.gif)  
  
### <a name="BKMK_EnableStats"></a>LDP で統計情報の制御を有効にするには  
  
1.  LDP.exe を開くと接続し、ドメイン コントローラーにバインドします。  
  
2.  **オプション**] メニューのをクリックして**コントロール**します。  
  
3.  [コントロール] ダイアログ ボックスで、展開、**定義済みの負荷**プルダウン メニューで、] をクリックして**検索の統計**] をクリックし、**[OK]**します。  
  
    ![ディレクトリ サービスの更新プログラム](media/Directory-Services-component-updates/GTR_ADDS_Controls.gif)  
  
4.  **参照**] メニューのをクリックして**検索**  
  
5.  [検索] ダイアログ ボックスで、選択、**オプション**ボタンをクリックします。  
  
6.  確認して、**拡張**検索オプション] ダイアログ ボックスを選択チェック ボックスをオン**OK**します。  
  
    ![ディレクトリ サービスの更新プログラム](media/Directory-Services-component-updates/GTR_ADDS_SearchOptions.gif)  
  
### <a name="try-this-use-ldp-to-return-query-statistics"></a>を試してください LDP を返すクエリ統計情報使用する。  
ドメイン コントローラー、またはドメインに参加しているクライアントまたは AD DS ツールがインストールされているサーバーから、次を実行します。  次を繰り返して、Windows Server 2012 DC と Windows Server 2012 R2 の DC を対象とします。  
  
1.  レビュー、[「より効率的な Microsoft AD 有効になっているアプリケーションの作成」](https://msdn.microsoft.com/library/ms808539.aspx)記事を参照して戻す、必要に応じてします。  
  
2.  LDP を使用して、検索の統計情報を有効にする (を参照してください[LDP で統計情報の制御を有効にする](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Directory-Services-component-updates.md#BKMK_EnableStats))  
  
3.  いくつかの LDAP 検索を実行し、結果の上部に統計情報を確認します。  同じの他の検索を繰り返すことがアクティビティ ドキュメントので、メモ帳テキスト ファイルにします。  
  
4.  LDAP の検索クエリ オプティマイザーのための属性のインデックスを最適化できるようにします。  
  
5.  完了に要する時間が長く検索を作成しようとしています (増加することも、**制限時間**タイムアウトしないので、検索オプション)。  
  
### <a name="additional-resources"></a>その他のリソース  
[Active Directory の検索とは何ですか。](https://technet.microsoft.com/library/cc783845(v=ws.10).aspx)  
  
[Active Directory の検索作業方法](https://technet.microsoft.com/library/cc755809(v=WS.10).aspx)  
  
[Microsoft Active Directory 対応アプリケーションをより効率的なを作成します。](https://msdn.microsoft.com/library/ms808539.aspx)  
  
[951581](https://support.microsoft.com/kb/951581) LDAP クエリの実行は、AD で予想より時間または LDS/ADAM ディレクトリ サービスおよびイベント ID 1644 を記録することがあります  
  
## <a name="BKMK_1644"></a>1644 イベントの改善  
  
### <a name="overview"></a>概要  
この更新プログラムは、トラブルシューティングのために役立つイベント ID 1644 に追加の LDAP 検索結果の統計を追加します。  さらに、時間ベースのしきい値にログを有効にするために使用できる新しいレジストリ値があります。  これらの機能強化では、Windows Server 2012 および Windows Server 2008 R2 SP1 KB 経由で利用可能になった[2800945](https://support.microsoft.com/kb/2800945)ができるように Windows Server 2008 SP2 とします。  
  
> [!NOTE]  
> -   その他の LDAP 検索の統計情報は、イベント ID 1644 または非効率的で高価な LDAP 検索のトラブルシューティングに役立つに追加されます。  
> -   (例: 検索時間のしきい値を指定することができます。 100 ミリ秒よりも時間がかかって検索ログのイベント 1644)、高コストと効率低下を招く検索結果のしきい値の値を指定することではなく  
  
### <a name="background"></a>バック グラウンド  
Active Directory パフォーマンスの問題をトラブルシューティングするには、中が明らかになること LDAP 検索アクティビティの問題を原因となる可能性があります。  ドメイン コントローラーによって処理される高価な非効率的なの LDAP クエリを表示できるようにログを有効にすることできます。  ログ記録を有効にするためにフィールド エンジニア リング診断値を設定する必要があり、必要に応じて、高価な/非効率的な検索結果のしきい値の値を指定できます。  フィールド エンジニア リング 5 の値にログ出力レベルを有効にするときにこれらの条件を満たしている任意の検索はイベント ID 1644 にディレクトリ サービス イベント ログに記録されます。  
  
イベントが含まれています。  
  
-   クライアント IP とポート  
  
-   ノードの開始  
  
-   フィルター  
  
-   検索範囲  
  
-   属性の選択  
  
-   サーバー コントロール  
  
-   アクセスしたエントリ  
  
-   返されるエントリ  
  
ただし、重要なデータは、イベントから不足しているインデックスが使用されての所要時間、検索操作と新機能で (存在する場合) などです。  
  
#### <a name="additional-search-statistics-added-to-event-1644"></a>追加の検索統計のイベント 1644 に追加  
  
-   使用中のインデックス  
  
-   参照するページ  
  
-   ディスクから読み取られたページ  
  
-   ディスクから preread ページ  
  
-   変更クリーン ページ  
  
-   変更のダーティ ページ  
  
-   検索時間  
  
-   最適化を妨げて属性  
  
#### <a name="new-time-based-threshold-registry-value-for-event-1644-logging"></a>ログのイベント 1644 用の新しい時間に基づくしきい値レジストリ値  
高コストと効率低下を招く検索結果のしきい値の値を指定するのではなく検索時間のしきい値を指定することができます。  かどうかはするが 50 ミリ秒を行ったすべての検索結果を記録する目的以上、指定 50 10 進]、[(フィールド エンジニア リング値を設定するには) に加えて 16 進数の 32 です。  
  
```  
Windows Registry Editor Version 5.00  
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Parameters]  
"Search Time Threshold (msecs)"=dword:00000032  
```  
  
#### <a name="comparison-of-the-old-and-new-event-id-1644"></a>古いと新しいイベント ID 1644 の比較  
古い  
  
![ディレクトリ サービスの更新プログラム](media/Directory-Services-component-updates/GTR_ADDS_Event1644_2012.gif)  
  
新機能  
  
![ディレクトリ サービスの更新プログラム](media/Directory-Services-component-updates/GTR_ADDS_Event1644_2012R2.gif)  
  
#### <a name="try-this-use-the-event-log-to-return-query-statistics"></a>イベント ログを使用してクエリ統計情報を返すを試してください。  
  
1.  次を繰り返して、Windows Server 2012 DC と Windows Server 2012 R2 の DC を対象とします。 各検索した後、2 つの Dc でイベント ID 1644s を確認します。  
  
2.  Regedit を使用して、時間ベースのしきい値を使用して、Windows Server 2012 R2 の DC と Windows Server 2012 DC の古いメソッドでイベント ID 1644 ログ記録を有効にします。  
  
3.  しきい値を超えていると、結果の上部に統計情報を確認するいくつかの LDAP 検索を実行します。  以前文書化されている LDAP クエリを使用し、同じの検索を繰り返します。  
  
4.  クエリ オプティマイザーことができないため、1 つまたは複数の属性のインデックスは作成されませんを最適化するために LDAP 検索を実行します。  
  
## <a name="BKMK_ADRepl"></a>Active Directory レプリケーション スループットの向上  
  
### <a name="overview"></a>概要  
AD レプリケーションでは、そのレプリケーション トランスポートの RPC を使用します。 既定では、RPC は、8 K 送信バッファーと 5 K パケット サイズを使用します。 これは、net、送信元のインスタンスは (約 15 K 相当のデータ) の 3 つのパケットを送信し、詳細を送信する前にラウンド トリップ ネットワークの待機します。 想定すると、3 ms ラウンドト リップ時間を最高のスループットになる、1 gbps または 10 Gbps のネットワーク上でも、40 mbps の周囲します。  
  
> [!NOTE]  
> -   この更新プログラムは、最大の AD レプリケーションのスループットが 40 mbps から約 600 Mbps に調整します。  
>   
>     -   ネットワークの数を削減する RPC 送信バッファーのサイズを増加しているラウンド トリップ  
> -   高速で最も顕著な影響があるネットワークの待機時間が長くします。  
  
この更新プログラムは、256 kb の 8 K から RPC 送信バッファーのサイズを変更することで約 600 Mbps に最大スループットを増加します。  この変更により、8 K より大きくなる TCP ウィンドウ サイズをラウンド トリップ ネットワークの数を削減します。  
  
> [!NOTE]  
> この動作を変更する構成可能な設定はありません。  
  
### <a name="additional-resources"></a>その他のリソース  
[Active Directory レプリケーション モデルのしくみ](https://technet.microsoft.com/library/cc772726(v=WS.10).aspx)  
  


