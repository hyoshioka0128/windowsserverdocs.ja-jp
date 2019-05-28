---
ms.assetid: 434fd617-373a-405e-bae4-da324ea83efc
title: Windows Server 2012 R2 AD FS の展開ガイド
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d2f597994aa74f453903e09f7d3eefd83f26faba
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192268"
---
# <a name="configure-a-federation-server"></a>フェデレーション サーバーを構成する

Active Directory フェデレーション サービスをインストールした後\(AD FS\)役割サービスをこのコンピューターをフェデレーション サーバーを構成する準備がコンピューターにします。 次のいずれかの操作を行うことができます。  
  
-   [新しいフェデレーション サーバー ファーム内の最初のフェデレーション サーバーを構成します。](assetId:///e340cf8f-acf3-4cba-8135-a9353b85e714#BKMK_1)  
  
-   [既存のフェデレーション サーバー ファームにフェデレーション サーバーを追加します。](assetId:///e340cf8f-acf3-4cba-8135-a9353b85e714#BKMK_2)  
  
## <a name="BKMK_1"></a>新しいフェデレーション サーバー ファーム内の最初のフェデレーション サーバーを構成します。  
  
### <a name="to-configure-the-first-federation-server-in-a-new-federation-server-farm-by-using-the-active-directory-federation-service-configuration-wizard"></a>Active Directory フェデレーション サービスの構成ウィザードを使用して、新しいフェデレーション サーバー ファームで最初のフェデレーション サーバーを構成するには  
  
> [!NOTE]  
> ドメイン管理者のアクセス許可を持っているか、この手順を実行する前にドメイン管理者の資格情報が使用可能ながあることを確認します。  
  
1.  サーバー マネージャーの **[ダッシュボード]** ページで、 **[通知]** フラグをクリックし、 **[このサーバーにフェデレーション サービスを構成します]** をクリックします。  
  
    **Active Directory フェデレーション サービス構成ウィザード**が開きます。  
  
2.  **[ようこそ]** ページで、 **[フェデレーション サーバー ファームに最初のフェデレーション サーバーを作成します]** を選択し、 **[次へ]** をクリックします。  
  
3.  **AD DS への接続** ページで、Active Directory のドメイン管理者のアクセス許可を使用してアカウントを指定\(AD\)クリックしてこのコンピューターが参加しているドメイン **次へ** .  
  
4.  **[サービスのプロパティの指定]** ページで次の操作を実行してから、 **[次へ]** をクリックします。  
  
    -   Secure Socket Layer を含む .pfx ファイルをインポート\(SSL\)証明書と以前取得したキー。 [手順 2。AD FS の SSL 証明書を登録](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md)、この証明書を取得して、フェデレーション サーバーとして構成するコンピューターにコピーします。 ウィザードを使用して .pfx ファイルをインポートするには、次のようにクリックします。**インポート**、し、ファイルの場所を参照します。 求められたら、.pfx ファイルのパスワードを入力します。  
  
    -   フェデレーション サービスの名前を指定します。 たとえば、 **fs.contoso.com**します。 この名前は、サブジェクトまたは証明書のサブジェクト代替名のいずれかに一致する必要があります。  
  
    -   フェデレーション サービスの表示名を指定します。 たとえば、 **Contoso Corporation**します。 ユーザーは、Active Directory フェデレーション サービスでこの名前を参照してください\(AD FS\)サインオン\-ページ。  
  
5.  **サービス アカウントの指定** ページで、サービス アカウントを指定します。 作成するか、既存のグループ管理サービス アカウントを使用することができます\(gMSA\)または既存のドメイン ユーザー アカウントを使用します。 新しい gMSA アカウントを作成するオプションを選択した場合は、新しいアカウントの名前を指定します。 既存の gMSA またはドメイン アカウントを使用するオプションを選択する場合はクリックして**選択**アカウントを選択します。  
  
    > [!NOTE]  
    > GMSA アカウントを使用する利点は、自動\-パスワード更新機能をネゴシエートします。  
  
    > [!WARNING]  
    > GMSA アカウントを使用する場合は、Windows Server 2012 オペレーティング システムを実行している環境内に少なくとも 1 つのドメイン コント ローラーが必要です。  
    >   
    > GMSA オプションが無効になっているし、エラー メッセージを表示する場合**KDS ルート キーが設定されていないためグループ管理サービス アカウントが使用できない**、次の Windows を実行して、ドメインで gMSA を有効にしたことができますドメイン コント ローラーは、Windows Server 2012 を実行または後で、Active Directory ドメインでの PowerShell コマンド:`Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`します。 ウィザードに戻り値をクリックして**前**、順にクリックします**次**に re\-入力、**サービス アカウントの指定**ページ。 GMSA オプションが有効にするようになりましたする必要があります。 これを選択し、使用する gMSA アカウント名を入力できます。  
  
6.  **構成データベースの指定**ページで、AD FS 構成データベースを指定してをクリックし、**次**します。 Windows Internal Database を使用してこのコンピューターにデータベースを作成する\(WID\)場所と Microsoft SQL Server のインスタンス名を指定することができます。  
  
    詳細については、「 [The Role of the AD FS Configuration Database](../../ad-fs/technical-reference/The-Role-of-the-AD-FS-Configuration-Database.md)」を参照してください。  
  
    > [!IMPORTANT]  
    > AD FS ファームを作成して構成データを格納する SQL Server を使用する場合は、SQL Server 2008 および SQL Server 2012、SQL Server 2014 などの新しいバージョンを使用することができます。  
  
7.  **[オプションの確認]** ページで、構成の選択内容を確認し、 **[次へ]** をクリックします。  
  
8.  **前\-必要条件のチェック** ページで、すべての前提条件チェックが正常に完了、ことを確認 をクリックし、**構成**します。  
  
9. **結果**ページで、結果を確認および構成が正常に完了するかどうかを確認し、順にクリックします**フェデレーション サービス展開を完了に必要な次の手順**します。 詳細については、次を参照してください。 [AD FS のインストールを完了するため次のステップ](https://go.microsoft.com/fwlink/p/?LinkId=286704)します。 **[閉じる]** をクリックしてウィザードを終了します。  
  
### <a name="BKMK_3"></a>Windows PowerShell を使用して新しいフェデレーション サーバー ファームで最初のフェデレーション サーバーを構成するには  
新規または既存の gMSA アカウントまたは既存のドメイン ユーザー アカウントを使用して、新しいフェデレーション サーバー ファームを作成できます。  
  
-   **新しい gMSA アカウントを使用して、新しいフェデレーション サーバーを作成する場合は、次の操作を行います。**  
  
    > [!IMPORTANT]  
    > 新しいフェデレーション サーバー ファームで最初のフェデレーション サーバーを作成するドメイン管理者のアクセス許可が必要です。  
  
    1.  フェデレーション サーバーとして構成するコンピューター上に必要な SSL 証明書がインポートされていることを確認します、**ローカル コンピューター\\マイ ストア**ディレクトリ。 Windows PowerShell コマンド ウィンドウで、次のコマンドを実行して、SSL 証明書がインポートされているかどうかを確認できます:`dir Cert:\LocalMachine\My`します。 証明書の拇印に表示されて、**ローカル コンピューター\\マイ ストア**ディレクトリ。  
  
    2.  ドメイン コント ローラーで、Windows PowerShell コマンド ウィンドウを開くし、ドメイン内、KDS ルート キーが作成されたかどうかを確認するには、次のコマンドを実行します。`Get-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`します。 それが作成されていない場合、出力が情報を表示しないように、キーを作成するには、次のコマンドを実行します。`Add-KdsRootKey –EffectiveTime (Get-Date).AddHours(-10)`します。  
  
    3.  をフェデレーション サーバーとして構成するコンピューターに、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  
  
        ```  
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_Name>$  
        ```  
  
        > [!WARNING]  
        > `$`前のコマンドの最後にサインインが必要です。  
  
        値を取得する`<certificate_thumbprint>`実行、 `dir Cert:\LocalMachine\My`、SSL 証明書のサムプリントを選択します。 値`<federation_service_name>`、フェデレーション サービスの名前は、たとえば、 **fs.contoso.com**します。  
  
        > [!NOTE]  
        > このコマンドを実行する最初の時間でない場合、追加、`OverwriteConfiguration`パラメーター。  
  
        > [!NOTE]  
        > 前のコマンドは、WID ファームを作成します。 SQL Server のサーバー ファームを作成する場合は、既にインストールされていて、SQL Server のインスタンスが必要です。  
        >   
        > SQL Server のインスタンスを使用する新しいファームで最初のフェデレーション サーバーを作成する次のコマンドを使用することができます:`Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name?\<SQL_instance_ name>;Integrated Security=True"`場所 **< SQL\_ホスト\_名 >** どの sql server の名前を指定しますサーバーが実行されていると **< SQL\_インスタンス\_名 >** SQL Server のインスタンスの名前を指定します。 SQL Server の既定のインスタンスを使用する場合は、使用、 **SQLConnectionString**の値"**データ ソース\=< SQL\_ホスト\_名 >; Integrated Security\=True**".  
  
        > [!IMPORTANT]  
        > AD FS ファームを作成し、SQL Server を使用して構成データを保存する場合は、SQL Server 2012 など、SQL Server 2008 以降のバージョンを使用できます。  
  
-   **既存のドメイン ユーザー アカウントを使用して、新しいフェデレーション サーバーを作成する場合は、次の操作を行います。**  
  
    1.  フェデレーション サーバーとして構成するコンピューター上に必要な SSL 証明書がインポートされていることを確認します、**ローカル コンピューター\\マイ ストア**ディレクトリ。 Windows PowerShell コマンド ウィンドウで、次のコマンドを実行して、SSL 証明書がインポートされているかどうかを確認できます:`dir Cert:\LocalMachine\My`します。 証明書の拇印に表示されて、**ローカル コンピューター\\マイ ストア**ディレクトリ。  
  
    2.  をフェデレーション サーバーとして構成するコンピューターに Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します:`$fscred = Get-Credential`します。 形式のドメインのフェデレーション サービス アカウントを使用するドメイン ユーザー アカウントの資格情報を入力\\ユーザー名。  
  
    3.  同じ Windows PowerShell コマンド ウィンドウで、次のコマンドを実行します。  
  
        ```  
        Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscred  
        ```  
  
        値を取得する **< 証明書\_拇印 >** 実行、 `dir Cert:\LocalMachine\My`、SSL 証明書のサムプリントを選択します。 値 **< フェデレーション\_サービス\_名 >** fs.contoso.com など、フェデレーション サービスの名前を指定します。  
  
        > [!NOTE]  
        > このコマンドを実行する最初の時間でない場合、追加、`OverwriteConfiguration`パラメーター。  
  
        > [!NOTE]  
        > 前のコマンドは、WID ファームを作成します。 SQL Server ファームを作成する場合は、既にインストールされていて、SQL Server のインスタンスが必要です。  
        >   
        > SQL Server のインスタンスを使用する新しいファームで最初のフェデレーション サーバーを作成する次のコマンドを使用することができます:`Install-AdfsFarm -CertificateThumbprint <certificate_thumbprint> -FederationServiceName <federation_service_name> -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"`場所**SQL\_ホスト\_名前**SQL Server がサーバーの名前を指定しますを実行していると**SQL\_インスタンス\_名前**SQL Server のインスタンスの名前を指定します。 SQL Server の既定のインスタンスを使用する場合は、使用、 **SQLConnectionString**の値"**データ ソース\=< SQL\_ホスト\_名 >; Integrated Security\=True**".  
  
        > [!IMPORTANT]  
        > AD FS ファームを作成して構成データを格納する SQL Server を使用する場合は、SQL Server 2008 および SQL Server 2012、SQL Server 2014 などの新しいバージョンを使用することができます。  
  
## <a name="BKMK_2"></a>既存のフェデレーション サーバー ファームにフェデレーション サーバーを追加します。  
  
> [!IMPORTANT]  
> 完了したことを確認します。[手順 3。AD FS 役割サービスをインストール](../../ad-fs/deployment/Install-the-AD-FS-Role-Service.md)このセクションでは、手順のいずれかを開始する前に、します。  
  
> [!IMPORTANT]  
> 取得していること、有効な SSL サーバー認証証明書この手順を完了する前に確認します。  
  
### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-the-active-directory-federation-service-configuration-wizard"></a>Active Directory フェデレーション サービスの構成ウィザードを使用して既存のフェデレーション サーバー ファームにフェデレーション サーバーを追加するには  
  
1.  サーバー マネージャーの **[ダッシュボード]** ページで、 **[通知]** フラグをクリックし、 **[このサーバーにフェデレーション サービスを構成します]** をクリックします。  
  
    **Active Directory フェデレーション サービス構成ウィザード**が開きます。  
  
2.  **へようこそ**  ページで、**フェデレーション サーバー ファームにフェデレーション サーバーを追加**、順にクリックします**次**します。  
  
3.  **AD DS への接続** ページで、クリックしてこのコンピューターが参加している AD ドメインのドメイン管理者のアクセス許可を使用してアカウントを指定**次**します。  
  
4.  **Specify Farm**ページで、WID を使用するファーム内のプライマリ フェデレーション サーバーの名前を指定するか、データベースのホスト名と SQL Server を使用する既存のフェデレーション サーバー ファームのデータベース インスタンスの名前を指定します。  
  
    > [!WARNING]  
    > Windows Server® 2012 R2、SQL Server の既定のインスタンスを指定する回避策は。 回避策では、ユーザー インターフェイスを使用します。 代わりに、手順を使用して、 [Windows PowerShell を使用して新しいフェデレーション サーバー ファームで最初のフェデレーション サーバーを構成する](Configure-a-Federation-Server.md#BKMK_3)します。  
  
    > [!IMPORTANT]  
    > AD FS ファームを作成し、SQL Server を使用して構成データを保存する場合は、SQL Server 2012 など、SQL Server 2008 以降のバージョンを使用できます。  
  
5.  **SSL 証明書の指定** ページで、SSL 証明書と以前に取得したキーを含む .pfx ファイルをインポートします。 この証明書は必須のサービス認証証明書です。 [手順 2。AD FS の SSL 証明書を登録](../../ad-fs/deployment/Enroll-an-SSL-Certificate-for-AD-FS.md)、するには、この証明書を取得し、フェデレーション サーバーとして構成するコンピューターにコピーします。 ウィザードを使用して .pfx ファイルをインポートするには、次のようにクリックします。**インポート**し、ファイルの場所を参照します。 求められたら、.pfx ファイルのパスワードを入力します。  
  
6.  **サービス アカウントの指定** ページで、最初のフェデレーション サーバー ファームの作成時に構成した同じサービス アカウントを指定します。 既存のグループ管理サービス アカウントまたは既存のドメイン ユーザー アカウントを使用することができます。  
  
    > [!IMPORTANT]  
    > 指定したアカウントは、このファーム内のプライマリ フェデレーション サーバーで使用されていたアカウントと同じアカウントである必要があります。  
  
7.  **[オプションの確認]** ページで、構成の選択内容を確認し、 **[次へ]** をクリックします。  
  
8.  **前\-必要条件のチェック** ページで、すべての前提条件チェックが正常に完了、ことを確認 をクリックし、**構成**します。  
  
9. **結果**ページで、結果を確認および構成が正常に完了するかどうかを確認し、順にクリックします**フェデレーション サービス展開を完了に必要な次の手順**します。 詳細については、次を参照してください。 [AD FS のインストールを完了するため次のステップ](https://go.microsoft.com/fwlink/p/?LinkId=286704)します。 **[閉じる]** をクリックしてウィザードを終了します。  
  
### <a name="to-add-a-federation-server-to-an-existing-federation-server-farm-via-windows-powershell"></a>Windows PowerShell を使用して既存のフェデレーション サーバー ファームにフェデレーション サーバーを追加するには  
既存の gMSA アカウントまたは既存のドメイン ユーザー アカウントを使用して、既存のファームにフェデレーション サーバーを追加できます。  
  
-   既存の gMSA アカウントを使用してファームにフェデレーション サーバーを参加させる場合は、次の操作を行います。  
  
    1.  フェデレーション サーバーとして構成するコンピューター上に必要な SSL 証明書がインポートされていることを確認します、**ローカル コンピューター\\マイ ストア**ディレクトリ。 Windows PowerShell コマンド ウィンドウで、次のコマンドを実行して、SSL 証明書がインポートされているかどうかを確認できます:`dir Cert:\LocalMachine\My`します。 証明書の拇印に表示されて、**ローカル コンピューター\\マイ ストア**ディレクトリ。  
  
    2.  フェデレーション サーバーとして構成するコンピューターで、Windows PowerShell コマンド ウィンドウを開き、次のコマンドを実行します。  
  
        ```  
        Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>  
        ```  
  
        `<domain>\<GMSA_name>` AD ドメインとそのドメインに gMSA アカウントの名前です。 `<first_federation_server_hostname>` この既存のファーム内のプライマリ フェデレーション サーバーのホスト名です。  
  
        値を取得する`<certificate_thumbprint>`を実行して`dir Cert:\LocalMachine\My`前の手順でします。  
  
        > [!NOTE]  
        > このコマンドを実行する最初の時間でない場合、追加、`OverwriteConfiguration`パラメーター。  
  
        > [!NOTE]  
        > 前のコマンドは、WID ファームのノードを作成します。 SQL Server を実行しているコンピューターのサーバー ファーム ノードを作成する場合は、既にインストールされていて、SQL Server のインスタンスが必要です。  
        >   
        > 次のコマンドを使用して SQL Server のインスタンスを使用している既存のファームにフェデレーション サーバーを追加することができます:`Add-AdfsFarmNode -GroupServiceAccountIdentifier <domain>\<GMSA_name>$ -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"`場所**SQL\_ホスト\_名前**SQL Server がサーバーの名前を指定しますを実行していると**SQL\_インスタンス\_名前**SQL Server のインスタンスの名前を指定します。 SQL Server の既定のインスタンスを使用する場合は、使用、 **SQLConnectionString**の値"**データ ソース\=< SQL\_ホスト\_名 >; Integrated Security\=True**".  
  
        > [!IMPORTANT]  
        > AD FS ファームを作成して構成データを格納する SQL Server を使用する場合は、SQL Server 2008 および SQL Server 2012、SQL Server 2014 などの新しいバージョンを使用することができます。  
  
-   既存のドメイン ユーザー アカウントを使用してファームにフェデレーション サーバーを参加させる場合は、次の操作を行います。  
  
    1.  をフェデレーション サーバーとして構成するコンピューターに Windows PowerShellcommand ウィンドウを開き、次のコマンドを実行します:`$fscred = get-credential`します。 形式のドメインのフェデレーション サービス アカウントを使用するドメイン ユーザー アカウントの資格情報を入力\\ユーザー名。  
  
    2.  フェデレーション サーバーとして構成するコンピューター上に必要な SSL 証明書がインポートされていることを確認します、**ローカル コンピューター\\マイ ストア**ディレクトリ。 Windows PowerShellcommand ウィンドウで、次のコマンドを実行して、SSL 証明書がインポートされているかどうかを確認できます:`dir Cert:\LocalMachine\My`します。 証明書の拇印に表示されて、**ローカル コンピューター\\マイ ストア**ディレクトリ。  
  
    3.  同じ Windows PowerShell コマンド ウィンドウで、次のコマンドを実行します。  
  
        ```  
        Add-AdfsFarmNode -ServiceAccountCredential $fscred -PrimaryComputerName <first_federation_server_hostname> -CertificateThumbprint <certificate_thumbprint>  
        ```  
  
        > [!NOTE]  
        > このコマンドを実行する最初の時間でない場合、追加、`OverwriteConfiguration`パラメーター。  
  
        > [!NOTE]  
        > 前のコマンドは、WID ファームのノードを作成します。 SQL Server を実行しているコンピューターのサーバー ファーム ノードを作成する場合は、既にインストールされていて、SQL Server のインスタンスが必要です。 次のコマンドを使用して SQL Server のインスタンスを使用して、既存のファームにフェデレーション サーバーを追加することができます:`Add-AdfsFarmNode -ServiceAccountCredential $fscred -SQLConnectionString "Data Source=<SQL_Host_Name>\<SQL_instance_ name>;Integrated Security=True"`場所**SQL\_ホスト\_名前**先のサーバーの名前を指定の SQL インスタンスサーバーが実行されていると**SQL\_インスタンス\_名前**SQL Server のインスタンスの名前を指定します。 SQL Server の既定のインスタンスを使用する場合は、使用、 **SQLConnectionString**の値"**データ ソース\=< SQL\_ホスト\_名 >; Integrated Security\=True**".  
  
        > [!IMPORTANT]  
        > AD FS ファームを作成して構成データを格納する SQL Server を使用する場合は、SQL Server 2008 および SQL Server 2012、SQL Server 2014 などの新しいバージョンを使用することができます。  
  
## <a name="see-also"></a>関連項目 

[AD FS 展開](../../ad-fs/AD-FS-Deployment.md)  

[Windows Server 2012 R2 AD FS 展開ガイドします。](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[フェデレーション サーバー ファームの展開](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

