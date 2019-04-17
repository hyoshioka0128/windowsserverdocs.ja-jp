---
ms.assetid: 3acaa977-ed63-4e38-ac81-229908c47208
title: "LDAP サーバー Cookie の処理方法"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 89369cb1e52a315520062ca5ecc96b66ac3e2bfc
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="how-ldap-server-cookies-are-handled"></a>LDAP サーバー Cookie の処理方法

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

LDAP では、大規模な結果にいくつかのクエリ結果に設定します。 このようなクエリでは、いくつかの問題を Windows Server に対して引き起こすおそれします。  
  
収集および構築これら膨大な結果セットは、重要な作業です。 属性の多くを内部表現から LDAP ネットワーク表現に変換する必要があります。 多くの属性内部の多くの場合バイナリ形式からの変換は、LDAP 応答フレーム内のテキスト ベースの utf-8 形式に発生する必要があります。  
  
別の課題は、非常に重要になるオブジェクトに簡単に数百の巨大な数万件の持つ結果セットはことです。 そのため、必要な多くの仮想アドレス空間ともネットワーク経由で転送問題があるように、すべての作業が失われた TCP セッションが転送中に分割する場合。  
  
この容量および運用上の問題を引き起こしていた Microsoft LDAP の開発者「ページング クエリ」と呼ばれる LDAP 拡張機能を作成します。 1 つの膨大なクエリを小さな結果セットのチャンクに分割する LDAP コントロールを実装します。 として RFC 標準になりました[RFC 2696](http://www.ietf.org/rfc/rfc2696)します。  
  
## <a name="cookie-handling-on-client"></a>クライアント上の cookie 処理  
ページング クエリ メソッドはクライアントによってまたはいずれかの設定ページ サイズを使用して、 [LDAP ポリシー](https://support.microsoft.com/kb/315071/en-us) ("MaxPageSize")。 クライアントは、常に、LDAP コントロールを送信してページングを有効にする必要があります。  

  
いる場合は多くの結果のクエリで、ある時点で許可されているオブジェクトの最大数に達しています。 LDAP サーバーは、応答メッセージをパッケージ化し、後で検索を継続する必要がある情報を含む、cookie を追加します。  
  
クライアント アプリケーションは、不透明な blob として cookie を処理する必要があります。 応答内のオブジェクト数を取得でき、cookie の有無に基づいて検索を継続することができます。クライアントは、ベース オブジェクトやフィルターなど、同じパラメーターで再度 LDAP サーバーにクエリを送信して検索を継続し、前の応答で返された cookie 値が含まれています。  
  
オブジェクトの数がページを満たさない場合、は、LDAP クエリが完了し、応答にページ cookie が含まれていません。 サーバーによって cookie が返されない場合、クライアントはページング検索が正常に完了を検討してください必要があります。  
  
サーバーでエラーが返された場合、クライアントにする必要がありますはページング検索が失敗する検討してください。 検索を再試行すると、最初のページから検索が再起動されます。  
  
## <a name="server-side-cookie-handling"></a>サーバー側の Cookie 処理  
Windows Server では、クライアントに cookie を返しし、ことがあります、サーバー上の cookie に関連する情報を格納します。 この情報は、キャッシュ内のサーバーに保存され、特定の制限の対象は。  
  
ここでは、サーバー上のキャッシュから情報を検索サーバーによってクライアントに送信された cookie もサーバーによって使用します。 クライアントはページング検索が引き続き発生するときに、Windows Server は使用、クライアントの cookie と関連情報については、サーバーの cookie キャッシュから検索を続行します。 場合は、サーバーは、何らかの理由によりサーバー キャッシュから関連 cookie 情報を見つけることができませんは、検索は中止され、クライアントにエラーが返されます。  
  
## <a name="how-the-cookie-pool-is-managed"></a>Cookie プールを管理する方法  
当然ながら、LDAP サーバーが、一度に 1 つ以上のクライアントを提供していると、一度に 1 つ以上もクライアントがサーバーの cookie キャッシュの使用を要求するクエリを起動できます。したがって、Windows Server の実装が、cookie プールの使用率の追跡、cookie プールが多すぎるリソースが実行されないように制限が所定の位置に配置されます。 制限は、LDAP ポリシーで、次の設定を使用して、管理者が設定できます。 既定値および説明のとおり。  
  
**MinResultSets: 4**  
  
LDAP サーバーはしない見て、後述の最大プール サイズ サーバーの cookie キャッシュ内のエントリを MinResultSets よりも少ないリソースを使用する必要がある場合。  
  
**MaxResultSetSize: 262、144 バイト数**  
  
サーバー上の合計の cookie キャッシュ サイズが MaxResultSetSize の最大値 (バイト単位) を超えない必要があります。 場合は、プールが MaxResultSetSize のバイト数よりも小さいか、まで MinResultSets cookie よりも少ないリソース プール内から、最も古い cookie は削除されます。 これで既定の設定を使用して、LDAP サーバーは、考慮するのみ保存されている 3 つの cookie がある場合は、[ok] 450 KB のプールを意味します。  
  
**MaxResultSetsPerConn: 10**  
  
LDAP サーバーよりも 1 つの LDAP 接続プール内の MaxResultSetsPerConn cookie できます。  
  
## <a name="handling-deleted-cookies"></a>削除された Cookie の処理  
すぐにすべてのケースで、アプリケーションのエラーは、LDAP サーバーのキャッシュから cookie 情報の削除が行われません。 アプリケーションは、スタート画面からページング検索を再起動し、別の試行で実行し、完了可能性があります。 一部のアプリケーションでは、この種の堅牢性を追加する再試行メカニズムがあります。  
  
一部のアプリケーションは、ページ検索を通過し、完了しない可能性があります。 これは、可能性がありますをそのまま使用 LDAP サーバー内のエントリの cookie キャッシュは、セクション 4 メカニズムによって処理されます。 これは、アクティブな LDAP 検索は、サーバーのメモリを解放するうえで不可欠です。  
  
サーバーでこのような cookie が削除され、クライアントがこの cookie のハンドルを検索を継続なりますか。LDAP サーバーは、cookie、サーバーの cookie キャッシュを見つけてクエリにエラーが返されますが、エラー応答をようになります。  
  
```  
00000057: LdapErr: DSID-xxxxxxxx, comment: Error processing control, data 0, v1db1  
```  
  
> [!NOTE]  
> "Dsid"16 進数の値は、LDAP サーバー バイナリのビルド バージョンによって異なります。  
  
## <a name="reporting-on-the-cookie-pool"></a>Cookie プールのレポート  
LDAP サーバーが、ログオン イベント カテゴリ「16 Ldap インターフェイス」を使用する機能、 [NTDS 診断キー](https://support.microsoft.com/kb/314980/en-us)します。 このカテゴリを「2」を設定する場合は、次のイベントを取得できます。  
  
```  
Log Name:      Directory Service  
Source:        Microsoft-Windows-ActiveDirectory_DomainService  
Event ID:      2898  
Task Category: LDAP Interface  
Level:         Information  
Description:  
Internal event: The LDAP server has reached the limit of the number of Result Sets it will maintain for a single connection.  A stored Result Set will be discarded.  This will result in a client being unable to continue a paged LDAP search.  
Maximum number of Result Sets allowed per LDAP connection:  
10  
Current number of Result Sets for this LDAP connection:  
11  
  
User Action  
The client should consider a more efficient search filter.  The limit for Maximum Result Sets per Connection may also be increased.  
  
```  
  
```  
Log Name:      Directory Service  
Source:        Microsoft-Windows-ActiveDirectory_DomainService  
Event ID:      2899  
Task Category: LDAP Interface  
Level:         Information  
Description:  
Internal event: The LDAP server has exceeded the limit of the LDAP Maximum Result Set Size. A stored Result Set will be discarded.  This will result in a client being unable to continue a paged LDAP search.   
  
Number of result sets currently stored:   
4   
Current Result Set Size:   
263504   
Maximum Result Set Size:   
262144   
Size of single Result Set being discarded:   
40876   
User Action   
The client should consider a more efficient search filter.  The limit for Maximum Result Set Size may also be increased.  
  
```  
  
イベントは、格納された cookie が削除されたことを通知します。 クライアントが、LDAP エラー、のみ、LDAP サーバーが、キャッシュの管理の制限に達したことを確認するには限りません。  場合によっては、LDAP クライアントがページング検索を破棄がある可能性があり、というエラーが表示されません。  
  
## <a name="monitoring-the-cookie-pool"></a>Cookie プールの監視  
場合は、ドメインで LDAP 検索エラーが発生することはありません、LDAP サーバー ページ検索 cookie プールを監視する必要があることはありません。 LDAP ページ検索に関連するエラー環境内で確認された場合は、cookie プールの管理者の制限に問題があります。  
  
イベント 2898 および 2899 は、LDAP サーバー管理者の制限に達したことを確認する唯一の方法です。 上記のエラーを処理するコントロールのために LDAP クエリにエラーが発生した場合、1 つまたは複数のセクション 4、取得するイベントに示されている LDAP ポリシー設定の制限を増やしてを見てください。  
  
DC や LDAP サーバーにイベント 2898 が発生した場合は、MaxResultSetsPerConn を 25 に設定するお勧めします。 1 つの LDAP 接続で 25 台を超えるの並列ページング検索は、通常ではありません。 イベント 2898 が解決されない場合は、LDAP クライアント アプリケーションで、エラーが発生するを調査してください。 何らかの理由でなページング検索結果の取得から抜け出せなく、cookie が保留のまま、新しいクエリが再起動された可能性になります。 ようにことを認識するかどうか、アプリケーションはある時点で十分な cookie、目的のためのイベント 2899 が、ドメイン コント ローラーにログオンしているときに 25 よりも MaxResultSetsPerConn の値を増やすことも、さまざまなプランになります。 DC や LDAP サーバーは、十分なメモリ (数 Gb の空きメモリ) を搭載したマシンで実行している場合をお勧めする LDAP サーバーに、MaxResultsetSize を設定する > 250 mb です。 この制限は非常に大規模なディレクトリ上でも LDAP ページ検索の大きなボリュームに対応するために十分です。  
  
250 MB 以上のプールでイベント 2899 が、返されたオブジェクト数が非常に高いで多数のクライアントを発生する可能性がありますが表示される場合は、非常に頻繁な方法で照会されます。 使用して収集したデータ、 [Active Directory データ コレクター セット](http://blogs.technet.com/b/askds/archive/2010/06/08/son-of-spa-ad-data-collector-sets-in-win2008-and-beyond.aspx)反復ページング クエリ、LDAP サーバーを見つけるに役立ちますビジー状態のことができます。 これらのクエリは、すべて使用するページのサイズに一致する「エントリが返される」の数で表示されます。  
  
可能であれば、アプリケーションの設計を確認し、頻度、データ ボリュームやこのデータを照会するクライアント インスタンスを別のアプローチを実装する必要があります。ソース コードへのアクセスには、このガイドのあるアプリケーションが発生した場合[効率的な AD-Enabled アプリケーションを作成する](https://msdn.microsoft.com/en-us/library/ms808539.aspx)アプリケーションが AD にアクセスするための最適な方法を理解するのに役立ちます。  
  
クエリの動作を変更できない場合 1 つの方法がよりレプリケートされたインスタンスのために必要な名前付けコンテキストと、クライアントを再配布して、最終的に、各 LDAP サーバーの負荷を軽減も追加します。  
  


