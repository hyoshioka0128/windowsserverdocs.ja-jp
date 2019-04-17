---
title: "Windows Server Essentials での内部設置型 Exchange サーバーを統合します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b56a21e2-c9e3-4ba9-97d9-719ea6a0854b
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: c2020e08b94800a9750f095a2f772afb14ba5f0b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="integrate-an-on-premises-exchange-server-with-windows-server-essentials"></a>Windows Server Essentials での内部設置型 Exchange サーバーを統合します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

このガイドでは、情報と設定および Windows Server Essentials を実行しているサーバーと Exchange Server を実行している社内サーバーを統合するための基本的な指示を提供します。  
  
 Windows Server Essentials ネットワークで Exchange Server を実行している社内サーバーを展開する前に、このガイドを読む必要があります。  
  
> [!NOTE]
>  Exchange Server 2010 では、Windows Server 2012 を実行しているコンピューターにインストールはサポートされません。  
  
## <a name="prerequisites"></a>前提条件  
 Windows Server Essentials ネットワークで Exchange Server をインストールする前に、このセクションで説明するタスクを完了することを確認します。  
  
-   [Windows Server Essentials を実行しているサーバーのセットアップします。](Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md#BKMK_SetUpSBS8)  
  
-   [Exchange Server をインストールするに 2 番目のサーバーを準備します。](Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md#BKMK_SecondServer)  
  
-   [インターネット ドメイン名を構成します。](Integrate-an-On-Premises-Exchange-Server-with-Windows-Server-Essentials.md#BKMK_DomainNames)  
  
###  <a name="BKMK_SetUpSBS8"></a>Windows Server Essentials を実行しているサーバーのセットアップします。  
 必要がありますが既にセットアップする Windows Server Essentials を実行しているサーバー。 Exchange Server を実行しているサーバーのドメイン コントローラーになります。 Windows Server Essentials を設定する方法については、次を参照してください。[Windows Server Essentials のインストール](../install/Install-Windows-Server-Essentials.md)します。  
  
###  <a name="BKMK_SecondServer"></a>Exchange Server をインストールするに 2 番目のサーバーを準備します。  
 実行中の Exchange Server 2010 を公式にサポートしている Windows Server オペレーティング システムのバージョンを実行している 2 番目のサーバーまたは Exchange Server 2013 では、Exchange Server をインストールする必要があります。 Windows Server Essentials ドメインに 2 番目のサーバーを参加する必要があります。  
  
 2 番目のサーバーを Windows Server Essentials ドメインに参加させる方法については、次を参照してください。2 番目のサーバーをネットワークに参加[接続](../use/Get-Connected-in-Windows-Server-Essentials.md)します。  
  
> [!NOTE]
>  Microsoft では、Windows Server Essentials を実行しているサーバーに Exchange Server をインストールすることはできません。  
  
###  <a name="BKMK_DomainNames"></a>インターネット ドメイン名を構成します。  
 Windows Server Essentials と Exchange Server を実行している社内サーバーを統合する必要があります登録したお客様のビジネスの有効なインターネット ドメイン名 (よう*contoso.com*)。 また、Exchange Server を必要とする DNS リソース レコードを作成する、ドメイン ネーム プロバイダーと連携する必要があります。  
  
 たとえば、会社インターネット ドメイン名が contoso.com との完全修飾ドメイン名 (FQDN) を使用する場合*mail.contoso.com*、Exchange Server を実行している社内サーバーを参照する、ドメイン ネーム プロバイダーと連携を次の表に、DNS リソース レコードを作成します。  
  
|リソース レコード名|レコードの種類|レコードの設定|説明|  
|--------------------------|-----------------|--------------------|-----------------|  
|メール|ホスト (A)|アドレス =*ISP によって割り当てられたパブリック IP アドレス*|Exchange Server mail.contoso.com 当てのメールが表示されます。<br /><br /> 独自の選択では、別の名前を使用できます。|  
|MX|メール エクスチェン ジャー (MX)|ホスト名 = @<br /><br /> アドレス mail.contoso.com =<br /><br /> 基本設定 = 0|電子メール メッセージ ルーティングを提供email@contoso.com内部設置型 Exchange Server を実行しているサーバーに到達します。|  
|SPF|テキスト (TXT)|v、mx spf1 を = ~ すべて|リソース レコードがスパムとして識別される、サーバーから送信された電子メールを防止します。|  
|autodiscover._tcp|サービス (SRV)|サービス: _autodiscover<br /><br /> プロトコル: _tcp<br /><br /> 優先順位: 0<br /><br /> 重み付け: 0<br /><br /> ポート: 443<br /><br /> ターゲット ホスト: mail.contoso.com|Microsoft Office Outlook およびモバイル デバイス、Exchange Server を実行している社内サーバーを自動的に検出を有効にします。<br /><br /> **注:**も、自動検出ホスト (A) リソース レコードを構成して、公開サーバーの IP アドレス、内部設置型 Exchange Server を実行しているレコードを指すことができます。 ただし場合は、このオプションを実装する必要がありますも用意する mail.contoso.com と autodiscover.contoso.com ドメイン名の両方をサポートするサブジェクト代替名 (SAN) SSL 証明書。|  
  
> [!NOTE]
>  -   インスタンスを置き換える*contoso.com*を登録したインターネット ドメイン名では、この例では。  
  
 Windows Server Essentials を実行しているサーバーを使用している FQDN と Exchange Server を実行している社内サーバーの異なる FQDN を選択する必要があります。 たとえば、ことができますを使用する*remote.contoso.com*コンピューターがインターネットから Windows Server Essentials を実行しているサーバーへのアクセスに使用する FQDN として。 使用することができます*mail.contoso.com*内部設置型 Exchange Server を実行しているサーバーに電子メールをルーティングするために使用する FQDN として。  
  
## <a name="install-exchange-server"></a>Exchange Server をインストールします。  
 Windows Server Essentials の Exchange Server 統合機能には、次のバージョンの Exchange Server がサポートしています。  
  
-   Exchange Server 2013  
  
-   Exchange Server 2010 Service Pack 1 (SP1)  
  
 現在の管理者アカウントを追加する 2 つ目のサーバーに Exchange Server をインストールする前にまず必要があります、**Enterprise Admins**グループ。  
  
#### <a name="to-add-the-current-administrator-account-to-the-enterprise-admins-group"></a>現在の管理者アカウントを Enterprise Admins グループに追加するには  
  
1.  Windows Server Essentials に管理者としてログオンします。  
  
2.  Windows PowerShell を管理者として実行します。  
  
3.  Windows PowerShell のコマンド プロンプトで次のように入力します。**Add-adgroupmember ˜Enterprise Admins $env:path: username**、し、Enter キーを押します。  
  
#### <a name="to-install-exchange-server"></a>Exchange Server をインストールするには  
  
1.  2 番目のサーバーに管理者としてログオンします。  
  
2.  インターネット ブラウザーを開きに移動し、[Exchange Server 展開アシスタント](https://go.microsoft.com/fwlink/p/?LinkID=249163)Web サイト。  
  
3.  をクリックして**On-premises Only**します。  
  
4.  インストールする Exchange Server のバージョン用の新しいインストール オプションをクリックします。  
  
    > [!NOTE]
    >  Windows Small Business Server のインストールから移行する場合は、移行手順をカバーする適切なアップグレード オプションを選択する必要があります。  
  
5.  次のページで、既定の設定をそのまま使用し、をクリックして**次**します。  
  
    > [!NOTE]
    >  Exchange Server の新しいインストールでパブリック フォルダーを使用する場合は、設定を変更する**はい**します。  
  
6.  Exchange サーバーを展開するチェックリストの手順に従います。  
  
     Exchange Server 展開アシスタントすることもできます。  
  
    -   チェックリストのコピーを印刷します。  
  
    -   チェックリストのコピーを電子メールの受信者に送信します。  
  
    -   チェックリストを PDF ファイルとしてダウンロードします。  
  
> [!NOTE]
>  -   Exchange Server を実行しているサーバー上の管理ツールのインストールを選択する必要があります。 管理ツールは、Windows Server Essentials の Exchange Server 統合機能が必要です。  
> -   設定することをお勧めを仮想ディレクトリを構成する必要がある場合、**InternalUrl**プロパティと同じ URL を**ExternalUrl**各仮想ディレクトリのプロパティ。 詳細については、次を参照してください。[を管理するクライアント アクセス サーバーの仮想ディレクトリ](https://go.microsoft.com/fwlink/p/?LinkId=251058)Exchange Server 2010 オンライン ヘルプ Web サイトにします。  
> -   内での Windows Server Essentials でリモート Web アクセス サイトから Outlook Web Access (OWA) にアクセスする場合は、OWA の外部 URL プロパティを設定する必要があります。  
  
 Exchange Server 2010 をクリーン セットアップでインストールする場合は、Exchange サーバーを設定する、また、次のスクリプトを使用することができます。  
  
#### <a name="to-use-scripts-to-set-up-exchange-server"></a>Exchange Server をセットアップするスクリプトを使用するには  
  
1.  メモ帳を開き、新しいファイルに次のスクリプトを貼り付けます。  
  
     `Import-Module ServerManager`  
  
     `Add-WindowsFeature NET-Framework,RSAT-ADDS,Web-Server,Web-Basic-Auth,Web-Windows-Auth,Web-Metabase,Web-Net-Ext,Web-Lgcy-Mgmt-Console,WAS-Process-Model,RSAT-Web-Server,Web-ISAPI-Ext,Web-Digest-Auth,Web-Dyn-Compression,NET-HTTP-Activation,Web-Asp-Net,Web-Client-Auth,Web-Dir-Browsing,Web-Http-Errors,Web-Http-Logging,Web-Http-Redirect,Web-Http-Tracing,Web-ISAPI-Filter,Web-Request-Monitor,Web-Static-Content,Web-WMI,RPC-Over-HTTP-Proxy  �Restart`  
  
2.  ファイルとして保存**InstallDependencies.ps1**します。  
  
3.  サーバー上の場所に Exchange SSL 証明書をコピーします。  
  
4.  新しいメモ帳ファイルを開き、ファイルに次のテキストをコピーします。  
  
     `param (`  
  
     `[string]`  
  
     `[Parameter(Mandatory=$true, HelpMessage = "The path to your Certificate file, must be a *.pfx format")]`  
  
     `$CertPath = "c:\certificates\ExchangeCertificate.pfx",`  
  
     `[Security.SecureString]`  
  
     `[Parameter(Mandatory=$true, HelpMessage = "The password of your cert")]`  
  
     `$CertPassword = $null,`  
  
     `[string]`  
  
     `[Parameter(Mandatory=$true, HelpMessage = "Domain Name, eg. contoso.com")]`  
  
     `$DomainName = "contoso.com",`  
  
     `[string]`  
  
     `[Parameter(Mandatory=$true, HelpMessage = "Server IP Address, eg. 192.168.0.1")]`  
  
     `$ServerIpAddress = "192.168.0.1",`  
  
     `[string]`  
  
     `[Parameter(Mandatory=$true, HelpMessage = "Internal Ip Range, eg. 192.168.0.0-192.168.0.255")]`  
  
     `$InternalIpRange = "192.168.0.0-192.168.0.255"`  
  
     `)`  
  
     `#Import Exchange Certificate, and Enable it for POP IIS IMAP SMTP services.`  
  
     `Import-ExchangeCertificate  �FileData ([Byte[]]$(Get-content -Path $CertPath  �Encoding byte  �ReadCount 0)) -Password:$CertPassword -Force | Enable-ExchangeCertificate -Services 'POP, IIS, IMAP, SMTP' -Force`  
  
     `#New AcceptedDomain and set it to default`  
  
     `New-AcceptedDomain  �Name "official name"  �DomainName $domainname`  
  
     `Set-AcceptedDomain  �Identity "official name"  �MakeDefault $true`  
  
     `#New EmailAddress Policy`  
  
     `$address = "%m@" + $DomainName`  
  
     `New-EmailAddressPolicy -Name "Windows Server Essentials Email Address Policy" -IncludedRecipients AllRecipients -EnabledPrimarySMTPAddressTemplate $address`  
  
     `#Set owa and ecp VirtualDirectory ExternalUrl`  
  
     `$hostname = "mail." + $DomainName`  
  
     `$owa = "https://" + $hostname + "/owa"`  
  
     `$ecp = "https://" + $hostname + "/ecp"`  
  
     `$activesync = "https://" + $hostname + "/Microsoft-Server-ActiveSync"`  
  
     `$oab = "https://" + $hostname + "/OAB"`  
  
     `$ews = "https://" + $hostname + "/EWS/Exchange.asmx"`  
  
     `Get-OwaVirtualDirectory | Set-OwaVirtualDirectory  �ExternalUrl $owa  �InternalUrl $owa`  
  
     `Get-EcpVirtualDirectory | Set-EcpVirtualDirectory  �ExternalUrl $ecp  �InternalUrl $ecp`  
  
     `Get-ActiveSyncVirtualDirectory | Set-ActiveSyncVirtualDirectory -ExternalUrl $activesync  �InternalUrl $activesync`  
  
     `Get-OABVirtualDirectory | Set-OABVirtualDirectory -ExternalUrl $oab -InternalUrl $oab -RequireSSL:$true`  
  
     `Get-WebServicesVirtualDirectory | Set-WebServicesVirtualDirectory -ExternalUrl $ews -InternalUrl $ews -BasicAuthentication:$True -Force`  
  
     `#Enable outlook Anywhere`  
  
     `Enable-OutlookAnywhere  �ClientAuthenticationMethod:Basic  �ExternalHostname:$hostname  �SSLOffloading:$false`  
  
     `#new receive/send connector`  
  
     `$machinename = get-content env:computername`  
  
     `$bindingIpaddress = $ServerIpAddress + ":25"`  
  
     `$RecevieConnectorName = $machinename + "\Default " + $machinename`  
  
     `Set-ReceiveConnector $RecevieConnectorName -RemoteIPRanges $InternalIpRange`  
  
     `New-ReceiveConnector -Name "WSE Internet Receive Connector" -Usage "Internet" -Bindings $bindingIpaddress -Fqdn $hostname -Enabled $true -Server $machinename -AuthMechanism Tls,BasicAuth,BasicAuthRequireTLS,Integrated`  
  
     `New-SendConnector -Name "WSE Internet SendConnector" -Usage "Internet" -AddressSpaces 'SMTP:*;1' -IsScopedConnector $false -DNSRoutingEnabled $true -UseExternalDNSServersEnabled $true -SourceTransportServers $machinename`  
  
5.  ネットワーク環境を反映するように、スクリプトの先頭にパラメーターを設定します。  
  
6.  ファイルとして保存**ConfigureExchange.ps1**します。  
  
7.  Windows PowerShell を管理者として実行します。  
  
8.  Windows PowerShell のコマンド プロンプトで次のように入力します。**Set-executionpolicy RemoteSigned**、し、Enter キーを押します。  
  
9. スクリプトを実行して**InstallDependencies.ps1**します。  
  
10. 管理者としてサーバー、および、Windows PowerShell の実行を再起動します。  
  
11. Windows PowerShell のコマンド プロンプトで次のスクリプトを実行します。  
  
     `E:\setup.com /mode:install /roles:mb,ht,ca /OrganizationName:"First Organization"`  
  
    > [!NOTE]
    >  必ず、Exchange Server セットアップ プログラムへの正しいパスを入力してください。  
  
12. Exchange Server のセットアップが完了したら、管理者として Exchange 管理シェルを開きます。  
  
13. Exchange 管理シェルのコマンド プロンプトで次のように入力します。**Set-executionpolicy RemoteSigned**、し、Enter キーを押します。  
  
14. スクリプトを実行して**ConfigureExchange.ps1**します。  
  
15. サーバーを再起動します。  
  
> [!NOTE]
>  自己発行の証明書ではなく、一般に信頼される SSL 証明書を使用する場合は、証明書の要求を作成し、選択した証明機関に送信するには、セットアップ ガイドの指示に従うことができます。 証明書要求を作成するのに、Exchange の PowerShell コマンドレットを使用することもできます。 次に例をします。  
>   
>  `New-ExchangeCertificate -GenerateRequest -SubjectName "C=US, S=Washington, L=Redmond, O=contoso, OU=contoso, CN=mail.contoso.com" -DomainName mail.contoso.com -PrivateKeyExportable $true | Set-Content -path "c:\Docs\MyCertRequest.req"`  
>   
>  ネットワーク環境を反映するようにスクリプトのパラメータをカスタマイズします。  
  
## <a name="post-installation-tasks"></a>Post-installation 後のタスク  
 このセクションでは、Windows Server Essentials ネットワークで Exchange Server を実行している社内サーバーのセットアップに固有の情報を含むインストール後の段階で完了する必要があります、サーバー構成タスクについて説明します。  
  
### <a name="add-the-public-email-domain-and-configure-the-email-address-policies"></a>パブリック電子メール ドメインを追加し、電子メール アドレス ポリシーを構成します。  
  
> [!NOTE]
>  これは、クリーン セットアップを実行している場合に必要なタスクです。 Windows Small Business Server から移行する場合は、この手順をスキップします。  
  
 電子メール ドメインを既定の承認済みのドメインを指定し、電子メール アドレス ポリシーを構成する必要があります。  
  
##### <a name="to-add-your-email-domain-as-the-default-accepted-domain"></a>承認済みドメインの既定値として、電子メール ドメインを追加するには  
  
1.  Exchange Server の記事の指示に従って[承認済みドメインを作成する](https://go.microsoft.com/fwlink/p/?LinkId=249174)を承認済みドメインを追加します。  
  
2.  管理者として 2 番目のサーバーにログオン、Exchange を開き、管理コンソールおよびに移動し、**ハブ トランスポート**のタブ、**組織の構成**します。  
  
3.  Exchange 管理コンソール作業ウィンドウで、新しい承認済みドメインを右クリックし、をクリックして**既定として設定**します。  
  
4.  Exchange Server の記事の指示に従って[電子メール アドレス ポリシーを作成する](https://go.microsoft.com/fwlink/p/?LinkId=249179)新しい電子メール アドレス ポリシーを作成します。 すべての電子メール アドレス以外の既定値を受け付けることができます。 電子メール アドレス、パブリック電子メール ドメインを指定します。  
  
### <a name="create-smtp-send-and-receive-connectors"></a>作成 SMTP 送信および受信コネクタ  
  
> [!NOTE]
>  これは、必要なタスクです。  
  
 SMTP 送信コネクタとメール メッセージの発信/着信伝送の SMTP 受信コネクタを構成する必要があります。  
  
 SMTP 送信コネクタを作成するには、Exchange Server の記事の指示に従います[SMTP 送信コネクタを作成する](https://technet.microsoft.com/library/aa997285.aspx)します。  
  
 SMTP 受信コネクタを作成するには、Exchange Server の記事の指示に従います[SMTP 受信コネクタを作成する](https://technet.microsoft.com/library/bb125159.aspx)します。  
  
 オプションとして、送信を作成するためには、このドキュメントで既にスクリプトを参照し、Exchange の PowerShell コマンドレットを使用して受信コネクタできます。  
  
### <a name="configure-the-network-router"></a>ネットワーク ルーターを構成します。  
  
> [!NOTE]
>  これは、クリーン セットアップを実行している場合に必要なタスクです。 Windows Small Business Server から移行する場合は、次を参照してください。[Windows Server Essentials へのサーバー データの移行](../migrate/Migrate-Server-Data-to-Windows-Server-Essentials.md)手順については、ネットワークを構成する方法。  
  
 少なくとも、ルーター上で、次のポート設定を構成する必要があります。  
  
|ルーター ポート|宛先 IP|宛先ポート|注:|  
|-----------------|--------------------|----------------------|----------|  
|25 (SMTP)|Exchange Server を実行している社内サーバーの内部 IP。|25||  
|80 (HTTP)|Windows Server Essentials を実行しているサーバーの内部 IP|80||  
|443 (HTTPS)|Windows Server Essentials を実行しているサーバーの内部 IP|443||  
  
 POP3 または IMAP メッセージング、ネットワーク上のプロトコルをサポートする場合は、またこれらのプロトコルに対するポート フォワーディングを構成する必要があります。 For-related については、セクションを参照して**クライアント アクセス サーバー**」トピックの「[Exchange ネットワーク ポートのリファレンス](https://go.microsoft.com/fwlink/p/?LinkId=250773)、Exchange Server TechNet ライブラリでします。  
  
> [!NOTE]
>  -   2 番目のサーバーの Exchange Server を実行しているし、Windows Server Essentials を実行しているサーバーの静的 IP アドレスを構成することをお勧めします。 Windows Server 2003 または Windows Server 2008 R2 を実行するコンピューターで静的 IP アドレスを構成する方法に関する手順については、次を参照してください[静的 IP アドレスを構成](https://technet.microsoft.com/library/cc754203\(v=ws.10\).aspx)、Windows Server TechNet ライブラリ。  
>   
>      **注:** DNS サーバーの設定は、常に Windows Server Essentials を実行しているサーバーの IP アドレスを指す必要があります。  
> -   ルーターで、Windows Server Essentials を実行しているサーバーと Exchange Server を実行しているサーバーの IP アドレスが予約されている、または DHCP IP アドレス範囲から外れているを確認します。  
> -   このセクションで、ルーター構成は、インターネット サービス プロバイダー (ISP) によって割り当てられている 1 つだけのパブリック IP アドレスであると想定します。 複数のパブリック IP アドレスがあれば、Windows Server Essentials を実行しているサーバーと Exchange Server を実行しているサーバーに、別の IP アドレスを割り当てるし、パブリック IP アドレスに基づくポート フォワーディングを作成できます。  
  
### <a name="enable-on-premises-exchange-server-integration-on-windows-server-essentials"></a>Windows Server Essentials での内部設置型 Exchange Server 統合を有効にします。  
  
> [!NOTE]
>  Windows Small Business Server インストールから移行する場合は、現時点では、この手順をスキップして、移行元サーバーで、Exchange Server の以前のインストールをアンインストールした後に実行することをお勧めします。  
  
 インストールして、Exchange Server を実行しているサーバーを構成した後は、Windows Server Essentials を実行しているサーバー上の内部設置型 Exchange Server 統合を有効にする必要があります。  
  
##### <a name="to-enable-on-premises-exchange-server-integration-from-the-dashboard"></a>ダッシュ ボードから社内 Exchange Server 統合を有効にするには  
  
1.  管理者は、Windows Server Essentials を実行しているサーバーにログオンし、ダッシュ ボードを開きます。  
  
2.  **ホーム**] ページで [ **[電子メール サービスへの接続**、] をクリックし、**、Exchange Server 統合**します。  
  
3.  [情報] ペインで、をクリックして**Exchange Server 統合をセットアップ**します。  
  
4.  ウィザードの指示に従います。  
  
### <a name="configure-a-reverse-proxy"></a>リバース プロキシを構成します。  
  
> [!NOTE]
>  これは、インターネット サービス プロバイダーから 1 つだけのインターネット接続がある場合に必要なタスクです。  
  
 Windows Server Essentials と Exchange Server の両方のネットワーク ユーザーをいくつかのリモート アクセス シナリオをサポートします。 たとえば、Windows Server Essentials を実行しているサーバーで Anywhere Access にした場合リモートでリモート Web アクセス サイトにアクセスまたはできます仮想プライベート ネットワーク (VPN) を使用して、Windows Server Essentials ネットワークにリモート接続を。 電子メール メッセージにリモートでアクセスするには、Outlook Anywhere、Outlook Web Access (OWA)、または ActiveSync を使用する必要があります。  
  
 Windows Server Essentials と Exchange Server を実行しているサーバーは両方が同じルーターに接続されているし、1 つだけへの着信インターネット接続、インターネット サービス プロバイダーからルーターがある場合は、宛先のホスト名に基づいて、インターネットから送信される各種のリモート アクセス要求をルーティングする、リバース プロキシ ソリューションを使用する必要があります。 Microsoft を使用することをお勧めリバース プロキシ ソリューションとして IIS アプリケーション要求ルーティング処理 (ARR) 拡張機能をサポートします。 IIS アプリケーション要求ルーティング処理の詳細については、次を参照してください。、[Web サイトのアプリケーション要求ルーティング処理](https://go.microsoft.com/fwlink/p/?LinkId=249181)します。  
  
##### <a name="to-install-and-configure-application-request-routing"></a>インストールして、アプリケーション要求ルーティング処理を構成するには  
  
1.  Windows Server Essentials に管理者としてログオンします。  
  
2.  インターネット ブラウザーを開きに移動、[Web サイトのアプリケーション要求ルーティング処理](https://go.microsoft.com/fwlink/p/?LinkId=249181)します。  
  
3.  ARR Web サイト] をクリックして**インストール**、ARR をインストールし、指示と  
  
    > [!NOTE]
    >  ARR のインストール中に、URL Rewrite Module を選択する必要があります。  
    >   
    >  ARR 2.5 用の KB 2589179 が正常にインストールしていない ARR のインストールの最後にエラーが表示される可能性があります。 このエラーは無視できます。  
  
4.  ARR のインストールが完了したら、再起動、**リモート デスクトップ ゲートウェイ**サービスが実行されていない場合。  
  
    > [!NOTE]
    >  ARR をインストールした後、**リモート デスクトップ ゲートウェイ**サービスを停止する可能性があります。 サービスを手動で再起動するを開き、**サービス**管理ツールと再起動、**リモート デスクトップ ゲートウェイ**サービス。  
  
5.  [ARR 2.5 用の KB2732764 をダウンロード](https://go.microsoft.com/fwlink/?LinkID=258302)、および Windows Server Essentials を実行しているサーバーで、更新プログラムをインストールします。  
  
6.  Windows Server Essentials を実行しているサーバーに Exchange Server の SSL 証明書ファイルをコピーします。 証明書ファイルは、秘密キーを含める必要があります、PFX ファイル形式である必要があります。  
  
    > [!NOTE]
    >  自己発行の証明書を使用している場合、Exchange Server の記事の指示に従って、[Exchange 証明書のエクスポート](https://technet.microsoft.com/library/dd351274.aspx)証明書をエクスポートします。  
  
7.  Windows Server Essentials のバージョンを実行しているに応じて、次のいずれかの操作を行います。  
  
    -   Windows Server essentials: を管理者としてコマンド ウィンドウを開き、%ProgramFiles%\Windows server \bin ディレクトリを開きます  
  
    -   Windows Server essentials: 管理者としてコマンド ウィンドウを開き、%Windir%\System32\Essentials ディレクトリを開きます。  
  
8.  インストール シナリオに応じて、次のいずれかの手順に従って ARR を構成します。  
  
    -   クリーン セットアップを実行する場合は、次のコマンドを実行します。  
  
         * * ARRConfig config cert * **証明書ファイルのパスを** * hostnames * * *Exchange Server のホスト名* ****  
  
        > [!NOTE]
        >  たとえば、* * ARRConfig config cert ***c:\temp\certificate.pfx*** hostnames * * * mail.contoso.com。  
        >   
        >  置換*mail.contoso.com*、証明書によって保護されているドメインの名前にします。  
  
    -   次のコマンドを実行する Windows Small Business Server から移行します。  
  
         * * ARRConfig config cert * **証明書ファイルのパスを** * hostnames * * *Exchange Server のホスト名** * targetserver * * *Exchange Server のサーバー名* ****  
  
         たとえば、* * ARRConfig config cert ***c:\temp\certificate.pfx*** hostnames ***mail.contoso.com*** targetserver * * * ExchangeSvr * * *  
  
         置換*mail.contoso.com*、ドメインの名前にします。 置換*ExchangeSvr*と Exchange Server を実行しているサーバーの名前。  
  
9. メッセージが表示されたら、証明書のパスワードを入力します。  
  
> [!NOTE]
>  -   提供するホスト名は、Exchange Server 用に購入した SSL 証明書に含まれている必要があります。  
> -   複数のホスト名があれば、それらを個別にコンマ (,) を使用します。  
  
 構成が動作することを確認するには、(https://mail の Exchange Server を実行しているサーバーの OWA Web サイトにアクセスしてください。。 *yourdomainname*.com/owa) ドメインのメンバーではないコンピューターからです。 接続の問題のトラブルシューティングにも使用できます、オンライン[Microsoft リモート接続アナライザー](https://go.microsoft.com/fwlink/p/?LinkId=249455)ツールです。  
  
### <a name="configure-split-dns-for-exchange-server"></a>構成の Exchange サーバー用に分割 DNS  
  
> [!NOTE]
>  これは、推奨されるタスクです。  
  
 分割 DNS を使用すると、DNS 要求が作成元によって、同じホスト名に対して DNS で異なる IP アドレスを構成できます。 クライアント コンピューターがイントラネット上にある場合は、DNS 要求はイントラネット IP アドレスに解決します。 クライアント コンピューターがインターネット上にある場合は、DNS 要求はインターネット IP アドレスに解決します。 これは、ユーザーに透過的です。  
  
 分割を構成することをお勧めの場所にかかわらず、ユーザーに常に同じホスト名を使用して Exchange サーバーにアクセスできるように DNS のサービスします。  
  
##### <a name="to-configure-split-dns-for-exchange-server"></a>Exchange Server の分割 DNS を構成するには  
  
1.  管理者は、Windows Server Essentials にログオンし、DNS マネージャーを開きます。  
  
2.  DNS マネージャー コンソール ツリーで、[サーバーを右クリックし] をクリックして**新しいゾーン**します。 **新しいゾーン ウィザード**が表示されます。  
  
3.  **ゾーンの種類**ページ、ウィザードの既定のオプションをそのまま使用し、をクリックして**次**します。  
  
4.  **Active Directory ゾーン レプリケーション スコープ**] ページで、既定のオプションをそのまま使用して、をクリックして**次**します。  
  
5.  **前方または逆引き参照ゾーン**ページをそのまま使用するか選択**前方参照ゾーン**、] をクリックし、**[次へ]**します。  
  
6.  **ゾーン名**] ページで、(たとえば、Exchange Server を実行しているサーバーの FQDN を入力します。*mail.contoso.com*)、] をクリックし、**次**します。  
  
7.  **動的更新**] ページで、既定のオプションを受け入れ、[ **[次へ]**、] をクリックし、**完了**します。  
  
8.  クリックして、新しい前方参照ゾーンを右クリックし、DNS マネージャー コンソール ツリーで、**新しいホスト (A または AAAA)**します。  
  
9. **新しいホスト**] ページで、そのまま使用、**名**フィールドは空白、Exchange Server を実行しているサーバーのイントラネット IP アドレスを入力し、クリックして**ホストの追加**します。  
  
    > [!NOTE]
    >  そのまま使用するときに、**名**フィールドは空白で、サーバーは既定で、親ドメイン名を使用します。  
  
10. **新しいホスト**] ページで [**完了**します。  
  
> [!NOTE]
>  ActiveSync を使用して、一部のメールボックス アカウントの電子メールを同期できない場合は、それらのアカウント ドメイン管理者などの 1 つまたは複数の保護グループのメンバーであるかどうかを決定します。 For-related に役立つ情報を参照してください、この問題を解決する[Exchange ActiveSync が HTTP 500 エラーが返される](https://technet.microsoft.com/library/dd439375\(EXCHG.80\).aspx)します。  
  
## <a name="related-topics"></a>関連するトピック  
 内部設置型 Exchange サーバーを統合する方法の詳細については、次のセクションを参照してください。  
  
### <a name="what-happens-if-i-disable-exchange-integration"></a>Exchange との統合を無効にするとどうなりますか。  
 内部設置型 Exchange サーバーとの統合を無効にした場合は、表示、作成、または Exchange Server メールボックスの管理に Windows Server Essentials ダッシュ ボードを使用することはできなくなります。  
  
### <a name="what-do-i-need-to-know-about-email-accounts"></a>メール アカウントについて知っておくには何が必要ですか。  
 ホスト型電子メール ソリューションは、サーバー上で構成されます。 Microsoft Office 365 などのホスト型電子メール プロバイダーのソリューションは、ネットワーク ユーザーに対する個別の電子メール アカウントを提供できます。 ユーザー アカウントを作成する Windows Server Essentials での追加、ユーザー アカウントのウィザードを実行すると、ウィザードは、利用可能なホスト型電子メール ソリューションにユーザー アカウントを追加しようとします。 同時に、ウィザードは、ユーザーに電子メール名 (エイリアス) を割り当て、(クォータ)、メールボックスの最大サイズを設定します。 メールボックスの最大サイズは、使用する電子メール プロバイダーによって異なります。 ユーザー アカウントを追加した後は、ユーザーのプロパティ ページからメールボックス エイリアスとクォータ情報を管理を続行することができます。 ユーザー アカウントとホスト型電子メール プロバイダーの完全な管理をホスト型プロバイダーの管理コンソールを使用します。 プロバイダーによって、管理コンソールを Web ベースのポータルまたはサーバー ダッシュ ボードのタブからアクセスできます。  
  
 ユーザー アカウントのウィザードの追加を実行するときに提供するエイリアスは、ユーザー エイリアスに推奨される名前としてホスト型電子メール プロバイダーに送信されます。 たとえば、ユーザー エイリアスが*FrankM*、ユーザーの電子メール アドレスがあります*FrankM@Contoso.com*します。  
  
 さらに、追加のユーザー アカウントのウィザードでユーザーに設定されているパスワードは、ホスト型電子メール ソリューション内のユーザーの最初のパスワードになります。  
  
 最後に、サーバーで、削除、ユーザー アカウントのウィザードを使用してユーザーを削除する場合、ウィザードも要求を送信も、システムからユーザーを削除するホスト型電子メール プロバイダー。 プロバイダーは、ユーザー アカウントと、アカウントに関連付けられている電子メールの両方を削除できます。  
  
 メール アカウントにアクセスする方法や、必要な電子メール クライアント ソフトウェアをセットアップする方法については、ユーザーの情報は、ホスト型電子メール プロバイダーによって提供されるヘルプ ドキュメントを参照してください。  
  
### <a name="what-is-a-mailbox-quota"></a>メールボックス クォータとは何ですか。  
 ネットワーク ユーザーの Exchange メールボックス データに割り当てられている記憶域の容量は、メールボックス クォータと呼ばれます。  
  
 実行すると、**Exchange Server 統合をセットアップ**ウィザード、ダッシュ ボード上でタスクを追加するユーザー アカウントのウィザード メールボックス クォータを適用して、クォータ サイズを指定するかどうかを選択することができますページを追加します。 既定で、**メールボックス クォータの強制適用**(オン)、オプションを選択し、ユーザーのメールボックスに 2 GB の記憶域領域が割り当てられます。 Exchange 管理者は、ビジネスのニーズに合わせてメールボックス クォータの設定をカスタマイズできます。  
  
## <a name="see-also"></a>参照してください。  
  
-   [Windows Server Essentials のシステム要件](../get-started/system-requirements.md)  
  
-   [電子メール統合を管理します。](Manage-Email-Service-Integration-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials を管理します。](Manage-Windows-Server-Essentials.md)
