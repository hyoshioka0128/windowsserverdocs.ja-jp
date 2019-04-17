---
ms.assetid: b11f7a65-ec7b-4c11-8dc4-d7cabb54cd94
title: "Active Directory レプリケーションの問題のトラブルシューティング"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: eb93ea7cab297d70aa86b71bd5466004e47bfeaf
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshooting-active-directory-replication-problems"></a>Active Directory レプリケーションの問題のトラブルシューティング

>適用対象: Windows Server 2016、Windows Server 2012 R2、Windows Server 2012


Active Directory レプリケーションの問題は、いくつかのさまざまなソースを持つことができます。 たとえば、ドメイン ネーム システム (DNS) の問題、ネットワークの問題、またはセキュリティの問題ことができますすべてと、Active Directory レプリケーションが失敗します。 

このトピックの残りの部分は、ツールと一般的な Active Directory レプリケーション エラーを修正する方法について説明します。 実践的ラボを Active Directory レプリケーションの問題をトラブルシューティングする方法を示す、次を参照してください[TechNet バーチャル ラボ: Active Directory レプリケーション エラーのトラブルシューティング。](https://go.microsoft.com/?linkid=9844718)

次のサブトピックでは、現象、原因、および特定のレプリケーション エラーを解決する方法について説明します。
   
[レプリケーション残留オブジェクトの問題の修正 (イベント ID 1388、1988、2042)](https://technet.microsoft.com/library/cc949124.aspx)
  
[レプリケーションのセキュリティの問題を解決します。](https://technet.microsoft.com/library/cc949132.aspx)

[レプリケーション DNS 参照の問題の解決 (イベント ID 1925、2087、2088)](https://technet.microsoft.com/library/cc949133.aspx)
  
[レプリケーション接続の問題の解決 (イベント ID 1925)](https://technet.microsoft.com/library/cc949131.aspx)
  
[レプリケーション トポロジの問題の解決 (イベント ID 1311)](https://technet.microsoft.com/library/cc949129.aspx)
  
[ディレクトリ レプリケーションをサポートする DNS 機能を確認します。](https://technet.microsoft.com/library/dd728017.aspx)
  
[レプリケーション エラー 8614 Active Directory とレプリケートできませんこのサーバーをこのサーバーと最後のレプリケーション以来、時間が廃棄 (tombstone) の有効期間を超えているため](https://technet.microsoft.com/library/replication-error-8614-the-active-directory-cannot-replicate-with-this-server-because-the-time-since-the-last-replication-with-this-server-has-exceeded-the-tombstone-lifetime.aspx)
     
[レプリケーション エラー 8524 DSA 操作は DNS 参照エラーのため続行できません。](https://technet.microsoft.com/library/replication-error-8524-the-dsa-operation-is-unable-to-proceed-because-of-a-dns-lookup-failure.aspx)
   
[レプリケーション エラー 8456 または 8457 ソース |。移行先サーバーは現在拒否して複製要求](https://technet.microsoft.com/library/replication-error-8456-the-source-server-is-currently-rejecting-replication-requests-or-replication-error-8457-the-destination-server-is-currently-rejecting-replication-requests.aspx)
   
[レプリケーション エラー 8453。レプリケーション アクセスが拒否されました](https://technet.microsoft.com/library/replication-error-8453-replication-access-was-denied.aspx)
  
[レプリケーション エラー 8452 名前付けコンテキストは削除処理中または指定されたサーバーからレプリケートされていません](https://technet.microsoft.com/library/replication-error-8452-the-naming-context-is-in-the-process-of-being-removed-or-is-not-replicated-from-the-specified-server.aspx)
   
[レプリケーション エラー 5 アクセスが拒否されました](https://technet.microsoft.com/library/replication-error-5-access-is-denied.aspx)
  

      
      

  
[レプリケーション エラー-2146893022 対象のプリンシパル名が正しくありません。](https://technet.microsoft.com/library/replication-error-2146893022-the-target-principal-name-is-incorrect.aspx)
  

      
      

  
[レプリケーション エラー 1753。エンドポイント マッパーから使用できるエンドポイントは](https://technet.microsoft.com/library/replication-error-1753-there-are-no-more-endpoints-available-from-the-endpoint-mapper.aspx)
  

      
      

  
[レプリケーション エラー 1722。RPC サーバーことはできません。](https://technet.microsoft.com/library/replication-error-1722-the-rpc-server-is-unavailable.aspx)
  

      
      

  
[レプリケーション エラー 1396。ログオン エラー、対象のアカウント名が正しくありません。](https://technet.microsoft.com/library/replication-error-1396-logon-failure-the-target-account-name-is-incorrect.aspx)
  

      
      

  
[レプリケーション エラー 1256。リモート システムは、利用可能なではありません。](https://technet.microsoft.com/library/replication-error-1256-the-remote-system-is-not-available.aspx)
  

      
      

  
[再試行の後も、ハード _ ディスク、ディスクの操作にアクセス中にレプリケーション エラー 1127 に失敗しました](https://technet.microsoft.com/library/replication-error-1127-while-accessing-the-hard-disk-a-disk-operation-failed-even-after-retries.aspx)
  

      
      

  
[レプリケーション エラー 8451 レプリケーション操作には、データベース エラーが発生しました。](https://technet.microsoft.com/library/replication-error-8451-the-replication-operation-encountered-a-database-error.aspx)
  

      
      

  
[レプリケーション エラー 8606 属性が足りませんに付与されたオブジェクトを作成するには](https://technet.microsoft.com/library/replication-error-8606-insufficient-attributes-were-given-to-create-an-object.aspx)
  

## <a name="introduction-and-resources-for-troubleshooting-active-directory-replication"></a>概要と Active Directory レプリケーションのトラブルシューティングに関するリソース

入力方向または出力方向のレプリケーション エラーによりレプリケーション トポロジ、レプリケーション スケジュール、ドメイン コントローラー、ユーザー、コンピューター、パスワード、セキュリティ グループ、グループ メンバーシップ、およびドメイン コントローラー間で一貫性のあるグループ ポリシーを表す Active Directory のオブジェクトです。 Directory 不統一の原因とレプリケーション エラー運用障害や、操作のために接続しているドメイン コントローラーによって、矛盾した結果のいずれかが発生することができます、グループ ポリシーのアプリケーションを防ぐやアクセス コントロールのアクセス許可。 Active Directory ドメイン サービス (AD DS) は、ネットワーク接続、名前解決、認証と承認、ディレクトリ データベース、レプリケーション トポロジ、およびレプリケーション エンジンによって異なります。 レプリケーションの問題の根本原因がすぐにわかるできない場合は、多数考えられる原因の間で原因を特定する可能性の高い原因の体系的な削除が必要です。 

レプリケーションの監視し、エラーの診断に役立つ UI ベース ツールでは、次を参照してください。[Active Directory レプリケーションのステータス ツール](https://www.microsoft.com/download/details.aspx?id=30005)します。 また、[実践的なラボ](https://go.microsoft.com/?linkid=9844718)Active Directory レプリケーションの状態およびその他のツールを使用して、エラーのトラブルシューティングをする方法を示したします。 

Active Directory のトラブルシューティングを Repadmin ツールを使用する方法を説明する包括的なドキュメントはレプリケーションが利用可能です。参照してください[監視およびトラブルシューティング Active Directory レプリケーションを使用して Repadmin](https://go.microsoft.com/fwlink/?LinkId=122830)します。

Active Directory レプリケーションの動作方法については、次のテクニカル リファレンスを参照してください。


- [Active Directory レプリケーション モデルのテクニカル リファレンス](https://go.microsoft.com/fwlink/?LinkId=65958)
- [アクティブ ディレクター レプリケーション トポロジのテクニカル リファレンス](https://go.microsoft.com/fwlink/?LinkId=93578)

## <a name="event-and-tool-solution-recommendations"></a>イベントおよびツール ソリューションの推奨事項

理想的には、赤 (エラー) とディレクトリ サービス イベント ログ内の黄色 (警告) イベントには、移行元または移行先のドメイン コントローラーでレプリケーション エラーを原因となっている特定の制約がお勧めします。 イベント メッセージには、ソリューションのための手順が示すように場合、は、イベントで説明されている手順を実行します。 Repadmin ツールやその他の診断ツールもレプリケーション エラーの解決に役立つ情報が提供されます。 

Repadmin を使用して、レプリケーションの問題のトラブルシューティングの詳細については、次を参照してください。[監視およびトラブルシューティング Active Directory レプリケーションを使用して Repadmin](https://go.microsoft.com/fwlink/?LinkId=122830)します。

## <a name="ruling-out-intentional-disruptions-or-hardware-failures"></a>意図的なものが混乱したり、ハードウェア障害は除きます

あります意図的な中断が原因のレプリケーション エラーが発生します。 たとえば、Active Directory レプリケーションの問題をトラブルシューティングする際にルール意図的な接続の切断とハードウェアの障害またはアップグレードをまず。

### <a name="intentional-disconnections"></a>意図的な接続の切断

ステージングのサイトでビルドされており、最終的な実稼働サイト (リモート サイトに、ブランチ オフィスなど) では、その展開を待機している現在オフラインになっているドメイン コントローラーとのレプリケーションをしようとしているドメイン コントローラーによっては、レプリケーション エラーが報告されて場合、は、それらのレプリケーション エラーを考慮することができます。 ドメイン コントローラーがドメイン コントローラーが再接続するまで継続的なエラーが発生した場合、長期にわたってレプリケーション トポロジから分離することを回避するには、メンバー サーバーとして最初にこのようなコンピューターを追加して、メディア (IFM) のメソッドからのインストールを使用して、Active Directory ドメイン サービス (AD DS) をインストールするを検討します。 Ntdsutil コマンド ライン ツールを使用すると、リムーバブル メディア (CD、DVD、またはその他のメディア) に保存して出荷先のサイトにインストール メディアを作成します。 次に、レプリケーションを使用せず、サイトでドメイン コントローラーで AD DS をインストールするのにインストール メディアを使用できます。 

### <a name="hardware-failures-or-upgradestitle"></a>ハードウェアの障害またはアップグレード</title>

レプリケーションの問題がハードウェア障害 (たとえば、マザーボード、ディスク サブシステム、またはハード ドライブの障害など) の結果として発生した場合は、ハードウェアの問題を解決できるように、サーバーの所有者を通知します。

定期的なハードウェアのアップグレードでは、ドメイン コントローラー サービスを停止することもあります。 サーバーの所有者は、このような障害を事前に通信するための適切なシステムであることを確認します。

### <a name="firewall-configuration"></a>ファイアウォールの構成

既定では、Active Directory レプリケーションのリモート プロシージャ コール (Rpc) はポート 135 を RPC エンドポイント マッパー (RPCSS) を介して使用可能なポートを動的に発生します。 セキュリティが強化された Windows ファイアウォールとその他のファイアウォールは、レプリケーションを許可するように正しく構成することを確認します。 Active Directory レプリケーションおよびポートの設定のポートを指定する方法の詳細については、次を参照してください。[224196、Microsoft サポート技術情報の記事](https://go.microsoft.com/fwlink/?LinkId=22578)します。 

Active Directory のレプリケーションを使用するポートについては、次を参照してください。[Active Directory レプリケーションのツールと設定](https://go.microsoft.com/fwlink/?LinkId=123774)します。 

ファイアウォール経由での Active Directory レプリケーションの管理については、次を参照してください。[ファイアウォール経由での Active Directory レプリケーション](https://go.microsoft.com/fwlink/?LinkId=123775)します。

## <a name="responding-to-failure-of-an-outdated-server-running-windows-2000-server"></a>Windows 2000 Server を実行して、古いサーバーの障害への応答

Windows 2000 Server を実行するドメイン コントローラーが廃棄 (tombstone) の有効期間の日数よりも長いの失敗した場合、ソリューションは常に同じです。 

1. 企業ネットワークからサーバーをプライベート ネットワークに移動します。
2. 強制的に削除する Active Directory か、オペレーティング システムの再インストールします。
3. サーバー オブジェクトを復元できないように、Active Directory からサーバーのメタデータを削除します。 

ほとんどの Windows オペレーティング システムでサーバーのメタデータをクリーンアップするスクリプトを使用することができます。 このスクリプトの使用については、次を参照してください。[Active Directory ドメイン コントローラーの削除メタデータ](https://go.microsoft.com/fwlink/?LinkID=123599)します。 

既定では、削除された NTDS 設定オブジェクトは、14 日間の自動的に復元します。 そのため、サーバーのメタデータを削除しない場合 (Ntdsutil またはメタデータのクリーンアップを実行する前に説明したスクリプトを使用)、サーバーのメタデータがディレクトリで、発生するレプリケーション試行を求められます再開します。 この場合、エラーが不足しているドメイン コントローラーを複製することができない結果として永続的に記録されます。

## <a name="root-causes"></a>根本的原因

意図的な接続の切断やハードウェアの障害、古い Windows 2000 ドメイン コントローラー、除外する場合のレプリケーションの問題の残りの部分ほとんどの場合がある次の根本的原因の 1 つ。 


- ネットワーク接続: ネットワーク接続を使用できない可能性がありますまたはネットワークの設定が正しく構成されていません。
- 名前解決: DNS の構成の不備がレプリケーション エラーが原因で発生します。
- 認証と承認: ドメイン コントローラーがレプリケーション パートナーに接続するときに「アクセス拒否」エラーが発生する認証と承認の問題。
- ディレクトリ データベース (格納): ディレクトリ データベースがレプリケーション タイムアウトに十分に速くトランザクションを処理できない可能性があります。
- レプリケーション エンジン: サイト間レプリケーション スケジュールが短すぎる場合は、レプリケーション キューは、出力方向のレプリケーション スケジュールで必要な時間で処理するには大きすぎる可能性があります。 ここでは、いくつかの変更のレプリケーションが停止している indefinitelypotentially をすることができますを廃棄 (tombstone) の有効期間を超えることを十分に長いです。
- レプリケーション トポロジ: ドメイン コントローラーでは、実際のワイド エリア ネットワーク (WAN) 接続または仮想プライベート ネットワーク (VPN) 接続にマップする AD DS のサイト間のリンクがあります。 [ネットワークのトポロジを実際のサイトでサポートされていない AD DS レプリケーション トポロジにオブジェクトを作成する場合、正しく構成されていないトポロジを必要とするレプリケーションは失敗します。

## <a name="general-approach-to-fixing-problems"></a>問題を解決する一般的な作成方法

レプリケーションの問題を解決するのには、次の一般的な方法を使用します。 


1. 毎日、レプリケーションの正常性を監視するか、毎日のレプリケーション ステータスを取得する Repadmin.exe を使用します。
2. イベント メッセージは、このガイドで説明されているメソッドを使用して、適切なタイミングで、報告されたエラーを解決しようとします。 ソフトウェアは、問題を引き起こしている可能性がある場合、は、その他のソリューションを続行する前に、ソフトウェアをアンインストールします。
3. 既知の方法でレプリケーションが失敗する原因になっている問題を解決できない場合、サーバーから AD DS を削除し、AD DS を再インストールします。 AD DS を再インストールの詳細については、次を参照してください。[Decommissioning a Domain Controller](https://go.microsoft.com/fwlink/?LinkId=128290)します。
4. AD DS を削除できない通常、サーバーがネットワークに接続している場合は、問題を解決するのには、次の方法のいずれかを使用します。
 

    - AD DS の削除でディレクトリ サービス復元モード (DSRM)、サーバーのメタデータのクリーンアップを強制し、AD DS を再インストールします。
    - オペレーティング システムを再インストールし、ドメイン コントローラーを再構築します。

AD DS の削除を強制の詳細については、次を参照してください。[ドメイン コントローラーの強制的な削除](https://go.microsoft.com/fwlink/?LinkId=128291)します。

## <a name="using-repadmin-to-retrieve-replication-statustitle"></a>Repadmin を使用して、レプリケーションの状態を取得するには</title>

レプリケーションの状態は、ディレクトリ サービスの状態を評価するための重要な方法です。 エラーなし、レプリケーションが動作している場合は、オンラインであるドメイン コントローラーがわかります。 また、次のシステムとサービスが動作しているがわかっています。


- DNS インフラストラクチャ
- Kerberos 認証プロトコル
- Windows タイム サービス (W32time)
- リモート プロシージャ コール (RPC)
- ネットワーク接続

Repadmin を使用すると、フォレスト内のすべてのドメイン コントローラのレプリケーションの状態を評価するコマンドを実行して毎日のレプリケーション ステータスを監視できます。 手順では、Microsoft Excel とレプリケーション エラーのフィルターで開くことができる .csv ファイルを生成します。

次の手順を使用すると、フォレスト内のすべてのドメイン コントローラーのレプリケーションの状態を取得します。 
      
要件
      
メンバーシップ**Enterprise Admins**、相当するものでは、この手順を完了するために必要な最低限またはします。 

ツール: 


- Repadmin.exe 
- Excel (Office)

### <a name="to-generate-a-repadmin-showrepl-spreadsheet-for-domain-controllers"></a>Repadmin を生成する /showrepl ドメイン コントローラーのワークシート



1. 管理者としてコマンド プロンプトを開きます。[スタート] メニュー コマンド プロンプトで、右クリックし、[管理者として実行] をクリックします。 ユーザー アカウント制御] ダイアログ ボックスが表示されたら、必要な場合、Enterprise Admins の資格情報を提供し、[続行] をクリックします。 
2. コマンド プロンプトで、次のコマンドを入力し、Enter キーを押します。`repadmin /showrepl * /csv &gt;showrepl.csv`
3. Excel を開きます。
4. Office ボタンをクリックして、[開く] をクリックして、showrepl.csv に移動およびし、[開く] をクリックします。
5. 非表示にするか、列 A とトランスポートの種類] 列を次のように削除します。
6. 非表示または削除する列を選択します。
      

    - 列を非表示に列を右クリックし、[非表示にする] をクリックします。
    - 列を削除するには、選択した列を右クリックし、[削除] をクリックします。
7. 列見出しの下にある 1 行を選択します。 [表示] タブで、ウィンドウ枠の固定をクリックし、上の固定行をクリックします。
8. スプレッドシート全体を選択します。 [データ] タブには、フィルターをクリックします。
9. 前回成功] 列で下向きの矢印をクリックし、昇順で並べ替え] をクリックします。
10. ソース DC] 列でのカスタム フィルターをクリックしてフィルター下向き矢印をクリックして、テキスト フィルター、] をポイントします。
11. オート] ダイアログ ボックスで [表示の行をクリックして含まれていません。 隣接するテキスト ボックスで、次のように入力します。<userInput>del</userInput>ビューからの結果を回避するためのドメイン コントローラーを削除します。
12. 手順 11、前回の障害の列は、使用する値が等しくなり、その値 0 を入力していないを繰り返します。
13. レプリケーション エラーを解決します。

フォレスト内の各ドメイン コントローラのスプレッドシートは、ソース レプリケーション パートナーを示しています、時間、レプリケーションが最後に発生したと名前付けコンテキスト (ディレクトリ パーティション) ごとの最後のレプリケーション エラーが発生した時刻。 オート Excel で使用すると、障害が発生しただけのドメイン コントローラーは、少なくともまたはほとんどの現在のドメイン コントローラーのみのドメイン コントローラーを操作するためのレプリケーションの正常性を表示し、レプリケーション パートナーが正常にレプリケートしていることを確認できます。

## <a name="replication-problems-and-resolutions"></a>レプリケーションの問題と解決策
    
レプリケーションの問題は、アプリケーションまたはサービスは、操作を試みるときに発生するさまざまなエラー メッセージで、イベント メッセージで報告されます。 理想的には、これらのメッセージは、監視のアプリケーションまたはレプリケーションの状態を取得するときに収集されます。

ほとんどのレプリケーションの問題は、ディレクトリ サービス イベント ログに記録されているイベント メッセージで識別されます。 出力にエラー メッセージの形式でのレプリケーションの問題を特定することがありますも、<system>repadmin/showrepl</system>コマンド。 

### <a name="repadmin-showrepl-error-messages-that-indicate-replication-problems"></a>Repadmin /showrepl レプリケーションの問題を示すエラー メッセージ

Active Directory レプリケーションの問題を識別するには、使用して、<system>repadmin/showrepl</system>コマンドを前のセクションで説明されているとします。 次の表は、根本的原因のエラーと、エラーの解決策を提供するトピックへのリンクと共に、このコマンドを生成するエラー メッセージを示します。


|Repadmin エラー|根本原因|解決策|
| --- | --- | --- |
|この最後のレプリケーションの後にサーバーが廃棄 (tombstone) の有効期間を超えました。|ドメイン コントローラーには、削除の廃棄されたをされているに十分な複製され、AD DS からガベージ コレクションは、長い名前付きのソース ドメイン コントローラーで入力方向のレプリケーションに失敗しました。|Event ID 2042: It has been too long since this machine replicated|
|受信近隣のありません。|Repadmin によって生成される出力の「近隣ノードの受信」セクション項目が表示されない場合 /showrepl、ドメイン コントローラー別のドメイン コントローラのレプリケーション リンクを確立できませんでした。|レプリケーション接続の問題の解決 (イベント ID 1925)| 
|アクセスが拒否されます。|次の 2 つのドメイン コントローラー間でレプリケーション リンクが存在しますが、認証エラーの結果としてレプリケーションは正しく実行できません。|レプリケーションのセキュリティの問題を解決します。| 
|前回の < 日付 - 時間 > で、「対象のアカウント名が正しくありません」で失敗しました|この問題は、接続、DNS、または認証の問題に関連することができます。 DNS エラーの場合は、ので、ローカル ドメイン コントローラがグローバル一意識別子 (GUID) で解決できませんでした-ベースのレプリケーション パートナーの DNS 名。|レプリケーション DNS 参照 (イベント ID 1925、2087、2088) の問題の修正のレプリケーション セキュリティの問題の解決 (イベント ID 1925) レプリケーション接続の問題を解決します。| 
|LDAP エラー 49 です。|ドメイン コントローラー コンピューター アカウントが同期されませんキー配布センター (KDC) で。|レプリケーションのセキュリティの問題を解決します。| 
|ローカル ホストへの LDAP 接続を開くことができません。|管理ツールは、AD DS に接続できませんでした。|レプリケーション DNS 参照の問題の解決 (イベント ID 1925、2087、2088)| 
|Active Directory レプリケーションが切断されました。|入力方向のレプリケーションの進行状況は、repadmin/sync コマンドを使用して手動で生成された要求などの優先順位の高いレプリケーション要求によって中断されました。|レプリケーションが完了するまで待ちます。 この情報メッセージは、通常の動作を示します。| 
|レプリケーションが投稿した、待機しています。| ドメイン コントローラーは複製要求を送信し、応答を待機しています。 レプリケーションでは、このソースから進行中です。|レプリケーションが完了するまで待ちます。 この情報メッセージは、通常の動作を示します。| 

次の表は、Active Directory の問題と、問題に関する解決策を提供するトピックへのリンクのレプリケーションでは、ルートと共にが原因で問題を示す可能性がある一般的なイベントを示します。 

|イベント ID とソース|根本原因|解決策|
| --- | --- | --- | 
|1311 NTDS KCC|AD DS のレプリケーションの構成情報は、ネットワークの物理トポロジを正確に反映されません。|レプリケーション トポロジの問題の解決 (イベント ID 1311)| 
|1388 NTDS レプリケーション|厳密なレプリケーションの整合性は効果であり、残留オブジェクトがドメイン コントローラーにレプリケートされました。|レプリケーション残留オブジェクトの問題の修正 (イベント ID 1388、1988、2042)|
|1925 NTDS KCC|書き込み可能なディレクトリ パーティションのレプリケーション リンクを確立するために失敗しました。 このイベントは、エラーに応じて、さまざまな原因を持つことができます。| レプリケーション接続 (イベント ID 1925) の問題の修正レプリケーション DNS 参照の問題の解決 (イベント ID 1925、2087、2088)| 
|1988 NTDS レプリケーション|ローカル ドメイン コントローラーが削除されているし、既にガーベジ コレクトために、ローカル ドメイン コントローラーに存在しないのソース ドメイン コントローラーからオブジェクトをレプリケートしようとしています。 この状況が解決されるまで、レプリケーションはこのパートナーの場合は、このディレクトリ パーティションの続行できません。|レプリケーション残留オブジェクトの問題の修正 (イベント ID 1388、1988、2042)|
|2042 NTDS レプリケーション|レプリケーションが発生していないパートナーと廃棄 (tombstone) の有効期間、およびレプリケーションを続行できません。|レプリケーション残留オブジェクトの問題の修正 (イベント ID 1388、1988、2042)| 
|2087 NTDS レプリケーション|AD DS は、IP アドレス、およびレプリケーションに失敗したにソース ドメイン コントローラーの DNS ホスト名を解決できませんでした。|レプリケーション DNS 参照の問題の解決 (イベント ID 1925、2087、2088)| 
|2088 NTDS レプリケーション |AD DS は、IP アドレスはレプリケーションが成功したにソース ドメイン コントローラーの DNS ホスト名を解決できませんでした。|レプリケーション DNS 参照の問題の解決 (イベント ID 1925、2087、2088)|
|5805 net Logon|コンピューター アカウントは、通常、同じコンピューター名のいずれかの複数のインスタンスまたはすべてのドメイン コントローラーにレプリケートされていないコンピューター名に発生する認証を行いに失敗しました。|レプリケーションのセキュリティの問題を解決します。| 

レプリケーションの概念の詳細については、次を参照してください。[Active Directory のレプリケーション テクノロジ](https://go.microsoft.com/fwlink/?LinkId=41950)します。
  
