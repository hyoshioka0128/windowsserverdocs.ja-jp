---
ms.assetid: 61ed00fd-51c7-4728-91fa-8501de9d8f28
title: SharePoint、Exchange、および RDG によるアプリケーションの発行
description: ''
author: billmath
manager: mtillman
ms.author: billmath
ms.date: 04/30/2018
ms.topic: article
ms.prod: windows-server
ms.technology: web-app-proxy
ms.openlocfilehash: 0e5c9779fae66e7edec3c1bba471d5cadbe48a72
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404238"
---
# <a name="publishing-applications-with-sharepoint-exchange-and-rdg"></a>SharePoint、Exchange、および RDG によるアプリケーションの発行

>適用先:Windows Server 2016

@no__t-このコンテンツは、オンプレミスバージョンの Web アプリケーションプロキシに関連しています。クラウド経由でオンプレミスアプリケーションへのセキュリティで保護されたアクセスを有効にするには、 [Azure AD アプリケーションプロキシのコンテンツ](https://azure.microsoft.com/documentation/articles/active-directory-application-proxy-get-started/)を参照してください。 **  

このトピックでは、Web アプリケーションプロキシを介して SharePoint Server、Exchange Server、またはリモートデスクトップゲートウェイ (RDP) を公開するために必要なタスクについて説明します。  

>[!NOTE]
>この情報はそのとおりに提供されます。  リモートデスクトップサービスでは、Azure アプリプロキシを使用して、[オンプレミスアプリケーションへの安全なリモートアクセスを提供する](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started)ことをサポートしています。

## <a name="BKMK_6.1"></a>SharePoint サーバーの公開  
Sharepoint サイトが要求ベースの認証または統合 Windows 認証用に構成されている場合は、Web アプリケーションプロキシを介して SharePoint サイトを発行できます。 事前認証に Active Directory フェデレーションサービス (AD FS) (AD FS) を使用する場合は、いずれかのウィザードを使用して証明書利用者を構成する必要があります。  

-   SharePoint サイトで要求ベース認証を使用する場合、証明書利用者信頼の追加ウィザードを利用し、アプリケーションに証明書利用者信頼を構成する必要があります。  

-   SharePoint サイトで統合 Windows 認証を使用する場合、非要求ベースの証明書利用者信頼の追加ウィザードを利用し、アプリケーションに証明書利用者信頼を構成する必要があります。 KDC を構成する場合、要求ベースの Web アプリケーションと共に IWA を使用できます。  

    統合 Windows 認証を使用してユーザーを認証できるようにするには、Web アプリケーションプロキシサーバーがドメインに参加している必要があります。  

    Kerberos 制約の委任をサポートするようにアプリケーションを構成する必要があります。 この作業は、どのアプリケーションについてもドメイン コントローラーで実行できます。 Windows Server 2012 R2 または Windows Server 2012 で実行されている場合は、バックエンドサーバーで直接アプリケーションを構成することもできます。 詳細については、「 [Kerberos 認証の新機能](https://technet.microsoft.com/library/hh831747.aspx)」を参照してください。 また、Web アプリケーションプロキシサーバーが、バックエンドサーバーのサービスプリンシパル名への委任用に構成されていることを確認する必要があります。 統合 Windows 認証を使用してアプリケーションを公開するように Web アプリケーションプロキシを構成する方法のチュートリアルについては、「[統合 windows 認証を使用する](assetId:///b0788958-627f-450f-877c-209b1bd0db52)ようにサイトを構成する」を参照してください。  

SharePoint サイトを代替アクセス マッピング (AAM) とホスト名の付いたサイト コレクションのいずれかを利用して構成する場合、異なる外部 URL とバックエンド サーバー URL を使用してアプリケーションを公開できます。 ただし、AAM またはホスト名の付いたサイト コレクションを使用して SharePoint サイトを構成しない場合、同じ外部 URL とバックエンド サーバー URL を使用する必要があります。  

## <a name="BKMK_6.2"></a>Exchange Server の公開  
次の表は、Web アプリケーションプロキシ経由で公開できる Exchange サービスと、これらのサービスに対してサポートされている事前認証を示しています。  


|    Exchange サービス    |                                                                            事前認証                                                                            |                                                                                                                                       メモ                                                                                                                                        |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Outlook Web アプリ     | -要求ベースでない認証を使用して AD FS<br />-パススルー<br />-オンプレミス Exchange 2013 サービスパック 1 (SP1) の要求ベースの認証を使用して AD FS |                                                                  詳しくは、次のトピックをご覧ください。[Outlook Web App と EAC で使用を使用して AD FS 要求ベースの認証を使用する](https://go.microsoft.com/fwlink/?LinkId=393723)                                                                  |
| Exchange コントロール パネル |                                                                               パススルー                                                                               |                                                                                                                                                                                                                                                                                    |
|    Outlook Anywhere    |                                                                               パススルー                                                                               | Outlook Anywhere を正しく機能させるには 3 つの URL を公開する必要があります。<br /><br />-自動検出 URL。<br />-Exchange サーバーの外部ホスト名。これは、クライアントが接続するために構成されている URL です。<br />-Exchange サーバーの内部 FQDN。 |
|  Exchange ActiveSync   |                                                     パススルー<br/> HTTP 基本認証プロトコルを使用した AD FS                                                      |                                                                                                                                                                                                                                                                                    |

統合 Windows 認証を使用して Outlook Web アプリを公開するには、非要求ベースの証明書利用者信頼の追加ウィザードを利用し、アプリケーションに証明書利用者信頼を構成する必要があります。  

Kerberos の制約付き委任を使用してユーザーを認証できるようにするには、Web アプリケーションプロキシサーバーがドメインに参加している必要があります。  

Kerberos 認証をサポートするようにアプリケーションを構成する必要があります。 さらに、web サービスが実行されているアカウントにサービスプリンシパル名 (SPN) を登録する必要があります。 これは、ドメインコントローラーまたはバックエンドサーバーで実行できます。 負荷分散された Exchange 環境では、別のサービスアカウントを使用する必要があります。「負荷分散された[クライアントアクセスサーバーの Kerberos 認証の構成](https://technet.microsoft.com/library/ff808312(v=exchg.150).aspx)」を参照してください。  

Windows Server 2012 R2 または Windows Server 2012 で実行されている場合は、バックエンドサーバーで直接アプリケーションを構成することもできます。 詳細については、「 [Kerberos 認証の新機能](https://technet.microsoft.com/library/hh831747.aspx)」を参照してください。 また、Web アプリケーションプロキシサーバーが、バックエンドサーバーのサービスプリンシパル名への委任用に構成されていることを確認する必要があります。  

## <a name="publishing-remote-desktop-gateway-through-web-application-proxy"></a>Web アプリケーションプロキシを介したリモートデスクトップゲートウェイの公開  
リモートアクセスゲートウェイへのアクセスを制限し、リモートアクセスの事前認証を追加する場合は、Web アプリケーションプロキシ経由でロールアウトできます。 これは、MFA を含む RDG の高度な事前認証があることを確認するための優れた方法です。 事前認証を使用しない発行もオプションであり、システムに単一のエントリポイントを提供します。  

#### <a name="how-to-publish-an-application-in-rdg-using-web-application-proxy-pass-through-authentication"></a>Web アプリケーションプロキシパススルー認証を使用して RDG でアプリケーションを公開する方法  

1. RD Web アクセス (rdweb) ロールと RD ゲートウェイ (rpc) ロールが同じサーバー上にあるか、異なるサーバーにあるかによって、インストールが異なります。  

2. RD Web アクセスと RD ゲートウェイの役割が同じ RDG サーバーでホストされている場合は、単純 @no__t に、などの Web アプリケーションプロキシにルート FQDN を発行できます。  

   2つの仮想ディレクトリを個別に発行することもできます。たとえば、<https://rdg.contoso.com/rdweb/> および https://rdg.contoso.com/rpc/ です。  

3. RD Web アクセスと RD ゲートウェイが別の RDG サーバーでホストされている場合は、2つの仮想ディレクトリを個別に発行する必要があります。 @No__t-0 や https://gateway.contoso.com/rpc/ など、同じまたは異なる外部 FQDN を使用できます。  

4. 外部と内部の FQDN が異なる場合は、RDWeb 発行ルールで要求ヘッダーの変換を無効にしないでください。 これは、Web アプリケーションプロキシサーバーで次の PowerShell スクリプトを実行することで行うことができますが、既定で有効になっている必要があります。

   ```  
   Get-WebApplicationProxyApplication applicationname | Set-WebApplicationProxyApplication -DisableTranslateUrlInRequestHeaders:$false  
   ```  

   > [!NOTE]  
   > RemoteApp やデスクトップ接続、iOS リモートデスクトップ接続などのリッチクライアントをサポートする必要がある場合は、パススルー認証を使用して RDG を発行する必要があるため、事前認証はサポートされていません。  

#### <a name="how-to-publish-an-application-in-rdg-using-web-application-proxy-with-pre-authentication"></a>事前認証を使用して Web アプリケーションプロキシを使用して RDG でアプリケーションを公開する方法  

1.  RDG による Web アプリケーションプロキシの事前認証は、Internet Explorer によって取得された事前認証 cookie をリモートデスクトップ接続クライアント (mstsc.exe) に渡すことによって機能します。 これは、リモートデスクトップ接続クライアント (mstsc.exe) によって使用されます。 これは、認証の証明としてリモートデスクトップ接続クライアントによって使用されます。  

    次の手順では、クライアントに送信されるリモートアプリ RDP ファイルに必要なカスタム RDP プロパティを含めるようにコレクションサーバーに指示します。 これにより、事前認証が必要であることがクライアントに通知され、事前認証サーバーアドレスのクッキーがリモートデスクトップ接続クライアント (mstsc.exe) に渡されます。 Web アプリケーションプロキシアプリケーションで HttpOnly 機能を無効にすることによって、リモートデスクトップ接続クライアント (mstsc.exe) は、ブラウザーで取得した Web アプリケーションプロキシ cookie を利用できます。  

    RD Web アクセスサーバーへの認証では、引き続き RD Web アクセスフォームログオンが使用されます。 これにより、RD Web アクセスログオンフォームによってクライアント側の資格情報ストアが作成されるため、ユーザー認証のプロンプト数が少なくなります。これにより、それ以降のリモートアプリの起動には、リモートデスクトップ接続クライアント (mstsc.exe) で使用できます。  

2.  最初に、要求に対応するアプリを公開する場合と同じように、AD FS で手動の証明書利用者信頼を作成します。 これは、事前認証を強制するために必要なダミーの証明書利用者信頼を作成する必要があることを意味します。これにより、公開されたサーバーに Kerberos の制約付き委任を使用せずに事前認証を受けることができます。 ユーザーが認証されると、他のすべてのものが渡されます。  

    > [!WARNING]  
    > 委任を使用することをお勧めしますが、mstsc SSO 要件を完全には解決しません。また、/rpc ディレクトリに委任するときに問題が発生する可能性があります。これは、クライアントが RD ゲートウェイ認証自体を処理することを想定しているためです。  

3.  証明書利用者信頼を手動で作成するには、AD FS 管理コンソールの次の手順に従います。  

    1.  **証明書利用者信頼の追加**ウィザードを使用する  

    2.  **[証明書利用者に関するデータを手動で入力する]** を選択します。  

    3.  すべての既定の設定をそのまま使用します。  

    4.  [証明書利用者信頼の識別子] に、RDG アクセスに使用する外部 FQDN を入力します (たとえば https://rdg.contoso.com/ )。  

        これは、Web アプリケーションプロキシでアプリを公開するときに使用する証明書利用者の信頼です。  

4.  サイトのルート (たとえば、 https://rdg.contoso.com/ ) を Web アプリケーションプロキシに発行します。 事前認証を AD FS に設定し、上記で作成した証明書利用者信頼を使用します。 これにより、/rdweb と/rpc が同じ Web アプリケーションプロキシ認証 cookie を使用できるようになります。  

    /Rdweb と/rpc を別のアプリケーションとして公開し、公開されているサーバーを別々に使用することもできます。 証明書利用者信頼に対して Web アプリケーションプロキシトークンが発行されるのと同じ証明書利用者信頼を使用して両方を発行し、同じ証明書利用者信頼で発行された複数のアプリケーション間で有効にする必要があるだけです。  

5.  外部と内部の FQDN が異なる場合は、RDWeb 発行ルールで要求ヘッダーの変換を無効にしないでください。 これは、Web アプリケーションプロキシサーバーで次の PowerShell スクリプトを実行することで行うことができますが、既定で有効になっている必要があります。

    ```  
    Get-WebApplicationProxyApplication applicationname | Set-WebApplicationProxyApplication -DisableTranslateUrlInRequestHeaders:$false 
    ```  

6.  RDG で公開されているアプリケーションで、Web アプリケーションプロキシの HttpOnly クッキープロパティを無効にします。 RDG ActiveX コントロールが Web アプリケーションプロキシの認証 cookie にアクセスできるようにするには、Web アプリケーションプロキシ cookie の HttpOnly プロパティを無効にする必要があります。  

    そのためには、 [Web アプリケーションプロキシ修正プログラム](https://support.microsoft.com/en-gb/kb/3000850)または[https://support.microsoft.com/en-gb/kb/3000850](https://support.microsoft.com/en-gb/kb/3000850)がインストールされている必要があります。  

    修正プログラムをインストールした後、関連するアプリケーション名を指定して、Web アプリケーションプロキシサーバーで次の PowerShell スクリプトを実行します。  

    ```  
    Get-WebApplicationProxyApplication applicationname | Set-WebApplicationProxyApplication -DisableHttpOnlyCookieProtection:$true  
    ```  

    HttpOnly を無効にすると、RDG ActiveX コントロールが Web アプリケーションプロキシの認証クッキーにアクセスできるようになります。  

7.  コレクションサーバーで関連する RDG コレクションを構成して、rdp ファイルで事前認証が必要であることをリモートデスクトップ接続クライアント (mstsc.exe) に知らせます。  

    -   Windows Server 2012 および Windows Server 2012 R2 では、次の PowerShell コマンドレットを RDG コレクションサーバーで実行することによってこれを実現できます。  

        ```
        Set-RDSessionCollectionConfiguration -CollectionName "<yourcollectionname>" -CustomRdpProperty "pre-authentication server address:s: <https://externalfqdn/rdweb/>`nrequire pre-authentication:i:1"
        ```

        を独自の値に置き換える場合は、< と > の角かっこを必ず削除してください。次に例を示します。

        ```
        Set-RDSessionCollectionConfiguration -CollectionName "MyAppCollection" -CustomRdpProperty "pre-authentication server address:s: https://rdg.contoso.com/rdweb/`nrequire pre-authentication:i:1"
        ```

    -   Windows Server 2008 R2 の場合:  

        1.  管理者特権を持つアカウントを使用して、ターミナルサーバーにログオンします。  

        2.  [**スタート** >**管理ツール** > **ターミナルサービス** >  TS RemoteApp Manager] にアクセスし**ます。**  

        3.  TS RemoteApp Manager の **[概要]** ウィンドウで、RDP 設定 の横にある **[変更]** をクリックします。  

        4.  **カスタム Rdp 設定** タブで、カスタム rdp 設定 ボックスに次の rdp 設定を入力します。  

            `pre-authentication server address: s: https://externalfqdn/rdweb/`  

            `require pre-authentication:i:1`  

        5.  終了したら、 **[適用]** をクリックします。  

            これは、クライアントに送信される RDP ファイルにカスタム RDP プロパティを含めるようにコレクションサーバーに指示します。 これにより、事前認証が必要であることがクライアントに通知され、事前認証サーバーアドレスのクッキーがリモートデスクトップ接続クライアント (mstsc.exe) に渡されます。 これは、Web アプリケーションプロキシアプリケーションで HttpOnly を無効にする場合と組み合わせて使用することで、リモートデスクトップ接続クライアント (mstsc.exe) がブラウザーで取得した Web アプリケーションプロキシ認証クッキーを利用できるようにします。  

            RDP の詳細については、「 [TS ゲートウェイ OTP シナリオの構成](https://technet.microsoft.com/library/cc731249(v=ws.10).aspx)」を参照してください。  

## <a name="BKMK_Links"></a>関連項目  

-   [Web アプリケーションプロキシを使用してアプリケーションを公開することを計画する](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn383650(v=ws.11))  

-   [Web アプリケーション プロキシのトラブルシューティング](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn770156(v=ws.11))  

-   [Web アプリケーションプロキシのチュートリアルガイド](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn280944(v=ws.11))  
