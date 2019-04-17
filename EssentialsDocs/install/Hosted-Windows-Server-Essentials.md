---
title: "ホスト型 Windows Server Essentials"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.openlocfilehash: 23e586c22ca14af7b02550e2fa1c9522e379170c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="hosted-windows-server-essentials"></a>ホスト型 Windows Server Essentials

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

このドキュメントには、ラボでの Windows Server Essentials を展開し、サービスとしての Windows Server Essentials を顧客に提供する予定があるホストに固有の情報が含まれます。  
  
## <a name="what-is-windows-server-essentials"></a>Windows Server Essentials とは何ですか。  
 Windows Server Essentials は、ほとんどの小規模企業に最適 server 環境を提供する最善の 64 ビット製品テクノロジが組み込まれて、クロスプレミスの小規模ビジネス ソリューションです。 Windows Server Essentials では、次のテクノロジが含まれています。  
  
 **サーバー オペレーティング システム:** Windows Server 2012 製品テクノロジは、Windows Server Essentials のコア部分を提供します。 詳細については、次を参照してください。、 [Windows Server 2012 の web サイト](https://www.microsoft.com/en-us/server-cloud/products/windows-server-2012-r2/default.aspx#fbid=ZH0GD_CRAWh)します。  
  
 **データ保護:** Windows Server Essentials が大幅に強化されたデータの保護機能を提供する Windows Server 2012 で使用できるいくつかの新しい機能を活用します。 [記憶域スペースの新機能](https://technet.microsoft.com/library/hh831739.aspx)動的にハード ドライブを追加および耐障害性のレベルを指定したデータ ボリュームを作成、異種ハード ドライブの物理的な記憶域容量の集計することができます。 Windows Server Essentials は、システムの完全バックアップを実行して、自体だけでなく、ネットワークに接続されているクライアント コンピューターに、サーバーのベア メタル復元ですか? 2 TB より大きいボリュームのサポートのようになりました。 Windows Server 2012 での新機能、 [Windows Azure Online Backup](https://technet.microsoft.com/library/hh831419.aspx)は Microsoft によって管理されるクラウド ベースの記憶域サービスのファイルとフォルダーを保護するために使用できます。 Windows Server Essentials も一元的に管理し、Windows 8.1 クライアントでは、ユーザーが管理者の支援を必要とせず、誤って削除または上書きされたファイルから回復するためのファイル履歴機能を構成します。  
  
 **Anywhere Access:**リモート Web アクセスは効率的でタッチ操作に適したブラウザー エクスペリエンスを提供いればとこからでもアプリケーションやデータにアクセスするがある、インターネットに接続し、ほぼすべてのデバイスを使用します。 Windows Server Essentials も、更新された Windows Phone アプリと新しいアプリ用 Windows 8.1 クライアント コンピューター、提供全体の検索に接続して、サーバーのファイルとフォルダーにアクセスできるように直感的にします。 ファイルも自動的にオフライン アクセスのキャッシュに保存し、サーバーへの接続が利用可能になったときに同期します。 Windows Server Essentials に数回クリックするだけの簡単でウィザードを使ったプロセスの仮想プライベート ネットワーク (VPN) を設定し、ユーザーに対する VPN アクセスの管理を合理化します。 クライアント コンピューターは、リモート オフィスに通う必要とせず、Windows SBS 環境に参加する VPN 接続を利用できます。  
  
 **ワークロードの柔軟性:** Windows Server Essentials を顧客にどのアプリケーションを選択できる柔軟性を許可するように設計されています、オンプレミスおよびクラウドで実行されるでサービスを実行します。 以前のバージョンの Windows Small Business Server Standard として含まれる Exchange Server がコンポーネント製品は、クラウド ベースのメッセージングおよびコラボレーション サービスを利用するお客様のコストと複雑さを追加します。 Windows Server Essentials では、お客様はご利用統合管理エクスペリエンスの同じ種類の Exchange サーバーの内部設置型のコピーを実行、ホスト型の Exchange サービスにサブスクライブまたは Microsoft Office 365 をサブスクライブすることも選択するかどうか。  
  
 **正常性の監視:**独自の正常性状態と、Windows 8.1、および実行する Windows 7、Mac OS X バージョン 10.5 以降のクライアント コンピューターの状態は Windows Server Essentials を監視します。 正常性状態の問題やコンピューターのバックアップ、サーバー記憶域、ディスク領域不足などに関連する問題を通知します。  
  
 **拡張機能:** Windows Server Essentials は、拡張性モデルの他のソフトウェア ベンダーがコア製品に機能と機能の追加は、新しい一連の web サービス Api が追加される Windows SBS 2011 Essentials 上に構築します。 既存の互換性も保持[ソフトウェア開発キット](https://msdn.microsoft.com/library/gg513958.aspx)(SDK) と[アドイン](https://pinpoint.microsoft.com/applications/search?fpt=300105&q=small+business+server+essentials)Windows SBS 2011 Essentials 用に作成します。  
  
## <a name="how-can-i-customize-an-image"></a>イメージをカスタマイズする方法は?  
 参照してください、 [Windows Server Essentials](https://go.microsoft.com/fwlink/p/?LinkID=249124)、Windows Server Essentials のカスタマイズ手順が追加された、標準の Windows Server sysprep プロセスです。 完了するには、カスタマイズ設定の指示に従って、[単純なカスタマイズ イメージの作成](https://technet.microsoft.com/en-us/library/jj200117)と[、イメージのカスタマイズ](https://technet.microsoft.com/en-us/library/jj200161)、指示に従って、[イメージの展開の準備](https://technet.microsoft.com/en-us/library/jj200142)、最終イメージをキャプチャします。  
  
 次の点に注意を払う必要があります。  
  
1.  任意のドライブのルートに SkipIC.txt ファイルを追加することで、初期構成 (IC) を省略してください。 、IC の前に、サーバーのインストール後 shift キーを押しながら f10 キーを押してコマンド プロンプト ウィンドウを起動し、c: 下に SkipIC.txt ファイルを作成/ドライブします。 カスタマイズ後 SkipIC.txt ファイルを削除するを忘れないでください。  
  
2.  を 90 GB より小さいディスク上の Windows Server Essentials を展開する必要がある場合は、sysprep の前にレジストリ キーを追加する必要があります。  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v HWRequirementChecks /t REG_DWORD /d 0 /f  
    ```  
  
 Sysprep 後 sysprep 済みのディスク イメージ、または再シールを Install.wim に新しい展開を使用できます。  
  
 Virtual Machine Manager を使用している場合は、実行中のインスタンスを使用してテンプレートを作成できます。 テンプレートを作成し、インスタンスが sysprep され、サーバーをシャット ダウンします。 ライブラリに格納した後で個別のインスタンスをせることができます。  
  
##  <a name="BKMK_automatedeployment"></a>デプロイメントを自動化する方法は?  
 カスタマイズされたイメージを取得した後は、独自のイメージの展開を行うことができます。 半無人インストールを行うために、WinPE セットアップ用の unattend.xml を提供/展開する必要があります。 完全無人インストールには、Windows Server Essentials の初期構成用の cfg.ini ファイルを提供する必要があります。  
  
1.  無人 WinPE セットアップのみを実行します。 これにより、WinPE セットアップのみを自動化され、インストールがエンド ・ ユーザー情報を提供できる Corp、ドメイン、および管理者自分で RDP 後にサーバーのセッションにできるように、初期構成前に停止されます。 これを行うには。  
  
    1.  Windows unattend.xml ファイルを指定します。 に従って、 [Windows 8.1 ADK](https://go.microsoft.com/fwlink/?LinkId=248694) 、ファイルを生成し、サーバー名、プロダクト キー、および管理者のパスワードを含むすべての必要な情報を提供します。 Unattend.xml ファイルの [Microsoft Windows のセットアップ」セクションでは、次に示す情報を提供します。  
  
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
  
    2.  お客様は初期構成を完了管理者と、サーバーには、RDP に unattend.xml ファイルで指定したパスワードを使用できるように、パブリック ip アドレスで RDP ポート 3389 を開く必要があります。  
  
    > [!NOTE]
    >  既定のパスワードを変更しない場合、サーバーのインストールはパスワードの入力を求める画面で停止します。**注**エンドユーザーは、既定の管理者アカウントを使用して、サーバーにログオンし、初期構成を実行する必要があります。  
  
 Virtual Machine Manager を使用している場合は、テンプレートから新しいインスタンスを作成する場合、コンソールで、管理者のパスワードを指定できます。  
  
1.  無人初期構成を含む、完全無人セットアップを実行します。 これを行うには。  
  
    1.  WinPE セットアップから、展開が起動した場合は、上記と同様の unattend.xml ファイルを提供します。  
  
    2.  Windows Server Essentials ADK セクションを参照してください[Cfg.ini ファイルの作成](https://technet.microsoft.com/en-us/library/jj200150)、cfg.ini を生成します。  
  
    3.  [InitialConfiguration] に情報を提供します。  
  
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
  
    4.  [PostOSInstall] に情報を提供します。  
  
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
  
    6.  上の WebDomainName 情報を指定しなかった場合は、顧客が RDP を使用して、サーバーに接続し、VPN 構成を完了できるように、ポート 3389 を開くを確認します。  
  
> [!NOTE]
>  VM ホスト サーバーと Windows Server Essentials VM のタイム ゾーン設定が同じであることを確認します。 それ以外の場合、いくつかの異なるエラーが発生する可能性があります (初期構成が失敗するデバイス情報が正しく更新されないなどの証明書関連タスク; 証明書がインストールした後、数時間機能しない可能性があります)。  
  
 展開後に、初期構成が成功したかどうかことを確認する hklm \software\microsoft\windows \setup で次のレジストリ キーを確認します。 場合ことを示します = ICDone & & ICStatus = 1、初期構成が正常に完了したことを意味します。  
  
## <a name="what-is-the-supported-network-topology"></a>サポートされているネットワーク トポロジとは何ですか。  
 ローミング クライアントから Windows Server Essentials を使用するには、VPN を有効にする必要があります。 VPN SSTP 接続用にポート 443 を有効にすることをお勧めします。 リモート Web アクセスまたは Web サービスのアプリのメディア サーバー機能が必要なポート 80 が有効にもする必要があります。  
  
 Windows PowerShell スクリプトを介して無人デプロイメント中に VPN の有効化を行うか、初期構成後にウィザードを使って構成できます。  
  

-   無人デプロイメント中に VPN を有効にするのを参照してください[デプロイメントを自動化する方法ですか?。](Hosted-Windows-Server-Essentials.md#BKMK_automatedeployment)このドキュメントで。  

-   無人デプロイメント中に VPN を有効にするのを参照してください[デプロイメントを自動化する方法ですか?。](../install/Hosted-Windows-Server-Essentials.md#BKMK_automatedeployment)このドキュメントで。  

  
-   Windows PowerShell を使用して VPN を有効に管理者権限で次のコマンドレットを実行し、すべての必要な情報を提供します。  
  
    ```  
    ##  
    ## To configure external domain and SSL certificate (if not yet done in unattended Initial Configuration).  
    ##  
  
    $myExternalDomainName = 'remote.contoso.com';   ## corresponds to A or AAAA DNS record(s) that can be resolved on Internet and routed to the server  
    $mySslCertificateFile = 'C:\ssl.pfx';   ## full path to SSL certificate file  
    $mySslCertificatePassword = ConvertTo-SecureString '******';   ## password for private key of the SSL certificate  
    $skipCertificateVerification = $true;   ## whether or not, skip verification for the SSL certificate  
  
    Add-Type -AssemblyName 'Wssg.Web.DomainManagerObjectModel';  
    [Microsoft.WindowsServerSolutions.RemoteAccess.Domains.DomainConfigurationHelper]::SetDomainNameAndCertificate($myExternalDomainName,$mySslCertificateFile,$mySslCertificatePassword,$skipCertificateVerification);  
    ##  
    ## To install VPN with static IPv4 pool (and allow all existing users to establish VPN).  
    ##  
  
    Install-WssVpnServer -IPv4AddressRange ('192.168.0.160','192.168.0.240') -ApplyToExistingUsers;  
    ```  
  
 場合は、サーバーを顧客に提供する前に、VPN 接続を提供できない場合は、エンドユーザーが RDP を使用して、サーバーに接続し、自分で構成を行うようにサーバー ポート 3389 がインターネット上で到達可能であることを確認します。  
  
 次に、次の 2 つ一般的なサーバー側のネットワーク トポロジと VPN/リモート Web アクセス (RWA) を構成する方法を示します。  
  
-   トポロジ 1 (推奨)  
  
    -   NAT デバイスの下にある別の仮想ネットワーク内のサーバー。  
  
    -   仮想ネットワークで DHCP サービスが有効になっているか、静的 IP アドレスを持つサーバーが割り当てられています。  
  
    -   サーバー ポート 443 は、パブリック IP ポート 443 から到達可能です。  
  
    -   VPN パススルーが、ポート 443 に対して許可されます。  
  
    -   VPN IPv4 アドレス プールは、サーバーのアドレスの同じサブネット内遠隔必要があります。  
  
    -   2 番目のサーバーには、同じサブネット内では、VPN アドレス プールから静的 IP を割り当てる必要があります。  
  
-   トポロジ 2:  
  
    -   サーバーは、プライベート IP アドレスを持ちます。  
  
    -   サーバー上のポート 443 は、パブリック IP アドレスのポート 443 から到達可能です。  
  
    -   VPN パススルーが、ポート 443 に対して許可されます。  
  
    -   VPN IPv4 アドレス プールは、別のサーバーのアドレスの範囲でです。  
  
 トポロジ 2 では、2 つ目のサーバーのシナリオはサポートされていません。  
  
## <a name="how-do-i-perform-common-tasks-via-windows-powershell"></a>Windows PowerShell を使用して一般的なタスクの実行方法  
 **リモート Web アクセスを有効にします。**  
  
```  
Enable-WssRemoteWebAccess [-SkipRouter] [-DenyAccessByDefault] [-ApplyToExistingUsers]  
```  
  
 例:  
  
```  
$Enable-WssRemoteWebAccess  œDenyAccessByDefault  œApplyToExistingUsers  
```  
  
 このコマンドは、自動的に構成されているルーターにリモート Web アクセスを有効にし、既存のすべてのユーザーの既定のアクセス許可を変更します。  
  
 **ユーザーを追加します。**  
  
```  
Add-WssUser [-Name] <string> [-Password] <securestring> [-AccessLevel <string> {User | Administrator}] [-FirstName <string>] [-LastName <string>] [-AllowRemoteAccess] [-AllowVpnAccess]   [<CommonParameters>]  
```  
  
 例:  
  
```  
$password = ConvertTo-SecureString "Passw0rd!" -asplaintext  œforce  
$Add-WssUser -Name User2Test -Password $password -Accesslevel Administrator -FirstName User2 -LastName Test  
```  
  
 このコマンドは、管理者パスワード Passw0rd User2Test という名前を追加しました。  
  
 **ユーザーの有効化/無効化**  
  
 例:  
  
```  
$CurrentUser = get-wssuser  œname user2test  
$CurrentUser.UserStatus = 0  
$CurrentUser.Commit()  
```  
  
 このコマンドは、user2test という名前のユーザーを無効になります。 UserStatus を 1 に設定すると、ユーザーが有効になります。  
  
 **サーバー フォルダーを追加します。**  
  
```  
Add-WssFolder [-Name] <string> [-Path] <string> [[-Description] <string>] [-KeepPermissions] [<CommonParameters>]  
```  
  
 例:  
  
```  
$Add-WssFolder -Name "MyTestFolder" -Path "C:\ServerFolders\MyTestFolder"  
```  
  
 このコマンドでは、指定された場所に MyTestFolder をという名前のサーバー フォルダーを追加します。  
  
## <a name="how-do-i-add-a-second-server-to-the-windows-server-essentials-domain"></a>Windows Server Essentials ドメインに 2 番目のサーバーを追加する方法  
 Windows Server Essentials は、ドメイン コント ローラーであるために、2 番目のサーバーを標準的なやり方でドメインに参加できます。  
  
## <a name="which-email-solutions-can-be-integrated"></a>どの電子メール ソリューションを統合することができますか。  
 Windows Server Essentials は、ボックスから次の 2 つの電子メール ソリューションとの統合をサポートしています: Office 365 と社内 Exchange します。 ホスト型電子メール ソリューションを実行している場合は、ホスト型電子メール ソリューションと Windows Server Essentials を統合するアドインを開発する必要があります。  
  
## <a name="how-do-i-migrate-on-premises-windows-sbs-201120082003-to-the-hosted-windows-server-essentials"></a>ホスト型 Windows Server Essentials にオンプレミス Windows SBS (2011/2008/2003) を移行する方法  
 移行ガイドでは、内部設置型 Windows Small Business Server (Windows SBS) Windows Server Essentials の移行に利用できます。 ホスト型環境に適用手順の一部とまったく同じされません可能性があります。 ただし、一般的なタスクおよび移行するワークロードは同じになります。 参照することをお勧め、[移行ガイド](https://go.microsoft.com/fwlink/p/?LinkID=254292)し、ホスティング環境に基づいて必要なカスタマイズを行います。  
  
 同じサブネット内の移行元サーバーと移行先サーバーを配置することをお勧めします。 これが可能でない場合することを確認します。  
  
-   移行元サーバーと移行先サーバーの内部 DNS 名は、互いに到達できます。  
  
-   すべての必要なポートが開いています。  
  
## <a name="how-can-i-upgrade-windows-server-essentials-to-windows-server-standard"></a>Windows Server Essentials を Windows Server Standard にアップグレードする方法ですか。  
 Windows Server Essentials は、Windows Server Standard にアップグレードできます。 ロックと制限を削除し、Windows Server Standard に不足しているパッケージを追加します。 詳細については、[ドキュメントをダウンロード](https://go.microsoft.com/fwlink/p/?LinkID=253181)します。  
  
## <a name="what-are-the-native-tools-for-monitoring-and-management"></a>監視と管理のためのネイティブ ツールとは何ですか。  
  
### <a name="group-policy-management"></a>グループ ポリシーの管理  
 Windows Server Essentials では、Windows Server 2012 でのネイティブ グループ ポリシー サポートを利用し、フォルダー リダイレクトおよびセキュリティの設定を構成するためのユーザー インターフェイスを提供します。  
  
> [!NOTE]
>  環境では、ホスト型のユーザー プロファイル フォルダーのリダイレクションが有効になっている場合をエンドユーザーが、データのサイズが大きいときにログオンできる時間が高くなります。  
  
### <a name="management-pack"></a>管理パック  
 Windows Server Essentials の管理パックは、ホストが多数の Windows Server Essentials サーバーにそれぞれの小規模企業専用の管理のために Windows Server Essentials での正常性アラート システム経由での監視機能を提供します。 このバージョンでの監視には、システムに重大なアラートのみが含まれています。  
  
#### <a name="management-pack-scope"></a>管理パックの範囲  
 この管理パックでは、Windows Server Essentials に固有の機能を監視するのに役立ちます。 Windows Server 2012 Standard オペレーティング システムの一般的な機能は監視しません。 Windows Server Essentials を監視するために、Windows Server Essentials の管理パックと、管理パックの Windows Server 2012 Standard の両方を使用する必要があります。  
  
#### <a name="mandatory-configuration"></a>必須の構成  
 次の手順では、管理パックを使用する前に実行する必要があります。  
  
1.  エージェントをインストールし、証明書の信頼を使用して信頼を構成します。 Windows Server Essentials はドメイン コント ローラーとして事前に構成されておよびその他のドメインまたはフォレストと信頼関係を持つことはできません、ため、System Center Operation Manager Agent は Windows Server Essentials にインストールする必要があり、証明書を使用して管理サーバーとの信頼を構成します。  
  
2.  管理パックをダウンロードします。 Operations Manager 2007 を使用して Windows Server Essentials を監視する必要がありますまずをダウンロードする、 [Windows Server オペレーティング システム管理パック](https://connect.microsoft.com/WindowsServer/Downloads/DownloadDetails.aspx?DownloadID=45010)管理パック カタログから。  
  
3.  管理パック ファイルをインポートします。 管理パックのローカライズされたバージョンを使用している場合は、メイン管理パック ファイルと言語パックの両方をインポートする必要があります。  
  
#### <a name="files-in-this-monitoring-pack"></a>この監視パック内のファイル  
 監視パック for Windows Server Essentials には、次のファイルが含まれています。  
  
-   Microsoft.Windows.Server.2012.Essentials.mp  
  
-   .Mp Microsoft.Windows.Server.2012.Essentials。 < locale\ >  
  
### <a name="back-up-and-restore"></a>バックアップおよび復元します。  
 Windows Server Essentials では、サーバーとクライアントの両方をバックアップすることができます。  
  
#### <a name="back-up-the-server"></a>サーバーをバックアップします。  
 Windows Server Essentials サーバーのバックアップの 2 つの方法をサポートしています。 オンプレミス バックアップとオフプレミス バックアップします。  
  
 **オンプレミス バックアップ**個別のディスクに定期的にブロック レベルの増分バックアップを実行することができます。 ホストとしてには、Windows Server Essentials VM に仮想ディスクを接続して、この仮想ディスクへのサーバー バックアップを構成する可能性があります。 仮想ディスクは、Windows Server Essentials VM とは異なる物理ディスクに存在する必要があります。  
  
-   Windows Server Essentials VM をバックアップする別のメカニズムがあり、Windows Server Essentials のネイティブ サーバー バックアップ機能を表示できるようにしてたくない場合をオフにすることと、Windows Server Essentials ダッシュ ボードからすべての関連ユーザー インターフェイスを削除する可能性があります。 詳細については、のサーバー バックアップのカスタマイズ」セクションを参照してください、 [ADK ドキュメント](https://go.microsoft.com/fwlink/p/?LinkID=249124)します。  
  
 **オフプレミス バックアップ**クラウド サービスに、サーバー データを定期的にバックアップすることができます。 ダウンロードして、Microsoft Azure Backup 統合モジュールの Windows Server Essentials を Microsoft によって提供される Azure Backup を利用してをインストールすることができます。  
  
 場合や、ユーザーは、別のクラウド サービスを必要に応じて、次の操作を行う必要があります。  
  
1.  Azure Backup の既定ではなく、希望のクラウド サービスへのリンクを提供するように、Windows Server Essentials ダッシュ ボードのユーザー インターフェイスを更新します。 詳細については、」を参照して、ユーザー設定の [イメージ] セクションで、 [ADK ドキュメント](https://go.microsoft.com/fwlink/p/?LinkID=249124)します。  
  
2.  (省略可能)構成およびクラウド バックアップ サービスを管理する Windows Server Essentials ダッシュ ボードのアドインを開発します。  
  
#### <a name="back-up-the-client"></a>クライアントをバックアップします。  
 Windows Server Essentials には、クライアント データのバックアップの 2 つの種類がサポートされています: フル クライアント バックアップ、およびファイル履歴。  
  
> [!NOTE]
>  クライアントのバックアップ データは、VPN 経由でクライアントからサーバーに転送する必要があるためパフォーマンスに影響があります。  
  
 **フル クライアント バックアップ**に既定では、Windows Server Essentials ネットワークに接続されているすべてのクライアント デバイスに対してします。 段階的に (システムおよびデータ) は、フル クライアント バックアップし、データ重複除去をサポートします。 バックアップ データは、Windows Server Essentials を実行しているサーバーになります。 失敗したクライアントは、以前のバックアップ ポイントに戻るには、そのデータを取得できます。 可能性がありますこの機能をオフにする、次の作成手順の「Cfg.ini ファイル、 [ADK ドキュメント](https://technet.microsoft.com/en-us/library/jj200150)します。  
  
 フル クライアント バックアップの注意事項を示します。  
  
-   パフォーマンス: 初期クライアント バックアップがあります時間がかかるアップロードされるデータ量が多いためです。  
  
-   安定性: もインターネット接続が安定しないクライアント側でします。 クライアントのバックアップが、再開できるように設計し、既定のチェックポイントは 40 GB まで (クライアント バックアップ データベースで、チェックポイントが作成されます 40 GB のデータのバックアップが完了するたびに) します。 信頼性が低いへのインターネット接続が予測される場合、小さい値にこの値を変更する可能性があります。  
  
    -   サーバーでのチェックポイント ジョブを有効にするには、レジストリ キー hklm \software\microsoft\windows server \backup\getcheckpointjobs を 1 に設定します。  
  
    -   クライアントでは、チェックポイントしきい値を変更するには、その既定値 (40 GB) から hklm \software\microsoft\windows server \backup\checkpointthreshold を変更します。  
  
-   クライアント ベア メタル回復: Windows プレインストール環境が VPN 接続をサポートしていないためクライアント ベア メタル回復はサポートされません。  
  
 **ファイル履歴**プロファイル データ (ライブラリ、デスクトップ、連絡先、お気に入り) をバックアップするための Windows 8.1 機能は、ネットワーク共有します。 Windows Server Essentials では、Windows Server Essentials に参加しているすべての Windows 8.1 クライアントのファイル履歴設定の集中管理できるようにします。 バックアップ データは、Windows Server Essentials を実行しているサーバーに格納されます。 オフにできますこの機能の作成手順に従っての「Cfg.ini ファイル、 [ADK ドキュメント](https://technet.microsoft.com/en-us/library/jj200150)します。  
  
### <a name="storage-management"></a>記憶域の管理  
 [記憶域スペースの新機能](https://technet.microsoft.com/library/hh831739.aspx)動的にハード ドライブを追加および耐障害性のレベルを指定したデータ ボリュームを作成、異種ハード ドライブの物理的な記憶域容量の集計することができます。 記憶域を拡張する Windows Server Essentials に iSCSI ディスクをアタッチすることもできます。  
  
## <a name="what-are-the-main-scenarios-i-should-test"></a>主なシナリオをテストする必要がありますとは何ですか。  
 ホストのパースペクティブから、次のシナリオをテストすることをお勧めします。  
  
 **サーバーの展開**  
  
-   ラボ環境で Windows Server Essentials サーバーを展開します。  
  
-   必要に応じて、Windows Server Essentials イメージをカスタマイズします。  
  
-   Windows Server Essentials デプロイメントを unattended ファイルと cfg.ini を自動化します。  
  
-   オンプレミス Windows SBS をホスト型 Windows Server Essentials に移行します。  
  
-   Windows Server Essentials から Windows Server 2012 にアップグレードします。  
  
 **サーバーの構成**  
  
-   どこからでもアクセス (VPN、リモート Web アクセス、DirectAccess) を構成します。  
  
-   記憶域とサーバー フォルダーを構成します。  
  
-   (該当する場合)サーバー バックアップ、オンライン バックアップ、クライアント バックアップ、ファイル履歴を構成します。  
  
-   (該当する場合)構成し、記憶域スペースを管理します。  
  
-   (該当する場合)電子メール ソリューション統合 (Office 365、ホスト型の Exchange、およびなど) を構成します。  
  
-   (該当する場合)メディア サーバーを構成します。  
  
 **サーバーの管理**  
  
-   ユーザーを管理します。  
  
-   構成し、アラートの電子メール通知を受信します。  
  
-   エラー/警告が発生した場合は、BPA を実行します。  
  
-   System Center 監視パックを構成します。  
  
-   破損が発生した場合、サーバーの回復を構成します。  
  
 **クライアント エクスペリエンス**  
  
-   クライアントの展開 (パーソナル コンピューターまたは Mac OS) インターネットを経由します。  
  
-   クライアントのスタート パッドを使用して、共有フォルダーにアクセスします。  
  
-   リモート Web アクセス経由でさまざまなデバイス (パーソナル コンピューター、電話、タブレット) からのサーバーの資産がアクセスします。  
  
-   Windows Phone 用の my Server アプリを導入するとします。  
  
-   (該当する場合)ファイル履歴、クライアント バックアップと復元 (BMR なし)、フォルダー リダイレクトします。  
  
-   (該当する場合)電子メール統合エクスペリエンス。  
  
## <a name="where-can-i-get-more-support"></a>多くのサポートはどこで入手できますか。  
 以下のリンクから SDK と ADK のドキュメントを取得できます。  
  
-   [SDK](https://go.microsoft.com/fwlink/p/?LinkID=248648)  
  
-   [ADK](https://go.microsoft.com/fwlink/p/?LinkID=249124)  
  
 接続] を使って機能チームにバグを報告することができます。 ログを生成する、サーバーとサーバーに参加して、クライアントの両方でフォルダーを zip: C:\ProgramData\Microsoft\Windows server \logs です。
