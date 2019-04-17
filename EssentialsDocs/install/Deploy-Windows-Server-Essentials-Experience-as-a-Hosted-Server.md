---
title: "Windows Server Essentials エクスペリエンスをホスト型サーバーとして展開します。"
description: "Windows Server Essentials を使用する方法について説明します。"
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
ms.openlocfilehash: c299d2b5f3d6b48693c473754a5205a7d26b5d6a
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="deploy-windows-server-essentials-experience-as-a-hosted-server"></a>Windows Server Essentials エクスペリエンスをホスト型サーバーとして展開します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

このドキュメントには、顧客にサービスとしての Windows Server Essentials エクスペリエンスを提供する予定がある Microsoft Windows Server 16 (と呼ばれるを Windows Server Essentials のドキュメントの残りの部分で) Windows Server Essentials エクスペリエンス役割を持つ、ラボでのインストールを展開するホストに固有の情報が含まれます。 このドキュメントには、次のセクションが含まれています。  
  

-   [Windows Server Essentials エクスペリエンスの概要](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_WSEEOverview)  
  
-   [Windows Server Essentials エクスペリエンスをホストしているの利点](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Benefits)  
  
-   [サポートされる展開オプション](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedDeployment)  
  
-   [サポートされているネットワーク トポロジ](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedToplogy)  
  
-   [Windows Server Essentials エクスペリエンス役割のイメージをカスタマイズします。](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_CustomizeImage)  
  
-   [Windows Server Essentials エクスペリエンスの展開を自動化します。](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_AutomateDeployment)  
  
-   [データの Windows Small Business Server から Windows Server Essentials エクスペリエンスへの移行します。](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Migrate)  
  
-   [Windows PowerShell を使用した一般的なタスクを実行します。](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_PowerShell)  
  
-   [Windows Server Essentials と電子メールの統合](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_EmailIntegration)  
  
-   [ネイティブ ツールを使用した監視し、管理](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Monitoring)  
  
-   [テスト シナリオ](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Scenarios)  
  
-   [サポート情報](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Support)  

-   [Windows Server Essentials エクスペリエンスの概要](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_WSEEOverview)  
  
-   [Windows Server Essentials エクスペリエンスをホストしているの利点](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Benefits)  
  
-   [サポートされる展開オプション](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedDeployment)  
  
-   [サポートされているネットワーク トポロジ](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_SupportedToplogy)  
  
-   [Windows Server Essentials エクスペリエンス役割のイメージをカスタマイズします。](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_CustomizeImage)  
  
-   [Windows Server Essentials エクスペリエンスの展開を自動化します。](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_AutomateDeployment)  
  
-   [データの Windows Small Business Server から Windows Server Essentials エクスペリエンスへの移行します。](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Migrate)  
  
-   [Windows PowerShell を使用した一般的なタスクを実行します。](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_PowerShell)  
  
-   [Windows Server Essentials と電子メールの統合](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_EmailIntegration)  
  
-   [ネイティブ ツールを使用した監視し、管理](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Monitoring)  
  
-   [テスト シナリオ](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Scenarios)  
  
-   [サポート情報](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_Support)  

  
##  <a name="BKMK_WSEEOverview"></a>Windows Server Essentials エクスペリエンスの概要  
 Windows Server Essentials エクスペリエンスは、Windows Server 2012 R2 Standard と Windows Server 2012 R2 Datacenter に記載されているサーバーの役割です。 Windows Server Essentials エクスペリエンス役割がインストールすると、Windows Server 2012 R2 を実行するサーバーで、顧客は、ロックや制限なく、Windows Server Essentials で利用可能なすべての機能の利用できます。 Windows Server Essentials エクスペリエンスには、小規模および中規模企業向けの次のクロスプレミス ソリューションが有効にします。  
  
-   **データ記憶域と保護**お客様を格納することができます"™ データを一元的な場所にし、サーバーと、ネットワーク内のクライアント コンピューター (75 台未満) をバックアップしてサーバーとクライアントのデータを保護するためです。  
  
-   **ユーザーの管理**ユーザーと、簡素化されたサーバー ダッシュ ボードを使用してグループを管理することができます。 さらに、Microsoft Azure Active Directory (Azure AD) との統合により、(たとえば、Office 365、Exchange Online、および SharePoint Online) は、Microsoft online services のデータに簡単アクセス ユーザーのドメイン資格情報を使用できます。  
  
-   **サービス統合**(Office 365、SharePoint Online、および Microsoft Azure Backup) などの Microsoft online services とサーバーを統合することができます。 サーバーは、サービスまたはサード パーティ プロバイダーによって提供されるサービスと統合することもできます。  
  
-   **Anywhere Access**、顧客が、サーバー、ネットワーク コンピューター、およびデータにアクセスできるからほぼどこからでも、インターネットに接続していると、ほぼすべてのデバイスを使用しています。 リモート Web アクセスによりアプリケーションや、効率的でタッチ操作に適したブラウザー エクスペリエンスを使用してデータにアクセスできます。 My Server アプリにより、Windows Phone または Microsoft ストア アプリからデータにアクセスできます。  
  
-   **メディア ストリーム配信**と Windows Server Essentials エクスペリエンスを有効になっているサーバーにメディア パッケージをインストールする場合、エンド カスタマーことができます、共有フォルダーに音楽、ビデオ、および写真を保存し、ネットワーク コンピューターまたはリモート Web アクセスからこれらのメディア ファイルにアクセスします。  
  
-   **正常性の監視**ネットワークのヘルス状態を監視し、カスタマイズされた正常性レポートを取得することができます。  
  
##  <a name="BKMK_Benefits"></a>Windows Server Essentials エクスペリエンスをホストしているの利点  
  既存の展開および管理フレームワークを展開し、Windows Server Essentials エクスペリエンス役割を構成する Windows Server を再利用できるように、Windows Server Essentials エクスペリエンスは、Windows Server の役割です。 Windows Server Essentials エクスペリエンス役割をホストするいると、次の利点があります。  
  
-   **展開を合理化**単に、Windows Server Essentials Experience 役割をオン、いくつかの最も一般的に使用される役割と機能が入っており、小規模および中規模企業のベスト プラクティスで構成します。 Windows Server Essentials の機能をカスタマイズしたり、いくつかの内部設置型機能を非表示にすることができます。 Windows Azure Pack を使用する場合は、Windows Server 2012 R2 での Windows Server Essentials エクスペリエンスのギャラリー テンプレートをダウンロードできます。  
  
-   **簡素化されたダッシュ ボード**: Windows Server Essentials ダッシュ ボードがサーバー フォルダー、サーバー記憶域、バックアップと復元、ユーザーまたはグループ アカウント、デバイス、リモート アクセス、および電子メールの管理などの一般的なタスクを簡略化します。 小規模および中規模企業のお客様は、テクニカル サポート ヘルプ デスクを呼び出すことではなく、日常の管理タスクを実行できます。  
  
-   **拡張**: Windows Server Essentials ダッシュ ボードおよび Windows Server Essentials コネクタ ソフトウェアは拡張可能です。 独自のブランドを追加し、サーバーとサービスについてのものを 1 つのエントリ ポイントがあるお客様できるように、統合サービスを提供できます。  
  
-   **モニター**監視および Windows Server Essentials を実行している複数のサーバーを管理する System Center 監視パックの新しいバージョンがあります。 管理パックをダウンロードするを参照してください。[System Center 管理パックの Windows Server Essentials](https://www.microsoft.com/download/details.aspx?id=40809)します。  
  
##  <a name="BKMK_SupportedDeployment"></a>サポートされる展開オプション  
  Windows Server Essentials エクスペリエンスは、新しい Active Directory 環境にドメイン コントローラーとして展開できます。または、既存の Active Directory 環境にドメイン メンバーとして展開できます。  
  
 Windows Server 2012 R2 Standard または Windows Server 2012 R2 Datacenter を展開して、Windows Server Essentials エクスペリエンス役割をインストールすることをお勧めします。 この展開方法では、Windows Server Essentials edition では、ロックや制限なしのすべての機能を取得します。  
  

 Windows Server Essentials エクスペリエンス役割を持つ Windows Server 2012 R2 のインストールに関する詳細については、次を参照してください。[Windows Server Essentials の構成とインストール](Install-and-Configure-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)します。  


  
##  <a name="BKMK_SupportedToplogy"></a>サポートされているネットワーク トポロジ  
 ローミング クライアントから Windows Server Essentials エクスペリエンスを使用するには、VPN を有効にする必要があります。 ローミング クライアントからサーバーにリモート アクセスを有効にするには、ポート 443 と、サーバー上のポート 80 を開く必要があります。  
  
 次に、次の 2 つ一般的なサーバー側のネットワーク トポロジと VPN およびリモート Web アクセスの構成方法を示します。  
  
-   **トポロジ 1** (これは、優先されるトポロジと、同じサブネット内のすべてのサーバーと VPN の IP 範囲がかかります)。  
  
    -   [ネットワーク アドレス変換 (NAT) デバイス別の仮想ネットワーク内のサーバーを設定します。  
  
    -   サーバーの静的 IP アドレスを割り当てることも、仮想ネットワークで DHCP サービスを有効にします。  
  
    -   サーバーのローカル ネットワーク アドレスをルーター上で、パブリック IP ポート 443 を転送します。  
  
    -   ポート 443 の VPN パススルーを許可します。  
  
    -   サーバーのアドレスと同じサブネットの範囲で、VPN IPv4 アドレス プールを設定します。  
  
    -   2 番目のサーバーに、同じサブネット内では、VPN アドレス プールから静的 IP アドレスを割り当てます。  
  
-   **トポロジ 2**:  
  
    -   サーバーのプライベート IP アドレスを割り当てます。  
  
    -   パブリック ポート 443 IP アドレスに到達するサーバー上のポート 443 を使用できます。  
  
    -   ポート 443 の VPN パススルーを許可します。  
  
    -   別の範囲を VPN IPv4 アドレス プールとサーバーのアドレスを割り当てます。  
  
 トポロジ 2 では、同じドメインに別のサーバーを追加できないため、2 つ目のサーバーのシナリオはサポートされません。  
  
 Windows PowerShell スクリプトを使用して、無人デプロイメント中に VPN を有効にすることができます、または、初期構成後にウィザードを使用して構成することができます。  
  
 VPN を有効に Windows PowerShell を使用して管理者特権を持つ Windows Server Essentials を実行しているサーバーで次のコマンドを実行し、必要なすべての情報を提供します。  
  
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
>  お客様が所有しているサーバーの前に、VPN 接続を提供することはできない場合、は、エンド ユーザーができるように、お客様は、リモート デスクトップ プロトコルを使用して、サーバーへの接続をして構成するサーバー ポート 3389 がインターネット経由で到達できることを確認します。  
  
##  <a name="BKMK_CustomizeImage"></a>Windows Server Essentials エクスペリエンス役割のイメージをカスタマイズします。  
 Windows Server Essentials エクスペリエンス役割を構成する前に、イメージをカスタマイズできます。 標準の Windows Server Sysprep プロセスについては、次を参照してください。[Windows アセスメント & デプロイメント キット](https://msdn.microsoft.com/library/hh825420.aspx)します。 Sysprep を使用して、イメージを準備した後に使用したり、新しい展開の Install.wim に再シールできます。  
  
 Virtual Machine Manager を使用している場合は、実行中のインスタンスを使用してテンプレートを作成できます。 このプロセスは Sysprep を使用して、インスタンスを準備し、そのコンピューターをシャット ダウンします。 テンプレートをライブラリに保存した後では、ケースバイ ケースで使用できます。  
  
 Windows Server Essentials エクスペリエンス役割をインストールした後は、Windows Server Essentials での機能をカスタマイズできます。 最も重要なカスタマイズの 1 つは、**IsHosted**レジストリ キー: **HKEY_LOCAL_MACHINE \software\microsoft\Windows Server \deployment\ishosted**します。  
  
 このキーが 0x1 に設定されている場合、オンプレミスの機能の一部を動作が変更されます。 これらの機能の変更は次のとおりです。  
  
-   **クライアント バックアップ**クライアント バックアップが新しく参加したクライアント コンピューターに対して既定で無効になります。  
  
-   **クライアント復元サービス**クライアント復元サービスが無効にして、ダッシュ ボードから、UI は表示されません。  
  
-   **ファイル履歴**サーバーで新しく作成されたユーザー アカウントのファイル履歴の設定が自動的に管理されません。  
  
-   **サーバー バックアップ**サーバーのバックアップ サービスが無効にして、サーバー バックアップ UI はダッシュ ボードに表示されます。  
  
-   **記憶域スペース**ダッシュ ボードを作成または記憶域スペースを管理するための UI は表示されません。  
  
-   **Anywhere Access**セットアップ Anywhere Access ウィザードを実行するときに既定でルーターと VPN の構成はスキップされます。  
  
 表示されている各機能の動作を制御する場合は、それぞれの対応するレジストリ キーを設定することができます。 レジストリ キーを設定する方法についてを参照してください、[のカスタマイズと Windows Server 2012 R2 での Windows Server Essentials の展開](https://technet.microsoft.com/library/dn293241.aspx)  
  
##  <a name="BKMK_AutomateDeployment"></a>Windows Server Essentials エクスペリエンスの展開を自動化します。  
 展開を自動化するには、まずオペレーティング システムを展開し、Windows Server Essentials Experience 役割をインストールする必要があります。  
  
-   自動的を展開する Windows Server 2012 R2 Standard または Windows Server 2012 R2 Datacenter の指示に従って、[Windows アセスメント & デプロイメント キット](https://msdn.microsoft.com/library/hh825420.aspx)します。  
  
-   Windows PowerShell を使用して、Windows Server Essentials Experience 役割をインストールする方法については、次を参照してください。[Windows Server Essentials の構成とインストール](https://technet.microsoft.com/library/dn281793.aspx)します。  
  
> [!NOTE]
>  ホストの仮想マシンと Windows Server Essentials エクスペリエンスのタイム ゾーン設定が同じであることを確認します。 それ以外の場合、いくつかのエラーが発生する可能性があります。 含まれます: サーバーの初期構成で成功したできない可能性があります証明書の関連するタスク、時間、Windows Server Essentials Experience 役割がインストールされているし、デバイスの情報が正しく更新されない後に、いくつかの証明書は使用できません。  
  
 展開後に、Windows PowerShell コマンドレットを使用して**Get-wssconfigurationstatus**かどうか、初期構成が成功したことを確認します。 返されるステータスは、次のいずれかにする必要があります: **Notstarted**、**FinishedWithWarning**、**を実行している**、**完了**、**失敗**、または**PendingReboot**します。  
  
 サーバーは、初期構成中に再起動されます。 この自動再起動を回避する場合は、初期構成を開始する前に、レジストリ キーを追加する、次のコマンドを使用できます。  
  
```  
New-ItemProperty "HKLM:\Software\Microsoft\Windows Server\Setup"Ã‚Â  -Name "WaitForReboot" -Value 1 -PropertyType "DWord" -Force -Confirm:$false  
  
```  
  
 初期構成の開始後を使用して**Get-wssconfigurationstatus**を初期構成のステータスを確認して、ステータスが**PendingReboot**、サーバーを再起動することができます。  
  
##  <a name="BKMK_Migrate"></a>データの Windows Small Business Server から Windows Server Essentials エクスペリエンスへの移行します。  
 Windows Server Essentials を実行しているサーバーに Windows Small Business Server 2011、Windows Small Business Server 2008、Windows Small Business Server 2003、または Windows Server Essentials を実行しているサーバーからデータを移行することができます。 レビュー、[Windows Server Essentials への移行](../migrate/Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)移行は、内部設置型 2migrations のためのガイドし、ホスティング環境に基づいて必要なカスタマイズを行います。  
  
> [!NOTE]
>  同じサブネット内の移行元サーバーと移行先サーバーを配置することをお勧めします。 これが可能でない場合することを確認します。  
>   
>  -   移行元サーバーと移行先サーバーが互いにアクセス"™ s 内部 DNS 名。  
> -   すべての必要なポートが開いています。  
  
 移行後に、ロックや制限を削除するには、ライセンスをアップグレードできます。 詳細については、次を参照してください。[Windows Server Essentials から Windows Server 2012 Standard への移行](https://technet.microsoft.com/library/jj247582.aspx)します。  
  
##  <a name="BKMK_PowerShell"></a>Windows PowerShell を使用した一般的なタスクを実行します。  
 このセクションでは、一部の Windows PowerShell を使用して実行できる一般的なタスクについて説明します。  
  
### <a name="enable-remote-web-access"></a>リモート Web アクセスを有効にします。  
 **構文**:  
  
 Enable-WssRemoteWebAccess[-SkipRouter][-DenyAccessByDefault][-ApplyToExistingUsers]  
  
 **例**:  
  
 $Enable-WssRemoteWebAccess œDenyAccessByDefault œApplyToExistingUsers  
  
 このコマンドは、自動的に構成されているルーターにリモート Web アクセスを有効にし、既存のすべてのユーザーの既定のアクセス許可を変更します。  
  
### <a name="add-user"></a>ユーザーを追加します。  
 **構文**:  
  
 Add-WssUser[-名] < string\ > [-パスワード] < securestring\ > [-AccessLevel < string\ > {ユーザー & #124;管理者}] [-FirstName < string\ >] [-< string\ > [氏名] [-AllowRemoteAccess] [-AllowVpnAccess] [< CommonParameters\ >]  
  
 **例**:  
  
 $password = ConvertTo-SecureString"Passw0rd!" -asplaintext œforce$ Add-wssuser-名前 User2Test-パスワード $password Accesslevel 管理者 - FirstName User2 LastName テスト  
  
 このコマンドは、管理者パスワード Passw0rd User2Test という名前を追加しました。  
  
### <a name="add-server-folder"></a>サーバー フォルダーを追加します。  
 **構文**:  
  
 Add-WssFolder[-名] < string\ > [-パス] < string\ > [の説明] < string\ >] [-KeepPermissions] [< CommonParameters\ >]  
  
 **例**:  
  
 $追加 WssFolder-名前"MyTestFolder"-"C:\ServerFolders\MyTestFolder"のパス  
  
 このコマンドでは、指定された場所に MyTestFolder をという名前のサーバー フォルダーを追加します。  
  
##  <a name="BKMK_EmailIntegration"></a>Windows Server Essentials と電子メールの統合  
 Office 365 を Windows Server Essentials エクスペリエンスを統合することができますか、Exchange Server をホストします。 お客様は、ホスト型電子メールを使用する場合は、Windows Server Essentials エクスペリエンスをホスト型電子メール ソリューションと統合するアドインを開発する必要があります。 詳細については、次を参照してください。[Windows Server Essentials SDK](https://msdn.microsoft.com/library/gg513877.aspx)します。  
  
##  <a name="BKMK_Monitoring"></a>ネイティブ ツールを使用した監視し、管理  
 このセクションでは、監視およびサーバーを管理する Windows Server 2012 R2 で利用可能なネィティブ ツールについて説明します。  
  
### <a name="group-policy"></a>グループ ポリシー  
  Windows Server Essentials エクスペリエンスは、Windows Server 2012 R2 でのネイティブ グループ ポリシー サポートを利用し、フォルダー リダイレクトとセキュリティ設定を構成するためのユーザー インターフェイスを提供します。  
  
> [!NOTE]
>  環境では、ホスト型、ユーザー プロファイルのフォルダーのリダイレクションが有効になっている場合は、データ サイズが大きいときにログインするエンド ユーザーの時間は、インストールを増やすことできます。  
  
### <a name="system-center-monitoring-pack"></a>System Center 監視パック  
 大規模な数の Windows Server Essentials を実行しているサーバーを管理するために正常性アラート システムは小規模企業専用の Windows Server Essentials エクスペリエンスの監視用の system Center 監視パックします。 詳細については、次を参照してください。[System Center 管理パックの Windows Server Essentials](https://www.microsoft.com/download/details.aspx?id=40809)します。  
  
### <a name="backup-and-restore"></a>バックアップと復元  
  Windows Server 2012 R2 と Windows Server Essentials エクスペリエンスでは、サーバーと、ネットワーク内のクライアント コンピューターをバックアップすることができます。  
  
#### <a name="server-backup"></a>サーバーのバックアップ  
 Windows Server Essentials サーバーをバックアップする 2 つの方法をサポートしています。オンプレミス バックアップとオフプレミス バックアップします。 独自のサーバー バックアップ ソリューションを展開する場合は、これらのオプションをカスタマイズできます。  
  
-   **オンプレミス バックアップ**個別のディスクに定期的にブロック レベルの増分バックアップを実行することができます。 ホストとしてには、Windows Server Essentials を実行している仮想マシンに仮想ハード_ディスクを接続し、このバーチャル ハード ディスクへのサーバー バックアップを構成する可能性があります。 仮想ハード_ディスクは、Windows Server Essentials を実行しているバーチャル マシンよりも、別の物理ディスクに配置する必要があります。  
  
    > [!NOTE]
    >  バーチャル マシンの他のバックアップ ソリューションがある、ユーザーに Windows Server Essentials のネイティブ サーバー バックアップ機能を表示したくない場合は、オフにし、ダッシュ ボードから関連ユーザー インターフェイスを削除します。 詳細については、次を参照してください。、[サーバー バックアップのカスタマイズ](https://technet.microsoft.com/library/dn293413.aspx)のセクション[Windows Server 2012 R2 での Windows Server Essentials の展開のカスタマイズと](https://technet.microsoft.com/library/dn293241.aspx)します。  
  
-   **オフプレミス バックアップ**サーバー データをクラウド ベースのサービスに定期的にバックアップすることができます。 ダウンロードして、Microsoft Azure Backup 統合モジュールの Windows Server Essentials を Microsoft によって提供される Azure Backup を利用してをインストールすることができます。  
  
     詳細については、統合 Windows Azure Backup と Windows Server Essentials」セクションを参照してください。[サーバー バックアップの管理](../manage/Manage-Server-Backup-in-Windows-Server-Essentials.md)します。  
  
     か、ユーザーは、別のクラウド サービスを必要に応じて場合、は、次を考慮してください。  
  
    -   Azure Backup の既定の代わりに、希望のクラウド サービスにリンクするように、ダッシュ ボードのユーザー インターフェイスを更新します。  
  
    -   (省略可能)構成し、クラウド ベースのバックアップ サービスの管理ダッシュ ボードのアドインを開発します。  
  
#### <a name="client-computer-backup"></a>クライアント コンピューターのバックアップ  
 Windows Server Essentials エクスペリエンスには、クライアント データのバックアップの 2 つの種類がサポートされています: フル クライアント バックアップとファイル履歴。  
  
> [!NOTE]
>  クライアントのバックアップ データは、VPN 経由でクライアントからサーバーに転送する必要があるためパフォーマンスに影響があります。  
  
##### <a name="full-client-backup"></a>フル クライアント バックアップ  
 フル クライアント バックアップは、Windows Server Essentials ネットワークに接続されているすべてのクライアント デバイスに対して既定でです。 完全に、クライアントは、システムの情報とデータをバックアップし、データ重複除去をサポートします。 バックアップ データは、Windows Server Essentials を実行しているサーバーに保存されます。 これにより、障害が発生したクライアントが、以前のバックアップ ポイントからデータを取得します。  
  
 フル クライアント コンピューター バックアップの注意事項を示します。  
  
-   **パフォーマンス**初期クライアント バックアップは、アップロードするデータ量が多いため時間がかかる可能性があります。  
  
-   **安定性**インターネット接続がクライアント側で安定したことがあります。 クライアントのバックアップが自動的に再開するように設計され、クライアント バックアップ データベースを 40 GB のデータをバックアップするたびにチェックポイントを作成します。 信頼性が低いへのインターネット接続が予測される場合、小さい値にこの値を変更することができます。  
  
    -   チェックポイント ジョブを有効にする: サーバーで、レジストリ キーを設定**hklm \software\microsoft\Windows Server \backup\getcheckpointjobs**を 1 にします。  
  
    -   チェックポイントしきい値を変更する: クライアントでは、次のように変更します。**hklm \software\microsoft\Windows Server \backup\checkpointthreshold**からその既定値 40 GB です。  
  
-   **クライアント ベア メタル回復**Windows プレインストール環境が VPN 接続をサポートしていないために、クライアント ベア メタル回復はサポートされません。 次の手順に従って、クライアント復元サービス タスクを非表示にする必要があります[Windows Server 2012 R2 での Windows Server Essentials の展開のカスタマイズと](https://technet.microsoft.com/library/dn293241.aspx)します。  
  
##### <a name="file-history"></a>ファイル履歴  
 ファイル履歴は、プロファイル データ (ライブラリ、デスクトップ、連絡先、お気に入り) をバックアップするためのネットワーク共有に Windows 8.1 および Windows 8 の機能です。 Windows Server Essentials ネットワークに参加している、Windows 8.1 または Windows 8 を実行しているすべてのコンピューターのファイル履歴の設定を一元的に管理できます。 バックアップ データは、Windows Server Essentials を実行しているサーバーに格納されます。 次の手順に従って、クライアント復元サービス タスクを非表示にする必要があります[のカスタマイズと Windows Server 2012 R2 での Windows Server Essentials の展開](https://technet.microsoft.com/library/dn293241.aspx)  
  
### <a name="storage-management"></a>記憶域の管理  
 記憶域スペースを使用すると、物理的な記憶域容量の集計、異種ハード ドライブを動的にハード ドライブを追加し、復元レベルを指定したデータ ボリュームを作成できます。 ホストまたはバーチャル マシン上でこれを行うことができます。 Windows Server Essentials を実行する仮想マシンでこの機能を非表示にする場合は、次の手順に[Windows Server 2012 R2 での Windows Server Essentials の展開のカスタマイズと](https://technet.microsoft.com/library/dn293241.aspx)します。  
  
##  <a name="BKMK_Scenarios"></a>テスト シナリオ  
 ホストのパースペクティブから、次のシナリオをテストすることをお勧めします。  
  

-   [サーバーの展開](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerDeploy)  
  
-   [サーバーの構成](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerConfig2)  
  
-   [サーバーの管理](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ServerManage)  
  
-   [クライアント エクスペリエンス](Deploy-Windows-Server-Essentials-Experience-as-a-Hosted-Server.md#BKMK_ClientXP)  

  
###  <a name="BKMK_ServerDeploy"></a>サーバーの展開  
 次のサーバーの展開シナリオをテストすることができます。  
  
-   ラボ、環境内でドメイン コントローラーとして Windows Server 2012 R2 を実行するサーバーを展開し、Windows Server Essentials Experience 役割をインストールします。  
  
-   ラボ環境で Windows Server 2012 R2 を実行しているサーバーを展開し、このサーバーを既存のドメインに参加させ、Windows Server Essentials Experience 役割をインストールします。  
  
-   必要に応じて、Windows Server Essentials イメージをカスタマイズします。  
  
-   無人セットアップ ファイルと Windows PowerShell、Windows Server Essentials の展開を自動化します。  
  
-   Windows Server Essentials を実行しているホスト型サーバーに Windows Small Business Server を実行している社内サーバーを移行します。  
  
###  <a name="BKMK_ServerConfig2"></a>サーバーの構成  
 次のサーバー構成シナリオをテストすることができます。  
  
-   Anywhere Access (仮想プライベート ネットワーク、リモート Web アクセス、および DirectAccess) を構成します。  
  
-   記憶域とサーバー フォルダーを構成します。  
  
-   BranchCache を有効にします。  
  
-   (該当する場合)サーバー バックアップ、オンライン バックアップ、クライアントのバックアップを構成し、ファイル履歴。  
  
-   (該当する場合)構成し、記憶域スペースを管理します。  
  
-   (該当する場合)電子メール ソリューション統合 (Office 365 とホスト型 Exchange Server) を構成します。  
  
-   (該当する場合)その他の Microsoft online services との統合を構成します。  
  
-   (該当する場合)メディア サーバーを構成します。  
  
###  <a name="BKMK_ServerManage"></a>サーバーの管理  
 次のサーバーの管理シナリオをテストすることができます。  
  
-   ユーザーとグループを管理します。  
  
-   構成し、アラートの電子メール通知を受信します。  
  
-   あるかどうか、エラーまたは警告メッセージを表示するベスト プラクティス アナライザーを実行します。  
  
-   System Center Operations Manager パックを構成します。  
  
-   オペレーティング システムの破損が発生した場合、サーバー回復を構成します。  
  
###  <a name="BKMK_ClientXP"></a>クライアント エクスペリエンス  
 次のエンド ユーザー シナリオをテストすることができます。  
  
-   インターネット (PC または Mac オペレーティング システム) 経由でクライアントを展開します。  
  
-   クライアントのスタート パッドを使用して、共有フォルダーにアクセスします。  
  
-   リモート Web アクセス経由でさまざまなデバイス (PC、電話、およびタブレット) からのサーバーの資産がアクセスします。  
  
-   Windows Phone の My Server アプリにアクセスします。  
  
-   (該当する場合)ファイル履歴のアクセス、クライアントのバックアップと復元、およびフォルダー リダイレクトします。  
  
-   (該当する場合)電子メール統合エクスペリエンスを確認します。  
  
##  <a name="BKMK_Support"></a>サポート情報  
 Windows Server Essentials ソフトウェア開発キット (SDK) と Windows Server Essentials アセスメントおよびデプロイメント キット (ADK) をダウンロードすることができます。  
  
-   [Windows Server Essentials ソフトウェア開発キット](https://msdn.microsoft.com/library/gg513877.aspx)SDK  
  
-   [カスタマイズし、Windows Server 2012 R2 での Windows Server Essentials の展開](https://technet.microsoft.com/library/dn293241.aspx)  
  
## <a name="see-also"></a>参照してください。  
  
-   [Windows Server Essentials の新機能](../get-started/what-s-new.md)  

-   [Windows Server Essentials をインストールします。](Install-Windows-Server-Essentials.md)  

-   [Windows Server Essentials を使ってみる](../get-started/get-started.md)
