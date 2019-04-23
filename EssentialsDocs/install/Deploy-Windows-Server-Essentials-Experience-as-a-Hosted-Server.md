---
title: Windows Server Essentials Experience をホストされたサーバーとして配置
description: Windows Server Essentials を使用する方法について説明します
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a455c6b4-b29f-4f76-8c6b-1578b6537717
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: b44b395a39a53194b73a0d503c2310edcbe53a2c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59876073"
---
# <a name="deploy-windows-server-essentials-experience-as-a-hosted-server"></a>Windows Server Essentials Experience をホストされたサーバーとして配置

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

このドキュメントに、ラボにインストールされている (呼ばれる Windows Server Essentials のドキュメントの残りの部分で) Windows Server Essentials エクスペリエンス役割を持つ Microsoft Windows Server 16 を展開しホストに固有の情報が含まれていて、顧客へのサービスとして Windows Server Essentials エクスペリエンスを提供する予定です。 このドキュメントには、次のセクションが含まれます。  
  

-   [Windows Server Essentials エクスペリエンスの概要](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_WSEEOverview)  
  
-   [Windows Server Essentials エクスペリエンスをホストする利点](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Benefits)  
  
-   [サポートされている展開オプション](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedDeployment)  
  
-   [サポートされているネットワーク トポロジ](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedToplogy)  
  
-   [Windows Server Essentials エクスペリエンス役割のイメージをカスタマイズします。](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_CustomizeImage)  
  
-   [Windows Server Essentials エクスペリエンスの展開を自動化します。](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_AutomateDeployment)  
  
-   [Windows Small Business Server からデータを Windows Server Essentials エクスペリエンスに移行します。](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Migrate)  
  
-   [Windows PowerShell を使用して一般的なタスクを実行します。](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_PowerShell)  
  
-   [Windows Server Essentials と電子メールの統合](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_EmailIntegration)  
  
-   [ネイティブ ツールを使用した監視し、管理](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Monitoring)  
  
-   [テストのシナリオ](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Scenarios)  
  
-   [サポート情報](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Support)  

-   [Windows Server Essentials エクスペリエンスの概要](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_WSEEOverview)  
  
-   [Windows Server Essentials エクスペリエンスをホストする利点](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Benefits)  
  
-   [サポートされている展開オプション](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedDeployment)  
  
-   [サポートされているネットワーク トポロジ](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedToplogy)  
  
-   [Windows Server Essentials エクスペリエンス役割のイメージをカスタマイズします。](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_CustomizeImage)  
  
-   [Windows Server Essentials エクスペリエンスの展開を自動化します。](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_AutomateDeployment)  
  
-   [Windows Small Business Server からデータを Windows Server Essentials エクスペリエンスに移行します。](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Migrate)  
  
-   [Windows PowerShell を使用して一般的なタスクを実行します。](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_PowerShell)  
  
-   [Windows Server Essentials と電子メールの統合](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_EmailIntegration)  
  
-   [ネイティブ ツールを使用した監視し、管理](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Monitoring)  
  
-   [テストのシナリオ](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Scenarios)  
  
-   [サポート情報](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Support)  

  
##  <a name="BKMK_WSEEOverview"></a> Windows Server Essentials エクスペリエンスの概要  
 Windows Server Essentials エクスペリエンスは、Windows Server 2012 R2 Standard および Windows Server 2012 R2 Datacenter で使用できるサーバー役割です。 Windows Server 2012 R2 を実行しているサーバーを Windows Server Essentials エクスペリエンス役割をインストールしているお客様は、ロックや制限なく Windows Server Essentials で使用可能なすべての機能を利用できます。 Windows Server Essentials エクスペリエンスには、小規模および中規模企業向けの次のクロスプレミス ソリューションが有効にします。  
  
-   **データ ストレージと保護**顧客を保存することができます"が、1 か所にデータ サーバーとクライアントのデータを保護するには、サーバーおよびネットワーク内のクライアント コンピューター (75 台未満) をバックアップするとします。  
  
-   **ユーザー管理** : 簡素化されたサーバー ダッシュボードを使用して、ユーザーとグループを管理することができます。 さらに、Microsoft Azure Active Directory (Azure AD) との統合は、ドメイン資格情報を使用してユーザーの (たとえば、Office 365、Exchange Online、および SharePoint Online) は、Microsoft online services のデータに簡単アクセスをできます。  
  
-   **サービスの統合**(Office 365、SharePoint Online、および Microsoft Azure Backup) などの Microsoft online services でサーバーを統合することができます。 サーバーは、サード パーティ プロバイダーによって提供されるサービスと統合することもできます。  
  
-   **Anywhere Access**: ユーザーは、事実上インターネット接続のあるどこからでも、ほとんどすべてのデバイスを使用して、サーバー、ネットワーク コンピューター、およびデータにアクセスできます。 リモート Web アクセスにより、簡単なタッチ操作に適したブラウザーを使用して、アプリケーションやデータにアクセスできます。 My Server アプリ、Windows Phone または Microsoft Store アプリからデータにアクセスできます。  
  
-   **メディア ストリーミング**エンド カスタマーが、共有フォルダーに音楽、ビデオ、および写真を格納し、ネットワーク上のコンピューターからこれらのメディア ファイルへのアクセスと Windows Server Essentials エクスペリエンスを有効になっているサーバーにメディア パッケージをインストールする場合、またはリモート Web アクセスします。  
  
-   **正常性の監視**: ネットワーク正常性を監視し、カスタマイズされた正常性レポートを取得することができます。  
  
##  <a name="BKMK_Benefits"></a> Windows Server Essentials エクスペリエンスをホストする利点  
  Windows Server Essentials エクスペリエンスは、既存の展開および管理フレームワークを展開して、Windows Server Essentials エクスペリエンス役割を構成する Windows Server を再利用できるように、Windows server のロールです。 Windows Server Essentials エクスペリエンス役割をホストには、次の利点が提供されます。  
  
-   **展開の合理化**によって単純に、Windows Server Essentials エクスペリエンス役割の有効化、最もよく使用される役割と機能が有効になり、小規模および中規模企業のベスト プラクティスで構成します。 Windows Server Essentials の機能をカスタマイズしたり、または一部のオンプレミスの機能を非表示にしたりすることができます。 Windows Azure Pack を使用する場合は、Windows Server 2012 R2 で Windows Server Essentials エクスペリエンスのギャラリー テンプレートをダウンロードできます。  
  
-   **簡素化されたダッシュボード**: Windows Server Essentials ダッシュボードにより、サーバー フォルダー、サーバー記憶域、バックアップと復元、ユーザーまたはグループ アカウント、デバイス、リモート アクセス、および電子メールの管理などの一般的なタスクが簡単になります。 小規模および中規模企業のお客様は、技術サポートのためにヘルプ デスクを呼び出すことなく、日常の管理タスクを実行できます。  
  
-   **拡張性** : Windows Server Essentials ダッシュボードおよび Windows Server Essentials コネクタ ソフトウェアは拡張可能です。 独自のブランドおよびサービス統合を追加できるため、お客様は、サーバーとサービスに関するすべてのものを 1 つのエントリ ポイントで利用できます。  
  
-   **監視**: Windows Server Essentials を実行している複数のサーバーの監視および管理に、System Center Monitoring Pack の新しいバージョンを使用できます。 管理パックをダウンロードするを参照してください。 [System Center 管理パックの Windows Server Essentials](https://www.microsoft.com/download/details.aspx?id=40809)します。  
  
##  <a name="BKMK_SupportedDeployment"></a> サポートされている展開オプション  
  Windows Server Essentials エクスペリエンスは、新しい Active Directory 環境でドメイン コント ローラーとして展開できます。または、ドメイン メンバーとして既存の Active Directory 環境にデプロイできます。  
  
 Windows Server 2012 R2 Standard または Windows Server 2012 R2 Datacenter では、最初に展開して、Windows Server Essentials エクスペリエンス役割をインストールすることをお勧めします。 この展開方法では、ロックや制限なく、Windows Server Essentials edition のすべての機能を取得できます。  
  

 Windows Server Essentials エクスペリエンス役割を持つ Windows Server 2012 R2 をインストールする方法の詳細については、次を参照してください。[のインストールと Windows Server Essentials の構成](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)します。  


  
##  <a name="BKMK_SupportedToplogy"></a> サポートされているネットワーク トポロジ  
 Windows Server Essentials エクスペリエンスをローミング クライアントから使用するには、VPN を有効にする必要があります。 ローミング クライアントからサーバーへのリモート アクセスを有効にするには、サーバーのポート 443 とポート 80 を開く必要があります。  
  
 ここでは、2 つの代表的なサーバー側のネットワーク トポロジと、VPN およびリモート Web アクセスの構成方法を示します。  
  
-   **トポロジ 1** (これは、優先されるトポロジで、すべてのサーバーと VPN の IP 範囲を同じサブネットに配置します):  
  
    -   ネットワーク アドレス変換 (NAT) デバイスの下で、個別の仮想ネットワークにサーバーをセットアップします。  
  
    -   仮想ネットワークで DHCP サービスを有効にするか、サーバーに静的 IP アドレスを割り当てます。  
  
    -   ルーターのパブリック IP ポート 443 をサーバーのローカル ネットワーク アドレスに転送します。  
  
    -   ポート 443 の VPN パススルーを許可します。  
  
    -   サーバーのアドレスと同じサブネット範囲に、VPN IPv4 アドレス プールを設定します。  
  
    -   2 台目のサーバーに、同じサブネット内だが、VPN アドレス プールの外部の静的 IP アドレスを割り当てます。  
  
-   **トポロジ 2**:  
  
    -   サーバーにプライベート IP アドレスを割り当てます。  
  
    -   サーバーのポート 443 がパブリック ポート 443 IP アドレスに到達することを許可します。  
  
    -   ポート 443 の VPN パススルーを許可します。  
  
    -   VPN IPv4 アドレス プールとサーバーのアドレスに別の範囲を割り当てます。  
  
 トポロジ 2 では、同じドメインに別のサーバーを追加できないため、2 台目のサーバーのシナリオはサポートされません。  
  
 Windows PowerShell スクリプトを使用して、無人展開時に VPN を有効にすることができます。または、初期構成後に、ウィザードで構成できます。  
  
 Windows PowerShell を使用して VPN を有効にするには、Windows Server Essentials を実行しているサーバーで、管理者特権で次のコマンドを実行し、必要なすべての情報を提供します。  
  
```  
##  
## To configure external domain and SSL certificate (if not yet done in unattended Initial Configuration).  
##  
  
$myExternalDomainName = 'remote.contoso.com';   ## corresponds to A or AAAA DNS record(s) that can be resolved on Internet and routed to the server  
$mySslCertificateFile = 'C:\ssl.pfx';   ## full path to SSL certificate file  
$mySslCertificatePassword = ConvertTo-SecureString  œAsPlainText  œForce '******';   ## password for private key of the SSL certificate  
$skipCertificateVerification = $true;   ## whether or not, skip verification for the SSL certificate  
  
Set-WssDomainNameConfiguration  œDomainName $myExternalDomainName  œCertificatePath $mySslCertificateFile  œCertificateFilePassword $mySslCertificatePassword  œNoCertificateVerification  
##  
## To install VPN with static IPv4 pool (and allow all existing users to establish VPN).  
##  
  
Install-WssVpnServer -IPv4AddressRange ('192.168.0.160','192.168.0.240') -ApplyToExistingUsers;  
  
```  
  
> [!NOTE]
>  お客様がサーバーの所有権を得る前に、VPN 接続を提供できない場合は、お客様がリモート デスクトップ プロトコルを使用して、サーバーに接続し、それを構成できるように、インターネット経由でサーバー ポート 3389 に到達できることを確認します。  
  
##  <a name="BKMK_CustomizeImage"></a> Windows Server Essentials エクスペリエンス役割のイメージをカスタマイズします。  
 Windows Server Essentials エクスペリエンス役割を構成する前に、イメージをカスタマイズできます。 標準 Windows Server Sysprep プロセスについては、「 [Windows アセスメント &amp; デプロイメント キット](https://msdn.microsoft.com/library/hh825420.aspx)」を参照してください。 Sysprep を使用してイメージを準備したら、それを使用したり、新しい展開用に Install.wim に再シールしたりすることができます。  
  
 Virtual Machine Manager を使用している場合、実行中のインスタンスを使用してテンプレートを作成できます。 このプロセスでは Sysprep を使用して、インスタンスを準備しますが、それによって、コンピューターがシャットダウンします。 テンプレートをライブラリに保存したら、ケースバイケースでそれを使用できます。  
  
 Windows Server Essentials エクスペリエンス役割をインストールした後は、Windows Server Essentials で機能をカスタマイズできます。 最も重要なカスタマイズの 1 つが **IsHosted** レジストリ キー**HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\Deployment\IsHosted** です。  
  
 このキーが 0x1 に設定されている場合、一部のオンプレミス機能の動作が変更されます。 これらの機能の変更は、次のとおりです。  
  
-   **クライアント バックアップ**: 新しく参加したクライアント コンピューターに対して、クライアント バックアップが既定でオフになります。  
  
-   **クライアント復元サービス**: クライアント復元サービスが無効にされ、その UI はダッシュボードに表示されません。  
  
-   **ファイル履歴**: 新しく作成されたユーザー アカウントのファイル履歴設定は、サーバーで自動的に管理されません。  
  
-   **サーバー バックアップ**: サーバー バックアップ サービスが無効にされ、サーバー バックアップ UI はダッシュボードに表示されません。  
  
-   **記憶域スペース**: 記憶域スペースの作成または管理のための UI はダッシュボードに表示されません。  
  
-   **Anywhere Access** : Anywhere Access のセットアップ ウィザードを実行すると、既定でルーターと VPN の構成がスキップされます。  
  
 示されている各機能の動作を制御したい場合は、それぞれの対応するレジストリ キーを設定できます。 レジストリ キーを設定する方法については、「 [Windows Server 2012 R2 での Windows Server Essentials のカスタマイズと展開](https://technet.microsoft.com/library/dn293241.aspx)」を参照してください。  
  
##  <a name="BKMK_AutomateDeployment"></a> Windows Server Essentials エクスペリエンスの展開を自動化します。  
 展開を自動化するには、まずオペレーティング システムを展開し、Windows Server Essentials エクスペリエンス役割をインストールして必要があります。  
  
-   Windows Server 2012 R2 Standard または Windows Server 2012 R2 Datacenter を自動的に展開する手順については、 [Windows アセスメント & デプロイメント キット](https://msdn.microsoft.com/library/hh825420.aspx)します。  
  
-   Windows PowerShell を使用して、Windows Server Essentials エクスペリエンス役割をインストールする方法については、次を参照してください。[のインストールと Windows Server Essentials の構成](https://technet.microsoft.com/library/dn281793.aspx)します。  
  
> [!NOTE]
>  ホストの仮想マシンと、Windows Server Essentials エクスペリエンスのタイム ゾーン設定が、同じであることを確認します。 同じでない場合、いくつかのエラーが発生する可能性があります。 含まれますサーバーの初期構成に成功したできない可能性があります関連タスクを証明書は、数時間後、Windows Server Essentials Experience 役割がインストールされていると、デバイス情報が更新されないのは、証明書が機能しない。正しくします。  
  
 展開後、Windows PowerShell コマンドレット **Get-WssConfigurationStatus** を使用して、初期構成が成功したかどうかを確認します。 返されるステータスは、次のいずれかになるはずです。**Notstarted**、**FinishedWithWarning**、**Running**、**Finished**、**Failed**、または **PendingReboot**。  
  
 サーバーは、初期構成中に再起動されます。 この自動再起動を回避する必要がある場合は、初期構成を開始する前に、次のコマンドを使用して、レジストリ キーを追加することができます。  
  
```  
New-ItemProperty "HKLM:\Software\Microsoft\Windows Server\Setup"Ã‚Â  -Name "WaitForReboot" -Value 1 -PropertyType "DWord" -Force -Confirm:$false  
  
```  
  
 初期構成の開始後に、**Get-WssConfigurationStatus** を使用して、初期構成のステータスを確認することができ、ステータスが **PendingReboot** の場合に、サーバーを再起動することができます。  
  
##  <a name="BKMK_Migrate"></a> Windows Small Business Server からデータを Windows Server Essentials エクスペリエンスに移行します。  
 Windows Server Essentials を実行するサーバーに Windows Small Business Server 2011、Windows Small Business Server 2008、Windows Small Business Server 2003、または Windows Server Essentials を実行しているサーバーからデータを移行することができます。 レビュー、 [Windows Server Essentials への移行](../migrate/Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)移行は、オンプレミスの 2migrations のためのガイドし、ホスティング環境に基づいて必要なカスタマイズを作成します。  
  
> [!NOTE]
>  移行元サーバーと移行先サーバーを同じサブネットに配置することをお勧めします。 それが無理な場合、次の点を確認する必要があります。  
>   
>  -   移行元サーバーと移行先サーバーは互いにアクセス"セント s 内部 DNS 名。  
> -   すべての必要なポートが開いている。  
  
 移行後、ライセンスをアップグレードして、ロックと制限を削除することができます。 詳細については、次を参照してください。 [Windows Server Essentials から Windows Server 2012 Standard への移行](https://technet.microsoft.com/library/jj247582.aspx)します。  
  
##  <a name="BKMK_PowerShell"></a> Windows PowerShell を使用して一般的なタスクを実行します。  
 ここでは、Windows PowerShell を使用して実行できる一般的ないくつかのタスクについて説明します。  
  
### <a name="enable-remote-web-access"></a>リモート Web アクセスを有効にする  
 **構文**:  
  
 Enable-WssRemoteWebAccess [-SkipRouter] [-DenyAccessByDefault] [-ApplyToExistingUsers]  
  
 **例**:  
  
 $Enable-WssRemoteWebAccess œDenyAccessByDefault œApplyToExistingUsers  
  
 このコマンドは、ルーターを自動的に構成する設定でリモート Web アクセスを有効にし、すべての既存ユーザーの既定のアクセス許可を変更します。  
  
### <a name="add-user"></a>ユーザーを追加する  
 **構文**:  
  
 追加 WssUser [-名] < 文字列\>[-パスワード] < securestring\> [-AccessLevel < 文字列\>{ユーザー&#124;管理者}] [-FirstName < 文字列\>] [-LastName < 文字列\>] [-AllowRemoteAccess] [-AllowVpnAccess] [< CommonParameters\>]  
  
 **例**:  
  
 $password = Convertto-securestring"Passw0rd!" -asplaintext œforce$ Add-wssuser-名前 User2Test-パスワード $password Accesslevel 管理者 - FirstName User2 LastName のテスト  
  
 このコマンドでは、管理者パスワード Passw0rd User2Test をという名前を追加しました。  
  
### <a name="add-server-folder"></a>サーバー フォルダーの追加  
 **構文**:  
  
 Add-WssFolder [-Name] <string\> [-Path] <string\> [[-Description] <string\>] [-KeepPermissions] [<CommonParameters\>]  
  
 **例**:  
  
 $Add-WssFolder -Name "MyTestFolder" -Path "C:\ServerFolders\MyTestFolder"  
  
 このコマンドでは、指定した位置に MyTestFolder をという名前のサーバー フォルダーを追加します。  
  
##  <a name="BKMK_EmailIntegration"></a> Windows Server Essentials と電子メールの統合  
 Office 365 と Windows Server Essentials エクスペリエンスを統合することができますか、Exchange Server をホストします。 お客様がホスト型電子メールを使用する場合は、Windows Server Essentials エクスペリエンスをホスト型電子メール ソリューションと統合するためのアドインを開発する必要があります。 詳細については、 [Windows Server Essentials SDK](https://msdn.microsoft.com/library/gg513877.aspx)を参照してください。  
  
##  <a name="BKMK_Monitoring"></a> ネイティブ ツールを使用した監視し、管理  
 このセクションでは、監視し、サーバーを管理する Windows Server 2012 R2 で使用可能なネィティブ ツールについて説明します。  
  
### <a name="group-policy"></a>グループ ポリシー  
  Windows Server Essentials エクスペリエンスは、Windows Server 2012 R2 のネイティブ グループ ポリシー サポートを利用し、フォルダー リダイレクトとセキュリティ設定を構成するためのユーザー インターフェイスを提供します。  
  
> [!NOTE]
>  ホストされている環境では、ユーザー プロファイルのフォルダーのリダイレクションが有効になっている場合、データ サイズが大きいと、エンド ユーザーのサインインに時間がかかる可能性があります。  
  
### <a name="system-center-monitoring-pack"></a>System Center 監視パック  
 多数の Windows Server Essentials を実行しているサーバーを管理するために正常性アラート システムは小規模企業専用の Windows Server Essentials エクスペリエンスの監視用 system Center 監視パックします。 詳細については、次を参照してください。 [System Center 管理パックの Windows Server Essentials](https://www.microsoft.com/download/details.aspx?id=40809)します。  
  
### <a name="backup-and-restore"></a>バックアップと復元  
  Windows Server Essentials エクスペリエンスを Windows Server 2012 R2 サーバーおよびネットワーク内のクライアント コンピューターをバックアップすることができます。  
  
#### <a name="server-backup"></a>サーバー バックアップ  
 Windows Server Essentials は、オンプレミス バックアップとオフプレミス バックアップの 2 つのサーバーのバックアップ方法をサポートします。 独自のサーバー バックアップ ソリューションを展開する場合は、これらのオプションをカスタマイズできます。  
  
-   **オンプレミス バックアップ** : 個別のディスクに定期的にブロックレベルの増分バックアップを実行できます。 ホストとして、Windows Server Essentials を実行している仮想マシンに仮想ハード ディスクを接続し、この仮想ハード ディスクへのサーバー バックアップを構成できます。 仮想ハード ディスクは、Windows Server Essentials を実行している仮想マシンと異なる物理ディスクに存在する必要があります。  
  
    > [!NOTE]
    >  仮想マシン用の他のバックアップ ソリューションがあり、ユーザーに、Windows Server Essentials のネイティブ サーバー バックアップ機能が表示されないようにする場合は、それをオフにし、ダッシュボードから関連ユーザー インターフェイスを削除することができます。 詳細については、「 [Windows Server 2012 R2 での Windows Server Essentials のカスタマイズと展開](https://technet.microsoft.com/library/dn293413.aspx) 」の「 [サーバー バックアップのカスタマイズ](https://technet.microsoft.com/library/dn293241.aspx)」セクションを参照してください。  
  
-   **オフプレミス バックアップ** : サーバー データをクラウド サービスに定期的にバックアップできます。 ダウンロードしてインストール、Microsoft Azure Backup 統合モジュールを Windows Server Essentials は Microsoft によって提供される Azure Backup を利用することができます。  
  
     詳細については、統合 Windows Azure Backup で Windows Server Essentials のセクションを参照してください[Manage Server Backup](../manage/Manage-Server-Backup-in-Windows-Server-Essentials.md)します。  
  
     別のクラウド サービスを選択する場合、次を考慮する必要があります。  
  
    -   既定の Azure Backup の代わりに、希望のクラウド サービスにリンクするように、ダッシュ ボードのユーザー インターフェイスを更新します。  
  
    -   (省略可能) クラウドベースのバックアップ サービスの構成と管理を行うためのダッシュボード用のアドインを開発します。  
  
#### <a name="client-computer-backup"></a>クライアント コンピューター バックアップ  
 Windows Server Essentials エクスペリエンスでは、フル クライアント バックアップとファイル履歴の 2 種類のクライアント データ バックアップをサポートしています。  
  
> [!NOTE]
>  クライアントのバックアップは、VPN 経由でデータをクライアントからサーバーに転送する必要があるため、パフォーマンスに影響する可能性があります。  
  
##### <a name="full-client-backup"></a>フル クライアント バックアップ  
 フル クライアント バックアップ は、Windows Server Essentials ネットワークに接続されているすべてのクライアント デバイスに対して既定でオンになっています。 クライアントのシステムの情報とデータを完全にバックアップし、データ重複除去をサポートします。 バックアップ データは、Windows Server Essentials を実行しているサーバーに格納されます。 これにより、障害が発生したクライアントで、以前のバックアップ ポイントからデータを取得できます。  
  
 次に、フル クライアント コンピューター バックアップの注意事項を示します。  
  
-   **パフォーマンス** : 初期クライアント バックアップは、アップロードするデータ量が多いため、時間がかかる場合があります。  
  
-   **安定性** : クライアント側のインターネット接続が安定しない場合があります。 クライアントのバックアップが自動的に再開するように設計および 40 GB のデータをバックアップするたびに、クライアント バックアップ データベースがチェックポイントを作成します。 インターネット接続の信頼性が低いことが予測される場合、この値を小さい値に変更できます。  
  
    -   チェックポイント ジョブを有効にするには、サーバーで、レジストリ キー **HKLM\Software\Microsoft\Windows Server\Backup\GetCheckPointJobs** を 1 に設定します。  
  
    -   チェックポイントしきい値を変更するには、クライアントでは、次のように変更します。 **hklm \software\microsoft\windows server \backup\checkpointthreshold**から 40 GB の場合は、その既定値。  
  
-   **クライアント ベア メタル回復** : Windows プレインストール環境では VPN 接続をサポートしないため、クライアント ベア メタル回復はサポートされません。 「 [Windows Server 2012 R2 での Windows Server Essentials のカスタマイズと展開](https://technet.microsoft.com/library/dn293241.aspx)」の手順に従って、クライアント復元サービス タスクを非表示にする必要があります。  
  
##### <a name="file-history"></a>ファイル履歴  
 ファイル履歴は、プロファイル データ (ライブラリ、デスクトップ、連絡先、お気に入り) をネットワーク共有にバックアップするための Windows 8.1 および Windows 8 の機能です。 Windows Server Essentials ネットワークに参加している Windows 8.1 または Windows 8 を実行しているすべてのコンピューターのファイル履歴設定を一元的に管理できます。 バックアップ データは、Windows Server Essentials を実行しているサーバーに保存されます。 「 [Windows Server 2012 R2 での Windows Server Essentials のカスタマイズと展開](https://technet.microsoft.com/library/dn293241.aspx)」の手順に従って、クライアント復元サービス タスクを非表示にする必要があります  
  
### <a name="storage-management"></a>記憶域の管理  
 記憶域により、異種ハード ドライブの物理記憶域容量の集計、ハード ドライブの動的な追加、復元レベルを指定したデータ ボリュームの作成が可能になります。 これは、ホストまたは仮想マシンで実行できます。 Windows Server Essentials を実行している仮想マシンでこの機能を非表示にする場合は「 [Windows Server 2012 R2 での Windows Server Essentials のカスタマイズと展開](https://technet.microsoft.com/library/dn293241.aspx)」の手順に従います。  
  
##  <a name="BKMK_Scenarios"></a> テストのシナリオ  
 ホストのパースペクティブから、次のシナリオをテストすることをお勧めします。  
  

-   [サーバーの展開](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerDeploy)  
  
-   [サーバーの構成](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerConfig2)  
  
-   [サーバーの管理](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerManage)  
  
-   [クライアント エクスペリエンス](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ClientXP)  

  
###  <a name="BKMK_ServerDeploy"></a> サーバーの展開  
 次のサーバーの展開シナリオをテストすることができます。  
  
-   、ラボ環境内でドメイン コント ローラーとして Windows Server 2012 R2 を実行しているサーバーを展開し、Windows Server Essentials エクスペリエンス役割をインストールしています。  
  
-   ラボ環境で Windows Server 2012 R2 を実行しているサーバーを展開し、このサーバーを既存のドメインに参加させる、Windows Server Essentials エクスペリエンス役割をインストールしています。  
  
-   必要に応じて Windows Server Essentials イメージをカスタマイズします。  
  
-   無人セットアップ ファイルと Windows PowerShell で Windows Server Essentials の展開を自動化します。  
  
-   Windows Small Business Server を実行しているオンプレミス サーバーを Windows Server Essentials を実行しているホスト型サーバーに移行します。  
  
###  <a name="BKMK_ServerConfig2"></a> サーバーの構成  
 次のサーバー構成シナリオをテストすることができます。  
  
-   Anywhere Access (仮想プライベート ネットワーク、リモート Web アクセス、および DirectAccess) を構成します。  
  
-   記憶域とサーバー フォルダーを構成します。  
  
-   BranchCache を有効にします。  
  
-   (適用できる場合) サーバー バックアップ、オンライン バックアップ、クライアント バックアップ、ファイル履歴を構成します。  
  
-   (適用できる場合) 記憶域を構成し、管理します。  
  
-   (適用できる場合) 電子メール ソリューション統合 (Office 365 とホスト型 Exchange Server) を構成します。  
  
-   (適用できる場合) その他の Microsoft オンライン サービスとの統合を構成します。  
  
-   (適用できる場合) メディア サーバーを構成します。  
  
###  <a name="BKMK_ServerManage"></a> サーバーの管理  
 次のサーバー管理のシナリオをテストすることができます。  
  
-   ユーザーおよびグループを管理します。  
  
-   アラートの電子メール通知を構成し、受信します。  
  
-   ベスト プラクティス アナライザーを実行し、エラーまたは警告メッセージが表示されるかどうかを確認します。  
  
-   System Center Operations Manager パックを構成します。  
  
-   オペレーティング システムの破損が発生した場合に、サーバー回復を構成します。  
  
###  <a name="BKMK_ClientXP"></a> クライアント エクスペリエンス  
 次のエンド ユーザー シナリオをテストすることができます。  
  
-   インターネット (PC または Mac オペレーティング システム) 経由でクライアントを展開します。  
  
-   クライアントのスタート パッドを使用して、共有フォルダーにアクセスします。  
  
-   リモート Web アクセス経由でさまざまなデバイス (PC、電話、タブレット) からサーバー資産にアクセスします。  
  
-   Windows Phone 用の My Server アプリにアクセスします。  
  
-   (適用できる場合) ファイル履歴、クライアント バックアップおよび復元、フォルダー リダイレクションにアクセスします。  
  
-   (適用できる場合) 電子メール統合エクスペリエンスを確認します。  
  
##  <a name="BKMK_Support"></a> サポート情報  
 Windows Server Essentials ソフトウェア開発キット (SDK) および Windows Server Essentials アセスメントおよびデプロイメント キット (ADK) をダウンロードすることができます。  
  
-   [Windows Server Essentials ソフトウェア開発キット](https://msdn.microsoft.com/library/gg513877.aspx)SDK  
  
-   [カスタマイズし、Windows Server 2012 R2 での Windows Server Essentials の展開](https://technet.microsoft.com/library/dn293241.aspx)  
  
## <a name="see-also"></a>関連項目  
  
-   [新機能 Windows Server Essentials の新機能](../get-started/what-s-new.md)  

-   [Windows Server Essentials をインストールします。](Install-Windows-Server-Essentials.md)  

-   [Windows Server Essentials を概要します。](../get-started/get-started.md)
