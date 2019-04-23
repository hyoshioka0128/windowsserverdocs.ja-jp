---
ms.assetid: 61ed00fd-51c7-4728-91fa-8501de9d8f28
title: SharePoint、Exchange、および RDG によるアプリケーションの発行
description: ''
author: billmath
manager: mtillman
ms.author: billmath
ms.date: 04/30/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: web-app-proxy
ms.openlocfilehash: 21ea6ecf717392027c1d00f818e230e2fe56a11d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826823"
---
# <a name="publishing-applications-with-sharepoint-exchange-and-rdg"></a>SharePoint、Exchange、および RDG によるアプリケーションの発行

>適用先:Windows Server 2016

**このコンテンツは、Web アプリケーション プロキシのオンプレミス バージョンに関連します。クラウドでオンプレミス アプリケーションに安全にアクセスを有効にするのを参照してください。、 [Azure AD アプリケーション プロキシのコンテンツ](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/)します。**  
  
このトピックでは、SharePoint Server、Exchange サーバーまたは Web アプリケーション プロキシを通じてリモート デスクトップ ゲートウェイ (RDP) を発行するために必要なタスクについて説明します。  

>[!NOTE]
>としてこの情報が提供されるのです。  リモート デスクトップ サービスをサポートし、使用することをお勧め[に安全にリモート アクセスを提供する Azure App プロキシ オンプレミス アプリケーション](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)します。
  
## <a name="BKMK_6.1"></a>SharePoint Server を公開します。  
クレーム ベース認証または統合 Windows 認証用 SharePoint サイトが構成されている場合は、Web アプリケーション プロキシ経由で SharePoint サイトを発行できます。 Active Directory フェデレーション サービス (AD FS) の事前認証を使用する場合、ウィザードの 1 つを使用して証明書利用者を構成する必要があります。  
  
-   SharePoint サイトで要求ベース認証を使用する場合、証明書利用者信頼の追加ウィザードを利用し、アプリケーションに証明書利用者信頼を構成する必要があります。  
  
-   SharePoint サイトで統合 Windows 認証を使用する場合、非要求ベースの証明書利用者信頼の追加ウィザードを利用し、アプリケーションに証明書利用者信頼を構成する必要があります。 KDC を構成する場合、要求ベースの Web アプリケーションと共に IWA を使用できます。  
  
    統合 Windows 認証を使用して認証できるように、Web アプリケーション プロキシ サーバーをドメインに参加する必要があります。  
  
    Kerberos 制約の委任をサポートするようにアプリケーションを構成する必要があります。 この作業は、どのアプリケーションについてもドメイン コントローラーで実行できます。 Windows Server 2012 R2 または Windows Server 2012 で実行されている場合は、バックエンド サーバーで直接アプリケーションを構成することもできます。 詳細については、「 [Kerberos 認証の新機能](https://technet.microsoft.com/library/hh831747.aspx)」を参照してください。 バックエンド サーバーのサービス プリンシパル名への委任、Web アプリケーション プロキシ サーバーが構成されていることを確認することも必要があります。 統合 Windows 認証を使用してアプリケーションを公開する Web アプリケーション プロキシを構成する方法のチュートリアルは、次を参照してください。[統合 Windows 認証を使用するようにサイト](assetId:///b0788958-627f-450f-877c-209b1bd0db52)します。  
  
SharePoint サイトを代替アクセス マッピング (AAM) とホスト名の付いたサイト コレクションのいずれかを利用して構成する場合、異なる外部 URL とバックエンド サーバー URL を使用してアプリケーションを公開できます。 ただし、AAM またはホスト名の付いたサイト コレクションを使用して SharePoint サイトを構成しない場合、同じ外部 URL とバックエンド サーバー URL を使用する必要があります。  
  
## <a name="BKMK_6.2"></a>Exchange Server を公開します。  
次の表では、Web アプリケーション プロキシとこれらのサービスの事前認証をサポートされている経由で公開できる Exchange サービスについて説明します。  
  
|Exchange サービス|事前認証|メモ|  
|--------------------|-----------------------|---------|  
|Outlook Web アプリ|、非要求ベース認証を使用して AD FS<br />-パススルー<br />、オンプレミス Exchange 2013 Service Pak 1 (SP1) のクレーム ベース認証を使用して AD FS|詳しくは、次のトピックをご覧ください。[Outlook Web App および eac で使用する AD FS のクレーム ベース認証を使用します。](https://go.microsoft.com/fwlink/?LinkId=393723)|  
|Exchange コントロール パネル|パススルー||  
|Outlook Anywhere|パススルー|Outlook Anywhere を正しく機能させるには 3 つの URL を公開する必要があります。<br /><br />-自動検出 URL です。<br />-Exchange サーバーの外部ホスト名つまり、URL に接続するクライアント用に構成されています。<br />-Exchange Server の内部 FQDN。|  
|Exchange ActiveSync|パススルー<br/> HTTP 基本認証プロトコルを使用して AD FS|| 詳細について参照してください。 https://docs.microsoft.com/windows-server/remote/remote-access/web-application-proxy/publishing-applications-using-ad-fs-preauthentication 
  
統合 Windows 認証を使用して Outlook Web アプリを公開するには、非要求ベースの証明書利用者信頼の追加ウィザードを利用し、アプリケーションに証明書利用者信頼を構成する必要があります。  
  
制約付き委任の Web アプリケーション プロキシ サーバーをドメインに参加する必要がありますの Kerberos を使用して認証できるようにします。  
  
Kerberos 認証をサポートするアプリケーションを構成する必要があります。 Web サービスが実行されているアカウントにサービス プリンシパル名 (SPN) を登録する必要するさらに これは、ドメイン コント ローラーまたはバックエンド サーバーで行うことができます。 負荷分散の Exchange 環境が代替のサービス アカウントを使用してこれが必要になりますを参照してください[Kerberos 認証クライアント アクセス サーバーの負荷分散の構成](https://technet.microsoft.com/library/ff808312(v=exchg.150).aspx)  
  
Windows Server 2012 R2 または Windows Server 2012 で実行されている場合は、バックエンド サーバーで直接アプリケーションを構成することもできます。 詳細については、「 [Kerberos 認証の新機能](https://technet.microsoft.com/library/hh831747.aspx)」を参照してください。 バックエンド サーバーのサービス プリンシパル名への委任、Web アプリケーション プロキシ サーバーが構成されていることを確認することも必要があります。  
  
## <a name="publishing-remote-desktop-gateway-through-web-application-proxy"></a>Web アプリケーション プロキシ経由のリモート デスクトップ ゲートウェイの発行  
リモート アクセス ゲートウェイにアクセスを制限し、リモート アクセスの事前認証を追加する場合、Web アプリケーション プロキシ経由ロールできます。 これは、MFA を含む RDG の事前認証を機能豊富ながあるかどうかを確認するに最適です。 事前認証なしの発行を使用してもオプションです、単一のシステムへのエントリ ポイントを提供します。  
  
#### <a name="how-to-publish-an-application-in-rdg-using-web-application-proxy-pass-through-authentication"></a>Web アプリケーション プロキシのパススルー認証を使用した RDG でアプリケーションを発行する方法  
  
1.  インストールがあるかによって異なりますが、RD Web アクセス (/rdweb)、RD ゲートウェイ (rpc) の役割が同じサーバー上または異なるサーバー。  
  
2.  RD Web アクセス、RD ゲートウェイのロールが同じ RDG サーバーでホストされている場合だけに発行できます FQDN ルート Web アプリケーション プロキシなど、 https://rdg.contoso.com/します。  
  
    発行することも、2 つの仮想ディレクトリに個別になど https://rdg.contoso.com/rdweb/と https://rdg.contoso.com/rpc/します。  
  
3.  RD Web アクセス、RD ゲートウェイが別々 の RDG サーバー上にホストされている場合は、2 つの仮想ディレクトリを個別に発行する必要があります。 など、同じまたは異なる外部 FQDN を使用することができます https://rdweb.contoso.com/rdweb/と https://gateway.contoso.com/rpc/します。  
  
4.  外部および内部の FQDN が異なる場合は、RDWeb 公開ルールに要求ヘッダーの変換が無効にする必要がありますできません。 これは、Web アプリケーション プロキシ サーバーで次の PowerShell スクリプトを実行して実行できますが、既定で有効にする必要があります。
  
    ```  
    Get-WebApplicationProxyApplication applicationname | Set-WebApplicationProxyApplication -DisableTranslateUrlInRequestHeaders:$false  
    ```  
  
    > [!NOTE]  
    > RemoteApp とデスクトップ接続や iOS のリモート デスクトップ接続などのリッチ クライアントをサポートする場合は、これらはサポートしない事前認証のため RDG パススルー認証を使用して発行する必要があるあります。  
  
#### <a name="how-to-publish-an-application-in-rdg-using-web-application-proxy-with-pre-authentication"></a>事前認証を使用した Web アプリケーション プロキシを使用した RDG でアプリケーションを発行する方法  
  
1.  Web アプリケーション プロキシの RDG の事前認証は、リモート デスクトップ接続クライアント (mstsc.exe) に渡される Internet Explorer で取得した、事前認証クッキーを渡すことによって機能します。 これは、リモート デスクトップ接続クライアント (mstsc.exe) によって使用されます。 リモート デスクトップ接続クライアントによって認証の証拠としてこれ使用されます。  
  
    次の手順では、クライアントに送信されるリモート アプリの RDP ファイルに必要なカスタム RDP プロパティを含めるコレクション サーバーを指示します。 これらは、クライアントを事前認証が必要です、リモート デスクトップ接続クライアント (mstsc.exe) にサーバーのアドレスを事前認証の cookie を渡すために指示します。 Web アプリケーション プロキシ アプリケーションで httponly が設定された機能を無効にすると協力して、これにより、ブラウザー経由で取得した Web アプリケーション プロキシのクッキーを利用するには、リモート デスクトップ接続クライアント (mstsc.exe) です。  
  
    RD Web アクセス サーバーへの認証、RD Web アクセス フォーム ログオンが使用されます。 これにより、最も少ない RD Web アクセスのログオン フォームには、後続のリモート アプリの起動のリモート デスクトップ接続クライアント (mstsc.exe) で使用できるクライアント側の資格情報ストアが作成されると、ユーザー認証の数が求められます。  
  
2.  最初に、作成手動証明書利用者の信頼を AD FS のクレーム対応アプリケーションを発行していたかのようです。 これは、Kerberos 制約付き委任せず、公開されたサーバーへの事前認証を取得するために、事前認証を適用するにはありますパーティの信頼証明書利用者のダミーを作成する必要があることを意味します。 ユーザーが認証されると、他のすべてがを介して渡されます。  
  
    > [!WARNING]  
    > 委任の使用をお勧めするが、mstsc SSO の要件を完全に解決しないし、自体 RD ゲートウェイ認証を処理するためにクライアントが求めているため、/rpc ディレクトリに委任時に問題があるかもしれません。  
  
3.  手動による証明書利用者の信頼を作成するには、次の AD FS 管理コンソールで、手順を実行します。  
  
    1.  使用して、**証明書利用者信頼の追加**ウィザード  
  
    2.  選択**証明書利用者に関するデータを手動で入力**します。  
  
    3.  すべての既定の設定をそのまま使用します。  
  
    4.  証明書利用者信頼の識別子の場合、たとえば RDG へのアクセスに使用する外部の FQDN を入力します。 https://rdg.contoso.com/します。  
  
        これは、Web アプリケーション プロキシでアプリを発行するときに使用する証明書利用者のパーティの信頼です。  
  
4.  発行サイトのルート (たとえば、 https://rdg.contoso.com/ ) Web アプリケーション プロキシ。 AD fs 事前認証を設定し、上記で作成した証明書利用者のパーティの信頼を使用します。 これは、/rdweb と同じ Web アプリケーション プロキシの認証クッキーを使用する/rpc に有効になります。  
  
    /Rdweb と/rpc 個別のアプリケーションとして公開して、パブリッシュされた別のサーバーを使用するもことができます。 Web アプリケーション プロキシ トークン Relying Party Trust の発行であるし、同じ証明書利用者信頼によって公開されたアプリケーション間では有効なため、同じ証明書利用者信頼を使用して両方を公開することを確認する必要があります。  
  
5.  外部および内部の FQDN が異なる場合は、RDWeb 公開ルールに要求ヘッダーの変換が無効にする必要がありますできません。 これは、Web アプリケーション プロキシ サーバーで次の PowerShell スクリプトを実行して実行できますが、既定で有効にする必要があります。
  
    ```  
    Get-WebApplicationProxyApplication applicationname | Set-WebApplicationProxyApplication -DisableTranslateUrlInRequestHeaders:$false 
    ```  
  
6.  発行済みアプリケーションの無効化、RDG で Web アプリケーション プロキシで httponly が設定された cookie のプロパティ。 Web アプリケーション プロキシの認証クッキーを RDG ActiveX コントロールのアクセスを許可するのには、Web アプリケーション プロキシの cookie の httponly が設定されたプロパティを無効にする必要です。  
  
    これにより、インストールするのには、次が必要です。 [Web アプリケーション プロキシの修正プログラム](https://support.microsoft.com/en-gb/kb/3000850)または[ https://support.microsoft.com/en-gb/kb/3000850](https://support.microsoft.com/en-gb/kb/3000850)します。  
  
    修正プログラムをインストールした後に、関連するアプリケーションの名前を指定する Web アプリケーション プロキシ サーバーで次の PowerShell スクリプトを実行します。  
  
    ```  
    Get-WebApplicationProxyApplication applicationname | Set-WebApplicationProxyApplication -DisableHttpOnlyCookieProtection:$true  
    ```  
  
    HttpOnly を無効化により、RDG ActiveX が Web アプリケーション プロキシの認証の cookie へのアクセスを制御します。  
  
7.  クライアント (mstsc.exe) を知ると、rdp ファイルでその事前認証が必要なリモート デスクトップ接続を使用するコレクションのサーバーに関連する RDG コレクションを構成します。  
  
    -   Windows Server 2012 および Windows Server 2012 R2 では、これは、RDG コレクション サーバーで、次の PowerShell コマンドレットを実行して実行できます。  
  
        ```
        Set-RDSessionCollectionConfiguration -CollectionName "<yourcollectionname>" -CustomRdpProperty "pre-authentication server address:s: <https://externalfqdn/rdweb/>`nrequire pre-authentication:i:1"
        ```
  
        削除するかどうかを確認します < と > たとえば、独自の値を置き換えるときに、角かっこ。
        
        ```
        Set-RDSessionCollectionConfiguration -CollectionName "MyAppCollection" -CustomRdpProperty "pre-authentication server address:s: https://rdg.contoso.com/rdweb/`nrequire pre-authentication:i:1"
        ```
  
    -   Windows Server 2008 r2:  
  
        1.  管理者特権を持つアカウントを使用してターミナル サーバーにログオンします。  
  
        2.  移動して**開始** >**管理ツール** > **ターミナル サービス** > **TS RemoteApp マネージャー。**  
  
        3.  **概要**マネージャーのウィンドウの TS RemoteApp、RDP の設定の横にあるをクリックして**変更**します。  
  
        4.  **カスタム RDP 設定** タブで、次のような RDP 設定を カスタム RDP 設定 ボックスに入力します。  
  
            `pre-authentication server address: s: https://externalfqdn/rdweb/`  
  
            `require pre-authentication:i:1`  
  
        5.  完了したら、クリックして**適用**します。  
  
            これは、クライアントに送信される RDP ファイルにカスタム RDP プロパティを含めるコレクション サーバーを指示します。 これらは、クライアントを事前認証が必要です、リモート デスクトップ接続クライアント (mstsc.exe) にサーバーのアドレスを事前認証の cookie を渡すために指示します。 これで、Web アプリケーション プロキシ アプリケーションで HttpOnly を無効にすると組み合わせてによりブラウザー経由で取得した Web アプリケーション プロキシの認証クッキーを利用するには、リモート デスクトップ接続クライアント (mstsc.exe) できます。  
  
            RDP の詳細については、次を参照してください。 [TS ゲートウェイの OTP のシナリオを構成する](https://technet.microsoft.com/library/cc731249(v=ws.10).aspx)します。  
  
## <a name="BKMK_Links"></a>参照してください。  
  
-   [Web アプリケーション プロキシを使用してアプリケーションを発行する計画](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383650(v=ws.11))  
  
-   [Web アプリケーション プロキシのトラブルシューティング](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn770156(v=ws.11))  
  
-   [Web アプリケーション プロキシのチュートリアル ガイド](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn280944(v=ws.11))  
