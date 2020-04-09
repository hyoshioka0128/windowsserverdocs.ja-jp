---
ms.assetid: 3acaa977-ed63-4e38-ac81-229908c47208
title: LDAP サーバー Cookie の処理方法
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: f90f53763e7a31ffed1fd820061910742e5cf98a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823235"
---
# <a name="how-ldap-server-cookies-are-handled"></a>LDAP サーバー Cookie の処理方法

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

LDAP では、一部のクエリによって膨大な結果セットが返されます。 このようなクエリにより、Windows Server にいくつかの問題が発生します。  
  
この膨大な結果セットの収集および構築は大変な作業です。 属性の多くを内部表現から LDAP ネットワーク表現に変換する必要があります。 多くの属性では、LDAP 応答フレームで、内部の (大抵の場合バイナリ) 形式からテキスト ベースの UTF-8 形式への変換が必要になります。  
  
別の問題として、何万個ものオブジェクトを持つ結果セットは、簡単に数百メガバイトの巨大なサイズになる点が挙げられます。 そのため、多くの仮想アドレス空間が必要になります。また、TCP セッションが転送中に停止した場合、すべての作業が失われるため、ネットワークでの転送にも問題があります。  
  
これらの容量およびロジスティックの問題により、Microsoft LDAP 開発者は、"ページングクエリ" と呼ばれる LDAP 拡張機能を作成するようになりました。 LDAP コントロールを実装し、1 つの膨大なクエリを大量の小さな結果セットに分割します。 [RFC 2696](http://www.ietf.org/rfc/rfc2696)として RFC 標準になりました。  
  
## <a name="cookie-handling-on-client"></a>クライアント上の Cookie 処理  
ページングクエリメソッドは、クライアントまたは[LDAP ポリシー](https://support.microsoft.com/kb/315071/en-us) ("maxpagesize") のいずれかで設定されたページサイズを使用します。 クライアントは、LDAP コントロールを送信してページングを常に有効にする必要があります。  

  
多くの結果を照会するクエリを使用する場合、ある時点でオブジェクトの最大許容数に到達します。 LDAP サーバーは、応答メッセージをパッケージ化し、後で検索を継続するために必要な情報を含む Cookie を追加します。  
  
クライアント アプリケーションは、不透明な BLOB として Cookie を処理する必要があります。 応答内のオブジェクト数を取得し、Cookie の有無に基づいて検索を継続できます。クライアントは、ベース オブジェクトやフィルターなど、同じパラメーターのクエリを LDAP サーバーに再度送信して検索を継続し、前の応答で返された Cookie 値を追加します。  
  
オブジェクトの数がページに収まらない場合、LDAP クエリは完了し、応答にページ cookie は含まれません。 サーバーから Cookie が返されない場合、クライアントはページング検索が正常に完了したと見なす必要があります。  
  
サーバーからエラーが返された場合、クライアントはページング検索が失敗したと見なす必要があります。 検索を再実行すると、検索が最初のページから再度開始されます。  
  
## <a name="server-side-cookie-handling"></a>サーバー側の Cookie 処理  
Windows Server はクライアントに Cookie を返し、Cookie に関連する情報をサーバー上に格納することがあります。 この情報はサーバー上のキャッシュに格納され、一定の制限があります。  
  
この場合、サーバーによってクライアントに送信された Cookie は、サーバー上のキャッシュから情報を参照する場合にもサーバーによって使用されます。 クライアントがページング検索を継続する場合、Windows Server は、サーバーの Cookie キャッシュのあらゆる関連情報に加えて、クライアントの Cookie も使用して検索を継続します。 何らかの理由でサーバーがサーバー キャッシュから関連 Cookie 情報を見つけられない場合、検索は中止され、クライアントにエラーが返されます。  
  
## <a name="how-the-cookie-pool-is-managed"></a>Cookie プールの管理方法  
当然のことながら、LDAP サーバーは一度に複数のクライアントにサービスを提供し、一度に複数のクライアントが、サーバーの Cookie キャッシュを使用する必要のあるクエリを起動できます。そのため、Windows Server の実装では、Cookie プールの使用状況が追跡され、制限が適用されるため、Cookie プールで大量のリソースが消費されることはありません。 制限は、LDAP ポリシーの次の設定を使用して管理者が設定できます。 既定値および説明は次のとおりです。  
  
**MinResultSets: 4**  
  
サーバーの Cookie キャッシュ内のエントリが MinResultSets よりも少ない場合、LDAP サーバーは、後述の最大プール サイズを確認することはありません。  
  
**MaxResultSetSize: 262、144 バイト**  
  
サーバー上の Cookie キャッシュの合計サイズが MaxResultSetSize の最大バイト数を超えてはいけません。 超える場合は、プールが MaxResultSetSize のバイト数より小さくなるか、プール内の Cookie が MinResultSets より少なくなるまで、最も古い Cookie から削除されます。 つまり、既定の設定を使用する場合、格納されている Cookie が 3 つしかない場合、LDAP サーバーは 450 KB のプールを問題ないと見なすことを意味しています。  
  
**MaxResultSetsPerConn: 10**  
  
LDAP サーバーは、プール内の 1 つの LDAP 接続に対して、MaxResultSetsPerConn よりも少ない数の Cookie を許可します。  
  
## <a name="handling-deleted-cookies"></a>削除された Cookie の処理  
LDAP サーバーのキャッシュから Cookie 情報を削除しても、すべての場合でアプリケーションのエラーが直ちに発生するわけではありません。 アプリケーションは最初からページング検索を再度開始し、別の試行で完了できます。 一部のアプリケーションにはこのような再試行メカニズムがあり、堅牢性が向上しています。  
  
一部のアプリケーションはページ検索を実行し、完了しないこともあります。 これにより、LDAP サーバーの Cookie キャッシュにエントリが作成される場合があり、セクション 4 のメカニズムで処理されます。 これは、アクティブな LDAP 検索のためのサーバーでメモリを解放するために必要不可欠です。  
  
サーバー上でこのような Cookie が削除され、クライアントがこの Cookie のハンドルを使用して検索を継続すると何が発生するでしょうか。LDAP サーバーは、サーバーの Cookie キャッシュ内に Cookie を見つけられず、クエリに対してエラーを返します。エラー応答は次のようなものになります。  
  
```  
00000057: LdapErr: DSID-xxxxxxxx, comment: Error processing control, data 0, v1db1  
```  
  
> [!NOTE]  
> "DSID" の背後にある16進値は、LDAP サーバーバイナリのビルドバージョンによって異なります。  
  
## <a name="reporting-on-the-cookie-pool"></a>Cookie プールのレポート機能  
LDAP サーバーには、 [NTDS 診断キー](https://support.microsoft.com/kb/314980/en-us)のカテゴリ "16 LDAP インターフェイス" を使用してイベントをログに記録する機能があります。 このカテゴリを "2" に設定すると、次のイベントを取得できます。  
  
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
  
このイベントは、格納された Cookie が削除されたことを通知します。 これは、クライアントで LDAP のエラーが発生したのではなく、LDAP サーバーがキャッシュの管理の制限に達したことのみを意味しています。  場合によっては、LDAP クライアントがページング検索を破棄すると、エラーが表示されないことがあります。  
  
## <a name="monitoring-the-cookie-pool"></a>Cookie プールの監視  
ドメインで LDAP 検索エラーが発生したことがない場合は、LDAP サーバーのページ検索 Cookie プールを監視する必要がない可能性があります。 使用する環境で LDAP ページ検索に関連するエラーが確認された場合は、Cookie プールの管理者の制限に問題がある可能性があります。  
  
イベント 2898 および 2899 は、LDAP サーバーが管理者の制限に達したかどうかを確認する唯一の方法です。 前述の制御処理エラーが原因で LDAP クエリにエラーが発生した場合は、取得するイベントに応じて、セクション 4 に記載された 1 つ以上の LDAP ポリシー設定の制限を増やしてみる必要があります。  
  
DC や LDAP サーバーにイベント 2898 が表示された場合は、MaxResultSetsPerConn を 25 に設定することをお勧めします。 1 つの LDAP 接続で 25 を超える並列ページング検索は普通ではありません。 イベント 2898 が引き続き表示される場合は、エラーが発生した LDAP クライアント アプリケーションを調査してみてください。 何らかの理由で余分なページング検索結果の取得から抜け出せなくなり、Cookie が保留のまま、新しいクエリが再度開始された可能性があります。 そのため、ある時点で目的に応じた十分な Cookie がアプリケーションにあるかを確認し、MaxResultSetsPerConn に 25 よりも大きな値を設定することもできます。ドメイン コントローラーにイベント 2899 が記録されている場合、計画は異なります。 DC および LDAP サーバーが、十分なメモリ (数 GB の空きメモリ) を搭載したマシンで稼動する場合、LDAP サーバーの MaxResultsetSize を 250 MB 以上に設定することをお勧めします。 この制限は、非常に大規模なディレクトリであっても、大量の LDAP ページ検索に十分に対応できます。  
  
250 MB 以上のプールでイベント 2899 が変わらず表示される場合は、多くのクライアントに非常に大量のオブジェクトが返され、非常に高い頻度でクエリを実行している可能性があります。 [Active Directory のデータ コレクター セット](https://blogs.technet.com/b/askds/archive/2010/06/08/son-of-spa-ad-data-collector-sets-in-win2008-and-beyond.aspx) を使用して収集できるデータは、LDAP サーバーを常にビジー状態にする、反復ページング クエリを検索するのに役立ちます。 これらのクエリはすべて、使用されたページのサイズに一致する "返されたエントリ" が多数表示されます。  
  
可能であれば、アプリケーションの設計を確認し、頻度が低く、データ量が少なく、このデータを照会するクライアントインスタンスの数が少ない別のアプローチを実装する必要があります。ソースコードにアクセスできるアプリケーションの場合、[効率的な Ad 対応アプリケーションを作成](https://msdn.microsoft.com/library/ms808539.aspx)するためのこのガイドは、アプリケーションが ad にアクセスするための最適な方法を理解するのに役立ちます。  
  
クエリの動作を変更できない場合は、必要な名前付けコンテキストのレプリケートされたインスタンスをさらに追加し、クライアントを再配布し、最終的に個々の LDAP サーバーの負荷を軽減する方法もあります。  
  


