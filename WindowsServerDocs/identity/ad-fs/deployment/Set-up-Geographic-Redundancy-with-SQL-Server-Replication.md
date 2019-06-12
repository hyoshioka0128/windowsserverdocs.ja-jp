---
title: 地理的冗長化を SQL Server レプリケーションのセットアップ
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: active-directory-federation-services
ms.author: billmath
ms.assetId: 7b9f9a4f-888c-4358-bacd-3237661b1935
ms.openlocfilehash: 00880d06835fad08538f634fdf2868146fc23b1a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442919"
---
# <a name="setup-geographic-redundancy-with-sql-server-replication"></a>地理的冗長化を SQL Server レプリケーションのセットアップ


> [!IMPORTANT]  
> AD FS ファームを作成して構成データを格納する SQL Server を使用する場合は、SQL Server 2008 以降を使用することができます。
  
AD FS 構成データベースとして SQL Server を使用する場合は、geo を設定することができます\-SQL Server レプリケーションを使用して、AD FS ファームの冗長性。 Geo\-アプリケーションは別に 1 つのサイトから切り替えることができるように、冗長性が地理的に離れた 2 つのサイト間でデータをレプリケートします。 これにより、1 つのサイトの障害には、することができます使用可能なすべての構成データ、2 つ目のサイトで。 詳細については、「SQL Server の地理的冗長性セクション」を参照してください[フェデレーション サーバー ファームを使用して SQL Server](../design/Federation-Server-Farm-Using-SQL-Server.md)します。  
  
## <a name="prerequisites"></a>前提条件  
インストールし、SQL server ファームを構成します。 詳細については、次を参照してください。 [ https://technet.microsoft.com/evalcenter/hh225126.aspx](https://technet.microsoft.com/evalcenter/hh225126.aspx)します。 最初の SQL Server で、SQL Server エージェント サービスが実行されているかどうかを確認し、自動開始に設定します。  
  
## <a name="create-the-second-replica-sql-server-for-geo-redundancy"></a>2 つ目の作成\(レプリカ\)geo の SQL Server\-冗長性  
  
1. SQL Server インストール\(詳細については、次を参照してください。 [ https://technet.microsoft.com/evalcenter/hh225126.aspx](https://technet.microsoft.com/evalcenter/hh225126.aspx)します。 レプリカの SQL server に結果として得られる CreateDB.sql と SetPermissions.sql スクリプト ファイルをコピーします。  
  
2. SQL Server エージェント サービスが実行されていることを確認し、自動開始に設定  
  
3. 実行**エクスポート\-AdfsDeploymentSQLScript** CreateDB.sql と SetPermissions.sql ファイルを作成するプライマリ AD FS ノードにします。  例:`PS:\>Export-AdfsDeploymentSQLScript -DestinationFolder . –ServiceAccountName CONTOSO\gmsa1$`します。  
   ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql2.png)
  
4. セカンダリ サーバーにスクリプトをコピーします。  CreateDB.sql スクリプトを開きます**SQL Management Studio**クリック**Execute**します。
   ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql4.png)

5. SetPermissions.sql スクリプトを開きます**SQL Management Studio**クリック**Execute**します。
   ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql6.png) 

   

> [!NOTE]
> コマンドラインから次を使用することもできます。 
> 
>    `c:\>sqlcmd –i CreateDB.sql`  
> 
>    `c:\>sqlcmd –i SetPermissions.sql` 
> 
> ## <a name="create-publisher-settings-on-the-initial-sql-server"></a>最初の SQL Server 上のパブリッシャーの設定を作成します。  
  
1. SQL Server Management studio から **レプリケーション**を右クリックして**ローカル パブリケーション**選択**新しい公開しています.** 
   ![地理的冗長性を設定](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql7.png) </br>  

2. パブリケーションの新規作成ウィザードの画面でクリックして**次**します。</br>
   ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql8.png) </br> 
  
3. **ディストリビューター**  ページでディストリビューターとしてローカル サーバーを選択してクリックして**次**します。  
   ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql9.png) </br>   

4. **スナップショット**フォルダー ページで、入力\\\SQL1\repldata 既定のフォルダーの代わりにします。 \(注:この共有を自分で作成する必要があります\)します。  
   ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql10.png) </br>   
  
5. 選択**AdfsConfigurationV3**パブリケーション データベースをクリックします**次**します。  
   ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql11.png) </br>
  
6. **パブリケーションの種類**、選択**マージ パブリケーション** をクリック**次**します。  
   ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql12.png) </br>
  
7. **サブスクライバーの種類**、選択**SQL Server 2008 またはそれ以降** をクリック**次**します。  
   ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql13.png) </br> 

8. **記事**選択ページ**テーブル**ノードをすべてのテーブルを選択し、**解除\-SyncProperties をチェック**テーブル\(ようすることはできませんレプリケート\)</br>
   ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql14.png) </br>    
  
9. **記事**] ページで、[**ユーザー定義関数**ノードをすべてのユーザー定義関数を選択し、をクリックして**次**.  
   ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql15.png) </br>    

10. **アーティクルの問題点**ページ クリック**次**。  
    ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql16.png) </br>   

11. **テーブル行のフィルター** ] ページで [**次**します。  
    ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql17.png) </br>   
12. **スナップショット エージェント**ページ、イミディ エイト] および [14 日間の既定値を選択して、をクリックして**次**します。  
    ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql18.png) </br>   
    SQL エージェントのドメイン アカウントを作成する必要があります。 」の手順に従って[ドメイン アカウント CONTOSO 用の構成の SQL ログイン\\sqlagent](Set-up-Geographic-Redundancy-with-SQL-Server-Replication.md#sqlagent)をこの新しい AD ユーザー用の SQL ログインを作成し、特定のアクセス許可を割り当てます。  
  
13. **エージェントのセキュリティ**] ページで [**セキュリティ設定**し、ユーザー名を入力します\/ドメイン アカウントのパスワード\(GMSA ではない\)SQL エージェントの作成とクリックして**OK**します。  **[次へ]** をクリックします。  
    ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql19.png) </br>  

14. **ウィザードのアクション**] ページで [**次**します。   
    ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql20.png) </br>

15. **ウィザードを完了** ページで、パブリケーションの名前を入力してをクリックして**完了**します。 
    ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql21.png) </br>  

16. パブリケーションを作成した後は、成功のステータスが表示されます。  **[閉じる]** をクリックします。
    ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql22.png) </br>  

17. バックアップ SQL Server Management Studio で、新しいパブリケーションを右クリックし をクリックして**レプリケーション モニターの起動**します。  
    ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql23.png) </br> 
  
## <a name="create-subscription-settings-on-the-replica-sql-server"></a>SQL Server レプリカのサブスクリプション設定を作成します。  
上記で説明したとおり、最初の SQL server パブリッシャーの設定を作成したことかどうかを確認し、次の手順を実行します。  
  
1. SQL Server Management studio で、レプリカ、SQL Server で **レプリケーション**を右クリックして**ローカル サブスクリプション**選択**新しいサブスクリプション.** .![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql24.png) </br>  

2. **サブスクリプションの新規作成ウィザード**] ページで [**次**します。
   ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql25.png) </br>   
  
3. **パブリケーション** ページで、ドロップダウン リストから、パブリッシャーを選択します。  展開**AdfsConfigurationV3**上記で作成したパブリケーションの名前を選択し、クリックして**次**します。  
   ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql26.png) </br> 
  
4. **マージ エージェントの場所**] ページで、[**サブスクライバーで各エージェントを実行する\(プル サブスクリプション\)** \(既定\)をクリックします。 **[次へ]** します。  
   ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql27.png) </br> これは、と共に、以下のサブスクリプションの種類を決定します競合の解決ロジック。 \(詳細については、次を参照してください。 [Detect and Resolve Merge Replication Conflicts して](https://technet.microsoft.com/library/ms151191.aspx)します。 </br>
 
5. **サブスクライバー** ] ページで、[ **AdfsConfigurationV3**サブスクライバー データベースをクリックします**次**します。  
   ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql28.png) </br> 
  
6. **マージ エージェント セキュリティ**] ページで [ **.** ユーザー名とドメイン アカウントのパスワードを入力\(GMSA ではない\)省略記号ボックスとクリックを使用して、SQL エージェントの作成**次**。
   ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql30.png) </br> 
  
7. **同期スケジュール**、選択**連続実行** をクリック**次**。 
   ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql31.png) </br> 
 
8. [**サブスクリプションの初期化**、] をクリックして**次**します。  
   ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql32.png) </br> 
  
9. **サブスクリプションの種類**、選択**クライアント** をクリック**次**します。  
  
   この機能の影響が記載されている[ここ](https://technet.microsoft.com/library/ms151191.aspx)と[ここ](https://technet.microsoft.com/library/ms151170.aspx)します。  基本的には、単純な「最初にパブリッシャー優先」の競合の解決を紹介し、他のサブスクライバーに再パブリッシュする必要はありません。  
   ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql33.png) </br>
   
10. **ウィザードのアクション**ことを確認 ページで、**サブスクリプションを作成**がチェックされ、をクリックして**次**。 
    ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql34.png) </br>

11. **ウィザードを完了**] ページで [**完了**します。 
    ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql35.png) </br>

12. サブスクリプションの作成プロセスが完了すると、成功が表示されます。 **[閉じる]** をクリックします。 
    ![地理的冗長性を設定します。](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql36.png) </br>
  
## <a name="verify-the-process-of-initialization-and-replication"></a>初期化とレプリケーションのプロセスを確認します。  
  
1.  プライマリ SQL server では、右\-クリックして、**レプリケーション**ノードをクリックします**レプリケーション モニターの起動**します。  
  
2.  **レプリケーション モニター**パブリケーションをクリックします。  
  
3.  **すべてのサブスクリプション** タブで、右クリックし、**詳細を表示する**します。  
  
    多数のエントリを参照してください。 できる**アクション**の初期レプリケーション。  
  
4.  さらに、検索すること、 **SQL Server エージェント\\ジョブ**ジョブを表示するノード\(s\)の文書の操作を実行するようにスケジュール\/サブスクリプション。  のみローカル ジョブが表示されるので、トラブルシューティングのために、パブリッシャーとサブスクライバーを確認してください。  右\-ジョブをクリックし、[**履歴の表示]** 実行履歴を表示し、結果にします。  
  
## <a name="sqlagent"></a>ドメイン アカウント CONTOSO 用の SQL ログインを構成する\\sqlagent  
  
1.  プライマリとレプリカ CONTOSO と呼ばれる SQL Server で新しいログインを作成\\sqlagent\(新しいドメイン ユーザーの名前で作成および構成、**エージェントのセキュリティ**上記の手順でページ。\)  
  
2.  SQL Server では、右\-作成したログインをクリックし、プロパティ を選択し、**ユーザー マッピング** タブで、このログインにマップ**AdfsConfiguration**と**AdfsArtifact**パブリックと db によるデータベースの\_genevaservice ロール。 ディストリビューション データベースにこのログインにマップして、db の追加も\_配布と adfsconfiguration の両方のテーブルの所有者ロール。  SQL server のプライマリとレプリカの両方に該当する場合は、これを行います。 詳細については、次を参照してください。 [Replication Agent Security Model](https://technet.microsoft.com/library/ms151868.aspx)します。  
  
3.  対応するドメイン アカウントの読み取りし、書き込みのディストリビューターとして構成されている共有のアクセス許可。  読み取り設定および書き込みアクセス許可の両方で共有とローカル ファイルのアクセス許可があることを確認してください。  
  
## <a name="configure-ad-fs-nodes-to-point-to-the-sql-server-replica-farm"></a>AD FS ノード構成\(s\) SQL Server レプリカのファーム をポイントするには  
Geo 冗長性を設定すると、これで、標準の AD FS「結合」ファームの機能のいずれかから AD FS 構成ウィザードの UI を使用して、または Windows PowerShell を使用してレプリカ SQL Server ファームを指すように AD FS ファームのノードを構成できます。  
  
AD FS 構成ウィザードの UI を使用する場合は、選択**フェデレーション サーバー ファームにフェデレーション サーバーを追加**します。 **しない**選択**フェデレーション サーバー ファーム内の最初のフェデレーション サーバーの作成**です。  
  
Windows PowerShell を使用する場合は、実行**追加\-AdfsFarmNode**します。 **しない**実行**インストール\-AdfsFarm**します。  
  
メッセージが表示されたら、SQL Server では、レプリカのホストとインスタンス名を提供**いない**初期の SQL server。  
