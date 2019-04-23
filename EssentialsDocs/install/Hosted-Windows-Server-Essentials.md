---
title: ホスト型 Windows Server Essentials
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fda5628c-ad23-49de-8d94-430a4f253802
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 1b78432ca92028bc96b2cbfc9fa40196f61e8bf8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833703"
---
# <a name="hosted-windows-server-essentials"></a>ホスト型 Windows Server Essentials

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

このドキュメントには、ホスト側は、ラボで Windows Server Essentials を展開し、サービスとしての Windows Server Essentials を顧客に提供するユーザーに固有の情報が含まれます。  
  
## <a name="what-is-windows-server-essentials"></a>Windows Server Essentials とは何ですか。  
 Windows Server Essentials は、ほとんどの小規模企業に適したサーバー環境を実現する最良の 64 ビット製品テクノロジが組み込まれています、クロスプレミスの小規模ビジネス ソリューションです。 Windows Server Essentials では、次のテクノロジが含まれます。  
  
 **サーバーのオペレーティング システム:** Windows Server 2012 製品テクノロジでは、Windows Server Essentials のコアを提供します。 詳しくは、 [Windows Server 2012 の Web サイト](https://www.microsoft.com/en-us/server-cloud/products/windows-server-2012-r2/default.aspx#fbid=ZH0GD_CRAWh)をご覧ください。  
  
 **データ保護:** Windows Server Essentials では、大幅に強化されたデータ保護機能を提供する Windows Server 2012 で使用できるいくつかの新しい機能を活用します。 [新しい記憶域機能](https://technet.microsoft.com/library/hh831739.aspx) により、異種ハード ドライブの物理記憶域容量の集計、ハード ドライブの動的な追加、復元レベルを指定したデータ ボリュームの作成が可能となりました。 Windows Server Essentials は、完全なシステム バックアップを実行して、自体だけでなく、ネットワークに接続されているクライアント コンピューターに、サーバーのベア メタル復元しますか? 2 TB を超えるボリューム対応のようになりました。 Windows Server 2012 の新機能として、 [Windows Azure Online Backup](https://technet.microsoft.com/library/hh831419.aspx) を使用して、Microsoft が管理しているクラウドベースの記憶域サービス内のファイルとフォルダーを保護できます。 Windows Server Essentials も一元的に管理し、ユーザーが管理者の支援を必要とせず、誤って削除または上書きされたファイルから回復する際に役立つ、Windows 8.1 クライアントのファイル履歴機能を構成します。  
  
 **Anywhere Access:** リモート Web アクセスにより、簡単なタッチ操作に適したブラウザーを使用し、インターネット接続を介して事実上どこからでもアプリケーションやデータにアクセスし、任意のデバイスを使用することができます。 Windows Server Essentials もは更新された Windows Phone アプリと新しいアプリを Windows 8.1 クライアントのコンピューター、直感的にユーザーを許可するのに全体の検索、接続、サーバーのファイルとフォルダーのアクセスします。 また、オフライン アクセスの場合、ファイルが自動的にキャッシュされ、サーバーへの接続が可能になったときに同期されます。 Windows Server Essentials をほんの数回のクリックの簡単、ウィザードによるプロセスの仮想プライベート ネットワーク (VPN) の設定をオンにおよび、ユーザーに対する VPN アクセスの管理を簡略化します。 クライアント コンピューターは、VPN 接続を利用して Windows SBS 環境にリモートで参加できるため、オフィスに通う必要がなくなります。  
  
 **ワークロードの柔軟性:** Windows Server Essentials は、顧客がどのアプリケーションとサービスをオンプレミスで実行し、どれをクラウドで実行を選択できる柔軟性をできるように設計されています。 前のバージョンでは、Windows Small Business Server Standard に Exchange Server がコンポーネント製品として含まれており、クラウドベースのメッセージングおよびコラボレーション サービスを利用する顧客にとって、コスト高と複雑化の要因となっていました。 Windows Server Essentials では、顧客活用すること、同じ種類の統合管理エクスペリエンスの Exchange Server のオンプレミスのコピーを実行、ホストされた Exchange サービスへのサブスクライブ、または Microsoft Office 365 をサブスクライブすることを選択するかどうか。  
  
 **正常性の監視:** Windows Server Essentials では、独自の正常性状態と 10.5 以降、Windows 8.1、Windows 7、および Mac OS X バージョンを実行するクライアント コンピューターの状態を監視します。 正常性状態では、コンピューターのバックアップ、サーバー記憶域、ディスク領域不足などに関連する案件または問題が通知されます。  
  
 **拡張性:** Windows Server Essentials は、コア製品に機能と機能を追加するには、他のソフトウェア ベンダーは、web サービス Api の新しいセットを追加する Windows SBS 2011 Essentials の機能拡張モデルに基づいています。 既存の [ソフトウェア開発キット](https://msdn.microsoft.com/library/gg513958.aspx) (SDK) や Windows SBS 2011 Essentials 用に作成された [アドイン](https://pinpoint.microsoft.com/applications/search?fpt=300105&q=small+business+server+essentials) との互換性も保持されます。  
  
## <a name="how-can-i-customize-an-image"></a>イメージをカスタマイズする方法  
 参照してください、 [Windows Server Essentials](https://go.microsoft.com/fwlink/p/?LinkID=249124)、これは Windows Server Essentials のカスタマイズ手順が追加された標準の Windows Server sysprep プロセスです。 カスタマイズを完了するには、「 [単純なカスタマイズ イメージの作成](https://technet.microsoft.com/library/jj200117) 」と「 [イメージのカスタマイズ](https://technet.microsoft.com/library/jj200161)」の手順に従った後、「 [イメージの展開の準備](https://technet.microsoft.com/library/jj200142) 」の手順に従って、最終イメージをキャプチャします。  
  
 次の点に注意を払う必要があります。  
  
1.  SkipIC.txt ファイルを任意のドライブのルートに追加することにより、初期構成 (IC) をスキップする必要があります。 サーバーをインストールした後、IC の前に、Shift キーを押しながら F10 を押してコマンド プロンプト ウィンドウを起動し、C:/ ドライブの下に SkipIC.txt ファイルを作成します。 カスタマイズ後、この SkipIC.txt ファイルを必ず削除する必要があります。  
  
2.  90 GB より小さいディスク上の Windows Server Essentials を展開する必要がある場合は、sysprep の前にレジストリ キーを追加する必要があります。  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v HWRequirementChecks /t REG_DWORD /d 0 /f  
    ```  
  
 sysprep 後、sysprep 済みのディスク イメージを使用するか、または新しいデプロイメント用に Install.wim に再シールできます。  
  
 Virtual Machine Manager を使用している場合、実行中のインスタンスを使用してテンプレートを作成できます。 テンプレートを作成すると、インスタンスが sysprep され、サーバーがシャットダウンします。 ライブラリに格納した後、インスタンスをケースバイケースで起動できます。  
  
##  <a name="BKMK_automatedeployment"></a> デプロイメントを自動化する方法は?  
 カスタマイズしたイメージを取得したら、独自のイメージを使ってデプロイメントを実行できます。 半無人インストールを実行するには、WinPE セットアップ用の unattend.xml を提供/展開する必要があります。 完全な無人インストールには、Windows Server Essentials の初期構成の cfg.ini ファイルを提供する必要があります。  
  
1.  無人 WinPE セットアップのみを実行します。 これにより、WinPE セットアップのみが自動化されます。初期構成前にインストールを停止し、エンド ユーザーが RDP 後に自分で会社、ドメイン、管理者情報をサーバー セッションに提供できるようにします。 これには、次の手順を実行します。  
  
    1.  Windows unattend.xml ファイルを提供します。 に従って、 [Windows 8.1 ADK](https://go.microsoft.com/fwlink/?LinkId=248694)をファイルを生成し、サーバー名、プロダクト キー、および管理者のパスワードを含むすべての必要な情報を提供します。 Unattend.xml ファイルの「Microsoft Windows のセットアップ」セクション次に示す情報を提供します。  
  
        ```  
        <InstallFrom>  
                 <MetaData>  
                     <Key>IMAGE/WINDOWS/EDITIONID</Key>  
                     <Value>ServerSolution</Value>  
                 </MetaData>  
                 <MetaData>  
                     <Key>IMAGE/WINDOWS/INSTALLATIONTYPE</Key>  
                     <Value>Server</Value>  
                 </MetaData>  
           </InstallFrom>  
        ```  
  
    2.  顧客は初期構成を完了管理者と、サーバーに rdp で接続する unattend.xml ファイルで指定されたパスワードを使用できるように、パブリック IP の RDP ポート 3389 を開く必要があります。  
  
    > [!NOTE]
    >  既定のパスワードを変更しない場合、サーバー インストールはパスワードの入力を求める画面で停止します。**注** エンド ユーザーは、既定の管理者アカウントを使用してサーバーにログオンし、初期構成を実行する必要があります。  
  
 Virtual Machine Manager を使用している場合、テンプレートから新しいインストールを作成したときに、コンソールで管理者パスワードを指定できます。  
  
1.  無人初期構成を含む、完全無人セットアップを実行します。 これには、次の手順を実行します。  
  
    1.  デプロイメントを WinPE セットアップから開始した場合、上で実行した方法で unattend.xml ファイルを指定します。  
  
    2.  Windows Server Essentials ADK セクションを参照して[Cfg.ini ファイルの作成](https://technet.microsoft.com/library/jj200150)cfg.ini を生成します。  
  
    3.  [InitialConfiguration] に情報を指定します。  
  
        ```  
        WebDomainName=yourdomainname  
        TrustedCertFileName=c:\cert\a.pfx  
        TrustedCertPassword=Enteryourpassword  
        EnableVPN=true  
        EnableRWA=true  
        ; Provide all information so that after setup is complete, your customer can use your domain name to visit the server directly with the admin/user information you provide in the [InitialConfiguration] section.  
  
        VpnIPv4StartAddress=<IPV4Address>  
        VpnIPv4EndAddress=<IPV4Address>  
        VpnBaseIPv6Address=<IPV6Address>  
        VpnIPv6PrefixLength=<number>  
        ; Provide this information. IPv4StartAddress and IPv4Endaddress are required so that your VPN client can acquire valid IP through this range.  
  
        IPv4DNSForwarder=<IPV4Address,IPV4Address,Â¦>  
        IPv6DNSForwarder=<IPV6Address,IPV6Address,Â¦>  
        ; Provide this information as needed according to your network environment settings.  
        ```  
  
    4.  [PostOSInstall] に情報を指定します。  
  
        ```  
        IsHosted=true   
        ; Must have, this will prevent Initial Configure webpage available for other computers under same subnet.  
  
        StaticIPv4Address=<IPV4Address>  
        StaticIPv4Gateway=<IPV4Address>  
        StaticIPv6Address=<IPV6Address>  
        StaticIPv6SubnetPrefixLength=<number>  
        StaticIPv6Gateway=<IPV6Address>  
        ; All these are optional if you have DHCP Server Service on the subnet, otherwise provide static IP here.  
        ```  
  
    5.  WebDomainName パラメーターを指定する場合は、サーバーのパブリック IP をポイントする DNS レコードも更新されていることを確認してください。  
  
    6.  上の WebDomainName 情報を指定しなかった場合、ポート 3389 を開いて、顧客が RDP を使用してサーバーに接続し、VPN 構成を終了できるようにします。  
  
> [!NOTE]
>  VM のホスト サーバーと Windows Server Essentials の VM のタイム ゾーン設定が同じであることを確認します。 同じでないと、さまざまなエラーが発生する可能性があります (証明書関連タスクで初期構成が失敗する、証明書がインストール後に数時間機能しない、デバイス情報が正しく更新されない、など)。  
  
 デプロイメント後、HKLM\software\microsoft\windows server\setup で次のレジストリ キーをチェックし、初期構成が成功したかどうかを確認します。 SetupStage == ICDone && ICStatus == 1 の場合、初期構成が正常に完了したことを示します。  
  
## <a name="what-is-the-supported-network-topology"></a>サポートされているネットワーク トポロジについて  
 Windows Server Essentials をローミング クライアントから使用するには、VPN を有効にする必要があります。 VPN SSTP 接続の場合、ポート 443 を有効にすることをお勧めします。 リモート Web アクセスまたは Web Service アプリにメディア サーバー機能が必要な場合、ポート 80 も有効にする必要があります。  
  
 VPN の有効化は、Windows PowerShell スクリプトを介して無人デプロイメント中に実行できます。または、初期構成後にウィザードを使って構成できます。  
  

-   無人デプロイメント中に VPN を有効にするには、このドキュメントの「 [How do I automate the deployment?](Hosted-Windows-Server-Essentials.md#BKMK_automatedeployment) 」を参照してください。  

-   無人デプロイメント中に VPN を有効にするには、このドキュメントの「 [How do I automate the deployment?](../install/Hosted-Windows-Server-Essentials.md#BKMK_automatedeployment) 」を参照してください。  

  
-   Windows PowerShell 経由で VPN を有効にするには、管理者権限で次のコマンドレットを実行し、必要なすべての情報を指定します。  
  
    ```  
    ##  
    ## To configure external domain and SSL certificate (if not yet done in unattended Initial Configuration).  
    ##  
  
    $myExternalDomainName = 'remote.contoso.com';   ## corresponds to A or AAAA DNS record(s) that can be resolved on Internet and routed to the server  
    $mySslCertificateFile = 'C:\ssl.pfx';   ## full path to SSL certificate file  
    $mySslCertificatePassword = ConvertTo-SecureString '******';   ## password for private key of the SSL certificate  
    $skipCertificateVerification = $true;   ## whether or not, skip verification for the SSL certificate  
  
    Add-Type -AssemblyName 'Wssg.Web.DomainManagerObjectModel';  
    [Microsoft.WindowsServerSolutions.RemoteAccess.Domains.DomainConfigurationHelper]::SetDomainNameAndCertificate($myExternalDomainName,$mySslCertificateFile,$mySslCertificatePassword,$skipCertificateVerification);  
    ##  
    ## To install VPN with static IPv4 pool (and allow all existing users to establish VPN).  
    ##  
  
    Install-WssVpnServer -IPv4AddressRange ('192.168.0.160','192.168.0.240') -ApplyToExistingUsers;  
    ```  
  
 サーバーを顧客に渡す前に VPN 接続を提供できない場合、サーバー ポート 3389 がインターネットに到達可能であることを確認し、エンド ユーザーが RDP を使用してサーバーに接続し、自分たちで構成を実行できるようにします。  
  
 ここでは、2 つの代表的なサーバー側のネットワーク トポロジと、VPN/リモート Web アクセス (RWA) の構成のしかたを示します。  
  
-   トポロジ 1 (推奨)  
  
    -   サーバーは、別の仮想ネットワークの NAT デバイスの下に存在します。  
  
    -   DHCP サービスが仮想ネットワークで有効になっているか、サーバーが静的 IP アドレスを使って割り当てられています。  
  
    -   サーバー ポート 443 に、パブリック IP ポート 443 から到達可能です。  
  
    -   VPN パススルーが、ポート 443 に対して許可されています。  
  
    -   VPN IPv4 アドレス プールの範囲は、サーバー アドレスの同じサブネット内である必要があります。  
  
    -   2 番目のサーバーには、同じサブネット内の、VPN アドレス プールの外にある静的 IP アドレスを割り当てる必要があります。  
  
-   トポロジ 2:  
  
    -   サーバーは、プライベート IP アドレスを所有しています。  
  
    -   サーバー上のポート 443 は、パブリック IP アドレスのポート 443 から到達可能です。  
  
    -   VPN パススルーが、ポート 443 に対して許可されています。  
  
    -   VPN IPv4 アドレス プールは、異なる範囲のサーバー アドレスに存在します。  
  
 トポロジ 2 では、2 つ目のサーバーのシナリオはサポートされていません。  
  
## <a name="how-do-i-perform-common-tasks-via-windows-powershell"></a>Windows PowerShell を経由して共通のタスクを実行する方法  
 **リモート Web アクセスを有効にします。**  
  
```  
Enable-WssRemoteWebAccess [-SkipRouter] [-DenyAccessByDefault] [-ApplyToExistingUsers]  
```  
  
 以下に例を示します。  
  
```  
$Enable-WssRemoteWebAccess  œDenyAccessByDefault  œApplyToExistingUsers  
```  
  
 このコマンドは、ルーターを自動的に構成する設定でリモート Web アクセスを有効にし、すべての既存ユーザーの既定のアクセス許可を変更します。  
  
 **ユーザーを追加します。**  
  
```  
Add-WssUser [-Name] <string> [-Password] <securestring> [-AccessLevel <string> {User | Administrator}] [-FirstName <string>] [-LastName <string>] [-AllowRemoteAccess] [-AllowVpnAccess]   [<CommonParameters>]  
```  
  
 以下に例を示します。  
  
```  
$password = ConvertTo-SecureString "Passw0rd!" -asplaintext  œforce  
$Add-WssUser -Name User2Test -Password $password -Accesslevel Administrator -FirstName User2 -LastName Test  
```  
  
 このコマンドでは、管理者パスワード Passw0rd User2Test をという名前を追加しました。  
  
 **ユーザーの有効化/無効化**  
  
 以下に例を示します。  
  
```  
$CurrentUser = get-wssuser  œname user2test  
$CurrentUser.UserStatus = 0  
$CurrentUser.Commit()  
```  
  
 このコマンドは、user2test という名前のユーザーを無効になります。 UserStatus を 1 に設定すると、このユーザーが有効になります。  
  
 **サーバー フォルダーを追加します。**  
  
```  
Add-WssFolder [-Name] <string> [-Path] <string> [[-Description] <string>] [-KeepPermissions] [<CommonParameters>]  
```  
  
 以下に例を示します。  
  
```  
$Add-WssFolder -Name "MyTestFolder" -Path "C:\ServerFolders\MyTestFolder"  
```  
  
 このコマンドでは、指定した位置に MyTestFolder をという名前のサーバー フォルダーを追加します。  
  
## <a name="how-do-i-add-a-second-server-to-the-windows-server-essentials-domain"></a>Windows Server Essentials ドメインに 2 番目のサーバーを追加する方法  
 Windows Server Essentials は、ドメイン コント ローラーであるために、2 番目のサーバーを標準の方法でドメインに参加できます。  
  
## <a name="which-email-solutions-can-be-integrated"></a>統合できる電子メール ソリューション  
 Windows Server Essentials には、2 つの電子メール ソリューションすぐとの統合がサポートされています。Office 365 と社内 Exchange の、2 つの Out-of-Box 電子メール ソリューションをサポートしています。 ホスト型電子メール ソリューションを実行している場合は、ホスト型電子メール ソリューションと Windows Server Essentials を統合するアドインを開発する必要があります。  
  
## <a name="how-do-i-migrate-on-premises-windows-sbs-201120082003-to-the-hosted-windows-server-essentials"></a>ホスト型 Windows Server Essentials をオンプレミス Windows SBS (2011/2008/2003) を移行する方法  
 移行ガイドは、オンプレミス Windows Small Business Server (Windows SBS) Windows Server Essentials への移行からに使用できます。 ホスト環境に応じて、手順の一部が多少異なる場合があります。 ただし、一般的なタスクおよび移行するワークロードは同じはずです。 [移行ガイド](https://go.microsoft.com/fwlink/p/?LinkID=254292) を参照し、ホスト環境に基づいて必要なカスタマイズを行うことをお勧めします。  
  
 ソース サーバーと移行先サーバーを同じサブネットに配置することをお勧めします。 それが無理な場合、次の点を確認する必要があります。  
  
-   ソース サーバーと移行先サーバーの内部 DNS 名に、互いに到達できる。  
  
-   すべての必要なポートが開いている。  
  
## <a name="how-can-i-upgrade-windows-server-essentials-to-windows-server-standard"></a>Windows Server Essentials を Windows Server Standard にアップグレードする方法はでしょうか。  
 Windows Server Essentials は、Windows Server Standard にアップグレードできます。 ロックと制限を削除し、Windows Server Standard に足りないパッケージを追加します。 詳細については、 [ドキュメントをダウンロードしてください](https://go.microsoft.com/fwlink/p/?LinkID=253181)。  
  
## <a name="what-are-the-native-tools-for-monitoring-and-management"></a>監視と管理のためのネイティブ ツール  
  
### <a name="group-policy-management"></a>グループ ポリシー管理  
 Windows Server Essentials では、Windows Server 2012 でのネイティブ グループ ポリシー サポートを利用し、フォルダー リダイレクトとセキュリティ設定を構成するためのユーザー インターフェイスを提供します。  
  
> [!NOTE]
>  ホストされている環境では、ユーザー プロファイルのフォルダーのリダイレクションが有効になっている場合、データ サイズが大きいと、エンド ユーザーのログオンに時間がかかる可能性があります。  
  
### <a name="management-pack"></a>管理パック  
 Windows Server Essentials 用管理パックは、ホストが多数のさまざまな小規模企業に専用の Windows Server Essentials サーバーを管理する Windows Server Essentials での正常性アラート システム経由での監視機能を提供します。 このバージョンでの監視には、システムの重要なアラートだけが含まれます。  
  
#### <a name="management-pack-scope"></a>管理パックの範囲  
 この管理パックを使用して、Windows Server Essentials に固有の機能を監視するのに役立ちます。 Windows Server 2012 Standard オペレーティング システムの一般的な機能は監視しません。 Windows Server Essentials を監視するには、Windows Server Essentials の管理パックと、管理パックの Windows Server 2012 Standard の両方を使用する必要があります。  
  
#### <a name="mandatory-configuration"></a>必須構成  
 管理パックを使用するには、次の手順を実行する必要があります。  
  
1.  エージェントをインストールし、証明書信頼を使用して信頼を構成します。 Windows Server Essentials では、ドメイン コント ローラーとして事前に構成およびその他のドメインまたはフォレストと信頼関係を持つことはできません、ため、System Center Operation Manager エージェントが Windows Server Essentials をインストールする必要がありの信頼の管理を構成サーバー証明書を使用します。  
  
2.  管理パックをダウンロードします。 を Operations Manager 2007 を使用して Windows Server Essentials を監視する必要があります最初にダウンロード、 [Windows Server オペレーティング システム管理パック](https://connect.microsoft.com/WindowsServer/Downloads/DownloadDetails.aspx?DownloadID=45010)管理パック カタログから。  
  
3.  管理パック ファイルをインポートします。 ローカライズ版の管理パックを使用している場合、メイン管理パック ファイルと言語パックの両方をインポートする必要があります。  
  
#### <a name="files-in-this-monitoring-pack"></a>この監視パック内のファイル  
 Monitoring Pack for Windows Server Essentials には、次のファイルが含まれます。  
  
-   Microsoft.Windows.Server.2012.Essentials.mp  
  
-   Microsoft.Windows.Server.2012.Essentials < ロケール\>.mp。  
  
### <a name="back-up-and-restore"></a>バックアップと復元  
 Windows Server Essentials サーバーとクライアントの両方をバックアップすることができます。  
  
#### <a name="back-up-the-server"></a>サーバーのバックアップ  
 Windows Server Essentials サーバーのバックアップの 2 つの方法をサポートしています。 オンプレミスのバックアップとオフプレミス バックアップします。  
  
 **オンプレミス バックアップ** では、別のディスクにブロックレベルの増分バックアップを定期的に実行できます。 ホストとして、Windows Server Essentials の VM に仮想ディスクを接続してサーバー バックアップをこの仮想ディスクを構成します。 仮想ディスクは、Windows Server Essentials の VM とは別の物理ディスクに配置する必要があります。  
  
-   オフにして、Windows Server Essentials からすべての関連ユーザー インターフェイスを削除する可能性があります、Windows Server Essentials の VM をバックアップする別のメカニズムがあり、ユーザーに、Windows Server Essentials のネイティブ サーバー バックアップ機能を表示したくない場合ダッシュ ボード。 詳細については、のサーバー バックアップのカスタマイズ」セクションを参照してください、 [ADK ドキュメント](https://go.microsoft.com/fwlink/p/?LinkID=249124)します。  
  
 **オフプレミス バックアップ** では、サーバー データをクラウド サービスに定期的にバックアップできます。 ダウンロードしてインストール、Microsoft Azure Backup 統合モジュールの Windows Server Essentials を Microsoft によって提供される Azure Backup を利用できます。  
  
 別のクラウド サービスを希望する場合、次を実行する必要があります。  
  
1.  既定の Azure Backup ではなく、希望のクラウド サービスへのリンクを提供するように、Windows Server Essentials ダッシュ ボードのユーザー インターフェイスを更新します。 詳細については、 [ADK ドキュメント](https://go.microsoft.com/fwlink/p/?LinkID=249124)の「イメージのカスタマイズ」セクションを参照してください。  
  
2.  (省略可能)Windows Server Essentials のダッシュ ボードを構成してクラウド バックアップ サービスを管理するので開発できます。  
  
#### <a name="back-up-the-client"></a>クライアントのバックアップ  
 Windows Server Essentials には、クライアント データのバックアップの 2 つの種類がサポートされています。 フル クライアント バックアップ、およびファイルの履歴。  
  
> [!NOTE]
>  クライアントのバックアップは、VPN 経由でデータをクライアントからサーバーに転送する必要があるため、パフォーマンスに影響する可能性があります。  
  
 **フル クライアント バックアップ**Windows Server Essentials ネットワークに接続されているすべてのクライアント デバイスで既定では。 フル クライアント (システムとデータ) の増分バックアップを実行し、データの重複除去をサポートします。 バックアップ データは、Windows Server Essentials を実行するサーバー上になります。 障害が発生したクライアントは、前のバックアップ ポイントまでのデータを取り戻すことができます。 でしたこの機能でオフにする、作成の手順の「Cfg.ini ファイルのセクション、 [ADK ドキュメント](https://technet.microsoft.com/library/jj200150)します。  
  
 次に、フル クライアント バックアップの注意事項を示します。  
  
-   パフォーマンス: 初期クライアント バックアップは、アップロードするデータ量が多いため、時間がかかる可能性があります。  
  
-   安定性: クライアント側のインターネット接続が安定しない場合があります。 クライアント バックアップは、再開できるように設計されています。既定のチェックポイントは 40 GB です (クライアント バックアップ データベースで、40 GB のデータがバックアップされるたびにチェックポイントが作成されます)。 インターネット接続の信頼性が低いことが予測される場合、この値を小さい値に変更できます。  
  
    -   チェックポイント ジョブを有効にするには、サーバーで、レジストリ キー HKLM\Software\Microsoft\Windows Server\Backup\GetCheckPointJobs を 1 に設定します。  
  
    -   チェックポイントしきい値を変更するには、クライアントで、HKLM\Software\Microsoft\Windows Server\Backup\CheckPointThreshold を既定値 (40 GB) から変更します。  
  
-   クライアント ベア メタル回復: Windows プレインストール環境では VPN 接続をサポートしないため、クライアント ベア メタル回復はサポートされません。  
  
 **ファイル履歴**がネットワーク共有へのプロファイル データ (ライブラリ、デスクトップ、連絡先、お気に入り) をバックアップするための Windows 8.1 の機能です。 Windows Server Essentials での Windows Server Essentials に参加しているすべての Windows 8.1 クライアントのファイル履歴設定を一元管理できます。 バックアップ データは、Windows Server Essentials を実行しているサーバーに保存されます。 オフにできますこの機能の作成手順の「Cfg.ini ファイルのセクション、 [ADK ドキュメント](https://technet.microsoft.com/library/jj200150)します。  
  
### <a name="storage-management"></a>記憶域の管理  
 [新しい記憶域機能](https://technet.microsoft.com/library/hh831739.aspx) により、異種ハード ドライブの物理記憶域容量の集計、ハード ドライブの動的な追加、復元レベルを指定したデータ ボリュームの作成が可能となりました。 記憶域を拡張する Windows Server Essentials に iSCSI ディスクを接続することもできます。  
  
## <a name="what-are-the-main-scenarios-i-should-test"></a>テストする必要があるメイン シナリオの詳細  
 ホストのパースペクティブから、次のシナリオをテストすることをお勧めします。  
  
 **サーバーの展開**  
  
-   ラボ環境で Windows Server Essentials サーバーをデプロイします。  
  
-   必要に応じて Windows Server Essentials イメージをカスタマイズします。  
  
-   無人セットアップ ファイルと cfg.ini と Windows Server Essentials の展開を自動化します。  
  
-   オンプレミス Windows SBS をホスト型 Windows Server Essentials に移行します。  
  
-   Windows Server Essentials から Windows Server 2012 にアップグレードします。  
  
 **サーバーの構成**  
  
-   Anywhere Access (VPN、リモート Web アクセス、DirectAccess) を構成します。  
  
-   記憶域とサーバー フォルダーを構成します。  
  
-   (適用できる場合) サーバー バックアップ、オンライン バックアップ、クライアント バックアップ、ファイル履歴を構成します。  
  
-   (適用できる場合) 記憶域を構成し、管理します。  
  
-   (適用できる場合) 電子メール ソリューション統合 (Office 365、ホスト型 Exchange など) を構成します。  
  
-   (適用できる場合) メディア サーバーを構成します。  
  
 **サーバーの管理**  
  
-   ユーザーを管理します。  
  
-   アラートの電子メール通知を構成し、受信します。  
  
-   エラー/警告の場合、BPA を実行します。  
  
-   System Center の監視パックを構成します。  
  
-   破損の場合、サーバー回復を構成します。  
  
 **クライアント エクスペリエンス**  
  
-   インターネット経由でのクライアントの展開 (パーソナル コンピューターまたは Mac OS)。  
  
-   クライアントのスタート パッドを使用して、共有フォルダーにアクセスします。  
  
-   リモート Web アクセス経由でさまざまなデバイス (パーソナル コンピューター、電話、タブレット) からサーバー資産にアクセスします。  
  
-   Windows Phone 用のマイ サーバー アプリ。  
  
-   (適用できる場合) ファイル履歴、クライアント バックアップ、復元 (BMR なし)、フォルダー リダイレクション。  
  
-   (適用できる場合) 電子メール統合エクスペリエンス。  
  
## <a name="where-can-i-get-more-support"></a>サポートの入手場所  
 下のリンクから SDK ドキュメントと ADK ドキュメントを入手できます。  
  
-   [SDK](https://go.microsoft.com/fwlink/p/?LinkID=248648)  
  
-   [ADK](https://go.microsoft.com/fwlink/p/?LinkID=249124)  
  
 [接続] を使って、バグを機能チームに報告できます。 ログを生成するには、サーバーと、サーバーに参加しているクライント上のフォルダーC:\ProgramData\Microsoft\Windows Server\Logs の ZIP ファイルを作成します。
