---
title: 社内 Exchange Server と Windows Server Essentials を統合する
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: b56a21e2-c9e3-4ba9-97d9-719ea6a0854b
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 13de76ba7e9452e6498479b060712d06c0571c1a
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85470887"
---
# <a name="integrate-an-on-premises-exchange-server-with-windows-server-essentials"></a>社内 Exchange Server と Windows Server Essentials を統合する

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

このガイドでは、Exchange Server を実行する社内サーバーをセットアップし、Windows Server Essentials を実行しているサーバーと統合するための情報と基本的な手順について説明します。

 Windows Server Essentials ネットワークで Exchange Server を実行する社内サーバーを展開する場合は、展開を試みる前にこのガイドをお読みください。

> [!NOTE]
>  Exchange Server 2010 では、Windows Server 2012 が実行されているコンピューターへのインストールはサポートしていません。

## <a name="prerequisites"></a>前提条件
 Windows Server Essentials ネットワークに Exchange Server をインストールする前に、このセクションに記載されている作業が完了していることを確認してください。

-   [Windows Server Essentials を実行するサーバーをセットアップする](Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md#BKMK_SetUpSBS8)

-   [Exchange Server のインストール先となる 2 台目のサーバーを準備する](Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md#BKMK_SecondServer)

-   [インターネット ドメイン名を構成する](Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md#BKMK_DomainNames)

###  <a name="set-up-a-server-that-is-running-windows-server-essentials"></a><a name="BKMK_SetUpSBS8"></a>Windows Server Essentials を実行しているサーバーをセットアップする
 Windows Server Essentials を実行するサーバーが既にセットアップされている必要があります。 このサーバーは、Exchange Server を実行するサーバーに対するドメイン コントローラーになります。 Windows Server Essentials を設定する方法については、「[Windows Server Essentials のインストール](../install/Install-Windows-Server-Essentials.md)」を参照してください。

###  <a name="prepare-a-second-server-on-which-to-install-exchange-server"></a><a name="BKMK_SecondServer"></a>Exchange Server をインストールする2台目のサーバーを準備する
 Exchange Server 2010 または Exchange Server 2013 の実行が正式にサポートされているバージョンの Windows Server オペレーティング システムを実行する 2 台目のサーバーを用意し、Exchange Server をインストールする必要があります。 その後、2 台目のサーバーを Windows Server Essentials ドメインに参加させる必要があります。

 2台目のサーバーを Windows Server Essentials ドメインに参加させる方法については、「 [Get Connected](../use/Get-Connected-in-Windows-Server-Essentials.md)」の「2台目のサーバーをネットワークに参加させる」を参照してください。

> [!NOTE]
>  Microsoft では、Windows Server Essentials を実行しているサーバーへの Exchange Server のインストールはサポートしていません。

###  <a name="configure-your-internet-domain-name"></a><a name="BKMK_DomainNames"></a>インターネットドメイン名を構成する
 Exchange Server が実行されている社内サーバーを Windows Server Essentials と統合するには、会社用の有効なインターネット ドメイン名 (*contoso.com* など) を登録済みであることが必要です。 また、ドメイン ネーム プロバイダーと連携して、Exchange Server で要求される DNS リソース レコードを作成する必要があります。

 たとえば、会社のインターネット ドメイン名が contoso.com の場合、Exchange Server を実行する社内サーバーを参照するために *mail.contoso.com* という完全修飾ドメイン名 (FQDN) を使用するには、ドメイン ネーム プロバイダーと連携して、次の表に示すような DNS リソース レコードを作成します。


| リソース レコード名 |     レコード タイプ     |                                                                         レコードの設定                                                                          |                                                                                                                                                                                                                                                              説明                                                                                                                                                                                                                                                              |
|----------------------|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         mail         |      ホスト (A)       |                                                        Address=*ISP によって割り当てられたパブリック IP アドレス*                                                         |                                                                                                                                                                                                   Exchange Server で mail.contoso.com 当てのメールを受信します。<br /><br /> 他の名前を任意に選択して使用できます。                                                                                                                                                                                                    |
|          MX          | メール エクスチェンジャー (MX) |                                            ホスト名=@<br /><br /> アドレス=mail.contoso.com<br /><br /> 優先順位=0                                             |                                                                                                                                                                                                      email@contoso.comExchange server を実行しているオンプレミスサーバーに到着するための電子メールメッセージのルーティングを提供します。                                                                                                                                                                                                       |
|         SPF          |     テキスト (TXT)      |                                                                        v=spf1 a mx ~all                                                                         |                                                                                                                                                                                                                      このサーバーから送信された電子メールがスパムとして識別されるのを防ぐためのリソース レコードです。                                                                                                                                                                                                                      |
|  autodiscover._tcp   |    サービス (SRV)    | サービス: _autodiscover<br /><br /> プロトコル: _tcp<br /><br /> 優先度:0<br /><br /> 重み:0<br /><br /> ポート:443<br /><br /> ターゲット ホスト: mail.contoso.com | Microsoft Office Outlook およびモバイル デバイスで、Exchange Server を実行している社内サーバーを自動的に検出できるようにします。<br /><br /> **注:** また、自動検出ホスト (A) リソースレコードを構成し、Exchange Server を実行しているオンプレミスサーバーのパブリック IP アドレスにレコードを指定することもできます。 ただし、このオプションを実装する場合は、mail.contoso.com と autodiscover.contoso.com の両方のドメイン名をサポートするサブジェクト代替名 (SAN) SSL 証明書も提供する必要があります。 |

> [!NOTE]
>  -   この例に含まれている *contoso.com* という部分は、実際に登録したインターネット ドメイン名で置き換えてください。

 Exchange Server を実行する社内サーバーには、Windows Server Essentials を実行しているサーバーで使用されている FQDN とは異なる FQDN を選択する必要があります。 たとえば、Windows Server Essentials を実行しているサーバーにインターネットからアクセスするときにコンピューターが使用する FQDN として、*remote.contoso.com* を選択できます。 一方、Exchange Server を実行している社内サーバーに電子メールをルーティングするための FQDN には、*mail.contoso.com* を使用できます。

## <a name="install-exchange-server"></a>Exchange Server のインストール
 Windows Server Essentials の Exchange Server 統合機能は、次のバージョンの Exchange Server をサポートしています。

- Exchange Server 2013

- Exchange Server 2010 Service Pack 1 (SP1)

  2 台目のサーバーに Exchange Server をインストールする前に、まず現在の管理者アカウントを **Enterprise Admins** グループに追加する必要があります。

#### <a name="to-add-the-current-administrator-account-to-the-enterprise-admins-group"></a>現在の管理者アカウントを Enterprise Admins グループに追加するには

1.  Windows Server Essentials に管理者としてログオンします。

2.  Windows PowerShell を管理者として実行します。

3.  Windows PowerShell コマンドプロンプトで、「 **add-adgroupmember "Enterprise Admins" $env: username**」と入力し、enter キーを押します。

#### <a name="to-install-exchange-server"></a>Exchange Server をインストールするには

1.  管理者として 2 台目のサーバーにログオンします。

2.  インターネット ブラウザーを開き、 [Exchange Server 展開アシスタント](https://go.microsoft.com/fwlink/p/?LinkID=249163) Web サイトにアクセスします。

3.  **[On-Premises Only]** をクリックします。

4.  インストールする Exchange Server のバージョンに応じた新規インストール オプションをクリックします。

    > [!NOTE]
    >  Windows Small Business Server のインストールから移行する場合は、移行の手順を含んでいる適切なアップグレード オプションを選択してください。

5.  次のページで、既定の設定を受け入れて **[次へ]** をクリックします。

    > [!NOTE]
    >  新規インストールの Exchange Server でパブリック フォルダーを使用する予定がある場合は、その設定を **[はい]** に変更してください。

6.  チェック リストに説明されている手順に従って、Exchange Server を展開します。

     Exchange Server 展開アシスタントでは、次の操作を実行することもできます。

    -   チェック リストのコピーを印刷する。

    -   チェック リストのコピーを電子メールの受信者に送信する。

    -   チェック リストを PDF ファイルとしてダウンロードする。

> [!NOTE]
> - Exchange Server を実行するサーバーでは、必ず管理ツールをインストールするように選択する必要があります。 管理ツールは、Windows Server Essentials の Exchange Server 統合機能に必要です。
>   -   仮想ディレクトリを構成する必要がある場合は、仮想ディレクトリごとに、**InternalUrl** プロパティを **ExternalUrl** プロパティと同じ URL に設定することをお勧めします。 詳細については、Exchange Server 2010 オンライン ヘルプ Web サイトで、 [クライアント アクセス サーバーの仮想ディレクトリの管理](https://go.microsoft.com/fwlink/p/?LinkId=251058) を参照してください。
>   -   Windows Server Essentials のリモート Web アクセス サイトから Outlook Web Access (OWA) にアクセスする場合は、OWA の外部 URL プロパティを設定する必要があります。

 Exchange Server 2010 をクリーン セットアップでインストールする場合は、次のスクリプトを使用して Exchange Server をセットアップすることもできます。

#### <a name="to-use-scripts-to-set-up-exchange-server"></a>スクリプトを使用して Exchange Server をセットアップするには

1.  メモ帳を開き、新しいファイルに次のスクリプトを貼り付けます。

```powershell
Import-Module ServerManager

Add-WindowsFeature NET-Framework,RSAT-ADDS,Web-Server,Web-Basic-Auth,Web-Windows-Auth,Web-Metabase,Web-Net-Ext,Web-Lgcy-Mgmt-Console,WAS-Process-Model,RSAT-Web-Server,Web-ISAPI-Ext,Web-Digest-Auth,Web-Dyn-Compression,NET-HTTP-Activation,Web-Asp-Net,Web-Client-Auth,Web-Dir-Browsing,Web-Http-Errors,Web-Http-Logging,Web-Http-Redirect,Web-Http-Tracing,Web-ISAPI-Filter,Web-Request-Monitor,Web-Static-Content,Web-WMI,RPC-Over-HTTP-Proxy  Restart
```

2. このファイルを **InstallDependencies.ps1** として保存します。

3. サーバーに Exchange SSL 証明書をコピーします。

4. メモ帳で新しいファイルを開き、次のテキストをファイルにコピーします。

```powershell
param (
    [string]
    [Parameter(Mandatory=$true, HelpMessage = "The path to your Certificate file, must be a *.pfx format")]
    $CertPath = "c:\certificates\ExchangeCertificate.pfx",
    [Security.SecureString]
    [Parameter(Mandatory=$true, HelpMessage = "The password of your cert")]
    $CertPassword = $null,
    [string]
    [Parameter(Mandatory=$true, HelpMessage = "Domain Name, eg. contoso.com")]
    $DomainName = "contoso.com",
    [string]
    [Parameter(Mandatory=$true, HelpMessage = "Server IP Address, eg. 192.168.0.1")]
    $ServerIpAddress = "192.168.0.1",
    [string]
    [Parameter(Mandatory=$true, HelpMessage = "Internal Ip Range, eg. 192.168.0.0-192.168.0.255")]
    $InternalIpRange = "192.168.0.0-192.168.0.255"
)

#Import Exchange Certificate, and Enable it for POP IIS IMAP SMTP services.

Import-ExchangeCertificate  -FileData ([Byte[]]$(Get-content -Path $CertPath  -Encoding byte  -ReadCount 0)) -Password:$CertPassword -Force | Enable-ExchangeCertificate -Services 'POP, IIS, IMAP, SMTP' -Force

#New AcceptedDomain and set it to default

New-AcceptedDomain  -Name "official name"  -DomainName $domainname

Set-AcceptedDomain  -Identity "official name"  -MakeDefault $true

#New EmailAddress Policy

$address = "%m@" + $DomainName

New-EmailAddressPolicy -Name "Windows Server Essentials Email Address Policy" -IncludedRecipients AllRecipients -EnabledPrimarySMTPAddressTemplate $address

#Set owa and ecp VirtualDirectory ExternalUrl

$hostname = "mail." + $DomainName

$owa = "https://" + $hostname + "/owa"

$ecp = "https://" + $hostname + "/ecp"

$activesync = "https://" + $hostname + "/Microsoft-Server-ActiveSync"

$oab = "https://" + $hostname + "/OAB"

$ews = "https://" + $hostname + "/EWS/Exchange.asmx"

Get-OwaVirtualDirectory | Set-OwaVirtualDirectory  -ExternalUrl $owa  -InternalUrl $owa

Get-EcpVirtualDirectory | Set-EcpVirtualDirectory  -ExternalUrl $ecp  -InternalUrl $ecp

Get-ActiveSyncVirtualDirectory | Set-ActiveSyncVirtualDirectory -ExternalUrl $activesync  -InternalUrl $activesync

Get-OABVirtualDirectory | Set-OABVirtualDirectory -ExternalUrl $oab -InternalUrl $oab -RequireSSL:$true

Get-WebServicesVirtualDirectory | Set-WebServicesVirtualDirectory -ExternalUrl $ews -InternalUrl $ews -BasicAuthentication:$True -Force

#Enable outlook Anywhere

Enable-OutlookAnywhere  -ClientAuthenticationMethod:Basic  -ExternalHostname:$hostname  -SSLOffloading:$false

#new receive/send connector

$machinename = get-content env:computername

$bindingIpaddress = $ServerIpAddress + ":25"

$ReceiveConnectorName = $machinename + "\Default " + $machinename

Set-ReceiveConnector $ReceiveConnectorName -RemoteIPRanges $InternalIpRange

New-ReceiveConnector -Name "WSE Internet Receive Connector" -Usage "Internet" -Bindings $bindingIpaddress -Fqdn $hostname -Enabled $true -Server $machinename -AuthMechanism Tls,BasicAuth,BasicAuthRequireTLS,Integrated

New-SendConnector -Name "WSE Internet SendConnector" -Usage "Internet" -AddressSpaces 'SMTP:*;1' -IsScopedConnector $false -DNSRoutingEnabled $true -UseExternalDNSServersEnabled $true -SourceTransportServers $machinename
```

5. ネットワーク環境に合わせて、スクリプトの先頭にあるパラメーターを設定します。

6. ファイルを **ConfigureExchange.ps1** として保存します。

7. Windows PowerShell を管理者として実行します。

8. Windows PowerShell のコマンド プロンプトで、「**Set-ExecutionPolicy RemoteSigned**」と入力し、Enter キーを押します。

9. **InstallDependencies.ps1** スクリプトを実行します。

10. サーバーを再起動してから、管理者として Windows PowerShell を実行します。

11. Windows PowerShell のコマンド プロンプトで、次のスクリプトを実行します。

    `E:\setup.com /mode:install /roles:mb,ht,ca /OrganizationName:"First Organization"`

   > [!NOTE]
   >  Exchange Server セットアップ プログラムのパスを正しく入力してください。

12. Exchange Server のセットアップが完了したら、管理者として Exchange 管理シェルを開きます。

13. Exchange 管理シェルのコマンド プロンプトで、「**Set-ExecutionPolicy RemoteSigned**」と入力し、Enter キーを押します。

14. **ConfigureExchange.ps1**スクリプトを実行します。

15. サーバーを再起動します。

> [!NOTE]
>  自己発行の証明書ではなく、公的に信頼された SSL 証明書を使用する場合は、セットアップガイドの手順に従って証明書要求を作成し、選択した証明機関に送信することができます。 証明書要求は、Exchange の PowerShell コマンドレットを使用して作成することもできます。 例を次に示します。
>
>  `New-ExchangeCertificate -GenerateRequest -SubjectName "C=US, S=Washington, L=Redmond, O=contoso, OU=contoso, CN=mail.contoso.com" -DomainName mail.contoso.com -PrivateKeyExportable $true | Set-Content -path "c:\Docs\MyCertRequest.req"`
>
>  スクリプトのパラメーターは、ネットワーク環境に合わせてカスタマイズしてください。

## <a name="post-installation-tasks"></a>インストール後の作業
 ここでは、インストール後に実行する必要のあるサーバー構成タスクについて説明します。これには、Windows Server Essentials ネットワークで Exchange Server を実行する社内サーバーをセットアップする場合に固有の情報も含まれます。

### <a name="add-the-public-email-domain-and-configure-the-email-address-policies"></a>パブリック電子メール ドメインを追加して電子メール アドレス ポリシーを構成する

> [!NOTE]
>  これは、クリーン セットアップを実行している場合に必要なタスクです。 Windows Small Business Server から移行している場合は、この手順を省略してください。

 電子メール ドメインを既定の承認済みドメインとして指定し、電子メール アドレス ポリシーを構成する必要があります。

##### <a name="to-add-your-email-domain-as-the-default-accepted-domain"></a>電子メール ドメインを既定の承認済みドメインとして追加するには

1.  Exchange Server の記事「 [承認済みドメインの作成](https://go.microsoft.com/fwlink/p/?LinkId=249174) 」に記載されている手順に従って、承認済みドメインを追加します。

2.  2 台目のサーバーに管理者としてログオンし、Exchange 管理コンソールを開いて、**[組織の構成]** の **[ハブ トランスポート]** タブを表示します。

3.  Exchange 管理コンソールの作業ウィンドウで、新しい承認済みドメインを右クリックし、**[既定値として設定]** をクリックします。

4.  Exchange Server の記事「 [電子メール アドレス ポリシーの作成](https://go.microsoft.com/fwlink/p/?LinkId=249179) 」に記載されている手順に従って、電子メール アドレス ポリシーを作成します。 電子メール アドレス以外は、すべての既定値をそのまま使用できます。 電子メール アドレスについては、お使いのパブリック電子メール ドメインを指定してください。

### <a name="create-smtp-send-and-receive-connectors"></a>SMTP 送信および受信コネクタを作成する

> [!NOTE]
>  このタスクは必須です。

 電子メール メッセージの発信/着信伝送のために、SMTP 送信コネクタと SMTP 受信コネクタを構成する必要があります。

 SMTP 送信コネクタを作成するには、Exchange Server の記事「 [SMTP 送信コネクタの作成](https://technet.microsoft.com/library/aa997285.aspx)」に記載されている手順に従います。

 SMTP 受信コネクタを作成するには、Exchange Server の記事「 [SMTP 受信コネクタの作成](https://technet.microsoft.com/library/bb125159.aspx)」に記載されている手順に従います。

 オプションとして、Exchange の PowerShell コマンドレットを使用して、このドキュメントで既に紹介したスクリプトで送信および受信コネクタを作成することもできます。

### <a name="configure-the-network-router"></a>ネットワーク ルーターを構成する

> [!NOTE]
>  これは、クリーン セットアップを実行している場合に必要なタスクです。 Windows Small Business Server から移行している場合、ネットワークの構成方法については、「[サーバー データの Windows Server Essentials への移行](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)」を参照してください。

 ルーターでは、少なくとも次のポート設定を構成する必要があります。

|ルーター ポート|宛先 IP|宛先ポート|注意|
|-----------------|--------------------|----------------------|----------|
|25 (SMTP)|Exchange Server を実行している社内サーバーの内部 IP。|25||
|80 (HTTP)|Windows Server Essentials を実行しているサーバーの内部 IP|80||
|443 (HTTPS)|Windows Server Essentials を実行しているサーバーの内部 IP|443||

 ネットワークで POP3 または IMAP メッセージング プロトコルをサポートする場合は、これらのプロトコルに対するポート転送も構成する必要があります。 関連情報については、Exchange Server TechNet ライブラリのトピック「 **ネットワーク ポートのリファレンス** 」の「 [クライアント アクセス サーバー](https://go.microsoft.com/fwlink/p/?LinkId=250773) 」を参照してください。

> [!NOTE]
> - Windows Server Essentials を実行しているサーバーと、Exchange Server を実行している 2 台目のサーバーには、静的 IP アドレスを構成することをお勧めします。 Windows Server 2003 または Windows Server 2008 R2 を実行しているコンピューターで静的 IP アドレスを構成する手順については、Windows Server TechNet ライブラリの「 [静的 IP アドレスを構成する](https://technet.microsoft.com/library/cc754203\(v=ws.10\).aspx) 」を参照してください。
>
>   **注:** DNS サーバーの設定は、常に Windows Server Essentials を実行しているサーバーの IP アドレスを指している必要があります。
>   -   ルーターで、Windows Server Essentials を実行しているサーバーの IP アドレスと Exchange Server を実行しているサーバーの IP アドレスが予約されているか、または DHCP IP アドレスの範囲から外れていることを確認してください。
>   -   このセクションのルーター構成では、インターネット サービス プロバイダー (ISP) によって割り当てられたパブリック IP アドレスが 1 つだけであると想定しています。 複数のパブリック IP アドレスがある場合は、Windows Server Essentials を実行しているサーバーと Exchange Server を実行しているサーバーに別々の IP アドレスを割り当て、パブリック IP アドレスに基づくポート フォワーディングを作成できます。

### <a name="enable-on-premises-exchange-server-integration-on-windows-server-essentials"></a>Windows Server Essentials で社内の Exchange Server との統合を有効にする

> [!NOTE]
>  Windows Small Business Server インストールから移行している場合は、今はこの手順を省略し、移行元サーバーで Exchange Server の以前のインストールをアンインストールしてから実行することをお勧めします。

 Exchange Server を実行するサーバーをインストールして構成したら、Windows Server Essentials を実行しているサーバーで、社内の Exchange Server との統合を有効にする必要があります。

##### <a name="to-enable-on-premises-exchange-server-integration-from-the-dashboard"></a>ダッシュボードから社内の Exchange Server との統合を有効にするには

1.  Windows Server Essentials を実行しているサーバーに管理者としてログオンし、ダッシュボードを開きます。

2.  **[ホーム]** ページで、**[電子メール サービスへの接続]** をクリックし、**[Exchange Server の統合]** をクリックします。

3.  情報ウィンドウで、**[Exchange Server 統合をセットアップする]** をクリックします。

4.  ウィザードの指示に従います。

### <a name="configure-a-reverse-proxy"></a>リバース プロキシを構成する

> [!NOTE]
>  これは、インターネット サービス プロバイダーからのインターネット接続が 1 つだけの場合に必要なタスクです。

 Windows Server Essentials と Exchange Server のどちらも、ネットワーク ユーザーのためにいくつかのリモート アクセス シナリオをサポートしています。 たとえば、Windows Server Essentials を実行しているサーバーで Anywhere Access を有効にすると、リモート Web アクセス サイトにリモートからアクセスしたり、仮想プライベート ネットワーク (VPN) を使用して Windows Server Essentials ネットワークにリモート接続したりできます。 電子メール メッセージにリモートからアクセスするには、Outlook Anywhere、Outlook Web Access (OWA)、または ActiveSync を使用する必要があります。

 Windows Server Essentials と Exchange Server を実行しているサーバーの両方が同じルーターに接続していて、インターネット サービス プロバイダーからルーターへの着信インターネット接続が 1 つしかない場合は、リバース プロキシ ソリューションを使用して、インターネットから送信される各種のリモート アクセス要求を、宛先のホスト名に基づいてルーティングする必要があります。 リバース プロキシ ソリューションとして、Microsoft でサポートされている IIS アプリケーション要求ルーティング処理 (ARR) 拡張機能を使用することをお勧めします。 IIS アプリケーション要求ルーティング処理の詳細については、 [アプリケーション要求ルーティング処理の Web サイト](https://go.microsoft.com/fwlink/p/?LinkId=249181)を参照してください。

##### <a name="to-install-and-configure-application-request-routing"></a>アプリケーション要求ルーティング処理をインストールして構成するには

1. Windows Server Essentials に管理者としてログオンします。

2. インターネット ブラウザーを開き、 [アプリケーション要求ルーティング処理の Web サイト](https://go.microsoft.com/fwlink/p/?LinkId=249181)にアクセスします。

3. ARR Web サイトで、**[インストール]** をクリックし、指示に従って ARR をインストールします。

   > [!NOTE]
   >  ARR のインストール中に、URL Rewrite Module を選択する必要があります。
   >
   >  ARR のインストールの最後に、ARR 2.5 用の KB 2589179 が正しくインストールされなかったというエラーが発生することがあります。 このエラーは無視してかまいません。

4. ARR のインストールが完了したら、**リモート デスクトップ ゲートウェイ** サービスが実行されている場合は再起動します。

   > [!NOTE]
   >  ARR をインストールした後は、**リモート デスクトップ ゲートウェイ** サービスが停止していることがあります。 手動でサービスを再起動するには、**サービス**管理ツールを開き、**[リモート デスクトップ ゲートウェイ]** サービスを再起動します。

5. [ARR 2.5 用の KB2732764 をダウンロード](https://go.microsoft.com/fwlink/?LinkID=258302)し、Windows Server Essentials を実行しているサーバーに更新プログラムをインストールします。

6. Windows Server Essentials を実行しているサーバーに Exchange Server の SSL 証明書ファイルをコピーします。 この証明書ファイルは、秘密キーを含んだ PFX ファイル形式にする必要があります。

   > [!NOTE]
   >  自己発行の証明書を使用する場合は、Exchange Server の記事「 [Exchange 証明書のエクスポート](https://technet.microsoft.com/library/dd351274.aspx) 」に記載されている手順に従って証明書をエクスポートしてください。

7. 実行している Windows Server Essentials のバージョンに応じて、次の手順を実行します。

   -   Windows Server Essentials の場合: 管理者としてコマンドウィンドウを開き、%ProgramFiles%\Windows Server\Bin ディレクトリを開きます。

   -   Windows Server Essentials の場合: 管理者としてコマンドウィンドウを開き、%Windir%\System32\Essentials ディレクトリを開きます。

8. インストール シナリオに応じて、次のいずれかの手順に従って ARR を構成します。

   - クリーン セットアップを実行している場合は、次のコマンドを実行します。

      **Arrconfig config-** _証明書ファイルへの証明書パス_ **-** _Exchange Server のホスト名ホスト名_

     > [!NOTE]
     >  たとえば、次のようになります。**Arrconfig config-cert** _c:\temp\certificate.pfx_ **-ホスト名** _mail.contoso.com_
     >
     >  *mail.contoso.com* は、証明書によって保護されているドメイン名に置き換えてください。

   - Windows Small Business Server から移行している場合は、次のコマンドを実行します。

      **Arrconfig config-** _証明書ファイルへの証明書パス_ **-** targetserver _host names for exchange_ server **-** _exchange server のサーバー名_

      たとえば、次のようになります。**Arrconfig config-cert** _c:\temp\certificate.pfx_ **-ホスト名** _mail.contoso.com_ **-targetserver** _exchangesvr」_

      *mail.contoso.com* は実際のドメイン名に、 *ExchangeSvr* は Exchange Server を実行しているサーバー名に置き換えてください。

9. 証明書のパスワードを求める画面が表示されたら、パスワードを入力します。

> [!NOTE]
> - Exchange Server 用に購入した SSL 証明書には、指定したホスト名が含まれている必要があります。
>   -   複数のホスト名がある場合は、コンマ (,) を使用して区切ります。

 構成が機能することを確認するには、Exchange Server を実行しているサーバーの OWA web サイト () にアクセスしてみてください https://mail 。 *ドメイン名*.com/owa) にアクセスします。 接続の問題のトラブルシューティングには、 [Microsoft リモート接続アナライザー](https://go.microsoft.com/fwlink/p/?LinkId=249455) ツールを使用することもできます。

### <a name="configure-split-dns-for-exchange-server"></a>Exchange Server 用に分割 DNS を構成する

> [!NOTE]
>  これは推奨タスクです。

 分割 DNS を使用すると、DNS 要求がどこから送信されたかに応じて、同じホスト名に対して DNS 内で異なる IP アドレスを構成することができます。 クライアント コンピューターがイントラネット上にある場合、DNS 要求はイントラネット IP アドレスに解決されます。 クライアント コンピューターがインターネット上にある場合、DNS 要求はインターネット IP アドレスに解決されます。 この違いをユーザーが意識することはほとんどありません。

 分割 DNS は、ユーザーがどこにいても、常に同じホスト名を使用して Exchange Server サービスにアクセスできるように構成することをお勧めします。

##### <a name="to-configure-split-dns-for-exchange-server"></a>Exchange Server 用に分割 DNS を構成するには

1.  管理者として Windows Server Essentials にログオンし、DNS マネージャーを開きます。

2.  DNS マネージャーのコンソール ツリーで、サーバーを右クリックして **[新しいゾーン]** をクリックします。 **新しいゾーン ウィザード**が表示されます。

3.  ウィザードの **[ゾーンの種類]** ページで、既定のオプションを受け入れて **[次へ]** をクリックします。

4.  **[Active Directory ゾーン レプリケーション スコープ]** ページで、既定のオプションを受け入れて **[次へ]** をクリックします。

5.  **[前方または逆引き参照ゾーン]** ページで、**[前方参照ゾーン]** を受け入れるか選択し、**[次へ]** をクリックします。

6.  **[ゾーン名]** ページで、Exchange Server を実行しているサーバーの FQDN (たとえば「*mail.contoso.com*」) を入力し、**[次へ]** をクリックします。

7.  **[動的更新]** ページで、既定のオプションを受け入れて **[次へ]** をクリックします。次に、**[完了]** をクリックします。

8.  DNS マネージャーのコンソール ツリーで、新しい前方参照ゾーンを右クリックし、**[新しいホスト (A または AAAA)]** をクリックします。

9. **[新しいホスト]** ページで、**[名前]** フィールドは空白のままにし、Exchange Server を実行しているサーバーのイントラネット IP アドレスを入力して、**[ホストの追加]** をクリックします。

    > [!NOTE]
    >  **[名前]** フィールドを空白にすると、親ドメイン名が既定で使用されます。

10. **[新しいホスト]** ページで、**[完了]** をクリックします。

> [!NOTE]
>  ActiveSync を使用していて、一部のメールボックス アカウントで電子メールを同期できない場合は、問題のあるアカウントが 1 つ以上の保護グループ (Domain Administrators など) のメンバーになっていないかどうかを確認します。 この問題の解決に役立つ関連情報については、「 [Exchange ActiveSync から HTTP 500 エラーが返された](https://technet.microsoft.com/library/dd439375\(EXCHG.80\).aspx)」を参照してください。

## <a name="related-topics"></a>関連トピック
 社内の Exchange Server との統合の詳細については、以下のセクションを参照してください。

### <a name="what-happens-if-i-disable-exchange-integration"></a>Exchange との統合を無効にすると、どうなりますか。
 社内の Exchange Server との統合を無効にすると、Windows Server Essentials ダッシュボードを使用して Exchange Server のメールボックスを表示、作成、または管理することはできなくなります。

### <a name="what-do-i-need-to-know-about-email-accounts"></a>電子メール アカウントについて知っておく必要があることは何ですか。
 サーバーにはホスト型の電子メール ソリューションが構成されています。 Microsoft Office 365 などのホスト型電子メールプロバイダーからのソリューションでは、ネットワークユーザー用に個別の電子メールアカウントを提供できます。 Windows Server Essentials でユーザー アカウントの追加ウィザードを実行してユーザー アカウントを作成するとき、ウィザードはユーザー アカウントを、使用可能なホスト型の電子メール ソリューションに追加しようとします。 同時に、ウィザードはユーザーに電子メール名 (エイリアス) を割り当て、メールボックスの最大サイズ (クォータ) を設定します。 メールボックスの最大サイズは、使用する電子メール プロバイダーによって異なります。 ユーザー アカウントを追加した後は、ユーザーのプロパティ ページからメールボックス エイリアスとクォータの情報の管理を続行することができます。 ユーザー アカウントとホスト型電子メール プロバイダーを完全に管理するには、ホスト型プロバイダーの管理コンソールを使用します。 プロバイダーによっては、Web ベースのポータルまたはサーバー ダッシュボードのタブのどちらからも管理コンソールにアクセスできます。

 ユーザー アカウントの追加ウィザードの実行時に指定したエイリアスは、ユーザー エイリアスに推奨される名前としてホスト型電子メール プロバイダーに送信されます。 たとえば、ユーザーエイリアスが*FrankM*の場合、ユーザーの電子メールアドレスはになり <em>FrankM@Contoso.com</em> ます。

 さらに、ユーザー アカウントの追加ウィザードでユーザー用に設定したパスワードは、ホスト型電子メール ソリューションでユーザーの最初のパスワードになります。

 最後に、サーバーでユーザー アカウントの削除ウィザードを使用してユーザーを削除する場合、ウィザードは要求をホスト型電子メール プロバイダーにも送信して、プロバイダーのシステムからもユーザーを削除します。 プロバイダーは、ユーザーのアカウントと、アカウントに関連付けられている電子メールの両方を削除する場合があります。

 必要な電子メール クライアント ソフトウェアをセットアップする方法に関するユーザー情報については、ホスト型電子メール プロバイダーから提供されるヘルプ ドキュメントを参照してください。

### <a name="what-is-a-mailbox-quota"></a>メールボックス クォータとは何ですか。
 ネットワークユーザーの Exchange メールボックスデータに割り当てられる記憶域の容量は、メールボックスクォータと呼ばれます。

 ダッシュボードで **[Exchange Server 統合をセットアップする]** タスクを実行すると、ユーザー アカウントの追加ウィザードにページが追加され、そのページで、メールボックス クォータを適用するかどうかを選択し、クォータ サイズを指定できます。 既定では、**[メールボックス クォータを適用する]** オプションが選択されていて (オン)、ユーザーのメールボックスに 2 GB の記憶域が割り当てられます。 Exchange 管理者は、会社のニーズに合わせてメールボックス クォータの設定をカスタマイズできます。

## <a name="additional-references"></a>その他のリファレンス

-   [Windows Server Essentials のシステム要件](../get-started/system-requirements.md)

-   [電子メール統合の管理](Manage-Email-Service-Integration-in-Windows-Server-Essentials.md)

-   [Windows Server Essentials の管理](Manage-Windows-Server-Essentials.md)
