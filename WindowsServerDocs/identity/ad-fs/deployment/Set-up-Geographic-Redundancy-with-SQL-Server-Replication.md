---
title: SQL Server レプリケーションを使用した地理的な冗長性の設定
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: active-directory-federation-services
ms.author: billmath
ms.assetId: 7b9f9a4f-888c-4358-bacd-3237661b1935
ms.openlocfilehash: 44f1f4598762f3d6e08430aa39b7cfa89eae4460
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86966594"
---
# <a name="setup-geographic-redundancy-with-sql-server-replication"></a>SQL Server レプリケーションを使用した地理的な冗長性の設定


> [!IMPORTANT]  
> AD FS ファームを作成し、SQL Server を使用して構成データを格納する場合は SQL Server 2008 以降を使用できます。
  
SQL Server を AD FS 構成データベースとして使用している場合は、 \- SQL Server レプリケーションを使用して、AD FS ファームの geo 冗長性を設定できます。 Geo \- 冗長性は、アプリケーションがあるサイトから別のサイトに切り替えることができるように、地理的に離れた2つのサイト間でデータをレプリケートします。 これにより、1つのサイトで障害が発生した場合でも、2番目のサイトですべての構成データを使用できるようになります。 詳細については、「 [SQL Server を使用したフェデレーションサーバーファーム](../design/Federation-Server-Farm-Using-SQL-Server.md)」の「地理的冗長性の SQL Server」セクションを参照してください。  
  
## <a name="prerequisites"></a>前提条件  
SQL server ファームをインストールして構成します。 詳細については、「[https://technet.microsoft.com/evalcenter/hh225126.aspx](https://www.microsoft.com/en-us/evalcenter/)」を参照してください。 最初の SQL Server で、SQL Server エージェントサービスが実行されていて、[自動開始] に設定されていることを確認します。  
  
## <a name="create-the-second-replica-sql-server-for-geo-redundancy"></a>\( \) Geo 冗長性のための2番目のレプリカ SQL Server を作成する \-  
  
1. インストール SQL Server \( 詳細については、「」を参照してください [https://technet.microsoft.com/evalcenter/hh225126.aspx](https://www.microsoft.com/en-us/evalcenter/) 。 生成された CreateDB および SetPermissions スクリプトファイルをレプリカ SQL server にコピーします。  
  
2. SQL Server エージェントサービスが実行されていて、自動開始に設定されていることを確認する  
  
3. プライマリ AD FS ノードで**Export \- AdfsDeploymentSQLScript**を実行して、CreateDB ファイルと SetPermissions ファイルを作成します。  たとえば、`PS:\>Export-AdfsDeploymentSQLScript -DestinationFolder . –ServiceAccountName CONTOSO\gmsa1$` となります。  
   ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql2.png)
  
4. スクリプトをセカンダリサーバーにコピーします。  **Sql Management Studio**で CreateDB スクリプトを開き、[**実行**] をクリックします。
   ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql4.png)

5. **Sql Management Studio**で SetPermissions スクリプトを開き、[**実行**] をクリックします。
   ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql6.png) 

   

> [!NOTE]
> また、コマンドラインから次のコードを使用することもできます。 
> 
>    `c:\>sqlcmd –i CreateDB.sql`  
> 
>    `c:\>sqlcmd –i SetPermissions.sql` 
> 
> ## <a name="create-publisher-settings-on-the-initial-sql-server"></a>初期 SQL Server に発行者設定を作成する  
  
1. SQL Server Management studio の [**レプリケーション**] で、[**ローカルパブリケーション**] を右クリックし、[**新しいパブリケーション** 
    ![ ] を選択します。地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql7.png) </br>  

2. パブリケーションの新規作成ウィザードの画面で、[**次へ**] をクリックします。</br>
   ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql8.png) </br> 
  
3. [**ディストリビューター** ] ページで、[ディストリビューターとしてローカルサーバー] を選択し、[**次へ**] をクリックします。  
   ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql9.png) </br>   

4. [**スナップショット**フォルダー] ページで、 \\ 既定のフォルダーの代わりに「\SQL1\repldata」と入力します。 \(注: この共有を自分で作成することが必要になる場合があり \) ます。  
   ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql10.png) </br>   
  
5. パブリケーションデータベースとして [ **AdfsConfigurationV3** ] を選択し、[**次へ**] をクリックします。  
   ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql11.png) </br>
  
6. [**パブリケーションの種類**] で、[**マージパブリケーション**] を選択し、[**次へ**] をクリックします。  
   ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql12.png) </br>
  
7. [**サブスクライバーの種類**] で**SQL Server 2008**以降を選択し、[**次へ**] をクリックします。  
   ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql13.png) </br> 

8. [**アーティクル**] ページで、[**テーブル**の選択] ノードを選択してすべてのテーブルを選択し、[ ** \- syncproperties の確認**] テーブルをレプリケートし \( ないようにします。\)</br>
   ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql14.png) </br>    
  
9. [**アーティクル**] ページで、[**ユーザー定義関数**] ノードを選択してすべてのユーザー定義関数を選択し、[**次へ**] をクリックします。  
   ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql15.png) </br>    

10. [**アーティクルの問題**] ページで、[**次へ**] をクリックします。  
    ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql16.png) </br>   

11. [**テーブル行のフィルター選択**] ページで、[**次へ**] をクリックします。  
    ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql17.png) </br>   
12. [**スナップショットエージェント**] ページで、[既定] [即時]、[14 日] の順に選択し、[**次へ**] をクリックします。  
    ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql18.png) </br>   
    場合によっては、SQL エージェントのドメインアカウントを作成する必要があります。 「[ドメインアカウント CONTOSO \\ SQLAGENT の sql ログインを構成](Set-up-Geographic-Redundancy-with-SQL-Server-Replication.md#sqlagent)する」の手順に従って、この新しい AD ユーザーの sql ログインを作成し、特定のアクセス許可を割り当てます。  
  
13. [**エージェントセキュリティ**] ページで、[**セキュリティ設定**] をクリックし、 \/ \( SQL エージェント用に作成された GMSA ではないドメインアカウントのユーザー名のパスワードを入力して、 \) [ **OK]** をクリックします。  **[次へ]** をクリックします。  
    ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql19.png) </br>  

14. [**ウィザードのアクション**] ページで、[**次へ**] をクリックします。   
    ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql20.png) </br>

15. [**ウィザードの完了**] ページで、パブリケーションの名前を入力し、[**完了**] をクリックします。 
    ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql21.png) </br>  

16. パブリケーションが作成されると、"成功" の状態が表示されます。  **[閉じる]** をクリックします。
    ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql22.png) </br>  

17. SQL Server Management Studio に戻り、新しいパブリケーションを右クリックして、[**レプリケーションモニターの起動**] をクリックします。  
    ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql23.png) </br> 
  
## <a name="create-subscription-settings-on-the-replica-sql-server"></a>レプリカ SQL Server でのサブスクリプション設定の作成  
前に説明したように、初期 SQL Server でパブリッシャー設定を作成したことを確認してから、次の手順を実行します。  
  
1. レプリカ SQL Server の SQL Server Management studio から、[**レプリケーション**] の下にある [**ローカルサブスクリプション**] を右クリックし、[**新しいサブスクリプション**] を選択します。![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql24.png) </br>  

2. [**サブスクリプションの新規作成ウィザード**] ページで、[**次へ**] をクリックします。
   ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql25.png) </br>   
  
3. [**パブリケーション**] ページで、ドロップダウンからパブリッシャーを選択します。  [ **AdfsConfigurationV3** ] を展開し、上で作成したパブリケーションの名前を選択して、[**次へ**] をクリックします。  
   ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql26.png) </br> 
  
4. [**マージエージェントの場所**] ページで、[**サブスクライバー \( \) で各エージェントを実行**する] を選択し、 \( \) [**次へ**] をクリックします。  
   ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql27.png) </br> これは、以下のサブスクリプションの種類と共に、競合解決ロジックを決定します。 \(詳細については、「[マージレプリケーションの競合の検出と解決](/sql/relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution?view=sql-server-ver15)」を参照してください。 </br>
 
5. [**サブスクライバー** ] ページで、サブスクライバーデータベースとして [ **AdfsConfigurationV3** ] を選択し、[**次へ**] をクリックします。  
   ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql28.png) </br> 
  
6. [**マージエージェントセキュリティ**] ページで、[ **...** ] をクリックし、 \( \) 省略記号ボックスを使用して SQL エージェント用に作成された GMSA ではないドメインアカウントのユーザー名とパスワードを入力して、[**次へ**] をクリックします。
   ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql30.png) </br> 
  
7. [**同期スケジュール**] で、[**連続実行**] を選択し、[**次へ**] をクリックします。 
   ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql31.png) </br> 
 
8. [**サブスクリプションの初期化**] で、[**次へ**] をクリックします。  
   ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql32.png) </br> 
  
9. [**サブスクリプションの種類**] で、[**クライアント**] を選択し、[**次へ**] をクリックします。  
  
   この点に[ついては、こちらと](/sql/relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution?view=sql-server-ver15)[こちら](/sql/relational-databases/replication/subscribe-to-publications?view=sql-server-ver15)に記載されています。  基本的には、単純な "最初からパブリッシャーへの優先" の競合解決を行い、他のサブスクライバーに再パブリッシュする必要はありません。  
   ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql33.png) </br>
   
10. [**ウィザードのアクション**] ページで、[**サブスクリプションの作成**] がオンになっていることを確認し、[**次へ**] をクリックします。 
    ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql34.png) </br>

11. [**ウィザードの完了**] ページで、[**完了**] をクリックします。 
    ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql35.png) </br>

12. サブスクリプションによって作成プロセスが完了すると、[success] \ (成功 \) と表示されます。 **[閉じる]** をクリックします。 
    ![地理的冗長性を設定する](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql36.png) </br>
  
## <a name="verify-the-process-of-initialization-and-replication"></a>初期化とレプリケーションのプロセスを確認する  
  
1.  プライマリ SQL server で、[ \- **レプリケーション**] ノードを右クリックし、[**レプリケーションモニターの起動**] をクリックします。  
  
2.  **レプリケーションモニター**で、パブリケーションをクリックします。  
  
3.  [**すべてのサブスクリプション**] タブで、右クリックして**詳細を表示**します。  
  
    初期レプリケーションの [**アクション**] の下に多くのエントリが表示されます。  
  
4.  さらに、[ **SQL Server エージェント \\ ジョブ**] ノードの下で、 \( \) パブリケーションサブスクリプションの操作を実行するようにスケジュールされているジョブを確認でき \/ ます。  ローカルジョブのみが表示されます。そのため、トラブルシューティングのために、パブリッシャーとサブスクライバーを確認してください。  \-ジョブを右クリックし、[**履歴の表示**] を選択して、実行履歴と結果を表示します。  
  
## <a name="configure-sql-login-for-the-domain-account-contososqlagent"></a><a name="sqlagent"></a>ドメインアカウント CONTOSO sqlagent の SQL ログインを構成します \\  
  
1.  \\ \( 前の手順で [**エージェントセキュリティ**] ページで作成および構成した新しいドメインユーザーの名前として、プライマリおよびレプリカ SQL Server に新しいログインを作成します。\)  
  
2.  SQL Server で、作成したログインを右クリックし、[プロパティ] を \- 選択します。次に、[**ユーザーマッピング**] タブで、このログインを public および db genevaservice roles を使用して**AdfsConfiguration**データベースと**AdfsArtifact**データベースにマップし \_ ます。 また、このログインをディストリビューションデータベースにマップし、 \_ ディストリビューションテーブルと adfsconfiguration テーブルの両方に対して db 所有者ロールを追加します。  これは、プライマリとレプリカの両方の SQL server に適用されます。 詳細については、「 [レプリケーション エージェント セキュリティ モデル](/sql/relational-databases/replication/security/replication-agent-security-model?view=sql-server-ver15)」を参照してください。  
  
3.  対応するドメインアカウントに、ディストリビューターとして構成されている共有に対する読み取りと書き込みのアクセス許可を与えます。  共有のアクセス許可とローカルファイルのアクセス許可の両方で、読み取りと書き込みのアクセス許可を設定していることを確認してください。  
  
## <a name="configure-ad-fs-nodes-to-point-to-the-sql-server-replica-farm"></a>\( \) SQL Server レプリカファームを指すように AD FS ノードを構成します  
Geo 冗長の設定が完了したので、AD FS 構成ウィザードの UI または Windows PowerShell を使用して、標準 AD FS "結合" ファームの機能を使用して、レプリカ SQL Server ファームをポイントするように AD FS ファームノードを構成できます。  
  
AD FS 構成ウィザードの UI を使用する場合は、[フェデレーションサーバー**ファームにフェデレーションサーバーを追加する**] を選択します。 [**フェデレーションサーバーファームに最初のフェデレーションサーバーを作成**する] を選択**しない**でください。  
  
Windows PowerShell を使用する場合は、 **Add \- add-adfsfarmnode**を実行します。 **Install \- AdfsFarm**を実行しない**で**ください。  
  
プロンプトが表示されたら、最初の SQL Server では**なく**、レプリカ SQL Server のホスト名とインスタンス名を指定します。  
