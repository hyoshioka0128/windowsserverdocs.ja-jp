---
title: 手順2詳細な DirectAccess サーバーを構成する
description: このトピックは、「Windows Server 2016 の詳細設定を使用して単一の DirectAccess サーバーを展開する」の一部です。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 35afec8e-39a4-463b-839a-3c300ab01174
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ec06ce13e5199897753a1d581d21211465729a5e
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86959214"
---
# <a name="step-2-configure-advanced-directaccess-servers"></a>手順2詳細な DirectAccess サーバーを構成する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、IPv4 と IPv6 混在環境で単一のリモート アクセス サーバーを使用する、高度なリモート アクセスの展開に必要なクライアントとサーバーの設定を構成する方法について説明します。 展開の手順を開始する前に記載されている計画の手順が完了したことを確認 [高度な DirectAccess 展開を計画](Plan-an-Advanced-DirectAccess-Deployment.md)します。  
  
|タスク|説明|  
|----|--------|  
|2.1. リモート アクセスの役割をインストールする|リモート アクセスの役割をインストールします。|  
|2.2. 展開の種類を構成する|DirectAccess と VPN、DirectAccess のみ、または VPN のみで展開の種類を構成します。|  
|[高度な DirectAccess 展開を計画する](Plan-an-Advanced-DirectAccess-Deployment.md)|DirectAccess クライアントを含むセキュリティ グループでリモート アクセス サーバーを構成します。|  
|2.4. リモート アクセス サーバーを構成する|リモート アクセス サーバー設定を構成します。|  
|2.5. インフラストラクチャ サーバーを構成する|組織で使用するインフラストラクチャ サーバーを構成します。|  
|2.6. アプリケーション サーバーを構成する|認証と暗号化を要求するようにアプリケーション サーバーを構成します。|  
|2.7. 構成の概要と代替 GPO|リモート アクセスの構成の概要を表示し、必要に応じて GPO を変更します。|  
|2.8. Windows PowerShell を使用してリモート アクセス サーバーを構成する方法|Windows PowerShell を使用してリモートアクセスを構成します。|  
  
> [!NOTE]  
> このトピックでは、説明した手順の一部を自動化するのに使用できる Windows PowerShell コマンドレットのサンプルを示します。 詳細については、「[コマンドレットの使用](https://go.microsoft.com/fwlink/p/?linkid=230693)」を参照してください。  
  
## <a name="21-install-the-remote-access-role"></a><a name="BKMK_Role"></a>2.1.  リモート アクセスの役割をインストールする  
リモート アクセスを展開するには、組織でリモート アクセス サーバーとして機能するサーバーにリモート アクセスの役割をインストールする必要があります。  
  
#### <a name="to-install-the-remote-access-role"></a>リモート アクセスの役割をインストールするには  
  
1.  サーバー マネージャー コンソールでのリモート アクセス サーバー上で、 **ダッシュ ボード**, 、] をクリックして **役割と機能の追加**します。  
  
2.  **[次へ]** を 3 回クリックして、**[サーバーの役割の選択する]** 画面に進みます。  
  
3.  **[サーバーの役割の選択]** ページで **[リモート アクセス]** を選択し、**[機能の追加]**、**[次へ]** の順にクリックします。  
  
4.  **[次へ]** を 5 回クリックします。  
  
5.  **[インストール オプションの確認]** ページで、**[インストール]** をクリックします。  
  
6.  **[インストールの進行状況]** ページで、インストールが正常に完了したことを確認し、**[閉じる]** をクリックします。  
  
![インストールの進行状況-成功](../../../media/Step-2-Configuring-DirectAccess-Servers/PowerShellLogoSmall.gif)***<em>Windows PowerShell の同等のコマンド</em>***  
  
次の Windows PowerShell コマンドレットは、前の手順と同じ機能を実行します。 各コマンドレットを単一行に入力します。ただし、ここでは、書式上の制約があるために、複数行に改行されて表示される場合があります。  
  
```  
Install-WindowsFeature RemoteAccess -IncludeManagementTools  
```  
  
## <a name="22-configure-the-deployment-type"></a><a name="BKMK_Deploy"></a>2.2.  展開の種類を構成する  
リモート アクセスは、リモート アクセス管理コンソールを使用して、次の 3 とおりの方法で展開できます。  
  
-   DirectAccess と VPN  
  
-   DirectAccess のみ  
  
-   VPN のみ  
  
このガイドでは、手順の例として、DirectAccess のみの展開を使います。  
  
#### <a name="to-configure-the-deployment-type"></a>展開の種類を構成するには  
  
1.  リモートアクセスサーバーで、リモートアクセス管理コンソールを開きます。 [**スタート**] 画面で、「**RAMgmtUI.exe**」と入力し、enter キーを押します。 [**ユーザー アカウント制御**] ダイアログ ボックスが表示されたら、表示された操作が正しいことを確認し、[**はい**] をクリックします。  
  
2.  リモート アクセス管理コンソールの中央ウィンドウで、**[リモート アクセスのセットアップ ウィザードを実行する]** をクリックします。  
  
3.  **[リモート アクセスの構成]** ダイアログ ボックスで、DirectAccess と VPN、DirectAccess のみ、または VPN のみのどれを展開するかをクリックします。  
  
## <a name="23-configure-directaccess-clients"></a><a name="BKMK_Clients"></a>2.3.  DirectAccess クライアントを構成する  
DirectAccess を使用するようにプロビジョニングするクライアント コンピューターは、選択したセキュリティ グループに属している必要があります。 DirectAccess の構成後、セキュリティ グループのクライアント コンピューターは、DirectAccess グループ ポリシー オブジェクト (GPO) を受信するようにプロビジョニングされます。 クライアント アクセスとリモート管理、またはリモート管理のみに DirectAccess の構成を許可する展開シナリオを構成することもできます。  
  
#### <a name="to-configure-directaccess-clients"></a>DirectAccess クライアントを構成するには  
  
1.  リモート アクセス管理コンソールの中央ウィンドウの **[手順 1: リモート クライアント]** 領域で、**[構成]** をクリックします。  
  
2.  DirectAccess クライアントのセットアップ ウィザードの **[展開シナリオ]** ページで、組織で使用する展開シナリオをクリックし (**[完全な DirectAccess]** または **[リモート管理のみ]**)、**[次へ]** をクリックします。  
  
3.  [**グループの選択**] ページで、[**追加**] をクリックします。  
  
4.  **[グループの選択]** ダイアログ ボックスで、DirectAccess クライアント コンピューターを含むセキュリティ グループを選択します。  
  
    > [!NOTE]  
    > セキュリティグループがリモートアクセスサーバーとは異なるフォレストにある場合は、リモートアクセスのセットアップウィザードを完了した後、[**タスク**] ウィンドウの [**管理サーバーの更新**] をクリックして、新しいフォレスト内のドメインコントローラーと Configuration Manager サーバーを検出します。  
  
5.  必要に応じて、**[モバイル コンピューターに対してのみ DirectAccess を有効にする]** チェック ボックスをオンにして、モバイル コンピューターのみが内部ネットワークにアクセスできるようにします。  
  
6.  必要に応じて、**[強制トンネリングを使用する]** チェック ボックスをオンにして、リモート アクセス サーバーですべての (内部ネットワークとインターネットへの) クライアント トラフィックをルーティングします。  
  
7.  **[次へ]** をクリックします。  
  
8.  **[Network Connectivity Assistant]** ページで、次の操作を実行します。  
  
    -   表に内部ネットワークへの接続の決定に使用するリソースを追加します。 他のリソースが構成されていない場合は、既定の Web プローブが自動的に作成されます。  
  
        > [!CAUTION]  
        > エンタープライズ ネットワークへの接続の決定に Web プローブの場所を構成するときは、1 つ以上の HTTP ベースのプローブが構成されていることを確認します。 **ping** プローブのみの構成は不十分で、接続状態の決定が不正確になる可能性があります。 これは、**ping** が IPsec から除外されている結果として、IPsec トンネルが確実に正しく確立できないためです。  
  
    -   接続の問題が発生した場合に、ユーザーが情報を送信できるように、ヘルプ デスクの電子メール アドレスを追加します。  
  
    -   DirectAccess 接続にわかりやすい名前を指定します。 この名前は、ユーザーが通知領域でネットワーク アイコンをクリックしたときに、ネットワークの一覧に表示されます。  
  
    -   必要に応じて、**[DirectAccess クライアントがローカルでの名前解決を使用できるようにする]** チェック ボックスをオンにします。  
  
        > [!NOTE]  
        > ローカルでの名前解決を有効にすると、Network Connectivity Assistant を実行するユーザーは、DirectAccess クライアント コンピューターで構成された DNS サーバーを使用する名前の解決を選択できます。  
  
9. **[完了]** をクリックします。  
  
## <a name="24-configure-the-remote-access-server"></a><a name="BKMK_Server"></a>2.4.  リモート アクセス サーバーを構成する  
リモート アクセスを展開するには、正しいネットワーク アダプターを使用したリモート アクセス サーバー、クライアント コンピューターが接続できるリモート アクセス サーバー向けのパブリック URL (ConnectTo アドレス)、ConnectTo アドレスに一致するサブジェクトを持つ IP-HTTPS 証明書、IPv6 設定、クライアント コンピューターの認証を構成する必要があります。  
  
#### <a name="to-configure-the-remote-access-server"></a>リモート アクセス サーバーを構成するには  
  
1.  リモート アクセス管理コンソールの中央ウィンドウの **[手順 2 リモート アクセス サーバー]** 領域で、**[構成]** をクリックします。  
  
2.  リモート アクセス サーバーのセットアップ ウィザードの **[ネットワーク トポロジ]** ページで、組織で使用する展開トポロジをクリックします。 [**クライアントからリモート アクセス サーバーへの接続に使用するパブリック名または IPv4 アドレスを入力してください**] に展開のパブリック名を入力し (この名前は IP-HTTPS 証明書のサブジェクト名に一致し、edge1.contoso.com などになります)、[**次へ**] をクリックします。  
  
3.  **[ネットワーク アダプター]** ページで、ウィザードは展開のネットワーク向けのネットワーク アダプターを自動的に検出します。 ウィザードで正しいネットワーク アダプターが検出されない場合は、正しいアダプターを手動で選択します。 ウィザードの前の手順で設定した展開セットのパブリック名に基づいて、ウィザードでは IP-HTTPS 証明書も自動的に検出されます。 ウィザードで正しい IP-HTTPS 証明書が検出されない場合は、**[参照]** をクリックして正しい証明書を手動で選択してから、**[次へ]** をクリックします。  
  
4.  **[プレフィックスの構成]** ページで (これは、内部ネットワークで IPv6 が展開されている場合にのみ表示されます)、ウィザードは、内部ネットワークで使用される IPv6 設定を自動的に検出します。 展開に追加のプレフィックスが必要な場合は、内部ネットワークのための IPv6 プレフィックス、DirectAccess クライアント コンピューターに割り当てる IPv6 プレフィックス、VPN クライアント コンピューターに割り当てる IPv6 プレフィックスを構成します。  
  
    > [!NOTE]  
    > 複数の内部 IPv6 プレフィックスは、2001:db8:1::/48;2001:db8:2::/48 のように、セミコロンで区切られた一覧を使用して指定できます。  
  
5.  **[認証]** ページで、次の操作を実行します。  
  
    -   **[ユーザー認証]** で、**[Active Directory の資格情報]** をクリックします。 2 要素認証を使用して展開を構成するには、**[2 要素認証]** をクリックします。 詳細については、「[OTP 認証を使用するリモート アクセスの展開](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831379(v=ws.11))」を参照してください。  
  
    -   マルチサイトと 2 要素の認証展開では、コンピューター証明書認証を使用する必要があります。 コンピューター証明書認証を使用するには、**[コンピューターの証明書を使用する]** チェック ボックスをオンにして、IPsec ルート証明書を選択します。  
  
    -   Windows 7 クライアントコンピューターが DirectAccess を介して接続できるようにするには、[ **windows 7 クライアントコンピューターが directaccess 経由で接続できるよう**にする] チェックボックスをオンにします。  
  
        > [!NOTE]  
        > この種の展開では、コンピューター証明書認証も使用する必要があります。  
  
6.  **[完了]** をクリックします。  
  
## <a name="25-configure-the-infrastructure-servers"></a><a name="BKMK_Infra"></a>2.5.  インフラストラクチャ サーバーを構成する  
リモート アクセス展開でインフラストラクチャ サーバーを構成するには、ネットワーク ロケーション サーバー、DNS 設定 (DNS サフィックス検索一覧を含む)、リモート アクセスで自動的に検出されない管理サーバーを構成する必要があります。  
  
#### <a name="to-configure-the-infrastructure-servers"></a>インフラストラクチャ サーバーを構成するには  
  
1.  リモート アクセス管理コンソールの中央ウィンドウの **[手順 3 インフラストラクチャ サーバー]** 領域で、**[構成]** をクリックします。  
  
2.  インフラストラクチャ サーバーのセットアップ ウィザードの **[ネットワーク ロケーション サーバー]** ページで、展開のネットワーク ロケーション サーバーの場所に一致するオプションをクリックします。 ネットワーク ロケーション サーバーがリモート Web サーバー上にある場合は、続行する前に **[検証]** をクリックします。 ネットワーク ロケーション サーバーがリモート アクセス サーバー上にある場合は、**[参照]** をクリックして関連する証明書を検索してから、**[次へ]** をクリックします。  
  
3.  テーブルの **[DNS]** ページに、名前解決ポリシー テーブル (NRPT) 除外として適用される追加の名前サフィックスを入力します。 ローカルの名前解決オプションを選択して、**[次へ]** をクリックします。  
  
4.  **[DNS サフィックス検索一覧]** ページで、リモート アクセス サーバーは展開のドメイン サフィックスを自動的に検出します。 **[追加]** ボタンと **[削除]** ボタンを使用して、使用するドメイン サフィックスの一覧からドメイン サフィックスを追加、削除します。 新しいドメイン サフィックスを追加するには、**[新しいサフィックス]** にサフィックスを入力して、**[追加]** をクリックします。 **[次へ]** をクリックします。  
  
5.  **[管理]** ページで、自動的に検出されない管理サーバーを追加して、**[次へ]** をクリックします。 リモートアクセスは、ドメインコントローラーと Configuration Manager サーバーを自動的に追加します。  
  
    > [!NOTE]  
    > サーバーは自動的に追加されますが、一覧には表示されません。 構成を最初に適用した後、Configuration Manager サーバーが一覧に表示されます。  
  
6.  **[完了]** をクリックします。  
  
## <a name="26-configure-application-servers"></a><a name="BKMK_App"></a>2.6。 アプリケーション サーバーを構成する  
リモート アクセス展開で、アプリケーション サーバーの構成はオプションの作業です。 リモート アクセスでは、選択したアプリケーション サーバーの認証が要求されますが、これはアプリケーション サーバー セキュリティ グループに含まれているかどうかで決定されます。 既定では、認証を必要とするアプリケーション サーバーへのトラフィックも暗号化されますが、アプリケーション サーバーへのトラフィックは暗号化せず、認証のみを使用する選択も可能です。  
  
> [!NOTE]  
> 暗号化を使用しない認証は、Windows Server 2012 R2、Windows Server 2012、または Windows Server 2008 R2 を実行しているアプリケーションサーバーでのみサポートされます。  
  
#### <a name="to-configure-application-servers"></a>アプリケーション サーバーを構成するには  
  
1.  リモート アクセス管理コンソールの中央ウィンドウの **[手順 4 アプリケーション サーバー]** 領域で、**[構成]** をクリックします。  
  
2.  DirectAccess アプリケーション サーバーのセットアップ ウィザードで、選択したアプリケーション サーバーに認証を要求するには、**[選択したアプリケーション サーバーにも認証を適用する]** をクリックします。 **[追加]** をクリックして、アプリケーション サーバー セキュリティ グループを選択します。  
  
3.  アクセスをアプリケーション サーバー セキュリティ グループ内のサーバーのみに制限するには、**[セキュリティ グループに含まれるサーバーへのアクセスのみを許可する]** チェック ボックスをオンにします。  
  
4.  暗号化せずに認証を使用するには、[トラフィックを暗号化しない] を選択し**ます。[認証のみを使用する**] チェックボックスをオンにします。  
  
5.  **[完了]** をクリックします。  
  
## <a name="27-configuration-summary-and-alternate-gpos"></a><a name="BKMK_GPO"></a>2.7。 構成の概要と代替 GPO  
リモート アクセス構成が完了すると、**[リモート アクセスの確認]** が表示されます。 次のものを含め、これまでに選択したすべての設定を確認できます。  
  
1.  **GPO 設定**: DirectAccess サーバー GPO 名およびクライアント GPO 名が一覧表示されます。 さらに、**[GPO 設定]** の見出しの横にある **[変更]** リンクをクリックして、GPO 設定を変更できます。  
  
2.  **リモート クライアント**: セキュリティ グループ、強制トンネリングの状態、接続検証方法、DirectAccess 接続名を含む DirectAccess クライアント構成が表示されます。  
  
3.  **リモート アクセス サーバー**: パブリック名/アドレス、ネットワーク アダプター構成、証明書情報、構成されている場合は OTP 情報を含む DirectAccess 構成が表示されます。  
  
4.  **インフラストラクチャ サーバー**: この一覧には、ネットワーク ロケーション サーバー URL、DirectAccess クライアントが使用する DNS サフィックス、管理サーバー情報が含まれます。  
  
5.  **アプリケーション サーバー**: 特定のアプリケーション サーバーに対するエンドツーエンド認証の状態に加えて、DirectAccess のリモート管理の状態が表示されます。  
  
## <a name="28-how-to-configure-the-remote-access-server-by-using-windows-powershell"></a><a name="BKMK_PS"></a>2.8。 Windows PowerShell を使用してリモート アクセス サーバーを構成する方法  
![Windows PowerShell](../../../media/Step-2-Configuring-DirectAccess-Servers/PowerShellLogoSmall.gif)**Windows powershell の同等のコマンド**  
  
次の Windows PowerShell コマンドレットは、前の手順と同じ機能を実行します。 各コマンドレットを単一行に入力します。ただし、ここでは、書式上の制約があるために、複数行に改行されて表示される場合があります。  
  
ルート**corp.contoso.com**を持つドメイン内でのみ directaccess のエッジトポロジで完全インストールを実行し、次のパラメーターを使用するには: サーバー GPO: **directaccess サーバー設定**、クライアント GPO: directaccess クライアント設定、内部ネットワークアダプター:**企業ネットワーク、外部ネットワークアダプター:** **Internet**、ConnectTto address: **edge1.contoso.com**、およびネットワークロケーションサーバー: **nls.corp.contoso.com**:  
  
```  
Install-RemoteAccess -Force -PassThru -ServerGpoName 'corp.contoso.com\DirectAccess Server Settings' -ClientGpoName 'corp.contoso.com\DirectAccess Client Settings' -DAInstallType 'FullInstall' -InternetInterface 'Internet' -InternalInterface 'Corpnet' -ConnectToAddress 'edge1.contoso.com' -NlsUrl 'https://nls.corp.contoso.com/'  
```  
  
CORP-APP1-CA という名前の証明機関によって発行された IPsec ルート証明書によるコンピューター証明書認証を使用するようにリモート アクセス サーバーを構成するには:  
  
```  
$certs = Get-ChildItem Cert:\LocalMachine\Root  
$IPsecRootCert = $certs | Where-Object {$_.Subject -Match "corp-APP1-CA"}  
Set-DAServer -IPsecRootCertificate $IPsecRootCert  
```  
  
**DirectAccessClients** という名前の DirectAccess クライアントを含むセキュリティ グループを追加して、既定の Domain Computers セキュリティ グループを削除するには:  
  
```  
Add-DAClient -SecurityGroupNameList @('corp.contoso.com\DirectAccessClients')  
Remove-DAClient -SecurityGroupNameList @('corp.contoso.com\Domain Computers')  
```  
  
(ノートブックとラップトップだけでなく) すべてのコンピューターのリモートアクセスを有効にし、Windows 7 クライアントのリモートアクセスを有効にするには、次のようにします。  
  
```  
Set-DAClient -OnlyRemoteComputers 'Disabled' -Downlevel 'Enabled'  
```  
  
わかりやすい接続名と Web プローブ URL を含めた DirectAccess クライアント エクスペリエンスを構成するには:  
  
```  
Set-DAClientExperienceConfiguration -FriendlyName 'Contoso DirectAccess Connection' -PreferLocalNamesAllowed $False -PolicyStore 'corp.contoso.com\DirectAccess Client Settings' -CorporateResources @('HTTP:https://directaccess-WebProbeHost.corp.contoso.com')  
```  
  
## <a name="previous-step"></a><a name="BKMK_Links"></a>前の手順  
  
-   [手順 1: 高度な DirectAccess インフラストラクチャを構成する](da-adv-configure-s1-infrastructure.md)  
  
## <a name="next-step"></a>次の手順  
  
-   [手順 3:展開を確認する](Step-3-Verify-the-Deployment.md)  
  
