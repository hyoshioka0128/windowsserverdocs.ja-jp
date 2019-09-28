---
ms.assetid: 434fd617-373a-405e-bae4-da324ea83efc
title: Windows Server 2012 R2 AD FS の展開ガイド
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: c549b52f697db889bf638470aca03f02e1323ed5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359733"
---
# <a name="configure-a-federation-server"></a>フェデレーション サーバーを構成する

コンピューターに Active Directory フェデレーションサービス (AD FS) \(AD FS\)役割サービスをインストールすると、このコンピューターをフェデレーションサーバーになるように構成することができます。 次のいずれかの操作を実行できます。  
  
-   [新しいフェデレーションサーバーファームで最初のフェデレーションサーバーを構成する](assetId:///e340cf8f-acf3-4cba-8135-a9353b85e714#BKMK_1)  
  
-   [フェデレーションサーバーを既存のフェデレーションサーバーファームに追加する](assetId:///e340cf8f-acf3-4cba-8135-a9353b85e714#BKMK_2)  
  
## <a name="BKMK_1"></a>新しいフェデレーションサーバーファームで最初のフェデレーションサーバーを構成する  
  
### <a name="to-configure-the-first-federation-server-in-a-new-federation-server-farm-by-using-the-active-directory-federation-service-configuration-wizard"></a>Active Directory フェデレーションサービス構成ウィザードを使用して、新しいフェデレーションサーバーファームの最初のフェデレーションサーバーを構成するには  
  
> [!NOTE]  
> この手順を実行する前に、ドメイン管理者のアクセス許可があること、またはドメイン管理者の資格情報が使用可能であることを確認してください。  
  
1.  サーバー マネージャーの **[ダッシュボード]** ページで、 **[通知]** フラグをクリックし、 **[このサーバーにフェデレーション サービスを構成します]** をクリックします。  
  
    **Active Directory フェデレーション サービス構成ウィザード**が開きます。  
  
2.  **[ようこそ]** ページで、 **[フェデレーション サーバー ファームに最初のフェデレーション サーバーを作成します]** を選択し、 **[次へ]** をクリックします。  
  
3.  **[AD DS への接続]** ページで、このコンピューターが参加している\(Active Directory AD\)ドメインのドメイン管理者アクセス許可を使用してアカウントを指定し、 **[次へ]** をクリックします。  
  
4.  **[サービスのプロパティの指定]** ページで次の操作を実行してから、 **[次へ]** をクリックします。  
  
    -   前の手順で取得した Secure Socket Layer \(SSL\)証明書とキーを含む .pfx ファイルをインポートします。 [手順 2:AD FS](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md)の SSL 証明書を登録します。この証明書を取得して、フェデレーションサーバーとして構成するコンピューターにコピーします。 ウィザードを使用して .pfx ファイルをインポートするには、 **[インポート]** をクリックし、ファイルの場所を参照します。 メッセージが表示されたら、.pfx ファイルのパスワードを入力します。  
  
    -   フェデレーションサービスの名前を指定します。 たとえば、 **fs.contoso.com**のようになります。 この名前は、証明書のサブジェクトまたはサブジェクト代替名のいずれかと一致する必要があります。  
  
    -   フェデレーションサービスの表示名を指定します。 たとえば、 **Contoso Corporation**とします。 ユーザーには、Active Directory フェデレーションサービス (AD FS) \(AD FS\)サインイン\-ページでこの名前が表示されます。  
  
5.  **[サービスアカウントの指定]** ページで、サービスアカウントを指定します。 既存のグループの管理されたサービスアカウント\(gMSA\)を作成または使用するか、既存のドメインユーザーアカウントを使用することができます。 新しい gMSA アカウントを作成するオプションを選択した場合は、新しいアカウントの名前を指定します。 既存の gMSA アカウントまたはドメインアカウントを使用するオプションを選択した場合は、 **[選択]** をクリックしてアカウントを選択します。  
  
    > [!NOTE]  
    > GMSA アカウントを使用する利点は、自動\-ネゴシエートパスワード更新機能です。  
  
    > [!WARNING]  
    > GMSA アカウントを使用する場合は、Windows Server 2012 オペレーティングシステムを実行している環境内に少なくとも1つのドメインコントローラーが必要です。  
    >   
    > GMSA オプションが無効になっていて、 **KDS ルートキーが設定されていないためにグループの管理されたサービスアカウントが使用できない**などのエラーメッセージが表示された場合は、ドメインで次の Windows PowerShell コマンドを実行して、ドメインで gMSA を有効にすることができます。Active Directory ドメインで Windows Server 2012 以降を実行しているコントローラー: `Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`。 ウィザードに戻り、 **[前]** へ をクリックし、 **[次へ]** を\-クリックして **[サービスアカウントの指定]** ページに戻ります。 GMSA オプションが有効になります。 これを選択し、使用する gMSA アカウント名を入力できます。  
  
6.  **[構成データベースの指定]** ページで、AD FS 構成データベースを指定し、 **[次へ]** をクリックします。 Windows Internal database \(WID\)を使用してこのコンピューターにデータベースを作成するか、Microsoft SQL Server の場所とインスタンス名を指定することができます。  
  
    詳細については、次を参照してください。 [、AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)します。  
  
    > [!IMPORTANT]  
    > AD FS ファームを作成し、SQL Server を使用して構成データを保存する場合は、SQL Server 2008 以降のバージョン (SQL Server 2012 や SQL Server 2014 を含む) を使用できます。  
  
7.  **[オプションの確認]** ページで、構成の選択内容を確認し、 **[次へ]** をクリックします。  
  
8.  [前提 **\-条件チェック**の実行] ページで、すべての前提条件の確認が正常に完了したことを確認し、 **[構成]** をクリックします。  
  
9. **[結果]** ページで結果を確認し、構成が正常に完了したかどうかを確認して、 **[フェデレーションサービスの展開を完了するために必要な次の手順]** をクリックします。 詳細については、「 [AD FS のインストールを完了するための次の手順](https://go.microsoft.com/fwlink/p/?LinkId=286704)」を参照してください。 **[閉じる]** をクリックしてウィザードを終了します。  
  
### <a name="BKMK_3"></a>Windows PowerShell を使用して新しいフェデレーションサーバーファームの最初のフェデレーションサーバーを構成するには  
新規または既存の gMSA アカウントまたは既存のドメインユーザーアカウントのいずれかを使用して、新しいフェデレーションサーバーファームを作成できます。  
  
-   **新しい gMSA アカウントを使用して新しいフェデレーションサーバーを作成する場合は、次の手順を実行します。**  
  
    > [!IMPORTANT]  
    > 新しいフェデレーションサーバーファームに最初のフェデレーションサーバーを作成するには、ドメイン管理者のアクセス許可が必要です。  
  
    1.  フェデレーションサーバーとして構成するコンピューターで、必要な SSL 証明書が**ローカル\\コンピューターの My Store**ディレクトリにインポートされていることを確認します。 Windows PowerShell コマンドウィンドウで次のコマンドを実行して、SSL 証明書がインポートされている`dir Cert:\LocalMachine\My`かどうかを確認できます。 証明書は、**ローカル\\コンピューターの My Store**ディレクトリにある拇印によって一覧表示されます。  
  
    2.  ドメインコントローラーで、Windows PowerShell コマンドウィンドウを開き、次のコマンドを実行して、KDS ルートキーがドメイン`Get-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`に作成されているかどうかを確認します。 出力に情報が表示されないように作成されていない場合は、次のコマンドを`Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`実行してキーを作成します。  
  
    3.  フェデレーションサーバーとして構成するコンピューターで、Windows PowerShell コマンドウィンドウを開き、次のコマンドを実行します。  
  
        ```  
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_Name>$  
        ```  
  
        > [!WARNING]  
        > 前のコマンドの最後にある符号が必要です。`$`  
  
        の`<certificate_thumbprint>`値を取得するには`dir Cert:\LocalMachine\My`、を実行し、SSL 証明書の拇印を選択します。 の`<federation_service_name>`値は、フェデレーションサービスの名前 (たとえば、 **fs.contoso.com**) です。  
  
        > [!NOTE]  
        > このコマンドを初めて実行する場合は、 `OverwriteConfiguration`パラメーターを追加します。  
  
        > [!NOTE]  
        > 前のコマンドは、WID ファームを作成します。 SQL Server サーバーファームを作成する場合は、SQL Server のインスタンスが既にインストールされ、動作している必要があります。  
        >   
        > 次のコマンドを使用して、SQL Server のインスタンスを使用する新しいファームに最初のフェデレーションサーバーを作成`Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name?\<SQL_instance_ name>;Integrated Security=True"`できます。 **<\_SQL\_ホスト名 >** は SQL Server を実行しているサーバーの名前です。 **< SQL\_インスタンス\_名 >** は SQL Server のインスタンスの名前です。 SQL Server の既定のインスタンスを使用する場合は、 **sqlconnectionstring**値として "**データ\=ソース\_<\_SQL ホスト名 >;\=統合セキュリティ True**" を使用します。  
  
        > [!IMPORTANT]  
        > AD FS ファームを作成し、SQL Server を使用して構成データを保存する場合は、SQL Server 2012 など、SQL Server 2008 以降のバージョンを使用できます。  
  
-   **既存のドメインユーザーアカウントを使用して新しいフェデレーションサーバーを作成する場合は、次の手順を実行します。**  
  
    1.  フェデレーションサーバーとして構成するコンピューターで、必要な SSL 証明書が**ローカル\\コンピューターの My Store**ディレクトリにインポートされていることを確認します。 Windows PowerShell コマンドウィンドウで次のコマンドを実行して、SSL 証明書がインポートされている`dir Cert:\LocalMachine\My`かどうかを確認できます。 証明書は、**ローカル\\コンピューターの My Store**ディレクトリにある拇印によって一覧表示されます。  
  
    2.  フェデレーションサーバーとして構成するコンピューターで、Windows PowerShell コマンドウィンドウを開き、コマンド`$fscred = Get-Credential`を実行します。 ドメイン\\ユーザー名の形式で、フェデレーションサービスアカウントに使用するドメインユーザーアカウントの資格情報を入力します。  
  
    3.  同じ Windows PowerShell コマンド ウィンドウで、次のコマンドを実行します。  
  
        ```  
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscred  
        ```  
  
        **< 証明書\_の拇印 >** の値を取得する`dir Cert:\LocalMachine\My`には、を実行し、SSL 証明書の拇印を選択します。 **< フェデレーション\_サービス\_名 >** の値は、フェデレーションサービスの名前です。たとえば、fs.contoso.com のようになります。  
  
        > [!NOTE]  
        > このコマンドを初めて実行する場合は、 `OverwriteConfiguration`パラメーターを追加します。  
  
        > [!NOTE]  
        > 前のコマンドは、WID ファームを作成します。 SQL Server ファームを作成する場合は、SQL Server のインスタンスが既にインストールされ、動作している必要があります。  
        >   
        > 次のコマンドを使用して、SQL Server のインスタンスを使用する新しいファームに最初のフェデレーションサーバーを作成`Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"`できます。ここで、 **sql\_ホスト\_名**は SQL Server を実行しているサーバーの名前、 **sqlインスタンス\_名は SQL Server のインスタンスの名前です。 \_** SQL Server の既定のインスタンスを使用する場合は、 **sqlconnectionstring**値として "**データ\=ソース\_<\_SQL ホスト名 >;\=統合セキュリティ True**" を使用します。  
  
        > [!IMPORTANT]  
        > AD FS ファームを作成し、SQL Server を使用して構成データを保存する場合は、SQL Server 2008 以降のバージョン (SQL Server 2012 や SQL Server 2014 を含む) を使用できます。  
  
## <a name="BKMK_2"></a>フェデレーションサーバーを既存のフェデレーションサーバーファームに追加する  
  
> [!IMPORTANT]  
> 手順 3. を完了[していることを確認します。このセクションの手順を](../../ad-fs/deployment/Install-the-AD-FS-Role-Service.md)開始する前に、AD FS の役割サービスをインストールしてください。  
  
> [!IMPORTANT]  
> この手順を実行する前に、有効な SSL サーバー認証証明書を取得していることを確認してください。  
  
### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-the-active-directory-federation-service-configuration-wizard"></a>Active Directory フェデレーションサービス構成ウィザードを使用してフェデレーションサーバーを既存のフェデレーションサーバーファームに追加するには  
  
1.  サーバー マネージャーの **[ダッシュボード]** ページで、 **[通知]** フラグをクリックし、 **[このサーバーにフェデレーション サービスを構成します]** をクリックします。  
  
    **Active Directory フェデレーション サービス構成ウィザード**が開きます。  
  
2.  **[ようこそ]** ページで、フェデレーションサーバー **[ファームにフェデレーションサーバーを追加する]** を選択し、 **[次へ]** をクリックします。  
  
3.  **[AD DS への接続]** ページで、このコンピューターが参加している AD ドメインのドメイン管理者アクセス許可を使用してアカウントを指定し、 **[次へ]** をクリックします。  
  
4.  **[ファームの指定]** ページで、WID を使用するファーム内のプライマリフェデレーションサーバーの名前を指定するか、SQL Server を使用する既存のフェデレーションサーバーファームのデータベースホスト名とデータベースインスタンス名を指定します。  
  
    > [!WARNING]  
    > Windows Server® 2012 R2 では、SQL Server の既定のインスタンスを指定するための回避策があります。 この回避策は、ユーザーインターフェイスを使用しないことです。 代わりに、「」の手順に従って、Windows PowerShell を使用して[新しいフェデレーションサーバーファームの最初のフェデレーションサーバーを構成](Configure-a-Federation-Server.md#BKMK_3)します。  
  
    > [!IMPORTANT]  
    > AD FS ファームを作成し、SQL Server を使用して構成データを保存する場合は、SQL Server 2012 など、SQL Server 2008 以降のバージョンを使用できます。  
  
5.  **[Ssl 証明書の指定]** ページで、以前に取得した ssl 証明書とキーを含む .pfx ファイルをインポートします。 この証明書は必須のサービス認証証明書です。 [手順 2:AD FS](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md)の SSL 証明書を登録します。この証明書を取得し、フェデレーションサーバーとして構成するコンピューターにコピーします。 ウィザードを使用して .pfx ファイルをインポートするには、 **[インポート]** をクリックし、ファイルの場所を参照します。 メッセージが表示されたら、.pfx ファイルのパスワードを入力します。  
  
6.  **[サービスアカウントの指定]** ページで、ファームに最初のフェデレーションサーバーを作成したときに構成したものと同じサービスアカウントを指定します。 既存のグループの管理されたサービスアカウントまたは既存のドメインユーザーアカウントを使用できます。  
  
    > [!IMPORTANT]  
    > 指定するアカウントは、このファームのプライマリフェデレーションサーバーで使用されていたアカウントと同じアカウントである必要があります。  
  
7.  **[オプションの確認]** ページで、構成の選択内容を確認し、 **[次へ]** をクリックします。  
  
8.  [前提 **\-条件チェック**の実行] ページで、すべての前提条件の確認が正常に完了したことを確認し、 **[構成]** をクリックします。  
  
9. **[結果]** ページで結果を確認し、構成が正常に完了したかどうかを確認して、 **[フェデレーションサービスの展開を完了するために必要な次の手順]** をクリックします。 詳細については、「 [AD FS のインストールを完了するための次の手順](https://go.microsoft.com/fwlink/p/?LinkId=286704)」を参照してください。 **[閉じる]** をクリックしてウィザードを終了します。  
  
### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-windows-powershell"></a>Windows PowerShell を使用して既存のフェデレーションサーバーファームにフェデレーションサーバーを追加するには  
既存の gMSA アカウントまたは既存のドメインユーザーアカウントを使用して、既存のファームにフェデレーションサーバーを追加できます。  
  
-   既存の gMSA アカウントを使用してフェデレーションサーバーをファームに参加させる場合は、次の手順を実行します。  
  
    1.  フェデレーションサーバーとして構成するコンピューターで、必要な SSL 証明書が**ローカル\\コンピューターの My Store**ディレクトリにインポートされていることを確認します。 Windows PowerShell コマンドウィンドウで次のコマンドを実行して、SSL 証明書がインポートされている`dir Cert:\LocalMachine\My`かどうかを確認できます。 証明書は、**ローカル\\コンピューターの My Store**ディレクトリにある拇印によって一覧表示されます。  
  
    2.  フェデレーションサーバーとして構成するコンピューターで、Windows PowerShell コマンドウィンドウを開き、次のコマンドを実行します。  
  
        ```  
        Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>  
        ```  
  
        `<domain>\<GMSA_name>`は、AD ドメインと、そのドメインの gMSA アカウントの名前です。 `<first_federation_server_hostname>`は、この既存のファーム内のプライマリフェデレーションサーバーのホスト名です。  
  
        の`<certificate_thumbprint>`値を取得するには、 `dir Cert:\LocalMachine\My`前の手順でを実行します。  
  
        > [!NOTE]  
        > このコマンドを初めて実行する場合は、 `OverwriteConfiguration`パラメーターを追加します。  
  
        > [!NOTE]  
        > 前のコマンドは、WID ファームノードを作成します。 SQL Server を実行しているコンピューターのサーバーファームノードを作成する場合は、SQL Server のインスタンスが既にインストールされ、動作している必要があります。  
        >   
        > 次のコマンドを使用して、SQL Server のインスタンスを使用している既存のファームにフェデレーションサーバーを`Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"`追加できます。ここで、 **sql\_ホスト\_名**は SQL Server を実行しているサーバーの名前、 **sqlインスタンス\_名は SQL Server のインスタンスの名前です。 \_** SQL Server の既定のインスタンスを使用する場合は、 **sqlconnectionstring**値として "**データ\=ソース\_<\_SQL ホスト名 >;\=統合セキュリティ True**" を使用します。  
  
        > [!IMPORTANT]  
        > AD FS ファームを作成し、SQL Server を使用して構成データを保存する場合は、SQL Server 2008 以降のバージョン (SQL Server 2012 や SQL Server 2014 を含む) を使用できます。  
  
-   既存のドメインユーザーアカウントを使用してフェデレーションサーバーをファームに参加させる場合は、次の手順を実行します。  
  
    1.  フェデレーションサーバーとして構成するコンピューターで、Windows PowerShellcommand ウィンドウを開き、コマンド`$fscred = get-credential`を実行します。 ドメイン\\ユーザー名の形式で、フェデレーションサービスアカウントに使用するドメインユーザーアカウントの資格情報を入力します。  
  
    2.  フェデレーションサーバーとして構成するコンピューターで、必要な SSL 証明書が**ローカル\\コンピューターの My Store**ディレクトリにインポートされていることを確認します。 Windows PowerShellcommand ウィンドウで次のコマンドを実行して、SSL 証明書がインポートされている`dir Cert:\LocalMachine\My`かどうかを確認できます。 証明書は、**ローカル\\コンピューターの My Store**ディレクトリにある拇印によって一覧表示されます。  
  
    3.  同じ Windows PowerShell コマンドウィンドウで、次のコマンドを実行します。  
  
        ```  
        Add-AdfsFarmNode -ServiceAccountCredential $fscred -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>  
        ```  
  
        > [!NOTE]  
        > このコマンドを初めて実行する場合は、 `OverwriteConfiguration`パラメーターを追加します。  
  
        > [!NOTE]  
        > 前のコマンドは、WID ファームノードを作成します。 SQL Server を実行しているコンピューターのサーバーファームノードを作成する場合は、SQL Server のインスタンスが既にインストールされ、動作している必要があります。 SQL Server のインスタンスを使用して、既存のファームにフェデレーションサーバーを追加するには、次の`Add-AdfsFarmNode -ServiceAccountCredential $fscred -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"`コマンドを使用します。ここで、 **\_SQL ホスト\_名**は SQL Server のインスタンスが実行されているサーバーの名前です。**SQL\_インスタンス\_名**は SQL Server のインスタンスの名前です。 SQL Server の既定のインスタンスを使用する場合は、 **sqlconnectionstring**値として "**データ\=ソース\_<\_SQL ホスト名 >;\=統合セキュリティ True**" を使用します。  
  
        > [!IMPORTANT]  
        > AD FS ファームを作成し、SQL Server を使用して構成データを保存する場合は、SQL Server 2008 以降のバージョン (SQL Server 2012 や SQL Server 2014 を含む) を使用できます。  
  
## <a name="see-also"></a>関連項目 

[AD FS 展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 展開ガイド](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[フェデレーション サーバー ファームの展開](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

