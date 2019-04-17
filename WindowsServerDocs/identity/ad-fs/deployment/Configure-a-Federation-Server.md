---
ms.assetid: 434fd617-373a-405e-bae4-da324ea83efc
title: "Windows Server 2012 R2 AD FS 展開ガイドします。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 13ce514dc5f3f70217a26c898cde6fe24d4967c6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="configure-a-federation-server"></a>フェデレーション サーバーを構成します。

>適用対象: Windows Server 2016、Windows Server 2012 R2

お使いのコンピューターに、Active Directory フェデレーション サービス \(AD FS\) 役割サービスをインストールした後は、フェデレーション サーバーになるには、このコンピューターを構成する準備ができたらします。 次のいずれかの操作を行うことができます。  
  
-   [新しいフェデレーション サーバー ファームに最初のフェデレーション サーバーを構成します。](assetId:///e340cf8f-acf3-4cba-8135-a9353b85e714#BKMK_1)  
  
-   [既存のフェデレーション サーバー ファームにフェデレーション サーバーを追加します。](assetId:///e340cf8f-acf3-4cba-8135-a9353b85e714#BKMK_2)  
  
## <a name="BKMK_1"></a>新しいフェデレーション サーバー ファームに最初のフェデレーション サーバーを構成します。  
  
### <a name="to-configure-the-first-federation-server-in-a-new-federation-server-farm-by-using-the-active-directory-federation-service-configuration-wizard"></a>Active Directory フェデレーション サービス構成ウィザードを使用して、新しいフェデレーション サーバー ファームに最初のフェデレーション サーバーを構成するには  
  
> [!NOTE]  
> ドメイン管理者のアクセス許可を持っているか、この手順を実行する前にドメイン管理者の資格情報が利用可能ながあることを確認します。  
  
1.  サーバー マネージャーに**ダッシュ ボード**] ページで [、**通知**フラグを設定すると、クリックして**サーバーで、フェデレーション サービスを構成**します。  
  
    **Active Directory フェデレーション サービス構成ウィザード**が開きます。  
  
2.  **ようこそ**] ページで、[**フェデレーション サーバー ファームに最初のフェデレーション サーバーを作成する**、] をクリックし、**[次へ]**します。  
  
3.  **AD DS への接続**] ページで、クリックしてこのコンピューターが参加している Active Directory \(AD\) ドメインのドメイン管理者のアクセス許可を使用して、アカウントを指定**次**します。  
  
4.  **サービスのプロパティの指定**] ページで、次の操作ををクリックして**次**:  
  
    -   Secure Socket Layer \(SSL\) 証明書と前に入手したキーを含む .pfx ファイルをインポートします。 [手順 2: AD FS の SSL 証明書を登録](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md)、この証明書を取得しているフェデレーション サーバーとして構成するコンピューターにコピーします。 ウィザードを使用して、.pfx ファイルをインポートする] をクリックして**インポート**、ファイルの場所を参照します。 入力を求められたら、.pfx ファイルのパスワードを入力します。  
  
    -   フェデレーション サービスの名前を指定します。 たとえば、**fs.contoso.com**します。この名前は、サブジェクトまたはサブジェクトの別名で証明書のいずれかに一致する必要があります。  
  
    -   フェデレーション サービスの表示名を指定します。 たとえば、**Contoso Corporation**します。 ユーザーは、Active Directory フェデレーション サービス \(AD FS\) sign\ でこの名前を参照してください-] ページでします。  
  
5.  **サービス アカウントの指定**] ページで、サービス アカウントを指定します。 作成する既存のグループ管理されたサービス アカウント \(gMSA\) を使用して既存のドメイン ユーザー アカウントを使用するか。 新しい gMSA アカウントを作成するオプションを選択する場合は、新しいアカウントの名前を指定します。 既存の gMSA またはドメイン アカウントを使用するオプションを選択する場合はクリックして**選択**にアカウントを選択します。  
  
    > [!NOTE]  
    > GMSA アカウントを使用する利点は、パスワードの自動ネゴシエート更新機能です。  
  
    > [!WARNING]  
    > GMSA アカウントを使用する場合は、Windows Server 2012 オペレーティング システムを実行している環境で、少なくとも 1 つのドメイン コントローラーが必要です。  
    >   
    > GMSA オプションが無効になっている場合など、エラー メッセージを参照してください**KDS ルート キーが設定されていないために、グループ管理サービス アカウントに使用されていない**、ドメイン コントローラーは、Windows Server 2012 を実行またはそれ以降は、Active Directory ドメイン内に、次の Windows PowerShell コマンドを実行して、ドメインに gMSA を有効にすることができます:`Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`します。 ウィザードに戻り値] をクリックして**前**、] をクリックし、**[次へ]**に再度-入力、**サービス アカウントの指定**ページ。 GMSA オプションが有効にするようになりました必要があります。 これを選択し、使用する gMSA アカウント名を入力できます。  
  
6.  **構成データベースの指定**] ページで、AD FS 構成データベースを指定してをクリックして**次**します。 Windows Internal Database \(WID\) を使用してこのコンピューターにデータベースを作成するか、場所と Microsoft SQL Server のインスタンス名を指定することができます。  
  
    詳細については、次を参照してください。[AD FS 構成データベースの役割](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)します。  
  
    > [!IMPORTANT]  
    > AD FS ファームを作成して構成データを格納する SQL Server を使用する場合は、SQL Server 2008 および SQL Server 2012、SQL Server 2014 などの新しいバージョンを使用することができます。  
  
7.  **オプションの確認**] ページで、構成の選択を確認してをクリックして**次**します。  
  
8.  **ファイル必要条件のチェック**] ページで、すべての前提条件チェックが正常に完了したことを確認] をクリックして**構成**します。  
  
9. **結果**] ページで、結果を確認し、構成が正常に完了するかどうかを確認してをクリックして**フェデレーション サービスの展開を完了するために必要な次の手順**します。 詳細については、次を参照してください。[AD FS のインストールを完了するため次の手順](https://go.microsoft.com/fwlink/p/?LinkId=286704)します。 をクリックして**閉じる**ウィザードを終了します。  
  
### <a name="BKMK_3"></a>Windows PowerShell を使用して、新しいフェデレーション サーバー ファームに最初のフェデレーション サーバーを構成するには  
新規または既存の gMSA アカウントまたは既存のドメイン ユーザー アカウントを使用して、新しいフェデレーション サーバー ファームを作成できます。  
  
-   **新しい gMSA アカウントを使用して、新しいフェデレーション サーバーを作成する場合は、次の操作を行います。**  
  
    > [!IMPORTANT]  
    > 新しいフェデレーション サーバー ファームに最初のフェデレーション サーバーを作成するドメイン管理者のアクセス許可が必要です。  
  
    1.  フェデレーション サーバーとして構成する場合、コンピューター上に必要な SSL 証明書がインポートされていることを確認して、**ローカル Computer\\My ストア**ディレクトリ。 Windows PowerShell コマンド ウィンドウで、次のコマンドを実行して、SSL 証明書がインポートされているかどうかを確認できます:`dir Cert:\LocalMachine\My`します。 拇印で証明書が表示されている、**ローカル Computer\\My ストア**ディレクトリ。  
  
    2.  ドメイン コントローラーで Windows PowerShell コマンド ウィンドウを開くし、ドメイン内、KDS ルート キーが作成されたかどうかを確認するには、次のコマンドを実行します。`Get-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`します。 それが作成されていない情報が表示されます、出力がないように場合、は、キーの作成に次のコマンドを実行します。`Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`します。  
  
    3.  フェデレーション サーバーとして構成する場合、コンピューターで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  
  
        ```  
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_Name>$  
        ```  
  
        > [!WARNING]  
        > `$`前のコマンドの最後にサインインが必要です。  
  
        値を取得する`<certificate_thumbprint>`実行、`dir Cert:\LocalMachine\My`、SSL 証明書の拇印を選択します。 値`<federation_service_name>`、フェデレーション サービスの名前は、たとえば、**fs.contoso.com**します。  
  
        > [!NOTE]  
        > このコマンドを実行する初めてでない場合、追加、`OverwriteConfiguration`パラメーター。  
  
        > [!NOTE]  
        > 前のコマンドでは、WID ファームを作成します。 SQL Server のサーバー ファームを作成する場合は、既にインストールされ、動作の SQL Server のインスタンスが必要です。  
        >   
        > SQL Server のインスタンスを使用する新しいファームに最初のフェデレーション サーバーを作成する、次のコマンドを使用することができます:`Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name?\<SQL_instance_ name>;Integrated Security=True"`場所**< SQL\_Host\_Name >**は、SQL Server を実行しているサーバーの名前と**< SQL\_instance\_name >**は SQL Server のインスタンスの名前です。 SQL Server の既定のインスタンスを使用する場合を使用して、**SQLConnectionString**の値"**データ Source\ < SQL\_Host\_Name > を =; Integrated Security\ = True**"です。  
  
        > [!IMPORTANT]  
        > AD FS ファームを作成して構成データを格納する SQL Server を使用する場合は、SQL Server 2008 および SQL Server 2012 などの新しいバージョンを使用することができます。  
  
-   **既存のドメイン ユーザー アカウントを使用して、新しいフェデレーション サーバーを作成する場合は、次の操作を行います。**  
  
    1.  フェデレーション サーバーとして構成する場合、コンピューター上に必要な SSL 証明書がインポートされていることを確認して、**ローカル Computer\\My ストア**ディレクトリ。 Windows PowerShell コマンド ウィンドウで、次のコマンドを実行して、SSL 証明書がインポートされているかどうかを確認できます:`dir Cert:\LocalMachine\My`します。 拇印で証明書が表示されている、**ローカル Computer\\My ストア**ディレクトリ。  
  
    2.  フェデレーション サーバーとして構成する場合、コンピューター上、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。`$fscred = Get-Credential`します。 形式のドメイン \\ ユーザー名にフェデレーション サービス アカウントを使用するドメイン ユーザー アカウントの資格情報を入力します。  
  
    3.  同じ Windows PowerShell コマンド ウィンドウで、次のコマンドを実行します。  
  
        ```  
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscred  
        ```  
  
        値を取得する**< certificate\_thumbprint >**実行、`dir Cert:\LocalMachine\My`、SSL 証明書の拇印を選択します。 値**< federation\_service\_name >** fs.contoso.com など、フェデレーション サービスの名前です。  
  
        > [!NOTE]  
        > このコマンドを実行する初めてでない場合、追加、`OverwriteConfiguration`パラメーター。  
  
        > [!NOTE]  
        > 前のコマンドでは、WID ファームを作成します。 SQL Server ファームを作成する場合は、既にインストールされ、動作の SQL Server のインスタンスが必要です。  
        >   
        > SQL Server のインスタンスを使用する新しいファームに最初のフェデレーション サーバーを作成する、次のコマンドを使用することができます:`Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"`場所**SQL\_Host\_Name**は、SQL Server を実行しているサーバーの名前と**SQL\_instance\_name**は SQL Server のインスタンスの名前です。 SQL Server の既定のインスタンスを使用する場合を使用して、**SQLConnectionString**の値"**データ Source\ < SQL\_Host\_Name > を =; Integrated Security\ = True**"です。  
  
        > [!IMPORTANT]  
        > AD FS ファームを作成して構成データを格納する SQL Server を使用する場合は、SQL Server 2008 および SQL Server 2012、SQL Server 2014 などの新しいバージョンを使用することができます。  
  
## <a name="BKMK_2"></a>既存のフェデレーション サーバー ファームにフェデレーション サーバーを追加します。  
  
> [!IMPORTANT]  
> 完了したことを確認[手順 3: AD FS 役割サービスをインストール](../../ad-fs/deployment/Install-the-AD-FS-Role-Service.md)、このセクションで、手順のいずれかを開始する前にします。  
  
> [!IMPORTANT]  
> 入手している有効な SSL サーバー認証証明書前に、この手順を完了したことを確認します。  
  
### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-the-active-directory-federation-service-configuration-wizard"></a>Active Directory フェデレーション サービス構成ウィザードを使用して既存のフェデレーション サーバー ファームにフェデレーション サーバーを追加するには  
  
1.  サーバー マネージャーに**ダッシュ ボード**] ページで [、**通知**フラグを設定すると、クリックして**サーバーで、フェデレーション サービスを構成**します。  
  
    **Active Directory フェデレーション サービス構成ウィザード**が開きます。  
  
2.  **ようこそ**] ページで、[**フェデレーション サーバー ファームにフェデレーション サーバーを追加**、] をクリックし、**[次へ]**します。  
  
3.  **AD DS への接続**] ページで、クリックしてこのコンピューターが参加している AD ドメインのドメイン管理者のアクセス許可を使用して、アカウントを指定**次**します。  
  
4.  **指定ファーム**ページで、WID を使用しているファーム内のプライマリ フェデレーション サーバーの名前を指定するか、データベースのホスト名と SQL Server を使用する既存のフェデレーション サーバー ファームのデータベースのインスタンス名を指定します。  
  
    > [!WARNING]  
    > Windows Server® 2012 R2 では、SQL Server の既定のインスタンスを指定する回避策はします。 回避策は、ユーザー インターフェイスを使用しないようにします。 代わりに、」の手順を使用して[を Windows PowerShell を使用して、新しいフェデレーション サーバー ファームに最初のフェデレーション サーバーを構成する](Configure-a-Federation-Server.md#BKMK_3)します。  
  
    > [!IMPORTANT]  
    > AD FS ファームを作成して構成データを格納する SQL Server を使用する場合は、SQL Server 2008 および SQL Server 2012 などの新しいバージョンを使用することができます。  
  
5.  **SSL 証明書の指定**] ページで、SSL 証明書と以前に入手したキーを含む .pfx ファイルをインポートします。 この証明書は、必要なサービスの認証証明書です。 [手順 2: AD FS の SSL 証明書を登録](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md)、この証明書を取得してフェデレーション サーバーとして構成するコンピューターにコピーします。 ウィザードを使用して、.pfx ファイルをインポートする] をクリックして**インポート**し、ファイルの場所を参照します。 入力を求められたら、.pfx ファイルのパスワードを入力します。  
  
6.  **サービス アカウントの指定**ページで、ファーム内の最初のフェデレーション サーバーを作成したときに構成したものと同じサービス アカウントを指定します。 既存のグループの管理されたサービス アカウントまたは既存のドメイン ユーザー アカウントを使用することができます。  
  
    > [!IMPORTANT]  
    > 指定したアカウントは、このファーム内のプライマリ フェデレーション サーバーで使用されていたアカウントと同じアカウントである必要があります。  
  
7.  **オプションの確認**] ページで、構成の選択を確認してをクリックして**次**します。  
  
8.  **ファイル必要条件のチェック**] ページで、すべての前提条件チェックが正常に完了したことを確認] をクリックして**構成**します。  
  
9. **結果**] ページで、結果を確認し、構成が正常に完了するかどうかを確認してをクリックして**フェデレーション サービスの展開を完了するために必要な次の手順**します。 詳細については、次を参照してください。[AD FS のインストールを完了するため次の手順](https://go.microsoft.com/fwlink/p/?LinkId=286704)します。 をクリックして**閉じる**ウィザードを終了します。  
  
### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-windows-powershell"></a>Windows PowerShell を使用して既存のフェデレーション サーバー ファームにフェデレーション サーバーを追加するには  
既存の gMSA アカウントまたは既存のドメイン ユーザー アカウントを使用して、既存のファームにフェデレーション サーバーを追加できます。  
  
-   既存の gMSA アカウントを使用してフェデレーション サーバー ファームへの参加する場合は、次の操作を行います。  
  
    1.  フェデレーション サーバーとして構成する場合、コンピューター上に必要な SSL 証明書がインポートされていることを確認して、**ローカル Computer\\My ストア**ディレクトリ。 Windows PowerShell コマンド ウィンドウで、次のコマンドを実行して、SSL 証明書がインポートされているかどうかを確認できます:`dir Cert:\LocalMachine\My`します。 拇印で証明書が表示されている、**ローカル Computer\\My ストア**ディレクトリ。  
  
    2.  フェデレーション サーバーとして構成する場合、コンピューターで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  
  
        ```  
        Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>  
        ```  
  
        `<domain>\<GMSA_name>` AD ドメインとそのドメイン内の gMSA アカウントの名前です。 `<first_federation_server_hostname>` この既存のファーム内のプライマリ フェデレーション サーバーのホスト名です。  
  
        値を取得する`<certificate_thumbprint>`を実行して`dir Cert:\LocalMachine\My`前の手順でします。  
  
        > [!NOTE]  
        > このコマンドを実行する初めてでない場合、追加、`OverwriteConfiguration`パラメーター。  
  
        > [!NOTE]  
        > 前のコマンドでは、WID ファーム ノードを作成します。 SQL Server を実行しているコンピューターのサーバーのファーム ノードを作成する場合は、既にインストールされ、動作の SQL Server のインスタンスが必要です。  
        >   
        > SQL Server のインスタンスを使用している既存のファームにフェデレーション サーバーを追加する、次のコマンドを使用することができます:`Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"`場所**SQL\_Host\_Name**は、SQL Server を実行しているサーバーの名前と**SQL\_instance\_name**は SQL Server のインスタンスの名前です。 SQL Server の既定のインスタンスを使用する場合を使用して、**SQLConnectionString**の値"**データ Source\ < SQL\_Host\_Name > を =; Integrated Security\ = True**"です。  
  
        > [!IMPORTANT]  
        > AD FS ファームを作成して構成データを格納する SQL Server を使用する場合は、SQL Server 2008 および SQL Server 2012、SQL Server 2014 などの新しいバージョンを使用することができます。  
  
-   既存のドメイン ユーザー アカウントを使用してフェデレーション サーバー ファームへの参加する場合は、次の操作を行います。  
  
    1.  フェデレーション サーバーとして構成する場合、コンピューターで、Windows PowerShellcommand ウィンドウを開き、次のコマンドを実行します。`$fscred = get-credential`します。 形式のドメイン \\ ユーザー名にフェデレーション サービス アカウントを使用するドメイン ユーザー アカウントの資格情報を入力します。  
  
    2.  フェデレーション サーバーとして構成する場合、コンピューター上に必要な SSL 証明書がインポートされていることを確認して、**ローカル Computer\\My ストア**ディレクトリ。 Windows PowerShellcommand] ウィンドウで、次のコマンドを実行して、SSL 証明書がインポートされているかどうかを確認できます:`dir Cert:\LocalMachine\My`します。 拇印で証明書が表示されている、**ローカル Computer\\My ストア**ディレクトリ。  
  
    3.  同じ Windows PowerShell コマンド ウィンドウで、次のコマンドを実行します。  
  
        ```  
        Add-AdfsFarmNode -ServiceAccountCredential $fscred -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>  
        ```  
  
        > [!NOTE]  
        > このコマンドを実行する初めてでない場合、追加、`OverwriteConfiguration`パラメーター。  
  
        > [!NOTE]  
        > 前のコマンドでは、WID ファーム ノードを作成します。 SQL Server を実行しているコンピューターのサーバーのファーム ノードを作成する場合は、既にインストールされ、動作の SQL Server のインスタンスが必要です。 SQL Server のインスタンスを使用して、既存のファームにフェデレーション サーバーを追加する、次のコマンドを使用することができます:`Add-AdfsFarmNode -ServiceAccountCredential $fscred -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"`場所**SQL\_Host\_Name**は、SQL Server のインスタンスが実行されているサーバーの名前と**SQL\_instance\_name**は SQL Server のインスタンスの名前です。 SQL Server の既定のインスタンスを使用する場合を使用して、**SQLConnectionString**の値"**データ Source\ < SQL\_Host\_Name > を =; Integrated Security\ = True**"です。  
  
        > [!IMPORTANT]  
        > AD FS ファームを作成して構成データを格納する SQL Server を使用する場合は、SQL Server 2008 および SQL Server 2012、SQL Server 2014 などの新しいバージョンを使用することができます。  
  
## <a name="see-also"></a>参照してください。 

[AD FS の展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 展開ガイドします。](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[フェデレーション サーバー ファームを展開します。](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

