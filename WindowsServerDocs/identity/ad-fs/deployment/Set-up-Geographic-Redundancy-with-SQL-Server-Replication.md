---
title: SQL Server レプリケーションを使用した地理的な冗長性の設定
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: active-directory-federation-services
ms.author: billmath
ms.assetId: 7b9f9a4f-888c-4358-bacd-3237661b1935
ms.openlocfilehash: 16cf1a237043aa546d4fc24164045aa9f9a1e6ac
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359819"
---
# <a name="setup-geographic-redundancy-with-sql-server-replication"></a>SQL Server レプリケーションを使用した地理的な冗長性の設定


> [!IMPORTANT]  
> AD FS ファームを作成し、SQL Server を使用して構成データを格納する場合は SQL Server 2008 以降を使用できます。
  
SQL Server を AD FS 構成データベースとして使用している場合は、SQL Server レプリケーションを使用して、AD FS ファームの geo @ no__t-0redundancy を設定できます。 Geo @ no__t-0redundancy は、アプリケーションがあるサイトから別のサイトに切り替えることができるように、地理的に離れた2つのサイト間でデータをレプリケートします。 これにより、1つのサイトで障害が発生した場合でも、2番目のサイトですべての構成データを使用できるようになります。 詳細については、「 [SQL Server を使用したフェデレーションサーバーファーム](../design/Federation-Server-Farm-Using-SQL-Server.md)」の「地理的冗長性の SQL Server」セクションを参照してください。  
  
## <a name="prerequisites"></a>前提条件  
SQL server ファームをインストールして構成します。 詳細については[https://technet.microsoft.com/evalcenter/hh225126.aspx](https://technet.microsoft.com/evalcenter/hh225126.aspx)、「」を参照してください。 最初の SQL Server で、SQL Server エージェントサービスが実行されていて、[自動開始] に設定されていることを確認します。  
  
## <a name="create-the-second-replica-sql-server-for-geo-redundancy"></a>Geo @ no__t-2redundancy の2番目の @no__t 0replica @ no__t-1 SQL Server を作成します。  
  
1. SQL Server @no__t をインストールします。詳細については、 [https://technet.microsoft.com/evalcenter/hh225126.aspx](https://technet.microsoft.com/evalcenter/hh225126.aspx)を参照してください。 生成された CreateDB および SetPermissions スクリプトファイルをレプリカ SQL server にコピーします。  
  
2. SQL Server エージェントサービスが実行されていて、自動開始に設定されていることを確認する  
  
3. プライマリ AD FS ノードで**Export @ no__t-1AdfsDeploymentSQLScript**を実行して、CreateDB ファイルと SetPermissions ファイルを作成します。  例: `PS:\>Export-AdfsDeploymentSQLScript -DestinationFolder . –ServiceAccountName CONTOSO\gmsa1$`。  
   ![Set 冗長を設定する @ no__t-1
  
4. スクリプトをセカンダリサーバーにコピーします。  **Sql Management Studio**で CreateDB スクリプトを開き、 **[実行]** をクリックします。
   ![Set 冗長を設定する @ no__t-1

5. **Sql Management Studio**で SetPermissions スクリプトを開き、 **[実行]** をクリックします。
   ![Set 冗長を設定する @ no__t-1 

   

> [!NOTE]
> また、コマンドラインから次のコードを使用することもできます。 
> 
>    `c:\>sqlcmd –i CreateDB.sql`  
> 
>    `c:\>sqlcmd –i SetPermissions.sql` 
> 
> ## <a name="create-publisher-settings-on-the-initial-sql-server"></a>初期 SQL Server に発行者設定を作成する  
  
1. SQL Server Management studio の **[レプリケーション]** で、 **[ローカルパブリケーション]** を右クリックし、 **[新しいパブリケーション]** を選択します。
    @ no__t-4Set 冗長性の設定 @ no__t-5 </br>  

2. パブリケーションの新規作成ウィザードの画面で、 **[次へ]** をクリックします。</br>
   ![Set 冗長を設定する @ no__t-1 </br> 
  
3. **ディストリビューター** ページで、ディストリビューターとしてローカルサーバー を選択し、**次へ** をクリックします。  
   ![Set 冗長を設定する @ no__t-1 </br>   

4. [**スナップショット**フォルダー] ページで、既定のフォルダーの代わりに \\ \ SQL1\repldata を入力します。 \(注:この共有を自分で作成する必要がある場合があります @ no__t-0 です。  
   ![Set 冗長を設定する @ no__t-1 </br>   
  
5. パブリケーションデータベースとして **[AdfsConfigurationV3]** を選択し、 **[次へ]** をクリックします。  
   ![Set 冗長を設定する @ no__t-1 </br>
  
6. **[パブリケーションの種類]** で、 **[マージパブリケーション]** を選択し、 **[次へ]** をクリックします。  
   ![Set 冗長を設定する @ no__t-1 </br>
  
7. **[サブスクライバーの種類]** で**SQL Server 2008**以降を選択し、 **[次へ]** をクリックします。  
   ![Set 冗長を設定する @ no__t-1 </br> 

8. **[アーティクル]** ページで **[テーブル]** の選択 ノードを選択し、すべてのテーブルを選択します。次に、 **no__t-3syncproperties** @no__t テーブルをオフにします。 @ no__t</br>
   ![Set 冗長を設定する @ no__t-1 </br>    
  
9. **[アーティクル]** ページで、 **[ユーザー定義関数]** ノードを選択してすべてのユーザー定義関数を選択し、 **[次へ]** をクリックします。  
   ![Set 冗長を設定する @ no__t-1 </br>    

10. **[アーティクルの問題]** ページで、 **[次へ]** をクリックします。  
    ![Set 冗長を設定する @ no__t-1 </br>   

11. **[テーブル行のフィルター選択]** ページで、 **[次へ]** をクリックします。  
    ![Set 冗長を設定する @ no__t-1 </br>   
12. **[スナップショットエージェント]** ページで、既定 即時、14 日 の順に選択し、 **[次へ]** をクリックします。  
    ![Set 冗長を設定する @ no__t-1 </br>   
    場合によっては、SQL エージェントのドメインアカウントを作成する必要があります。 この新しい AD ユーザーの SQL ログインを作成し、特定のアクセス許可を割り当てるには、「[ドメインアカウント CONTOSO @ no__t-1sqlagent の sql ログインを構成](Set-up-Geographic-Redundancy-with-SQL-Server-Replication.md#sqlagent)するには」の手順に従います。  
  
13. **[エージェントセキュリティ]** ページで、 **[セキュリティ設定]** をクリックし、ドメイン @no__t アカウントのユーザー名 @ no__t-2password を入力します。このとき、SQL エージェント用に作成された GMSA @ no__t は指定せず、[ **OK]** をクリックします。  **[次へ]** をクリックします。  
    ![Set 冗長を設定する @ no__t-1 </br>  

14. **[ウィザードのアクション]** ページで、 **[次へ]** をクリックします。   
    ![Set 冗長を設定する @ no__t-1 </br>

15. **[ウィザードの完了]** ページで、パブリケーションの名前を入力し、 **[完了]** をクリックします。 
    ![Set 冗長を設定する @ no__t-1 </br>  

16. パブリケーションが作成されると、"成功" の状態が表示されます。  **[閉じる]** をクリックします。
    ![Set 冗長を設定する @ no__t-1 </br>  

17. SQL Server Management Studio に戻り、新しいパブリケーションを右クリックして、 **[レプリケーションモニターの起動]** をクリックします。  
    ![Set 冗長を設定する @ no__t-1 </br> 
  
## <a name="create-subscription-settings-on-the-replica-sql-server"></a>レプリカ SQL Server でのサブスクリプション設定の作成  
前に説明したように、初期 SQL Server でパブリッシャー設定を作成したことを確認してから、次の手順を実行します。  
  
1. レプリカ SQL Server の SQL Server Management studio から、 **[レプリケーション]** の下にある **[ローカルサブスクリプション]** を右クリックし、 **[新しいサブスクリプション]** を選択します。![Set 冗長を設定する @ no__t-1 </br>  

2. **[サブスクリプションの新規作成ウィザード]** ページで、 **[次へ]** をクリックします。
   ![Set 冗長を設定する @ no__t-1 </br>   
  
3. **[パブリケーション]** ページで、ドロップダウンからパブリッシャーを選択します。  **[AdfsConfigurationV3]** を展開し、上で作成したパブリケーションの名前を選択して、 **[次へ]** をクリックします。  
   ![Set 冗長を設定する @ no__t-1 </br> 
  
4. **マージエージェントの場所** ページで、サブスクライバーで各エージェントを実行する を選択し **\(pull サブスクリプション @ no__t-3** \(the 既定値の @ no__t) を選択し、**次へ** をクリックします。  
   ![Set 冗長を設定する @ no__t-1 </br> これは、以下のサブスクリプションの種類と共に、競合解決ロジックを決定します。 @no__t。詳細については、「[マージレプリケーションの競合の検出と解決](https://technet.microsoft.com/library/ms151191.aspx)」を参照してください。 </br>
 
5. **[サブスクライバー]** ページで、サブスクライバーデータベースとして **[AdfsConfigurationV3]** を選択し、 **[次へ]** をクリックします。  
   ![Set 冗長を設定する @ no__t-1 </br> 
  
6. **[マージエージェントセキュリティ]** ページで、 **[...]** をクリックし、ドメイン @no__t アカウントのユーザー名とパスワードを入力します。そのためには、省略記号ボックスを使用して SQL エージェント用に作成された GMSA @ no__t ではなく、 **[次へ]** をクリックします。
   ![Set 冗長を設定する @ no__t-1 </br> 
  
7. **[同期スケジュール]** で、 **[連続実行]** を選択し、 **[次へ]** をクリックします。 
   ![Set 冗長を設定する @ no__t-1 </br> 
 
8. **[サブスクリプションの初期化]** で、 **[次へ]** をクリックします。  
   ![Set 冗長を設定する @ no__t-1 </br> 
  
9. **[サブスクリプションの種類]** で、 **[クライアント]** を選択し、 **[次へ]** をクリックします。  
  
   この点に[ついては、こちらと](https://technet.microsoft.com/library/ms151191.aspx)[こちら](https://technet.microsoft.com/library/ms151170.aspx)に記載されています。  基本的には、単純な "最初からパブリッシャーへの優先" の競合解決を行い、他のサブスクライバーに再パブリッシュする必要はありません。  
   ![Set 冗長を設定する @ no__t-1 </br>
   
10. **[ウィザードのアクション]** ページで、 **[サブスクリプションの作成]** がオンになっていることを確認し、 **[次へ]** をクリックします。 
    ![Set 冗長を設定する @ no__t-1 </br>

11. **[ウィザードの完了]** ページで、 **[完了]** をクリックします。 
    ![Set 冗長を設定する @ no__t-1 </br>

12. サブスクリプションによって作成プロセスが完了すると、[success] \ (成功 \) と表示されます。 **[閉じる]** をクリックします。 
    ![Set 冗長を設定する @ no__t-1 </br>
  
## <a name="verify-the-process-of-initialization-and-replication"></a>初期化とレプリケーションのプロセスを確認する  
  
1.  プライマリ SQL server で、 **[レプリケーション]** ノードを右クリックし、 **[レプリケーションモニターの起動]** をクリックします。  
  
2.  **レプリケーションモニター**で、パブリケーションをクリックします。  
  
3.  **[すべてのサブスクリプション]** タブで、右クリックして**詳細を表示**します。  
  
    初期レプリケーションの **[アクション]** の下に多くのエントリが表示されます。  
  
4.  さらに、 **[SQL Server エージェント @ no__t-1Jobs]** ノードの下で、パブリケーション @ no__t-4subscription の操作を実行するようにスケジュールされているジョブ @ no__t-2s @ no__t を確認できます。  ローカルジョブのみが表示されます。そのため、トラブルシューティングのために、パブリッシャーとサブスクライバーを確認してください。  右 @ no__t をクリックしてジョブをクリックし、 **[履歴の表示]** を選択して実行履歴と結果を表示します。  
  
## <a name="sqlagent"></a>ドメインアカウント CONTOSO @ no__t-1 sqlagent の SQL ログインを構成します。  
  
1.  前の手順の **[エージェントセキュリティ]** ページで作成および構成した新しいドメインユーザーの、CONTOSO @ no__t-0sqlagent \(the という名前のプライマリおよび SQL Server レプリカに新しいログインを作成します。 \)  
  
2.  SQL Server で、作成したログインを右クリックし、プロパティ を選択します。次に、**ユーザーマッピング** タブで、このログインを**AdfsConfiguration**および**AdfsArtifact**データベースにマップします。このログインは、public および db @ no__t-4genevaservice ロールを使用します。 また、このログインをディストリビューションデータベースにマップし、ディストリビューションテーブルと adfsconfiguration テーブルの両方に db @ no__t-0owner ロールを追加します。  これは、プライマリとレプリカの両方の SQL server に適用されます。 詳細については、「[レプリケーションエージェントのセキュリティモデル](https://technet.microsoft.com/library/ms151868.aspx)」を参照してください。  
  
3.  対応するドメインアカウントに、ディストリビューターとして構成されている共有に対する読み取りと書き込みのアクセス許可を与えます。  共有のアクセス許可とローカルファイルのアクセス許可の両方で、読み取りと書き込みのアクセス許可を設定していることを確認してください。  
  
## <a name="configure-ad-fs-nodes-to-point-to-the-sql-server-replica-farm"></a>SQL Server レプリカファームを指すように AD FS ノード @ no__t を構成します。  
Geo 冗長の設定が完了したので、AD FS 構成ウィザードの UI または Windows PowerShell を使用して、標準 AD FS "結合" ファームの機能を使用して、レプリカ SQL Server ファームをポイントするように AD FS ファームノードを構成できます。  
  
AD FS 構成ウィザードの UI を使用する場合は、[フェデレーションサーバー**ファームにフェデレーションサーバーを追加する**] を選択します。 [**フェデレーションサーバーファームに最初のフェデレーションサーバーを作成**する] を選択**しない**でください。  
  
Windows PowerShell を使用する場合は、 **Add @ no__t-1AdfsFarmNode**を実行します。 **Install @ no__t-2AdfsFarm** **を実行しないでください**。  
  
プロンプトが表示されたら、最初の SQL Server では**なく**、レプリカ SQL Server のホスト名とインスタンス名を指定します。  
