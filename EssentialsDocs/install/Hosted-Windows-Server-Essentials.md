---
title: ホスト型 Windows Server Essentials
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.topic: article
ms.assetid: fda5628c-ad23-49de-8d94-430a4f253802
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 55d4059361189a0117bfd197c030fb860a1b10bd
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181228"
---
# <a name="hosted-windows-server-essentials"></a>ホスト型 Windows Server Essentials

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

このドキュメントには、Windows Server Essentials をラボに展開し、Windows Server Essentials をサービスとして顧客に提供するホストに固有の情報が含まれています。

## <a name="what-is-windows-server-essentials"></a>Windows Server Essentials とは
 Windows Server Essentials はクロスプレミスの小規模ビジネスソリューションです。このソリューションには、小規模企業の大部分に適したサーバー環境を提供するための、最高レベルの64ビット製品テクノロジが組み込まれています。 Windows Server Essentials には、次のテクノロジが含まれています。

 **サーバーのオペレーティングシステム:** Windows Server 2012 製品テクノロジは、Windows Server Essentials の中核を提供します。 詳しくは、 [Windows Server 2012 の Web サイト](https://www.microsoft.com/server-cloud/products/windows-server-2012-r2/default.aspx#fbid=ZH0GD_CRAWh)をご覧ください。

 **データ保護:** Windows Server Essentials では、Windows Server 2012 で利用できるいくつかの新機能を活用して、データ保護機能を大幅に向上させています。 [新しい記憶域機能](https://technet.microsoft.com/library/hh831739.aspx) により、異種ハード ドライブの物理記憶域容量の集計、ハード ドライブの動的な追加、復元レベルを指定したデータ ボリュームの作成が可能となりました。 Windows Server Essentials は、サーバー自体と、ネットワークに接続されているクライアントコンピューターの完全なシステムバックアップとベアメタル復元を実行できます。また、2 TB を超えるボリュームがサポートされるようになりました。 Windows Server 2012 の新機能として、 [Windows Azure Online Backup](https://technet.microsoft.com/library/hh831419.aspx) を使用して、Microsoft が管理しているクラウドベースの記憶域サービス内のファイルとフォルダーを保護できます。 また、Windows Server Essentials では、Windows 8.1 クライアントのファイル履歴機能も一元的に管理および構成されるため、ユーザーは管理者の支援を必要とせずに、誤って削除または上書きされたファイルから回復できます。

 **Anywhere Access:** リモート Web アクセスにより、簡単なタッチ操作に適したブラウザーを使用し、インターネット接続を介して事実上どこからでもアプリケーションやデータにアクセスし、任意のデバイスを使用することができます。 また、Windows Server Essentials は、更新された Windows Phone アプリと Windows 8.1 クライアントコンピューター用の新しいアプリも提供します。これにより、ユーザーは直感的に接続して、サーバー上のファイルやフォルダーにアクセスして、検索することができます。 また、オフライン アクセスの場合、ファイルが自動的にキャッシュされ、サーバーへの接続が可能になったときに同期されます。 Windows Server Essentials を使用すると、仮想プライベートネットワーク (VPN) のセットアップが、わずか数回のクリックでウィザードを使用して簡単に実行できるようになり、ユーザーに対する VPN アクセスの管理が容易になります。 クライアント コンピューターは、VPN 接続を利用して Windows SBS 環境にリモートで参加できるため、オフィスに通う必要がなくなります。

 **ワークロードの柔軟性:** Windows Server Essentials は、オンプレミスで実行され、クラウドで実行されるアプリケーションとサービスを柔軟に選択できるように設計されています。 前のバージョンでは、Windows Small Business Server Standard に Exchange Server がコンポーネント製品として含まれており、クラウドベースのメッセージングおよびコラボレーション サービスを利用する顧客にとって、コスト高と複雑化の要因となっていました。 Windows Server Essentials では、オンプレミスの Exchange Server のコピーを実行するか、ホスト型 Exchange サービスをサブスクライブするか、Microsoft Office 365 にサブスクライブするかにかかわらず、お客様は同じ種類の統合管理エクスペリエンスを利用できます。

 **正常性の監視:** Windows Server Essentials は、独自の正常性状態と、Windows 8.1、Windows 7、Mac OS X バージョン10.5 以降を実行しているクライアントコンピューターの状態を監視します。 正常性状態では、コンピューターのバックアップ、サーバー記憶域、ディスク領域不足などに関連する案件または問題が通知されます。

 **拡張性:** Windows Server Essentials は、Windows SBS 2011 Essentials の拡張モデルに基づいて構築されています。これにより、他のソフトウェアベンダーがコア製品に機能を追加できるようになり、web サービス Api の新しいセットが追加されます。 既存の [ソフトウェア開発キット](https://msdn.microsoft.com/library/gg513958.aspx) (SDK) や Windows SBS 2011 Essentials 用に作成された [アドイン](https://pinpoint.microsoft.com/applications/search?fpt=300105&q=small+business+server+essentials) との互換性も保持されます。

## <a name="how-can-i-customize-an-image"></a>イメージをカスタマイズする方法
 「Windows server [essentials](https://go.microsoft.com/fwlink/p/?LinkID=249124)」を参照してください。これは、Windows server essentials のカスタマイズ手順が追加された標準の windows server sysprep プロセスです。 カスタマイズを完了するには、「 [単純なカスタマイズ イメージの作成](https://technet.microsoft.com/library/jj200117) 」と「 [イメージのカスタマイズ](https://technet.microsoft.com/library/jj200161)」の手順に従った後、「 [イメージの展開の準備](https://technet.microsoft.com/library/jj200142) 」の手順に従って、最終イメージをキャプチャします。

 次の点に注意を払う必要があります。

1. SkipIC.txt ファイルを任意のドライブのルートに追加することにより、初期構成 (IC) をスキップする必要があります。 サーバーをインストールした後、IC の前に、Shift キーを押しながら F10 を押してコマンド プロンプト ウィンドウを起動し、C:/ ドライブの下に SkipIC.txt ファイルを作成します。 カスタマイズ後、この SkipIC.txt ファイルを必ず削除する必要があります。

2. Windows Server Essentials を 90 GB よりも小さいディスクに展開する必要がある場合は、sysprep の前にレジストリキーを追加する必要があります。

   ```
   %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v HWRequirementChecks /t REG_DWORD /d 0 /f
   ```

   sysprep 後、sysprep 済みのディスク イメージを使用するか、または新しいデプロイメント用に Install.wim に再シールできます。

   Virtual Machine Manager を使用している場合、実行中のインスタンスを使用してテンプレートを作成できます。 テンプレートを作成すると、インスタンスが sysprep され、サーバーがシャットダウンします。 ライブラリに格納した後、インスタンスをケースバイケースで起動できます。

##  <a name="how-do-i-automate-the-deployment"></a><a name="BKMK_automatedeployment"></a>デプロイを自動化操作方法には
 カスタマイズしたイメージを取得したら、独自のイメージを使ってデプロイメントを実行できます。 半無人インストールを実行するには、WinPE セットアップ用の unattend.xml を提供/展開する必要があります。 完全無人インストールを実行するには、Windows Server Essentials 初期構成の cfg.ini ファイルも指定する必要があります。

1. 無人 WinPE セットアップのみを実行します。 これにより、WinPE セットアップのみが自動化されます。初期構成前にインストールを停止し、エンド ユーザーが RDP 後に自分で会社、ドメイン、管理者情報をサーバー セッションに提供できるようにします。 これを行うには、次の手順を実行します。

   1.  Windows unattend.xml ファイルを提供します。 [WINDOWS 8.1 ADK](https://go.microsoft.com/fwlink/?LinkId=248694)に従ってファイルを生成し、サーバー名、プロダクトキー、管理者パスワードなど、すべての必要な情報を指定します。 unattend.xml ファイルの「Microsoft-Windows-Setup」セクションで、次のように情報を入力します。

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

   2.  RDP ポート3389をパブリック IP で開いて、顧客が unattend.xml ファイルで指定された管理者とパスワードを使用してサーバーに RDP 接続し、初期構成を完了できるようにする必要があります。

   > [!NOTE]
   >  既定のパスワードを変更しない場合、サーバー インストールはパスワードの入力を求める画面で停止します。**注** エンド ユーザーは、既定の管理者アカウントを使用してサーバーにログオンし、初期構成を実行する必要があります。

   Virtual Machine Manager を使用している場合、テンプレートから新しいインストールを作成したときに、コンソールで管理者パスワードを指定できます。

2. 無人初期構成を含む、完全無人セットアップを実行します。 これを行うには、次の手順を実行します。

   1.  デプロイメントを WinPE セットアップから開始した場合、上で実行した方法で unattend.xml ファイルを指定します。

   2.  cfg.ini を生成するには、Windows Server Essentials ADK のセクション「 [Cfg.ini ファイルを作成](https://technet.microsoft.com/library/jj200150)する」を参照してください。

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

   5.  WebDomainName パラメーターを指定する場合は、サーバーのパブリック IP を指すように DNS レコードも更新されていることを確認します。

   6.  上の WebDomainName 情報を指定しなかった場合、ポート 3389 を開いて、顧客が RDP を使用してサーバーに接続し、VPN 構成を終了できるようにします。

> [!NOTE]
>  VM ホストサーバーと Windows Server Essentials VM のタイムゾーン設定が同じであることを確認してください。 同じでないと、さまざまなエラーが発生する可能性があります (証明書関連タスクで初期構成が失敗する、証明書がインストール後に数時間機能しない、デバイス情報が正しく更新されない、など)。

 デプロイメント後、HKLM\software\microsoft\windows server\setup で次のレジストリ キーをチェックし、初期構成が成功したかどうかを確認します。 SetupStage == ICDone && ICStatus == 1 の場合、初期構成が正常に完了したことを示します。

## <a name="what-is-the-supported-network-topology"></a>サポートされているネットワーク トポロジについて
 ローミングクライアントから Windows Server Essentials を使用するには、VPN を有効にする必要があります。 VPN SSTP 接続の場合、ポート 443 を有効にすることをお勧めします。 リモート Web アクセスまたは Web Service アプリにメディア サーバー機能が必要な場合、ポート 80 も有効にする必要があります。

 VPN の有効化は、Windows PowerShell スクリプトを介して無人デプロイメント中に実行できます。または、初期構成後にウィザードを使って構成できます。


- 無人デプロイメント中に VPN を有効にするには、このドキュメントの「 [How do I automate the deployment?](Hosted-Windows-Server-Essentials.md#BKMK_automatedeployment) 」を参照してください。

- 無人デプロイメント中に VPN を有効にするには、このドキュメントの「 [How do I automate the deployment?](../install/Hosted-Windows-Server-Essentials.md#BKMK_automatedeployment) 」を参照してください。


- Windows PowerShell 経由で VPN を有効にするには、管理者権限で次のコマンドレットを実行し、必要なすべての情報を指定します。

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

  サーバーを顧客に渡す前に VPN 接続を提供できない場合、サーバー ポート 3389 がインターネットに到達可能であることを確認し、エンド ユーザーが RDP を使用してサーバーに接続し、自分たちで構成を実行できるようにします。

  ここでは、2 つの代表的なサーバー側のネットワーク トポロジと、VPN/リモート Web アクセス (RWA) の構成のしかたを示します。

- トポロジ 1 (推奨)

  -   サーバーは、別の仮想ネットワークの NAT デバイスの下に存在します。

  -   DHCP サービスが仮想ネットワークで有効になっているか、サーバーが静的 IP アドレスを使って割り当てられています。

  -   サーバー ポート 443 に、パブリック IP ポート 443 から到達可能です。

  -   VPN パススルーが、ポート 443 に対して許可されています。

  -   VPN IPv4 アドレス プールの範囲は、サーバー アドレスの同じサブネット内である必要があります。

  -   2 番目のサーバーには、同じサブネット内の、VPN アドレス プールの外にある静的 IP アドレスを割り当てる必要があります。

- トポロジ 2:

  -   サーバーは、プライベート IP アドレスを所有しています。

  -   サーバー上のポート443は、パブリック IP アドレス s ポート443から到達可能です。

  -   VPN パススルーが、ポート 443 に対して許可されています。

  -   VPN IPv4 アドレス プールは、異なる範囲のサーバー アドレスに存在します。

  トポロジ 2 を使用する場合、2 番目のサーバーというシナリオはサポートされません。

## <a name="how-do-i-perform-common-tasks-via-windows-powershell"></a>Windows PowerShell を経由して共通のタスクを実行する方法
 **リモート Web アクセスを有効にする**

```
Enable-WssRemoteWebAccess [-SkipRouter] [-DenyAccessByDefault] [-ApplyToExistingUsers]
```

 例:

```
$Enable-WssRemoteWebAccess  œDenyAccessByDefault  œApplyToExistingUsers
```

 このコマンドは、ルーターを自動的に構成する設定でリモート Web アクセスを有効にし、すべての既存ユーザーの既定のアクセス許可を変更します。

 **ユーザーの追加**

```
Add-WssUser [-Name] <string> [-Password] <securestring> [-AccessLevel <string> {User | Administrator}] [-FirstName <string>] [-LastName <string>] [-AllowRemoteAccess] [-AllowVpnAccess]   [<CommonParameters>]
```

 例:

```
$password = ConvertTo-SecureString "Passw0rd!" -asplaintext  œforce
$Add-WssUser -Name User2Test -Password $password -Accesslevel Administrator -FirstName User2 -LastName Test
```

 このコマンドは、User2Test という名前の管理者をパスワード Passw0rd! で追加します。

 **ユーザーの有効/無効**

 例:

```
$CurrentUser = get-wssuser  œname user2test
$CurrentUser.UserStatus = 0
$CurrentUser.Commit()
```

 このコマンドは、user2test という名前のユーザーを無効にします。 UserStatus を 1 に設定すると、このユーザーが有効になります。

 **サーバー フォルダーの追加**

```
Add-WssFolder [-Name] <string> [-Path] <string> [[-Description] <string>] [-KeepPermissions] [<CommonParameters>]
```

 例:

```
$Add-WssFolder -Name "MyTestFolder" -Path "C:\ServerFolders\MyTestFolder"
```

 このコマンドを実行すると、指定した場所に MyTestFolder という名前のサーバーフォルダーが追加されます。

## <a name="how-do-i-add-a-second-server-to-the-windows-server-essentials-domain"></a>2台目のサーバーを Windows Server Essentials ドメインに追加操作方法には、
 Windows Server Essentials はドメインコントローラーなので、標準の方法で2番目のサーバーをドメインに参加させることができます。

## <a name="which-email-solutions-can-be-integrated"></a>統合できる電子メール ソリューション
 Windows Server Essentials は、Office 365 とオンプレミス Exchange の2つの電子メールソリューションとの統合をサポートしています。 独自のホスト型電子メールソリューションを実行している場合は、Windows Server Essentials をホスト型電子メールソリューションと統合するためのアドインを開発する必要があります。

## <a name="how-do-i-migrate-on-premises-windows-sbs-201120082003-to-the-hosted-windows-server-essentials"></a>オンプレミスの Windows SBS (2011/2008/2003) をホストされている Windows Server Essentials に移行操作方法ますか?
 移行ガイドは、オンプレミスの Windows Small Business Server (Windows SBS) から Windows Server Essentials への移行に使用できます。 ホスト環境に応じて、手順の一部が多少異なる場合があります。 ただし、一般的なタスクおよび移行するワークロードは同じはずです。 [移行ガイド](https://go.microsoft.com/fwlink/p/?LinkID=254292) を参照し、ホスト環境に基づいて必要なカスタマイズを行うことをお勧めします。

 ソース サーバーと移行先サーバーを同じサブネットに配置することをお勧めします。 それが無理な場合、次の点を確認する必要があります。

-   ソース サーバーと移行先サーバーの内部 DNS 名に、互いに到達できる。

-   すべての必要なポートが開いている。

## <a name="how-can-i-upgrade-windows-server-essentials-to-windows-server-standard"></a>Windows Server Essentials を Windows Server Standard にアップグレードするにはどうすればよいですか。
 Windows Server Essentials を Windows Server Standard にアップグレードできます。 ロックと制限を削除し、Windows Server Standard に足りないパッケージを追加します。 詳細については、 [ドキュメントをダウンロードしてください](https://go.microsoft.com/fwlink/p/?LinkID=253181)。

## <a name="what-are-the-native-tools-for-monitoring-and-management"></a>監視と管理のためのネイティブ ツール

### <a name="group-policy-management"></a>グループ ポリシー管理
 Windows Server Essentials は、Windows Server 2012 でネイティブグループポリシーサポートを利用し、フォルダーリダイレクトとセキュリティ設定を構成するためのユーザーインターフェイスを提供します。

> [!NOTE]
>  ホストされている環境では、ユーザー プロファイルのフォルダーのリダイレクションが有効になっている場合、データ サイズが大きいと、エンド ユーザーのログオンに時間がかかる可能性があります。

### <a name="management-pack"></a>管理パック
 Windows Server Essentials 管理パックは、Windows Server Essentials の正常性アラートシステムに対する監視機能を提供します。これにより、さまざまな小規模企業に専用の多数の Windows Server Essentials サーバーをホストして管理することができます。 このバージョンでの監視には、システムの重要なアラートだけが含まれます。

#### <a name="management-pack-scope"></a>管理パックの範囲
 この管理パックは、Windows Server Essentials 固有の機能を監視するのに役立ちます。 Windows Server 2012 Standard オペレーティング システムの一般的な機能は監視しません。 Windows Server Essentials を監視するには、windows server Essentials 管理パックと Windows Server 2012 Standard 用管理パックの両方を使用する必要があります。

#### <a name="mandatory-configuration"></a>必須の構成
 管理パックを使用するには、次の手順を実行する必要があります。

1.  エージェントをインストールし、証明書信頼を使用して信頼を構成します。 Windows Server Essentials はドメインコントローラーとして事前に構成されており、他のドメインまたはフォレストとの信頼を持つことができないため、System Center Operation Manager エージェントを Windows Server Essentials にインストールし、証明書を使用して管理サーバーとの信頼を構成する必要があります。

2.  管理パックをダウンロードします。 Operations Manager 2007 を使用して Windows Server Essentials を監視するには、まず、管理パックカタログから[Windows Server オペレーティングシステム管理パック](https://connect.microsoft.com/WindowsServer/Downloads/DownloadDetails.aspx?DownloadID=45010)をダウンロードする必要があります。

3.  管理パック ファイルをインポートします。 ローカライズ版の管理パックを使用している場合、メイン管理パック ファイルと言語パックの両方をインポートする必要があります。

#### <a name="files-in-this-monitoring-pack"></a>この監視パック内のファイル
 Windows Server Essentials 用監視パックには、次のファイルが含まれています。

-   Microsoft.Windows.Server.2012.Essentials.mp

-   Microsoft. Server... <locale. \> mp

### <a name="back-up-and-restore"></a>バックアップと復元
 Windows Server Essentials では、サーバーとクライアントの両方をバックアップできます。

#### <a name="back-up-the-server"></a>サーバーのバックアップ
 Windows Server Essentials では、オンプレミスバックアップとオフプレミスバックアップの2つのサーバーバックアップ方法がサポートされています。

 **オンプレミス バックアップ** では、別のディスクにブロックレベルの増分バックアップを定期的に実行できます。 ホストとして、仮想ディスクを Windows Server Essentials VM に接続し、この仮想ディスクへのサーバーバックアップを構成することができます。 仮想ディスクは、Windows Server Essentials VM とは別の物理ディスクに配置する必要があります。

- Windows Server Essentials VM をバックアップする別のメカニズムがあり、ユーザーに Windows server essentials のネイティブサーバーバックアップ機能を表示させたくない場合は、windows server essentials ダッシュボードから無効にして、関連するすべてのユーザーインターフェイスを削除することができます。 詳細については、 [ADK ドキュメント](https://go.microsoft.com/fwlink/p/?LinkID=249124)の「サーバーバックアップのカスタマイズ」セクションを参照してください。

  **オフプレミス バックアップ** では、サーバー データをクラウド サービスに定期的にバックアップできます。 Windows Server Essentials 用の Microsoft Azure Backup 統合モジュールをダウンロードしてインストールし、Microsoft が提供する Azure Backup を活用することができます。

  別のクラウド サービスを希望する場合、次を実行する必要があります。

1.  既定の Azure Backup ではなく、優先するクラウドサービスへのリンクを提供するように、Windows Server Essentials ダッシュボードのユーザーインターフェイスを更新します。 詳細については、 [ADK ドキュメント](https://go.microsoft.com/fwlink/p/?LinkID=249124)の「イメージのカスタマイズ」セクションを参照してください。

2.  OptionalWindows Server Essentials ダッシュボード用のアドインを開発して、クラウドバックアップサービスを構成および管理します。

#### <a name="back-up-the-client"></a>クライアントのバックアップ
 Windows Server Essentials では、フルクライアントバックアップとファイル履歴の2種類のクライアントデータバックアップがサポートされています。

> [!NOTE]
>  クライアントのバックアップは、VPN 経由でデータをクライアントからサーバーに転送する必要があるため、パフォーマンスに影響する可能性があります。

 **完全なクライアントバックアップ**は、Windows Server Essentials ネットワークに接続されているすべてのクライアントデバイスに対して、既定でに設定されています。 フル クライアント (システムとデータ) の増分バックアップを実行し、データの重複除去をサポートします。 バックアップデータは、Windows Server Essentials を実行しているサーバー上にあります。 障害が発生したクライアントは、前のバックアップ ポイントまでのデータを取り戻すことができます。 この機能をオフにするには、 [ADK ドキュメント](https://technet.microsoft.com/library/jj200150)の「Cfg.ini ファイルを作成する」セクションの手順に従ってください。

 次に、フル クライアント バックアップの注意事項を示します。

- パフォーマンス: 初期クライアント バックアップは、アップロードするデータ量が多いため、時間がかかる可能性があります。

- 安定性: クライアント側のインターネット接続が安定しない場合があります。 クライアント バックアップは、再開できるように設計されています。既定のチェックポイントは 40 GB です (クライアント バックアップ データベースで、40 GB のデータがバックアップされるたびにチェックポイントが作成されます)。 インターネット接続の信頼性が低いことが予測される場合、この値を小さい値に変更できます。

  -   チェックポイント ジョブを有効にするには、サーバーで、レジストリ キー HKLM\Software\Microsoft\Windows Server\Backup\GetCheckPointJobs を 1 に設定します。

  -   チェックポイントしきい値を変更するには、クライアントで、HKLM\Software\Microsoft\Windows Server\Backup\CheckPointThreshold を既定値 (40 GB) から変更します。

- クライアント ベア メタル回復: Windows プレインストール環境では VPN 接続をサポートしないため、クライアント ベア メタル回復はサポートされません。

  **ファイル履歴**は、プロファイルデータ (ライブラリ、デスクトップ、連絡先、お気に入り) をネットワーク共有にバックアップするための Windows 8.1 の機能です。 Windows Server Essentials では、Windows Server Essentials に参加しているすべての Windows 8.1 クライアントのファイル履歴設定を一元的に管理できます。 バックアップ データは、Windows Server Essentials を実行しているサーバーに保存されます。 この機能をオフにするには、 [ADK ドキュメント](https://technet.microsoft.com/library/jj200150)の「Cfg.ini ファイルを作成する」セクションの手順に従ってください。

### <a name="storage-management"></a>記憶域の管理
 [新しい記憶域機能](https://technet.microsoft.com/library/hh831739.aspx) により、異種ハード ドライブの物理記憶域容量の集計、ハード ドライブの動的な追加、復元レベルを指定したデータ ボリュームの作成が可能となりました。 また、Windows Server Essentials に iSCSI ディスクを接続して、記憶域を拡張することもできます。

## <a name="what-are-the-main-scenarios-i-should-test"></a>テストする必要があるメイン シナリオの詳細
 ホストのパースペクティブから、次のシナリオをテストすることをお勧めします。

 **サーバーの展開**

- ラボ環境で Windows Server Essentials サーバーを展開します。

- 必要に応じて Windows Server Essentials イメージをカスタマイズします。

- 無人セットアップファイルと cfg.ini を使用して、Windows Server Essentials の展開を自動化します。

- オンプレミスの Windows SBS をホスト型 Windows Server Essentials に移行します。

- Windows Server Essentials から Windows Server 2012 にアップグレードします。

  **サーバーの構成**

- Anywhere Access (VPN、リモート Web アクセス、DirectAccess) を構成します。

- 記憶域とサーバー フォルダーを構成します。

- (適用できる場合) サーバー バックアップ、オンライン バックアップ、クライアント バックアップ、ファイル履歴を構成します。

- (適用できる場合) 記憶域を構成し、管理します。

- (適用できる場合) 電子メール ソリューション統合 (Office 365、ホスト型 Exchange など) を構成します。

- (適用できる場合) メディア サーバーを構成します。

  **Server Management**

- ユーザーを管理します。

- アラートの電子メール通知を構成し、受信します。

- エラー/警告の場合、BPA を実行します。

- System Center の監視パックを構成します。

- 破損の場合、サーバー回復を構成します。

  **クライアントエクスペリエンス**

- インターネット経由でのクライアントの展開 (パーソナル コンピューターまたは Mac OS)。

- クライアントのスタート パッドを使用して、共有フォルダーにアクセスします。

- リモート Web アクセス経由でさまざまなデバイス (パーソナル コンピューター、電話、タブレット) からサーバー資産にアクセスします。

- Windows Phone 用のマイ サーバー アプリ。

- (適用できる場合) ファイル履歴、クライアント バックアップ、復元 (BMR なし)、フォルダー リダイレクション。

- (適用できる場合) 電子メール統合エクスペリエンス。

## <a name="where-can-i-get-more-support"></a>サポートの入手場所
 下のリンクから SDK ドキュメントと ADK ドキュメントを入手できます。

- [SDK](https://go.microsoft.com/fwlink/p/?LinkID=248648)

- [ADK](https://go.microsoft.com/fwlink/p/?LinkID=249124)

  [接続] を使って、バグを機能チームに報告できます。 ログを生成するには、サーバーと、サーバーに参加しているクライント上のフォルダーC:\ProgramData\Microsoft\Windows Server\Logs の ZIP ファイルを作成します。
