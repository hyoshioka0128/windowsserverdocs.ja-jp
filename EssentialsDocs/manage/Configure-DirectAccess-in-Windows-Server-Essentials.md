---
title: "Windows Server Essentials で DirectAccess を構成します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c959b6fc-c67e-46cd-a9cb-cee71a42fa4c
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: cc336dcd2a5418aa79254108c941a02147112e8f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="configure-directaccess-in-windows-server-essentials"></a>Windows Server Essentials で DirectAccess を構成します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

このトピックでは、シームレスにネットワークに接続する、組織のインターネットが搭載されているリモートの場所から仮想プライベート ネットワーク (VPN) 接続を確立せず、モバイルのユーザーを有効にする Windows Server Essentials で DirectAccess を構成するための手順を示します。 DirectAccess は、Windows 8.1、Windows 8、および Windows 7 コンピューターからモバイル ワーカー社内と社外で同じ接続性を提供できます。  
  
 、Windows Server Essentials で [ドメインに 1 つ以上の Windows Server Essentials サーバーが含まれている場合 DirectAccess は、ドメイン コント ローラーで構成する必要があります。  
  
> [!NOTE]
>  このトピックでは、Windows Server Essentials サーバーがドメイン コント ローラーの場合は、DirectAccess を構成するための手順を示します。 Windows Server Essentials サーバーがドメイン メンバーである場合は、次のドメインのメンバーでの DirectAccess を構成する手順[既存のリモート アクセス (VPN) の展開に DirectAccess を追加](https://technet.microsoft.com/library/jj574220.aspx)代わりにします。  
  
## <a name="process-overview"></a>プロセスの概要  
 Windows Server Essentials で DirectAccess を構成するには、次の手順を実行します。  
  
> [!IMPORTANT]
>  前に、Windows Server Essentials で DirectAccess を構成するため、このガイドの手順を使用して、サーバーで VPN を有効にする必要があります。 手順については、次を参照してください。 [VPN の管理](Manage-VPN-in-Windows-Server-Essentials.md)します。  
  
-   [手順 1: リモート アクセス管理ツールをサーバーに追加します。](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_AddRAM)  
  
-   [手順 2: サーバーのネットワーク アダプターのアドレスを静的 IP アドレスに変更します。](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_AddStaticIP)  
  
-   [手順 3: ネットワーク ロケーション サーバーの証明書と DNS レコードを準備します。](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS)  
  
    -   [手順 3 a: Web サーバー証明書テンプレートの完全なアクセス許可を Authenticated Users に付与](#BKMK_GrantFullPermissions)  
  
    -   [手順 3 b: 外部ネットワークからは解決できない共通名で、ネットワーク ロケーション サーバー用の証明書の登録](#BKMK_EnrollaCertificate)  
  
    -   [手順 3 c: DNS サーバーに新しいホストを追加して、Windows Server Essentials サーバー アドレスにマップします。](#BKMK_MapNewHosttoServerAddress)  
  
-   [手順 4: DirectAccess クライアント コンピューターのセキュリティ グループを作成します。](#BKMK_AddSecurityGroup)  
  
-   [手順 5: 有効にして DirectAccess を構成します。](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableConfigureDA)  
  
    -   [ステップ 5 a: リモート アクセス管理コンソールを使用して DirectAccess を有効にします。](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableDA)  
  
    -   [手順 5b: RRAS GPO (Windows Server Essentials のみ) から、無効な IPv6Prefix を削除します。](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_RemoveIPv6)  
  
    -   [手順 5c:windows: DirectAccess を使用する Windows 7 Enterprise を実行しているクライアント コンピューターを有効にします。](#BKMK_Step4cWindows7Setup)  
  
    -   [手順 5 d: ネットワーク ロケーション サーバーを構成します。](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NLS)  
  
    -   [手順 5e:ipsec: IPsec チャネルを確立するときに CA 証明書をバイパスするレジストリ キーを追加](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_CA)  
  
-   [手順 6: DirectAccess サーバーの名前解決ポリシー テーブル設定を構成します。](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NRPT)  
  
-   [手順 7: DirectAccess サーバー Gpo の TCP および UDP のファイアウォール規則を構成します。](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_TCPUDP)  
  
-   [手順 8: IP-HTTPS インターフェイスをリッスンするように DNS64 の構成を変更します。](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS64)  
  
-   [手順 9: WinNat サービス用にポートを予約します。](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_ExemptPort)  
  
-   [手順 10: WinNat サービスを再起動します。](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_WinNAT)  
  
> [!NOTE]
>  [付録: が DirectAccess を Windows PowerShell を使用して設定](#BKMK_AppendixBPowerShellScript)では、DirectAccess セットアップを実行するのに使用できる Windows PowerShell スクリプトを提供します。  
  
##  <a name="BKMK_AddRAM"></a>手順 1: リモート アクセス管理ツールをサーバーに追加します。  
  
#### <a name="to-add-remote-access-management-tools"></a>リモート アクセス管理ツールを追加するには  
  
1.  [開始] ページの左下隅で、サーバー] をクリックして、**サーバー マネージャー**アイコン。  
  
     Windows Server Essentials でサーバー マネージャーを開くにはそれを検索する必要があります。 [開始] ページで、次のように入力します。**サーバー マネージャー**、] をクリックし、**サーバー マネージャー** 、検索結果でします。 サーバー マネージャーを開始] ページにピン留めに、検索結果でサーバー マネージャーを右クリックし] をクリックして**スタートにピン留め**します。  
  
2.  場合、**ユーザー アカウント制御**警告メッセージが表示されます] をクリックして**はい**します。  
  
3.  サーバー マネージャー ダッシュ ボードで、をクリックして**管理**、] をクリックし、**追加の役割と機能**します。  
  
4.  追加の役割と機能のウィザードには、次の操作を行います。  
  
    1.  **インストールの種類**] ページで [**役割ベースまたは機能ベースのインストール**します。  
  
    2.  **サーバーの選択] ページ**(または**対象サーバーの選択**Windows Server Essentials でのページ)、] をクリックして**サーバー プールからサーバーを選択**します。  
  
    3.  **機能**] ページで、展開**リモート サーバー管理ツール (インストール済み)**、展開**リモート アクセス管理ツール (インストール済み)**、展開**役割管理ツール (インストール済み)**、展開**リモート アクセス管理ツール**、し、[**リモート アクセス GUI ツールとコマンド ライン ツール**します。  
  
    4.  ウィザードを完了するための手順に従います。  
  
##  <a name="BKMK_AddStaticIP"></a>手順 2: サーバーのネットワーク アダプターのアドレスを静的 IP アドレスに変更します。  
 DirectAccess では、静的 IP アドレスを持つアダプターが必要です。 サーバー上のローカル ネットワーク アダプターの IP アドレスを変更する必要があります。  
  
#### <a name="to-add-a-static-ip-address"></a>静的 IP アドレスを追加するには  
  
1.  [開始] ページで、開く**コントロール パネルの [**します。  
  
2.  をクリックして**ネットワークとインターネット**、] をクリックし、**ネットワークの状態とタスクを表示**します。  
  
3.  [タスク] ウィンドウで、**ネットワークと共有センター**、] をクリックして**アダプター設定を変更する**します。  
  
4.  ローカル ネットワーク アダプターを右クリックし、をクリックして**プロパティ**します。  
  
5.  **ネットワーク**] タブ、[**インターネット プロトコル バージョン 4 (Tcp/ipv4)**、] をクリックし、**プロパティ**します。  
  
6.  **全般**] タブ、[**次の IP アドレスを使用して**、し、使用する IP アドレスを入力します。  
  
     サブネット マスクの既定値が自動的に表示されます、**サブネット マスク**ボックス。 既定値はそのまま使用するか、使用するサブネット マスクの値を入力します。  
  
7.  **デフォルト ゲートウェイ**ボックス、デフォルト ゲートウェイの IP アドレスを入力します。  
  
8.  **優先 DNS サーバー**ボックスに、DNS サーバーの IP アドレスを入力します。  
  
    > [!NOTE]
    >  ループバック ネットワーク (127.0.0.1 など) ではなく (たとえば「192.168.x.x」) を DHCP によってネットワーク アダプターに割り当てられている IP アドレスを使用します。 割り当てられた IP アドレスを調べるには、実行**ipconfig**コマンド プロンプトでします。  
  
9. **代替 DNS サーバー**ボックスに、存在する場合、代替の DNS サーバーの IP アドレスを入力します。  
  
10. をクリックして**OK**、] をクリックし、**閉じる**します。  
  
> [!IMPORTANT]
>  前方のポート 80 および 443 をサーバーの新しい静的 IP アドレスにルーターを構成することを確認します。  
  
##  <a name="BKMK_DNS"></a>手順 3: ネットワーク ロケーション サーバーの証明書と DNS レコードを準備します。  
 ネットワーク ロケーション サーバーの証明書と DNS レコードを準備するのには、次のタスクを実行します。  
  
-   [手順 3 a: Web サーバー証明書テンプレートの完全なアクセス許可を Authenticated Users に付与](#BKMK_GrantFullPermissions)  
  
-   [手順 3 b: 外部ネットワークからは解決できない共通名で、ネットワーク ロケーション サーバー用の証明書の登録](#BKMK_EnrollaCertificate)  
  
-   [手順 3 c: DNS サーバーに新しいホストを追加して、Windows Server Essentials サーバー アドレスにマップします。](#BKMK_MapNewHosttoServerAddress)  
  
###  <a name="BKMK_GrantFullPermissions"></a>手順 3 a: Web サーバー証明書テンプレートの完全なアクセス許可を Authenticated Users に付与  
 最初のタスクでは、証明機関で Web サーバーの証明書テンプレートのユーザーを認証する完全なアクセス許可を付与します。  
  
####  <a name="BKMK_ToGrantFullPermissions"></a>フル アクセス許可を与える Authenticated Users、Web サーバーの証明書テンプレートの s  
  
1.  **開始**] ページで、開く**証明機関**します。  
  
2.  コンソール ツリーで、下にある**証明機関 (ローカル)**、展開**< servername\ >-CA**、右クリック**証明書テンプレート**、] をクリックし、**管理**します。  
  
3.  **証明機関 (ローカル)**、右クリックして**Web サーバー**、] をクリックし、**プロパティ**します。  
  
4.  [Web サーバーのプロパティ] で、**セキュリティ**] タブで、をクリックして**Authenticated Users**を選択**フル コントロール**、] をクリックし、 **[ok]**します。  
  
5.  再起動**Active Directory 証明書サービス**します。 コントロール パネルで、開く**ローカル サービスの表示**します。 サービスの一覧で、右クリックして**Active Directory Certificate Services**、] をクリックし、**再起動**します。  
  
###  <a name="BKMK_EnrollaCertificate"></a>手順 3 b: 外部ネットワークからは解決できない共通名で、ネットワーク ロケーション サーバー用の証明書の登録  
 次に、外部ネットワークからは解決できない共通名で、ネットワーク ロケーション サーバー用の証明書を登録します。  
  
####  <a name="BKMK_ToEnrollaCertificate"></a>ネットワーク ロケーション サーバー用の証明書を登録するには  
  
1.  **開始**] ページで、開く**mmc** (Microsoft 管理コンソール)。  
  
2.  場合、**ユーザー アカウント制御**警告メッセージが表示されたら、] をクリックして**はい**します。  
  
     Microsoft 管理コンソール (MMC) を開きます。  
  
3.  **ファイル**] メニューのをクリックして**スナップインの追加/削除**します。  
  
4.  **リモート スナップインの追加と**ボックスで、をクリックして**証明書**、] をクリックし、**追加**します。  
  
5.  **証明書スナップイン**] ページで [**コンピューター アカウント**、] をクリックし、 **[次へ]**します。  
  
6.  **コンピューターの選択**] ページで [**ローカル コンピューター**、] をクリックして**完了**、] をクリックし、 **[ok]**します。  
  
7.  コンソール ツリーで、展開**証明書 (ローカル コンピュータ)**、展開**個人**、右クリック**証明書**、[**すべてのタスク**、] をクリックして**新しい証明書の要求**します。  
  
8.  証明書の登録ウィザードが表示されたら、] をクリックして**次**します。  
  
9. **証明書登録ポリシーの選択**] ページで [**次**します。  
  
10. **証明書の要求**] ページで、[、 **Web サーバー**チェック ボックスをオンし、**の詳細については、この証明書を登録するために必要な**します。  
  
11. **証明書のプロパティ**ボックスで、次の設定の入力**サブジェクト名**:  
  
    1.  **種類**[**共通名**します。  
  
    2.  **値**(たとえば、Directaccess-nls.contoso.local」)、ネットワーク ロケーション サーバーの名前を入力し、[クリックして**追加**します。  
  
    3.  をクリックして**OK**、] をクリックし、**登録**します。  
  
12. 証明書の登録が完了したら、クリックして**完了**します。  
  
###  <a name="BKMK_MapNewHosttoServerAddress"></a>手順 3 c: DNS サーバーに新しいホストを追加して、Windows Server Essentials サーバー アドレスにマップします。  
 DNS 構成を完了するには、DNS サーバーに新しいホストを追加し、Windows Server Essentials サーバー アドレスにマップします。  
  
####  <a name="BKMK_ToMapNewHosttoServerAddress"></a>Windows Server Essentials サーバー アドレスに新しいホストにマップ  
  
1.  [開始] ページで、DNS マネージャーを開きます。 DNS マネージャーを開くには、検索**dnsmgmt.msc**、] をクリックし、 **dnsmgmt.msc**結果にします。  
  
2.  DNS マネージャー コンソール ツリーで、ローカル サーバーを展開し、**前方参照ゾーン**サーバー ドメインのサフィックスを持つゾーンを右クリックし、[クリックして**新しいホスト (A または AAAA)**します。  
  
3.  名前 (Directaccess-nls.contoso.local など) のサーバーの IP アドレスと対応するサーバー アドレス (192.168.x.x など) を入力します。  
  
4.  をクリックして**ホストの追加**、] をクリックして**OK**、] をクリックし、**完了**します。  
  
##  <a name="BKMK_AddSecurityGroup"></a>手順 4: DirectAccess クライアント コンピューターのセキュリティ グループを作成します。  
 次に、DirectAccess クライアント コンピューターを使用するセキュリティ グループを作成し、グループにコンピューター アカウントを追加します。  
  
#### <a name="to-add-a-security-group-for-client-computers-that-use-directaccess"></a>DirectAccess を使用するクライアント コンピューターのセキュリティ グループを追加するには  
  
1.  サーバー マネージャー ダッシュ ボードで、をクリックして**ツール**、] をクリックし、 **Active Directory ユーザーとコンピューター**します。  
  
    > [!NOTE]
    >  表示されない場合**Active Directory ユーザーとコンピューター**上、**ツール**] メニューの [機能をインストールする必要があります。 Active Directory ユーザーとグループをインストールするには、管理者として、次の Windows PowerShell コマンドレットを実行します。`Install-WindowsFeature RSAT-ADDS-Tools`します。 詳細については、次を参照してください。[インストールまたはリモート サーバー管理ツール パックを削除する](https://technet.microsoft.com/library/cc730825.aspx)します。  
  
2.  コンソール ツリーで、サーバーを展開し、右クリックして**ユーザー**、] をクリックして**新規**、] をクリックし、**グループ**します。  
  
3.  グループ名を入力し、グループのスコープ、およびグループの種類 (セキュリティ グループを作成)、] をクリックし、 **OK**します。  
  
 新しいセキュリティ グループに追加されて、**ユーザー**フォルダー。  
  
#### <a name="to-add-computer-accounts-to-the-security-group"></a>セキュリティ グループにコンピューター アカウントを追加するには  
  
1.  サーバー マネージャー ダッシュ ボードで、をクリックして**ツール**、] をクリックし、 **Active Directory ユーザーとコンピューター**します。  
  
2.  コンソール ツリーで、サーバーを展開し、をクリックして**ユーザー**します。  
  
3.  ユーザー アカウントと、サーバー上のセキュリティ グループの一覧で、DirectAccess 用に作成したセキュリティ グループを右クリックし、をクリックして**プロパティ**します。  
  
4.  **メンバー** ] タブ、[**追加**します。  
  
5.  ダイアログ ボックスでは、セミコロン (;) で区切って、グループに追加するコンピューター アカウントの名前を入力します。 をクリックして**名前の確認**します。  
  
6.  コンピューター アカウントが検証されたら、クリックして**OK**します。 をクリックして**OK**もう一度します。  
  
> [!NOTE]
>  使用することも、**のメンバー** ] タブの [セキュリティ グループにアカウントを追加するコンピューター アカウントのプロパティ。  
  
##  <a name="BKMK_EnableConfigureDA"></a>手順 5: 有効にして DirectAccess を構成します。  
 有効にし、Windows Server Essentials での DirectAccess の構成には、次の手順を実行する必要があります。  
  
-   [ステップ 5 a: リモート アクセス管理コンソールを使用して DirectAccess を有効にします。](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableDA)  
  
-   [手順 5b: RRAS GPO (Windows Server Essentials のみ) から、無効な IPv6Prefix を削除します。](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_RemoveIPv6)  
  
-   [手順 5c:windows: DirectAccess を使用する Windows 7 Enterprise を実行しているクライアント コンピューターを有効にします。](#BKMK_Step4cWindows7Setup)  
  
-   [手順 5 d: ネットワーク ロケーション サーバーを構成します。](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NLS)  
  
-   [手順 5e:ipsec: IPsec チャネルを確立するときに CA 証明書をバイパスするレジストリ キーを追加](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_CA)  
  
###  <a name="BKMK_EnableDA"></a>ステップ 5 a: リモート アクセス管理コンソールを使用して DirectAccess を有効にします。  
 ここでは、Windows Server Essentials で DirectAccess を有効にするための手順を説明します。 構成していない VPN サーバーにまだ場合、行う必要がありますをこの手順を開始する前にします。 手順については、次を参照してください。 [VPN の管理](Manage-VPN-in-Windows-Server-Essentials.md)します。  
  
##### <a name="to-enable-directaccess-by-using-the-remote-access-management-console"></a>リモート アクセス管理コンソールを使用して DirectAccess を有効にするには  
  
1.  [開始] ページで、開く**リモート アクセス管理**します。  
  
2.  DirectAccess の有効化ウィザードでは、次の操作を行います。  
  
    1.  レビュー **DirectAccess の前提条件**、] をクリック**次**します。  
  
    2.  **グループの選択**タブ、DirectAccess クライアント用に作成したセキュリティ グループを追加します。 (セキュリティ グループを作成していない場合は、次を参照してください[手順 4: DirectAccess クライアントのセキュリティ グループにコンピューターを作成](#BKMK_AddSecurityGroup)手順についてはします。)。  
  
    3.  **グループの選択**] タブ、[**モバイル コンピューターのみに DirectAccess の有効化**モバイル コンピューターに DirectAccess を使用して、クリックして、サーバーにリモート アクセスを有効にする場合**[次へ]**します。  
  
    4.  **ネットワーク トポロジ**、サーバーのトポロジを選択し、[クリックして**次**します。  
  
    5.  **DNS サフィックス検索一覧**必要な場合、クライアント コンピューターの追加の DNS サフィックスを追加し、[クリックして**次**します。  
  
        > [!NOTE]
        >  既定では、DirectAccess の有効化ウィザードは既に現在のドメインの DNS サフィックスを追加します。 ただし、必要な場合の詳細を追加することができます。  
  
    6.  適用され、必要に応じて変更するグループ ポリシー オブジェクト (Gpo) を確認します。  
  
    7.  をクリックして**次**、] をクリックし、**完了**します。  
  
    8.  管理者特権モードで、次の Windows PowerShell コマンドを実行して、リモート アクセス管理サービスを再起動します。  
  
        ```powershell  
        Restart-Service RaMgmtSvc   
        ```  
  
###  <a name="BKMK_RemoveIPv6"></a>手順 5b: RRAS GPO (Windows Server Essentials のみ) から、無効な IPv6Prefix を削除します。  
  このセクションでは、Windows Server Essentials を実行しているサーバーに適用されます。  
  
 管理者として Windows PowerShell を開き、次のコマンドを実行します。  
  
```powershell  
gpupdate  
$key = Get-ChildItem -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\RemoteAccess\config\MachineSIDs | Where-Object{$_.GetValue("IPv6RrasPrefix") -ne $null}  
Remove-GPRegistryValue -Name "DirectAccess Server Settings" -Key $key.Name -ValueName IPv6RrasPrefix  
gpupdate  
```  
  
###  <a name="BKMK_Step4cWindows7Setup"></a>手順 5c:windows: DirectAccess を使用する Windows 7 Enterprise を実行しているクライアント コンピューターを有効にします。  
 Windows 7 Enterprise を実行しているクライアント コンピューターを使っている場合は、これらのコンピューターから DirectAccess を有効にするのには、次の手順を完了します。  
  
##### <a name="to-enable--windows-7-enterprise-computers-to-use-directaccess"></a>Windows 7 Enterprise 使用してコンピューターに DirectAccess を有効にするには  
  
1.  サーバーの開始] ページで、開く**リモート アクセス管理**します。  
  
2.  リモート アクセス管理コンソールで、をクリックして**構成**します。 その後、[、**セットアップの詳細**] ウィンドウで、**手順 2**、] をクリックして**編集**します。  
  
     リモート アクセス サーバーのセットアップ ウィザードが開きます。  
  
3.  **認証**] タブで、(Windows Server Essentials サーバーの CA 証明書を選択することができます) 信頼されたルート証明書となる証明機関 (CA) 証明書を選択します。 をクリックして**を有効にする Windows 7 クライアント コンピューターを DirectAccess 経由で接続を**、] をクリックし、**次**します。  
  
4.  ウィザードを完了するための手順に従います。  
  
> [!IMPORTANT]
>  Windows Server Essentials サーバーに UR1 がプレインストールされていなかった場合は、DirectAccess 経由で接続している Windows 7 Enterprise コンピューターの既知の問題があります。 環境での DirectAccess 接続を有効にするには、追加の手順を実行する必要があります。  
>   
>  1.  説明されている修正プログラムをインストール[Microsoft サポート技術情報 (KB) 記事 2796394](https://support.microsoft.com/kb/2796394) 、Windows Server Essentials サーバーにします。 サーバーを再起動します。  
> 2.  説明されている修正プログラムをインストールし、 [Microsoft サポート技術情報 (KB) 記事 2615847](https://support.microsoft.com/kb/2615847) Windows 7 コンピューターごとにします。  
>   
>      この問題は、Windows Server Essentials で解決されました。  
  
###  <a name="BKMK_NLS"></a>手順 5 d: ネットワーク ロケーション サーバーを構成します。  
 ここでは、ネットワーク ロケーション サーバーの設定を構成する手順を説明します。  
  
> [!NOTE]
>  開始する前に、< SystemDrive\ > \inetpub\wwwroot フォルダーの内容を < SystemDrive\ > \Program Files\Windows server \bin\webapps\site\insideoutside フォルダーにコピーします。 < SystemDrive\ > \Program Files\Windows \bin\webapps\site フォルダーの default.aspx ファイルを < SystemDrive\ > \Program Files\Windows server \bin\webapps\site\insideoutside フォルダーにもコピーします。  
  
##### <a name="to-configure-the-network-location-server"></a>ネットワーク ロケーション サーバーを構成するには  
  
1.  [開始] ページで、開く**リモート アクセス管理**します。  
  
2.  リモート アクセス管理コンソールで、をクリックして**構成**、し、[、**リモート アクセスのセットアップ**詳細ウィンドウの [**手順 3**、] をクリックして**編集**します。  
  
3.  リモート アクセス サーバーのセットアップ ウィザードで上、**ネットワーク ロケーション サーバー** ] タブで、[**ネットワーク ロケーション サーバーがリモート アクセス サーバーに展開されている**、し、事前に発行した証明書を選択し、(で[手順 3: ネットワーク ロケーション サーバーの証明書と DNS レコードを準備する](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS))。  
  
4.  クリックして、ウィザードを完了するための指示に従って**完了**します。  
  
###  <a name="BKMK_CA"></a>手順 5e:ipsec: IPsec チャネルを確立するときに CA 証明書をバイパスするレジストリ キーを追加  
 次の手順では、IPsec チャネルが確立されているときに CA 証明書をバイパスするサーバーを構成します。  
  
##### <a name="to-add-a-registry-key-to-bypass-the-ca-certification"></a>CA 証明書をバイパスするレジストリ キーを追加するには  
  
1.  [開始] ページで、開く**regedit** (レジストリ エディター)。  
  
2.  レジストリ エディターで、展開**HKEY_LOCAL_MACHINE**、展開**システム**、展開**CurrentControlSet**、展開**サービス**、展開と**IKEEXT**します。  
  
3.  下にある**IKEEXT**、右クリックして**パラメーター**、] をクリックして**新規**、] をクリックし、 **DWORD (32 ビット) 値**します。  
  
4.  新しく追加された値の名前を変更**ikeflags**します。  
  
5.  をダブルクリック**ikeflags**、設定、**種類**に**16 進**、値に設定します**8000**、] をクリックし、 **[ok]**します。  
  
> [!NOTE]
>  管理者特権モードで、次の Windows PowerShell コマンドを使用すると、このレジストリ キーを追加します。  
>   
>  `Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\IKEEXT\Parameters -Name ikeflags -Type DWORD -Value 0x8000`  
  
##  <a name="BKMK_NRPT"></a>手順 6: DirectAccess サーバーの名前解決ポリシー テーブル設定を構成します。  
 このセクションでは、DirectAccess クライアント Gpo で内部アドレス (例: contoso.local サフィックスを持つエントリ) の名前解決ポリシー テーブル (NPRT) エントリを編集する方法について説明し、IPHTTPS インターフェイス アドレスを設定します。  
  
#### <a name="to-configure-name-resolution-policy-table-entries"></a>名前解決ポリシー テーブル エントリを設定するには  
  
1.  [開始] ページで、開く**グループ ポリシーの管理**します。  
  
2.  グループ ポリシー管理コンソールで、既定のフォレストとドメインをクリックし、右クリック、 **DirectAccess クライアントの設定**、] をクリックし、**編集**します。  
  
3.  をクリックして**コンピューター構成**、] をクリックして**ポリシー**、] をクリックして**Windows 設定**、] をクリックし、**名前解決ポリシー**します。 DNS サフィックスに一致する名前空間を持つエントリを選択し、クリックして**規則の編集**します。  
  
4.  をクリックして、 **DirectAccess の DNS 設定**タブ。選択し、**この規則で directaccess を有効にする DNS 設定**します。 DNS サーバーの一覧で、IP-HTTPS インターフェイスの IPv6 アドレスを追加します。  
  
    > [!NOTE]
    >  次の Windows PowerShell コマンドを使用すると、IPv6 アドレスを取得します。  
    >   
    >  `(Get-NetIPInterface -InterfaceAlias IPHTTPSInterface | Get-NetIPAddress -PrefixLength 128)[1].IPAddress`  
  
##  <a name="BKMK_TCPUDP"></a>手順 7: DirectAccess サーバー Gpo の TCP および UDP のファイアウォール規則を構成します。  
 このセクションでは、DirectAccess サーバー Gpo の TCP および UDP のファイアウォール規則を構成する手順を説明します。  
  
#### <a name="to-configure-firewall-rules"></a>ファイアウォール規則を構成するには  
  
1.  [開始] ページで、開く**グループ ポリシーの管理**します。  
  
2.  グループ ポリシー管理コンソールで、既定のフォレストとドメインをクリックし、右クリック、 **DirectAccess サーバーの設定**、] をクリックし、**編集**します。  
  
3.  をクリックして**コンピューターの構成**、] をクリックして**ポリシー**、] をクリックして**Windows 設定**、] をクリックして**セキュリティ設定**、] をクリックして**セキュリティが強化された Windows ファイアウォール**、レベルが [次へ] をクリックして**セキュリティが強化された Windows ファイアウォール**、] をクリックし、**受信の規則**します。 右クリック**ドメイン名のサーバー (TCP 受信)**、] をクリックし、**プロパティ**します。  
  
4.  をクリックして、**スコープ**] タブとで、**ローカル IP アドレス**一覧で、IP-HTTPS インターフェイスの IPv6 アドレスを追加します。  
  
5.  同じ手順を繰り返して**(UDP で) のドメイン ネーム サーバー**します。  
  
##  <a name="BKMK_DNS64"></a>手順 8: IP-HTTPS インターフェイスをリッスンするように DNS64 の構成を変更します。  
 次の Windows PowerShell コマンドを使用して、IP-HTTPS インターフェイスをリッスンするように DNS64 の構成を変更する必要があります。  
  
```powershell  
Set-NetDnsTransitionConfiguration  �AcceptInterface IPHTTPSInterface  
```  
  
##  <a name="BKMK_ExemptPort"></a>手順 9: WinNat サービス用にポートを予約します。  
 WinNat サービス用にポートを予約するのにには、次の Windows PowerShell コマンドを使用します。 「192.168.1.100」は、Windows Server Essentials サーバーの実際の IPv4 アドレスに置き換えます。  
  
```powershell  
Set-NetNatTransitionConfiguration  �IPv4AddressPortPool @("192.168.1.100, 10000-47000")  
```  
  
> [!IMPORTANT]
>  アプリケーションとポートの競合を避けるために、WinNat サービス用に予約するポートの範囲にポート 6602 が含まれていないことを確認します。  
  
##  <a name="BKMK_WinNAT"></a>手順 10: WinNat サービスを再起動します。  
 次の Windows PowerShell コマンドを実行して、Windows NAT ドライバー (WinNat) サービスを再起動します。  
  
```powershell  
Restart-Service winnat  
```  
  
##  <a name="BKMK_AppendixBPowerShellScript"></a>付録: Windows PowerShell を使用して DirectAccess のセットアップ  
 このセクションでは、セットアップして Windows PowerShell を使用して DirectAccess を構成する方法について説明します。  
  
### <a name="preparation"></a>準備  
 DirectAccess 用にサーバーの構成を開始する前に、次の操作を行う必要があります。  
  
1.  」の手順に従って[手順 3: ネットワーク ロケーション サーバーの証明書と DNS レコードを準備する](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS)という名前の証明書を登録する**Directaccess-nls.contoso.com** (ここで**contoso.com**実際の内部ドメイン名に置き換えられます)、およびネットワーク ロケーション サーバー (NLS) の DNS レコードを追加します。  
  
2.  という名前のセキュリティ グループを追加**DirectAccessClients** Active Directory にし、DirectAccess 機能を提供するクライアント コンピューターを追加します。 詳細については、次を参照してください。[手順 4: DirectAccess クライアントのセキュリティ グループにコンピューターを作成](#BKMK_AddSecurityGroup)します。  
  
### <a name="commands"></a>コマンド  
  
> [!IMPORTANT]
>  Windows Server Essentials では、不要な IPv6 プレフィックスの GPO を削除する必要はありません。 次のラベルのコード セクションを削除します。`# [WINDOWS SERVER 2012 ESSENTIALS ONLY] Remove the unnecessary IPv6 prefix GPO`します。  
  
```powershell  
# Add Remote Access role if not installed yet  
$ra = Get-WindowsFeature RemoteAccess  
If ($ra.Installed -eq $FALSE) { Add-WindowsFeature RemoteAccess }  
  
# Server may need to restart if you installed RemoteAccess role in the above step  
  
# Set the internet domain name to access server, replace contoso.com below with your own domain name  
$InternetDomain = "www.contoso.com"  
#Set the SG name which you create for DA clients  
$DaSecurityGroup = "DirectAccessClients"  
#Set the internal domain name  
$InternalDomain = [System.DirectoryServices.ActiveDirectory.Domain]::GetCurrentDomain().Name  
  
# Set static IP and DNS settings  
$NetConfig = Get-WmiObject Win32_NetworkAdapterConfiguration -Filter "IPEnabled=$true"  
$CurrentIP = $NetConfig.IPAddress[0]  
$SubnetMask = $NetConfig.IPSubnet | Where-Object{$_ -like "*.*.*.*"}  
$NetConfig.EnableStatic($CurrentIP, $SubnetMask)  
$NetConfig.SetGateways($NetConfig.DefaultIPGateway)  
$NetConfig.SetDNSServerSearchOrder($CurrentIP)  
  
# Get physical adapter name and the certificate for NLS server  
$Adapter = (Get-WmiObject -Class Win32_NetworkAdapter -Filter "NetEnabled=$true").NetConnectionId  
$Certs = dir cert:\LocalMachine\My  
$nlscert = $certs | Where-Object{$_.Subject -like "*CN=DirectAccess-NLS*"}  
  
# Add regkey to bypass CA cert for IPsec authentication  
Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\IKEEXT\Parameters -Name ikeflags -Type DWORD -Value 0x8000  
  
# Install DirectAccess.   
Install-RemoteAccess -NoPrerequisite -DAInstallType FullInstall -InternetInterface $Adapter -InternalInterface $Adapter -ConnectToAddress $InternetDomain -nlscertificate $nlscert -force  
  
#Restart Remote Access Management service  
Restart-Service RaMgmtSvc  
  
# [WINDOWS SERVER 2012 ESSENTIALS ONLY] Remove the unnecessary IPv6 prefix GPO   
  
gpupdate  
$key = Get-ChildItem -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\RemoteAccess\config\MachineSIDs | Where-Object{$_.GetValue("IPv6RrasPrefix") -ne $null}  
Remove-GPRegistryValue -Name "DirectAccess Server Settings" -Key $key.Name -ValueName IPv6RrasPrefix  
gpupdate  
  
# Enable client computers running Windows 7 to use DirectAccess  
$allcertsinroot = dir cert:\LocalMachine\root  
$rootcert = $allcertsinroot | Where-Object{$_.Subject -like "*-CAA*"}  
Set-DAServer  �IPSecRootCertificate $rootcert[0]  
Set  �DAClient  �OnlyRemoteComputers Disabled -Downlevel Enabled  
  
#Set the appropriate security group used for DA client computers. Replace the group name below with the one you created for DA clients  
Add-DAClient -SecurityGroupNameList $DaSecurityGroup   
Remove-DAClient -SecurityGroupNameList "Domain Computers"  
  
# Gather DNS64 IP address information  
$Remoteaccess = get-remoteaccess  
$IPinterface = get-netipinterface -InterfaceAlias IPHTTPSInterface | get-netipaddress -PrefixLength 128  
$DNS64IP=$IPInterface[1].IPaddress  
$Natconfig = Get-NetNatTransitionConfiguration  
  
# Configure TCP and UDP firewall rules for the DirectAccess server GPO  
$GpoName = 'GPO:'+$InternalDomain+'\DirectAccess Server Settings'  
Get-NetFirewallRule -PolicyStore $GpoName -Displayname "Domain Name Server (TCP-IN)"|Get-NetFirewallAddressFilter | Set-NetFirewallAddressFilter -LocalAddress $DNS64IP  
Get-NetFirewallrule -PolicyStore $GpoName -Displayname "Domain Name Server (UDP-IN)"|Get-NetFirewallAddressFilter | Set-NetFirewallAddressFilter -LocalAddress $DNS64IP  
  
# Configure the name resolution policy settings for the DirectAccess server, replace the DNS suffix below with the one in your domain  
$Suffix = '.' + $InternalDomain  
set-daclientdnsconfiguration -DNSsuffix $Suffix -DNSIPAddress $DNS64IP  
  
# Change the DNS64 configuration to listen to IP-HTTPS interface  
Set-NetDnsTransitionConfiguration -AcceptInterface IPHTTPSInterface  
  
# Copy the necessary files to NLS site folder  
XCOPY 'C:\inetpub\wwwroot' 'C:\Program Files\Windows Server\Bin\WebApps\Site\insideoutside' /E /Y  
XCOPY 'C:\Program Files\Windows Server\Bin\WebApps\Site\Default.aspx' 'C:\Program Files\Windows Server\Bin\WebApps\Site\insideoutside' /Y  
  
# Reserve ports for the WinNat service  
Set-NetNatTransitionConfiguration  �IPv4AddressPortPool @("192.168.1.100, 10000-47000")  
  
# Restart the WinNat service  
Restart-Service winnat  
```  
  
## <a name="see-also"></a>参照してください。  
  
-   [Anywhere Access を管理します。](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Windows Server Essentials を管理します。](Manage-Windows-Server-Essentials.md)
