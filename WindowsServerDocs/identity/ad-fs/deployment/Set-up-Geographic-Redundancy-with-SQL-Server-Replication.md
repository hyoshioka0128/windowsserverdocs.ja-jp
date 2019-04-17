---
title: "地理的な冗長性を SQL Server レプリケーションをセットアップします。"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: active-directory-federation-services
ms.author: billmath
ms.assetId: 7b9f9a4f-888c-4358-bacd-3237661b1935
ms.openlocfilehash: a9f29c1eb19a8241eac5afb5c87581e6c988c3c8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="setup-geographic-redundancy-with-sql-server-replication"></a>地理的な冗長性を SQL Server レプリケーションをセットアップします。

>適用対象: Windows Server 2016、Windows Server 2012 R2

> [!IMPORTANT]  
> AD FS ファームを作成して構成データを格納する SQL Server を使用する場合は、SQL Server 2008 以降を使用することができます。
  
AD FS 構成データベースとして SQL Server を使用する場合は、SQL Server レプリケーションを使用して AD FS ファーム用 geo\ 冗長性をセットアップできます。 アプリケーションは、1 つのサイトから別に切り替えることができるように、Geo\ 冗長性は 2 つの地理的に離れているサイト間でデータをレプリケートします。 これにより、1 つのサイトの障害が発生した場合ことができます利用可能なすべての構成データ、2 番目のサイトにします。 詳細についてを参照してください「SQL Server の地理的な冗長性セクション」[フェデレーション サーバー ファームを使用して SQL Server](../design/Federation-Server-Farm-Using-SQL-Server.md)します。  
  
## <a name="prerequisites"></a>前提条件  
インストールし、SQL server ファームを構成します。 詳細については、次を参照してください。[https://technet.microsoft.com/evalcenter/hh225126.aspx](https://technet.microsoft.com/evalcenter/hh225126.aspx)します。 初期の SQL Server で SQL Server エージェント サービスが実行されていることを確認し、自動開始を設定します。  
  
## <a name="create-the-second-replica-sql-server-for-geo-redundancy"></a>Geo\ 冗長性のための 2 つ目の \(replica\) SQL Server を作成します。  
  
1.  SQL Server のインストール \ (詳細については、次を参照してください。[https://technet.microsoft.com/evalcenter/hh225126.aspx](https://technet.microsoft.com/evalcenter/hh225126.aspx)します。 レプリカの SQL server に、結果として得られる CreateDB.sql ファイルと SetPermissions.sql スクリプト ファイルをコピーします。  
  
2.  SQL Server エージェント サービスが実行されていることを確認し、自動開始設定  
  
3.  実行**では AdfsDeploymentSQLScript** CreateDB.sql と SetPermissions.sql ファイルを作成するプライマリ AD FS ノードでします。  例:`PS:\>Export-AdfsDeploymentSQLScript -DestinationFolder . –ServiceAccountName CONTOSO\gmsa1$`します。  
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql2.png)
  
4.  セカンダリ サーバーに、スクリプトをコピーします。  CreateDB.sql のスクリプトを開く**SQL Management Studio** ] をクリック**Execute**します。
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql4.png)

5. SetPermissions.sql スクリプトを開きます**SQL Management Studio** ] をクリック**Execute**します。
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql6.png) 

   

>[!NOTE]
>また、コマンド ラインから、次を使用することができます。 
>
>    `c:\>sqlcmd –i CreateDB.sql`  
>  
>    `c:\>sqlcmd –i SetPermissions.sql` 
> 
## <a name="create-publisher-settings-on-the-initial-sql-server"></a>初期の SQL Server の発行元の設定を作成します。  
  
1.  SQL Server Management studio を下にある**レプリケーション**、右クリックして**ローカル パブリケーション**を選択し、**新規パブリケーション.**<ph x="4">
![</ph>地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql7.png) </br>  

2.  パブリケーションの新規作成ウィザードの画面でクリックして**次**します。</br>
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql8.png) </br> 
  
3.  **ディストリビュータ**] ページでディストリビュータとしてローカル サーバーを選択してクリックして**次**します。  
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql9.png) </br>   

4.  **スナップショット**フォルダー] ページで、既定のフォルダーの代わりに \\\SQL1\repldata を入力します。 \ (注: この共有 yourself\ を作成する必要があります)。  
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql10.png) </br>   
  
5.  選択**AdfsConfigurationV3**、パブリケーション データベース] をクリックと**次**します。  
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql11.png) </br>
  
6.  **パブリケーションの種類**、選択**マージ パブリケーション**] をクリック**次**します。  
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql12.png) </br>
  
7.  [**サブスクライバーの種類の**、選択**SQL Server 2008 以降**] をクリック**[次へ]**します。  
 ![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql13.png) </br> 

8.  **記事**選択ページ**テーブル**ノードでは、すべてのテーブルを選択し、次を**まだチェック SyncProperties**表 \ (このしないで replicated\)</br>
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql14.png) </br>    
  
9.  **記事**] ページで、[**ユーザー定義関数**ノードをすべてのユーザー定義関数を選択し、をクリックして**次**.  
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql15.png) </br>    

10. **問題の記事**ページ] をクリック**[次へ]**します。  
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql16.png) </br>   

11. **テーブル行のフィルタ**] ページで [**次**します。  
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql17.png) </br>   
12. **スナップショット エージェント**] ページで、即時レンダリングと 14 日間の既定の設定を選択して、[**次**します。  
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql18.png) </br>   
SQL エージェントのドメイン アカウントを作成する必要があります。 手順を使用して[CONTOSO\\sqlagent ドメイン アカウントの構成の SQL ログイン](Set-up-Geographic-Redundancy-with-SQL-Server-Replication.md#sqlagent)をこの新しい AD ユーザー用の SQL ログインを作成し、特定のアクセス許可を割り当てます。  
  
13. **エージェント セキュリティ**] ページで [**セキュリティ設定**ドメイン アカウントの username\/パスワードの入力と \ (GMSA\ しない) と用の作成、SQL エージェント] をクリック**[OK]**します。  をクリックして**次**します。  
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql19.png) </br>  

14. **ウィザードのアクション**] ページで [**次**します。   
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql20.png) </br>

15. **ウィザードを完了**] ページで、パブリケーションの名前を入力してをクリックして**完了**します。 
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql21.png) </br>  

16. パブリケーションを作成した後の成功のステータスが表示されます。  をクリックして**閉じる**します。
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql22.png) </br>  

17. SQL Server Management Studio で新しい文書を右クリックし] をクリックして戻る**レプリケーション モニターの起動**します。  
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql23.png) </br> 
  
## <a name="create-subscription-settings-on-the-replica-sql-server"></a>SQL Server レプリカのサブスクリプションの設定を作成します。  
前述のよう、初期の SQL Server の発行元の設定を作成することを確認し、次の手順を完了します。  
  
1.  SQL Server、SQL Server Management studio からのレプリカの下にある**レプリケーション**、右クリックして**ローカル サブスクリプション**を選択し、**新しいサブスクリプション.**.![地理的な冗長性の設定](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql24.png) </br>  

2.  **サブスクリプションの新規作成ウィザード**] ページで [**次**します。
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql25.png) </br>   
  
3.  **パブリケーション**] ページで、ドロップダウン リストから、発行元を選択します。  展開**AdfsConfigurationV3**上に作成されたパブリケーションの名前を選択し、クリックして**次**します。  
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql26.png) </br> 
  
4.  **マージ エージェントの場所**] ページで、[**そのサブスクライバー \(pull subscriptions\) で各エージェントを実行**\(the default\)] をクリック**[次へ]**します。  
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql27.png) </br> これには、と共に、以下のサブスクリプションの種類を決定の競合の解決策ロジックします。 \ (詳細については、次を参照してください。[検出とマージ レプリケーションの競合を解決する](https://technet.microsoft.com/library/ms151191.aspx)します。 </br>
 
5.  **サブスクライバー** ] ページで、[ **AdfsConfigurationV3**サブスクライバー データベースおよびクリックとして**[次へ]**します。  
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql28.png) </br> 
  
6.  **マージ エージェント セキュリティ**] ページで [ **.**ユーザー名とドメイン アカウントのパスワードを入力 \ (GMSA\ されません) が、SQL エージェントの省略記号のボックスを使用して作成し] をクリック**次**します。
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql30.png) </br> 
  
7.  **同期スケジュール**、選択**継続的に実行**] をクリック**次**します。 
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql31.png) </br> 
 
8.  [**サブスクリプションの初期化**、] をクリックして**次**します。  
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql32.png) </br> 
  
9.  **サブスクリプションの種類**、選択**クライアント**] をクリック**次**します。  
  
    この場合の影響が記載されている[次のとおり](https://technet.microsoft.com/library/ms151191.aspx)と[ここ](https://technet.microsoft.com/library/ms151170.aspx)します。  基本的には、単純な「最初の発行元の wins に」競合の解決必要になることと、その他のサブスクライバに再発行する必要はありません。  
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql33.png) </br>
   
10. **ウィザードのアクション**ことを確認] ページで、**サブスクリプションの作成**が確認され] をクリックして**次**します。 
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql34.png) </br>

11. **ウィザードを完了**] ページで [**完了**します。 
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql35.png) </br>

12. サブスクリプションが作成プロセスを完了すると、成功が表示されます。 をクリックして**閉じる**します。 
![地理的な冗長性を設定します。](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql36.png) </br>
  
## <a name="verify-the-process-of-initialization-and-replication"></a>初期化し、レプリケーション プロセスを確認します。  
  
1.  プライマリ SQL サーバーで、右クリック、**レプリケーション**ノードとクリック**レプリケーション モニターの起動**します。  
  
2.  **レプリケーション モニター**、パブリケーション] をクリックします。  
  
3.  **すべてのサブスクリプション**] タブで、右クリックし、**詳細を表示する**します。  
  
    下にある多くのエントリを参照することができます**アクション**の初期レプリケーション。  
  
4.  さらに、下にある情報を参照することができます、**SQL Server Agent\\Jobs** publication\/サブスクリプションの操作を実行する、job\(s\) を表示するノードをスケジュールします。  のみローカル ジョブが表示され、トラブルシューティングのため、パブリッシャとサブスクライバにチェックして確認しておきます。  ジョブを右クリックし、**履歴を表示する**ビューの実行履歴と結果をします。  
  
## <a name="sqlagent"></a>ドメイン アカウント CONTOSO\\sqlagent 用の SQL ログインを構成します。  
  
1.  プライマリとレプリカ CONTOSO\\sqlagent と呼ばれる SQL Server の新しいログインの作成 \ (新しいドメインのユーザーの名前が作成されで構成されている、**エージェント セキュリティ**上記の手順でページ \)。  
  
2.  SQL server、右クリックし、作成したのプロパティ] を選択し、ログイン、**ユーザー マッピング**] タブで、このログインにマップ**AdfsConfiguration**と**AdfsArtifact**パブリックおよび db\_genevaservice の役割を持つデータベース。 ディストリビューション データベースでは、このログにマップし、配布および adfsconfiguration テーブルの両方の db\_owner 役割を追加します。  プライマリとレプリカの両方の SQL server に適切に実行します。 詳細については、次を参照してください。[レプリケーション エージェントのセキュリティ モデル](https://technet.microsoft.com/library/ms151868.aspx)します。  
  
3.  対応するドメイン アカウントの読み取りを提供し、ディストリビュータとして構成されている共有にアクセス許可を記述します。  設定の読み取りおよび書き込み共有のアクセス許可とローカル ファイルのアクセス許可の両方のアクセス許可があることを確認してください。  
  
## <a name="configure-ad-fs-nodes-to-point-to-the-sql-server-replica-farm"></a>SQL Server レプリカ ファームを指す node\(s\) を AD FS を構成します。  
地理的な冗長性をセットアップするようになったポイント、レプリカの SQL Server ファーム機能を使用して、標準的な AD FS「参加」ファーム、AD FS 構成ウィザードの UI からいずれかまたは Windows PowerShell を使用する AD FS ファーム ノードを構成できます。  
  
AD FS 構成ウィザードの UI を使用する場合は、選択**フェデレーション サーバー ファームにフェデレーション サーバーを追加**します。 **そうではない**選択**フェデレーション サーバー ファームに最初のフェデレーション サーバーを作成する**します。  
  
Windows PowerShell を使用する場合は、実行**アドオン AdfsFarmNode**します。 **そうではない**実行**Install\ AdfsFarm**します。  
  
レプリカ、SQL Server のホストとインスタンス名を求められたら、**いない**初期の SQL server。  
