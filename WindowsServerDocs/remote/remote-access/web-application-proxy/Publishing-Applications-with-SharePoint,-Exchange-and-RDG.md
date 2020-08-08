---
ms.assetid: 61ed00fd-51c7-4728-91fa-8501de9d8f28
title: SharePoint、Exchange、および RDG によるアプリケーションの発行
author: billmath
manager: mtillman
ms.author: billmath
ms.date: 04/30/2018
ms.topic: article
ms.openlocfilehash: 115a55ab9ddfde42027a991d172f92c3d62c4613
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87939793"
---
# <a name="publishing-applications-with-sharepoint-exchange-and-rdg"></a>SharePoint、Exchange、および RDG によるアプリケーションの発行

> 適用先:Windows Server 2016

**このコンテンツは、オンプレミスバージョンの Web アプリケーションプロキシに関連しています。クラウド経由でオンプレミスアプリケーションへの安全なアクセスを実現するには、 [Azure AD アプリケーションプロキシのコンテンツ](/azure/active-directory/manage-apps/application-proxy)を参照してください。**

このトピックでは、Web アプリケーションプロキシを介して SharePoint Server、Exchange Server、またはリモートデスクトップゲートウェイ (RDP) を公開するために必要なタスクについて説明します。

> [!NOTE]
> この情報はそのとおりに提供されます。  リモートデスクトップサービスでは、Azure アプリプロキシを使用して、[オンプレミスアプリケーションへの安全なリモートアクセスを提供する](/azure/active-directory/active-directory-application-proxy-get-started)ことをサポートしています。

## <a name="publish-sharepoint-server"></a><a name="BKMK_6.1"></a>SharePoint Server の公開
Sharepoint サイトが要求ベースの認証または統合 Windows 認証用に構成されている場合は、Web アプリケーションプロキシを介して SharePoint サイトを発行できます。 事前認証に Active Directory フェデレーションサービス (AD FS) (AD FS) を使用する場合は、いずれかのウィザードを使用して証明書利用者を構成する必要があります。

-   SharePoint サイトで要求ベース認証を使用する場合、証明書利用者信頼の追加ウィザードを利用し、アプリケーションに証明書利用者信頼を構成する必要があります。

-   SharePoint サイトで統合 Windows 認証を使用する場合、非要求ベースの証明書利用者信頼の追加ウィザードを利用し、アプリケーションに証明書利用者信頼を構成する必要があります。 KDC を構成する場合、要求ベースの Web アプリケーションと共に IWA を使用できます。

    統合 Windows 認証を使用してユーザーを認証できるようにするには、Web アプリケーションプロキシサーバーがドメインに参加している必要があります。

    Kerberos 制約の委任をサポートするようにアプリケーションを構成する必要があります。 この作業は、どのアプリケーションについてもドメイン コントローラーで実行できます。 Windows Server 2012 R2 または Windows Server 2012 で実行されている場合は、バックエンドサーバーで直接アプリケーションを構成することもできます。 詳細については、「 [Kerberos 認証の新機能](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831747(v=ws.11))」を参照してください。 また、Web アプリケーションプロキシサーバーが、バックエンドサーバーのサービスプリンシパル名への委任用に構成されていることを確認する必要があります。 統合 Windows 認証を使用してアプリケーションを公開するように Web アプリケーションプロキシを構成する方法のチュートリアルについては、「[統合 windows 認証を使用する](/previous-versions/orphan-topics/ws.11/dn308246(v=ws.11))ようにサイトを構成する」を参照してください。

SharePoint サイトを代替アクセス マッピング (AAM) とホスト名の付いたサイト コレクションのいずれかを利用して構成する場合、異なる外部 URL とバックエンド サーバー URL を使用してアプリケーションを公開できます。 ただし、AAM またはホスト名の付いたサイト コレクションを使用して SharePoint サイトを構成しない場合、同じ外部 URL とバックエンド サーバー URL を使用する必要があります。

## <a name="publish-exchange-server"></a><a name="BKMK_6.2"></a>Exchange Server の公開
次の表は、Web アプリケーションプロキシ経由で公開できる Exchange サービスと、これらのサービスに対してサポートされている事前認証を示しています。


|    Exchange サービス    |                                                                            事前認証                                                                            |                                                                                                                                       メモ                                                                                                                                        |
|------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    Outlook Web アプリ     | -要求ベースでない認証を使用して AD FS<br />-パススルー<br />-オンプレミス Exchange 2013 サービスパック 1 (SP1) の要求ベースの認証を使用して AD FS |                                                                  詳細については、次のトピックを参照してください。 [AD FS のクレームベース認証を Outlook Web App および EAC で使用する](https://go.microsoft.com/fwlink/?LinkId=393723)                                                                  |
| Exchange コントロール パネル |                                                                               パススルー                                                                               |                                                                                                                                                                                                                                                                                    |
|    Outlook Anywhere    |                                                                               パススルー                                                                               | Outlook Anywhere を正しく機能させるには 3 つの URL を公開する必要があります。<p>-自動検出 URL。<br />-Exchange サーバーの外部ホスト名。これは、クライアントが接続するために構成されている URL です。<br />-Exchange サーバーの内部 FQDN。 |
|  Exchange ActiveSync   |                                                     パススルー<br/> HTTP 基本認証プロトコルを使用した AD FS                                                      |                                                                                                                                                                                                                                                                                    |

統合 Windows 認証を使用して Outlook Web アプリを公開するには、非要求ベースの証明書利用者信頼の追加ウィザードを利用し、アプリケーションに証明書利用者信頼を構成する必要があります。

Kerberos の制約付き委任を使用してユーザーを認証できるようにするには、Web アプリケーションプロキシサーバーがドメインに参加している必要があります。

Kerberos 認証をサポートするようにアプリケーションを構成する必要があります。 さらに、web サービスが実行されているアカウントにサービスプリンシパル名 (SPN) を登録する必要があります。 これは、ドメインコントローラーまたはバックエンドサーバーで実行できます。 負荷分散された Exchange 環境では、別のサービスアカウントを使用する必要があります。「負荷分散された[クライアントアクセスサーバーの Kerberos 認証の構成](/exchange/configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help)」を参照してください。

Windows Server 2012 R2 または Windows Server 2012 で実行されている場合は、バックエンドサーバーで直接アプリケーションを構成することもできます。 詳細については、「 [Kerberos 認証の新機能](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831747(v=ws.11))」を参照してください。 また、Web アプリケーションプロキシサーバーが、バックエンドサーバーのサービスプリンシパル名への委任用に構成されていることを確認する必要があります。

## <a name="publishing-remote-desktop-gateway-through-web-application-proxy"></a>Web アプリケーションプロキシを介したリモートデスクトップゲートウェイの公開
リモートアクセスゲートウェイへのアクセスを制限し、リモートアクセスの事前認証を追加する場合は、Web アプリケーションプロキシ経由でロールアウトできます。 これは、MFA を含む RDG の高度な事前認証があることを確認するための優れた方法です。 事前認証を使用しない発行もオプションであり、システムに単一のエントリポイントを提供します。

#### <a name="how-to-publish-an-application-in-rdg-using-web-application-proxy-pass-through-authentication"></a>Web アプリケーションプロキシパススルー認証を使用して RDG でアプリケーションを公開する方法

1. RD Web アクセス (rdweb) ロールと RD ゲートウェイ (rpc) ロールが同じサーバー上にあるか、異なるサーバーにあるかによって、インストールが異なります。

2. RD Web アクセスと RD ゲートウェイの役割が同じ RDG サーバーでホストされている場合は、単に、などの Web アプリケーションプロキシにルート FQDN を発行でき https://rdg.contoso.com/ ます。

   2つの仮想ディレクトリ (やなど) を個別に発行することもできます <https://rdg.contoso.com/rdweb/> https://rdg.contoso.com/rpc/ 。

3. RD Web アクセスと RD ゲートウェイが別の RDG サーバーでホストされている場合は、2つの仮想ディレクトリを個別に発行する必要があります。 同じまたは異なる外部 FQDN (やなど) を使用 https://rdweb.contoso.com/rdweb/ でき https://gateway.contoso.com/rpc/ ます。

4. 外部と内部の FQDN が異なる場合は、RDWeb 発行ルールで要求ヘッダーの変換を無効にしないでください。 これは、Web アプリケーションプロキシサーバーで次の PowerShell スクリプトを実行することで行うことができますが、既定で有効になっている必要があります。

   ```PowerShell
   Get-WebApplicationProxyApplication applicationname | Set-WebApplicationProxyApplication -DisableTranslateUrlInRequestHeaders:$false
   ```

   > [!NOTE]
   > RemoteApp やデスクトップ接続、iOS リモートデスクトップ接続などのリッチクライアントをサポートする必要がある場合は、パススルー認証を使用して RDG を発行する必要があるため、事前認証はサポートされていません。

#### <a name="how-to-publish-an-application-in-rdg-using-web-application-proxy-with-pre-authentication"></a>事前認証を使用して Web アプリケーションプロキシを使用して RDG でアプリケーションを公開する方法

1.  RDG による Web アプリケーションプロキシの事前認証は、Internet Explorer によって取得された事前認証 cookie をリモートデスクトップ接続クライアント (mstsc.exe) に渡すことによって機能します。 これは、リモートデスクトップ接続クライアント (mstsc.exe) によって使用されます。 これは、認証の証明としてリモートデスクトップ接続クライアントによって使用されます。

    次の手順では、クライアントに送信されるリモートアプリ RDP ファイルに必要なカスタム RDP プロパティを含めるようにコレクションサーバーに指示します。 これにより、事前認証が必要であることがクライアントに伝えられ、事前認証サーバーアドレスのクッキーがリモートデスクトップ接続クライアント (mstsc.exe) に渡されます。 Web アプリケーションプロキシアプリケーションで HttpOnly 機能を無効にすることと共に、リモートデスクトップ接続クライアント (mstsc.exe) は、ブラウザーを通じて取得した Web アプリケーションプロキシの cookie を利用できます。

    RD Web アクセスサーバーへの認証では、引き続き RD Web アクセスフォームログオンが使用されます。 これにより、RD Web アクセスログオンフォームによってクライアント側の資格情報ストアが作成され、それ以降のリモートアプリ起動時にリモートデスクトップ接続クライアント (mstsc.exe) が使用できるようになるため、ユーザー認証のプロンプト数が少なくなります。

2.  最初に、要求に対応するアプリを公開する場合と同じように、AD FS で手動の証明書利用者信頼を作成します。 これは、事前認証を強制するために必要なダミーの証明書利用者信頼を作成する必要があることを意味します。これにより、公開されたサーバーに Kerberos の制約付き委任を使用せずに事前認証を受けることができます。 ユーザーが認証されると、他のすべてのものが渡されます。

    > [!WARNING]
    > 委任を使用することをお勧めしますが、mstsc SSO 要件を完全には解決しません。また、/rpc ディレクトリに委任するときに問題が発生する可能性があります。これは、クライアントが RD ゲートウェイ認証自体を処理することを想定しているためです。

3.  証明書利用者信頼を手動で作成するには、AD FS 管理コンソールの次の手順に従います。

    1.  **証明書利用者信頼の追加**ウィザードを使用する

    2.  [**証明書利用者に関するデータを手動で入力する**] を選択します。

    3.  すべての既定の設定をそのまま使用します。

    4.  証明書利用者信頼の識別子には、たとえば、RDG アクセスに使用する外部 FQDN を入力し https://rdg.contoso.com/ ます。

        これは、Web アプリケーションプロキシでアプリを公開するときに使用する証明書利用者の信頼です。

4.  サイトのルート (たとえば、 https://rdg.contoso.com/ ) を Web アプリケーションプロキシに発行します。 事前認証を AD FS に設定し、上記で作成した証明書利用者信頼を使用します。 これにより、/rdweb と/rpc が同じ Web アプリケーションプロキシ認証 cookie を使用できるようになります。

    /Rdweb と/rpc を別のアプリケーションとして公開し、公開されているサーバーを別々に使用することもできます。 証明書利用者信頼に対して Web アプリケーションプロキシトークンが発行されるのと同じ証明書利用者信頼を使用して両方を発行し、同じ証明書利用者信頼で発行された複数のアプリケーション間で有効にする必要があるだけです。

5.  外部と内部の FQDN が異なる場合は、RDWeb 発行ルールで要求ヘッダーの変換を無効にしないでください。 これは、Web アプリケーションプロキシサーバーで次の PowerShell スクリプトを実行することで行うことができますが、既定で有効になっている必要があります。

    ```PowerShell
    Get-WebApplicationProxyApplication applicationname | Set-WebApplicationProxyApplication -DisableTranslateUrlInRequestHeaders:$true
    ```

6.  RDG で公開されているアプリケーションで、Web アプリケーションプロキシの HttpOnly クッキープロパティを無効にします。 RDG ActiveX コントロールが Web アプリケーションプロキシの認証 cookie にアクセスできるようにするには、Web アプリケーションプロキシ cookie の HttpOnly プロパティを無効にする必要があります。

    このためには、 [WINDOWS RT 8.1、Windows 8.1、および Windows Server 2012 R2 (が kb3000850) の2014年11月の更新プログラムのロールアップ](https://support.microsoft.com/kb/3000850)をインストールする必要があります。

    修正プログラムをインストールした後、関連するアプリケーション名を指定して、Web アプリケーションプロキシサーバーで次の PowerShell スクリプトを実行します。

    ```PowerShell
    Get-WebApplicationProxyApplication applicationname | Set-WebApplicationProxyApplication -DisableHttpOnlyCookieProtection:$true
    ```

    HttpOnly を無効にすると、RDG ActiveX コントロールが Web アプリケーションプロキシの認証クッキーにアクセスできるようになります。

7.  コレクションサーバーで関連する RDG コレクションを構成して、rdp ファイルで事前認証が必要であることをリモートデスクトップ接続クライアント (mstsc.exe) に知らせます。

    -   Windows Server 2012 および Windows Server 2012 R2 では、次の PowerShell コマンドレットを RDG コレクションサーバーで実行することによってこれを実現できます。

        ```PowerShell
        Set-RDSessionCollectionConfiguration -CollectionName "<yourcollectionname>" -CustomRdpProperty "pre-authentication server address:s: <https://externalfqdn/rdweb/>`nrequire pre-authentication:i:1"
        ```

        を独自の値に置き換える場合は、< と > の角かっこを必ず削除してください。次に例を示します。

        ```PowerShell
        Set-RDSessionCollectionConfiguration -CollectionName "MyAppCollection" -CustomRdpProperty "pre-authentication server address:s: https://rdg.contoso.com/rdweb/`nrequire pre-authentication:i:1"
        ```

    -   Windows Server 2008 R2 では、次の操作を行います。

        1.  管理者特権を持つアカウントを使用して、ターミナルサーバーにログオンします。

        2.  [**スタート**] [  > **管理ツール**] [  >  **ターミナルサービス**TS RemoteApp マネージャー] にアクセス  >  **します。**

        3.  TS RemoteApp Manager の [**概要**] ウィンドウで、[RDP 設定] の横にある [**変更**] をクリックします。

        4.  [**カスタム Rdp 設定**] タブで、[カスタム rdp 設定] ボックスに次の rdp 設定を入力します。

            `pre-authentication server address: s: https://externalfqdn/rdweb/`

            `require pre-authentication:i:1`

        5.  終了したら、[**適用**] をクリックします。

            これは、クライアントに送信される RDP ファイルにカスタム RDP プロパティを含めるようにコレクションサーバーに指示します。 これにより、事前認証が必要であることがクライアントに通知され、事前認証サーバーアドレスのクッキーがリモートデスクトップ接続クライアント (mstsc.exe) に渡されます。 これは、Web アプリケーションプロキシアプリケーションで HttpOnly を無効にすることと組み合わせて使用することで、リモートデスクトップ接続クライアント (mstsc.exe) は、ブラウザーで取得した Web アプリケーションプロキシ認証 cookie を利用できます。

            RDP の詳細については、「 [TS ゲートウェイ OTP シナリオの構成](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc731249(v=ws.10))」を参照してください。

## <a name="see-also"></a><a name="BKMK_Links"></a>関連項目

- [Web アプリケーション プロキシを使用してアプリケーションを公開することを計画する](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn383650(v=ws.11))

- [Web アプリケーション プロキシのトラブルシューティング](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn770156(v=ws.11))

- [Web アプリケーション プロキシのチュートリアル ガイド](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/dn280944(v=ws.11))
