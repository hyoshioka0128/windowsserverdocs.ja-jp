---
title: Windows Server Essentials での DirectAccess の構成
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: c959b6fc-c67e-46cd-a9cb-cee71a42fa4c
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: a9ebd7af7f748a1e2af4a47ca5b590137cd33b3d
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85470907"
---
# <a name="configure-directaccess-in-windows-server-essentials"></a>Windows Server Essentials での DirectAccess の構成

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

このトピックでは、Windows Server Essentials で DirectAccess を構成する手順について説明します。これにより、モバイルユーザーは、仮想プライベートネットワーク (VPN) 接続を確立せずに、インターネットに接続された任意のリモートの場所から組織のネットワークにシームレスに接続できるようになります。 DirectAccess では、Windows 8.1、Windows 8、および Windows 7 コンピューターから、オフィス内外で同じ接続エクスペリエンスをモバイルワーカーに提供できます。

 Windows Server Essentials で、ドメインに複数の Windows Server Essentials サーバーが含まれている場合は、ドメインコントローラーで DirectAccess を構成する必要があります。

> [!NOTE]
>  このトピックでは、Windows Server Essentials サーバーがドメインコントローラーである場合に DirectAccess を構成する手順について説明します。 Windows Server Essentials サーバーがドメインメンバーの場合は、「[既存のリモートアクセス (VPN) 展開に directaccess を追加](https://technet.microsoft.com/library/jj574220.aspx)する」のドメインメンバーで directaccess を構成する手順に従います。

## <a name="process-overview"></a>プロセスの概要
 Windows Server Essentials で DirectAccess を構成するには、次の手順を実行します。

> [!IMPORTANT]
>  このガイドの手順を使用して Windows Server Essentials で DirectAccess を構成する前に、サーバー上で VPN を有効にする必要があります。 手順については、「 [VPN の管理](Manage-VPN-in-Windows-Server-Essentials.md)」を参照してください。

-   [手順 1:サーバーにリモート アクセス管理ツールを追加する](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_AddRAM)

-   [手順 2:サーバーのネットワーク アダプター アドレスを静的 IP アドレスに変更する](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_AddStaticIP)

-   [手順 3:ネットワーク ロケーション サーバーの証明書と DNS レコードを準備する](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS)

    -   [手順 3a: 認証されたユーザーに Web サーバーの証明書テンプレートの完全なアクセス許可を付与する](#BKMK_GrantFullPermissions)

    -   [手順 3b:外部ネットワークからは解決できない共通名を使用して、ネットワーク ロケーション サーバーの証明書を登録する](#BKMK_EnrollaCertificate)

    -   [手順 3c:DNS サーバーに新しいホストを追加し、Windows Server Essentials サーバー アドレスにマップする](#BKMK_MapNewHosttoServerAddress)

-   [手順 4:DirectAccess クライアント コンピューターのセキュリティ グループを作成する](#BKMK_AddSecurityGroup)

-   [手順 5:DirectAccess を有効にして構成する](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableConfigureDA)

    -   [手順 5a:リモート アクセス管理コンソールを使用して DirectAccess を有効にする](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableDA)

    -   [手順 5b: RRAS GPO の無効な IPv6Prefix を削除する (Windows Server Essentials のみ)](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_RemoveIPv6)

    -   [手順 5c:Windows 7 Enterprise を実行しているクライアント コンピューターが DirectAccess を使用できるようにする](#BKMK_Step4cWindows7Setup)

    -   [手順 5d:ネットワーク ロケーション サーバーを構成する](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NLS)

    -   [手順 5e:IPsec チャネルを確立するときに CA 証明書をバイパスするレジストリ キーを追加する](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_CA)

-   [手順 6:DirectAccess サーバーの名前解決ポリシー テーブル設定を構成する](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NRPT)

-   [手順 7:DirectAccess サーバーの GPO で TCP および UDP のファイアウォール規則を構成する](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_TCPUDP)

-   [手順 8:DNS64 の構成を変更して IP-HTTPS インターフェイスをリッスンする](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS64)

-   [手順 9:WinNat サービス用にポートを予約する](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_ExemptPort)

-   [手順 10:WinNat サービスを再起動する](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_WinNAT)

> [!NOTE]
>  [付録:Windows PowerShell を使用して DirectAccess をセットアップする](#BKMK_AppendixBPowerShellScript) では、DirectAccess セットアップを実行するために使用できる Windows PowerShell スクリプトを提供します。

##  <a name="step-1-add-remote-access-management-tools-to-your-server"></a><a name="BKMK_AddRAM"></a>手順 1: サーバーにリモートアクセス管理ツールを追加する

#### <a name="to-add-remote-accregss-management-tools--reg"></a>リモートの Acc 管理ツールを追加するには &reg;&reg;

1.  サーバーで、スタート ページの左下隅にある [**サーバー マネージャー**] アイコンをクリックします。

     Windows Server Essentials では、サーバーマネージャーを検索して開く必要があります。 スタート ページで、「**Server Manager**」と入力して、検索結果の [**サーバー マネージャー**] をクリックします。 サーバー マネージャーをスタート ページにピン留めするには、検索結果のサーバー マネージャーを右クリックして、[**スタートにピン留め**] をクリックします。

2.  **ユーザー アカウント制御**の警告メッセージが表示されたら、**[はい]** をクリックします。

3.  サーバー マネージャー ダッシュボードで、[**管理**] をクリックし、[**役割と機能の追加**] をクリックします。

4.  役割と機能の追加ウィザードで、次の操作を行います。

    1.  **[インストールの種類]** ページで、**[役割ベースまたは機能ベースのインストール]** をクリックします。

    2.  [**サーバーの選択] ページ**(または Windows Server Essentials の [**対象サーバーの選択**] ページ) で、[サーバー**プールからサーバーを選択**] をクリックします。

    3.  [**機能**] ページで、[**リモート サーバー管理ツール**] (インストール済み) を展開し、[**リモート アクセス管理ツール**] (インストール済み) を展開し、[**役割管理ツール**] (インストール済み) を展開し、[**リモート アクセス管理ツール**] を展開して、[**リモート アクセス GUI ツールとコマンド ライン ツール**] を選択します。

    4.  指示に従ってウィザードを完了します。

##  <a name="step-2-change-the-network-adapter-address-of-the-server-to-a-static-ip-address"></a><a name="BKMK_AddStaticIP"></a>手順 2: サーバーのネットワークアダプターアドレスを静的 IP アドレスに変更する
 DirectAccess では、静的 IP アドレスを持つアダプターが必要です。 このため、サーバーのローカル ネットワーク アダプターの IP アドレスを変更する必要があります。

#### <a name="to-add-a-static-ip-address"></a>静的 IP アドレスを追加するには

1.  スタート ページで [**コントロール パネル**] を開きます。

2.  **[ネットワークとインターネット]** をクリックし、**[ネットワークの状態とタスクの表示]** をクリックします。

3.  **[ネットワークと共有センター]** の作業ウィンドウで、**[アダプターの設定の変更]** をクリックします。

4.  ローカル ネットワーク アダプターを右クリックし、**[プロパティ]** をクリックします。

5.  **[ネットワーク]** タブで、**[インターネット プロトコル バージョン 4 (TCP/IPv4)]** をクリックし、**[プロパティ]** をクリックします。

6.  **[全般]** タブで、**[次の IP アドレスを使う]** をクリックし、使用する IP アドレスを入力します。

     **[サブネット マスク]** ボックスに、サブネット マスクの既定値が自動的に入力されます。 既定値をそのまま使用するか、使用するサブネット マスクの値を入力します。

7.  **[デフォルト ゲートウェイ]** ボックスに、デフォルト ゲートウェイの IP アドレスを入力します。

8.  **[優先 DNS サーバー]** ボックスに、DNS サーバーの IP アドレスを入力します。

    > [!NOTE]
    >  ループバック ネットワーク (127.0.0.1 など) ではなく、DHCP によってネットワーク アダプターに割り当てられた IP アドレス (192.168.X.X など) を使用します。 割り当てられた IP アドレスを検索するには、コマンド プロンプトで **ipconfig** を実行します。

9. 代替 DNS サーバーがある場合は、**[代替 DNS サーバー]** ボックスにその IP アドレスを入力します。

10. **[OK]** をクリックし、**[閉じる]** をクリックします。

> [!IMPORTANT]
>  ルーターの構成で、ポート 80 および 443 をルーターの新しい静的 IP アドレスに転送していることを確認してください。

##  <a name="step-3-prepare-a-certificate-and-dns-record-for-the-network-location-server"></a><a name="BKMK_DNS"></a>手順 3: ネットワークロケーションサーバーの証明書と DNS レコードを準備する
 ネットワーク ロケーション サーバーの証明書と DNS レコードを準備をするには、次のタスクを実行します。

-   [手順 3a: 認証されたユーザーに Web サーバーの証明書テンプレートの完全なアクセス許可を付与する](#BKMK_GrantFullPermissions)

-   [手順 3b:外部ネットワークからは解決できない共通名を使用して、ネットワーク ロケーション サーバーの証明書を登録する](#BKMK_EnrollaCertificate)

-   [手順 3c: DNS サーバーに新しいホストを追加し、それを Windows Server Essentials サーバーアドレスにマップします。](#BKMK_MapNewHosttoServerAddress)

###  <a name="step-3a-grant-full-permissions-to-authenticated-users-for-the-web-servers-certificate-template"></a><a name="BKMK_GrantFullPermissions"></a>手順 3a: 認証されたユーザーに Web サーバーの証明書テンプレートの完全なアクセス許可を付与する
 最初のタスクでは、証明機関の Web サーバーの証明書テンプレートに対してユーザーを認証するための完全なアクセス許可を付与します。

####  <a name="to-grant-full-permissions-to-authenticated-users-for-the-web-servers-certificate-template"></a><a name="BKMK_ToGrantFullPermissions"></a>認証されたユーザーに Web サーバーの証明書テンプレートの完全なアクセス許可を付与するには

1.  [**スタート**] ページで、[**証明機関**] を開きます。

2.  コンソールツリーの [**証明機関 (ローカル)**] で、[ **<servername \> -CA**] を展開し、[**証明書テンプレート**] を右クリックして、[**管理**] をクリックします。

3.  [**証明機関 (ローカル)**] で、[**Web サーバー**] を右クリックして、[**プロパティ**] をクリックします。

4.  Web サーバー プロパティの [**セキュリティ**] タブで、[**Authenticated Users**] をクリックし、[**フル コントロール**] を選択して、[**OK**] をクリックします。

5.  [**Active Directory 証明書サービス**] を再起動します。 コントロール パネルで、[**ローカル サービスの表示**] を開きます。 サービスの一覧で、[**Active Directory 証明書サービス**] を右クリックして、[**再起動**] をクリックします。

###  <a name="step-3b-enroll-a-certificate-for-the-network-location-server-with-a-common-name-that-is-unresolvable-from-the-external-network"></a><a name="BKMK_EnrollaCertificate"></a>手順 3b: 外部ネットワークから解決できない共通名を使用して、ネットワークロケーションサーバーの証明書を登録する
 次に、外部ネットワークからは解決できない共通名を使用して、ネットワーク ロケーション サーバーの証明書を登録します。

####  <a name="to-enroll-a-certificate-for-the-network-location-server"></a><a name="BKMK_ToEnrollaCertificate"></a>ネットワークロケーションサーバーの証明書を登録するには

1.  [**スタート**] ページで、[**MMC**] (Microsoft 管理コンソール) を開きます。

2.  **ユーザー アカウント制御**の警告メッセージが表示されたら、**[はい]** をクリックします。

     Microsoft 管理コンソール (MMC) が開きます。

3.  [**ファイル**] メニューで、[**スナップインの追加と削除**] をクリックします。

4.  [**スナップインの追加と削除**] ボックスで、[**証明書**] をクリックし、[**追加**] をクリックします。

5.  **[証明書スナップイン]** ページで、**[コンピューター アカウント]** をクリックし、**[次へ]** をクリックします。

6.  **[コンピューターの選択]** ページで、**[ローカル コンピューター]** をクリックし、**[完了]** をクリックします。次に、**[OK]** をクリックします。

7.  コンソール ツリーで、[**証明書 (ローカル コンピューター)**] を展開し、[**個人**] を展開し、[**証明書**] を右クリックして、[**すべてのタスク**] で [**新しい証明書の要求**] をクリックします。

8.  証明書の登録ウィザードが表示されたら、[**次へ**] をクリックします。

9. [**証明書の登録ポリシーの選択**] ページで、[**次へ**] をクリックします。

10. [**証明書の要求**] ページで、[**Web サーバー**] チェック ボックスをオンにして、[**この証明書を登録するにはもう少し情報が必要です**] をクリックします。

11. [**証明書のプロパティ**] ボックスで、[**サブジェクト名**] に次の設定を入力します。

    1.  [**種類**] に [**共通名**] を選択します。

    2.  [**値**] にネットワーク ロケーション サーバーの名前 (DirectAccess-NLS.contoso.local など) を入力し、[**追加**] をクリックします。

    3.  [**OK**] をクリックし、[**登録**] をクリックします。

12. 証明書の登録が完了したら、[**完了**] をクリックします。

###  <a name="step-3c-add-a-new-host-on-the-dns-server-and-map-it-to-the-windows-server-essentials-server-address"></a><a name="BKMK_MapNewHosttoServerAddress"></a>手順 3c: DNS サーバーに新しいホストを追加し、それを Windows Server Essentials サーバーアドレスにマップする
 DNS 構成を完了するには、DNS サーバーに新しいホストを追加し、Windows Server Essentials サーバーアドレスにマップします。

####  <a name="to-map-a-new-host-to-the-windows-server-essentials-server-address"></a><a name="BKMK_ToMapNewHosttoServerAddress"></a>新しいホストを Windows Server Essentials サーバーアドレスにマップするには

1.  スタート ページで DNS マネージャーを開きます。 DNS マネージャーを開くには、「 **dnsmgmt.msc**」を検索して、結果の [ **dnsmgmt.msc** ] をクリックします。

2.  DNS マネージャーコンソールツリーで、[ローカルサーバー]、[**前方参照ゾーン**] の順に展開し、サーバーのドメインサフィックスがあるゾーンを右クリックして、[**新しいホスト (A または AAAA)**] をクリックします。

3.  サーバーの名前と IP アドレス (たとえば「DirectAccess-NLS.contoso.local」)、および対応するサーバー アドレス (たとえば「192.168.x.x」) を入力します。

4.  [**ホストの追加**] をクリックし、[**OK**] をクリックして、[**完了**] をクリックします。

##  <a name="step-4-create-a-security-group-for-directaccess-client-computers"></a><a name="BKMK_AddSecurityGroup"></a>手順 4: DirectAccess クライアントコンピューターのセキュリティグループを作成する
 次に、DirectAccess クライアント コンピューターを使用するセキュリティ グループを作成し、コンピューター アカウントをグループに追加します。

#### <a name="to-add-a-security-group-for-client-computers-that-use-directaccess"></a>DirectAccess を使用するクライアント コンピューターにセキュリティ グループを追加するには

1. サーバー マネージャー ダッシュボードで、[**ツール**] をクリックし、[**Active Directory ユーザーとコンピューター**] をクリックします。

   > [!NOTE]
   >  [**ツール**] メニューに [**Active Directory ユーザーとコンピューター**] が表示されない場合は、この機能をインストールする必要があります。 Active Directory ユーザーとグループをインストールするには、管理者として次の Windows PowerShell コマンドレットを実行します。 `Install-WindowsFeature RSAT-ADDS-Tools` 詳細については、「 [リモート サーバー管理ツール パックのインストールまたは削除](https://technet.microsoft.com/library/cc730825.aspx)」を参照してください。

2. コンソール ツリーで、サーバーを展開して、[**ユーザー**] を右クリックし、[**新規**] をクリックし、[**グループ**] をクリックします。

3. グループ名、グループのスコープ、およびグループの種類を入力して (セキュリティ グループを作成)、[**OK**] をクリックします。

   新しいセキュリティ グループが [**ユーザー**] フォルダーに追加されます。

#### <a name="to-add-computer-accounts-to-the-security-group"></a>コンピューター アカウントをセキュリティ グループに追加するには

1.  サーバー マネージャー ダッシュボードで、[**ツール**] をクリックし、[**Active Directory ユーザーとコンピューター**] をクリックします。

2.  コンソール ツールで、サーバーを展開して [**ユーザー**] をクリックします。

3.  サーバーのユーザー アカウントとセキュリティ グループの一覧で、DirectAccess 用に作成したセキュリティ グループを右クリックして、[**プロパティ**] をクリックします。

4.  [**メンバー**] タブで [**追加**] をクリックします。

5.  ダイアログ ボックスで、グループに追加するコンピューター アカウントの名前をセミコロン (;) で区切って入力します。 次に [**名前の確認**] をクリックします。

6.  コンピューター アカウントが検証されたら、[**OK**] をクリックします。 もう一度、[**OK**] をクリックします。

> [!NOTE]
>  コンピューター アカウントのプロパティの [**メンバー**] タブを使用して、セキュリティ グループにアカウントを追加することもできます。

##  <a name="step-5-enable-and-configure-directaccess"></a><a name="BKMK_EnableConfigureDA"></a>手順 5: DirectAccess を有効にして構成する
 Windows Server Essentials で DirectAccess を有効にして構成するには、次の手順を完了する必要があります。

-   [手順 5a:リモート アクセス管理コンソールを使用して DirectAccess を有効にする](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_EnableDA)

-   [手順 5b: RRAS GPO の無効な IPv6Prefix を削除する (Windows Server Essentials のみ)](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_RemoveIPv6)

-   [手順 5c:Windows 7 Enterprise を実行しているクライアント コンピューターが DirectAccess を使用できるようにする](#BKMK_Step4cWindows7Setup)

-   [手順 5d:ネットワーク ロケーション サーバーを構成する](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_NLS)

-   [手順 5e:IPsec チャネルを確立するときに CA 証明書をバイパスするレジストリ キーを追加する](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_CA)

###  <a name="step-5a-enable-directaccess-by-using-the-remote-access-management-console"></a><a name="BKMK_EnableDA"></a>手順 5a: リモートアクセス管理コンソールを使用して DirectAccess を有効にする
 このセクションでは、Windows Server Essentials で DirectAccess を有効にする手順について説明します。 まだサーバー上で VPN を構成していない場合は、この手順を開始する前に構成する必要があります。 手順については、「 [VPN の管理](Manage-VPN-in-Windows-Server-Essentials.md)」を参照してください。

##### <a name="to-enable-directaccess-by-using-the-remote-access-management-console"></a>リモート アクセス管理コンソールを使用して DirectAccess を有効にするには

1.  スタート ページで、[**リモート アクセス管理**] を開きます。

2.  DirectAccess の有効化ウィザードで、次の操作を行います。

    1.  [**DirectAccess の前提条件**] を確認し、[**次へ**] をクリックします。

    2.  [**グループの選択**] タブで、DirectAccess クライアント用に先ほど作成したセキュリティ グループを追加します。 (セキュリティグループを作成していない場合は、「[手順 4: DirectAccess クライアントコンピューターのセキュリティグループを作成](#BKMK_AddSecurityGroup)する」を参照してください)。

    3.  モバイル コンピューターから DirectAccess を使用してサーバーにリモート アクセスできるようにする場合は、**[グループの選択]** タブで、**[モバイル コンピューターに対してのみ DirectAccess を有効にする]** をクリックします。**[次へ]** をクリックします。

    4.  **[ネットワーク トポロジ]** で、サーバーのトポロジを選択し、**[次へ]** をクリックします。

    5.  **[DNS サフィックス検索一覧]** で、必要に応じてクライアント コンピューターのために DNS サフィックスを追加し、**[次へ]** をクリックします。

        > [!NOTE]
        >  既定では、DirectAccess の有効化ウィザードによって既に現在のドメインの DNS サフィックスが追加されています。 必要に応じて他の DNS サフィックスを追加できます。

    6.  適用されるグループ ポリシー オブジェクト (GPO) を確認し、必要に応じて変更します。

    7.  **[次へ]** をクリックし、 **[完了]** をクリックします。

    8.  管理者特権モードで次の Windows PowerShell コマンドを実行して、リモート アクセス管理サービスを再起動します。

        ```powershell
        Restart-Service RaMgmtSvc
        ```

###  <a name="step-5b-remove-the-invalid-ipv6prefix-in-rras-gpo-windows-server-essentials-only"></a><a name="BKMK_RemoveIPv6"></a>手順 5b: RRAS GPO の無効な IPv6Prefix を削除する (Windows Server Essentials のみ)
  このセクションは、Windows Server Essentials を実行しているサーバーに適用されます。

 管理者として Windows PowerShell を開き、次のコマンドを実行します。

```powershell
gpupdate
$key = Get-ChildItem -Path HKLM:\SOFTWARE\Policies\Microsoft\Windows\RemoteAccess\config\MachineSIDs | Where-Object{$_.GetValue("IPv6RrasPrefix") -ne $null}
Remove-GPRegistryValue -Name "DirectAccess Server Settings" -Key $key.Name -ValueName IPv6RrasPrefix
gpupdate
```

###  <a name="step-5c-enable-client-computers-running-windows-7-enterprise-to-use-directaccess"></a><a name="BKMK_Step4cWindows7Setup"></a>手順 5c: Windows 7 Enterprise を実行しているクライアントコンピューターで DirectAccess を使用できるようにする
 Windows 7 Enterprise を実行しているクライアントコンピューターがある場合は、次の手順を実行して、これらのコンピューターから DirectAccess を有効にします。

##### <a name="to-enable--windows-7-enterprise-computers-to-use-directaccess"></a>Windows 7 Enterprise コンピューターで DirectAccess を使用できるようにするには

1.  サーバーのスタートページで、[**リモートアクセス管理**] を開きます。

2.  リモート アクセス管理コンソールで、[**構成**] をクリックします。 次に、[**設定の詳細**] ウィンドウの [**ステップ 2**] で、[**編集**] をクリックします。

     リモート アクセス サーバーのセットアップ ウィザードが開きます。

3.  [**認証**] タブで、信頼されたルート証明書となる証明機関 (ca) 証明書を選択します (Windows Server Essentials サーバーの ca 証明書を選択できます)。 [**Windows 7 クライアント コンピューターが DirectAccess を使用して接続できるようにする**] をクリックし、[**次へ**] をクリックします。

4.  指示に従ってウィザードを完了します。

> [!IMPORTANT]
>  Windows Server Essentials サーバーに UR1 がプレインストールされていない場合、DirectAccess 経由で接続している Windows 7 Enterprise コンピューターでは既知の問題があります。 この環境で DirectAccess 接続を有効にするには、次の追加の手順を実行する必要があります。
>
> 1. [Microsoft サポート技術情報 (KB) の記事 2796394](https://support.microsoft.com/kb/2796394)に記載されている修正プログラムを Windows Server Essentials サーバーにインストールします。 サーバーを再起動します。
>    2. 次に、 [Microsoft サポート技術情報 (KB) の記事 2615847](https://support.microsoft.com/kb/2615847)に記載されている修正プログラムを各 Windows 7 コンピューターにインストールします。
>
>    この問題は、Windows Server Essentials で解決されました。

###  <a name="step-5d-configure-the-network-location-server"></a><a name="BKMK_NLS"></a>手順 5d: ネットワークロケーションサーバーを構成する
 ここでは、ネットワーク ロケーション サーバーの設定を構成する手順について詳しく説明します。

> [!NOTE]
>  開始する前に、<SystemDrive \inetpub\wwwroot フォルダーの内容を \> <systemdrive \> Files\Windows Server\Bin\WebApps\Site\insideoutside フォルダーにコピーします。 また、default.aspx ファイルを <SystemDrive の \> Files\Windows Server\Bin\WebApps\Site フォルダーから <systemdrive/ \> Files\Windows Server\Bin\WebApps\Site\insideoutside フォルダーにコピーします。

##### <a name="to-configure-the-network-location-server"></a>ネットワーク ロケーション サーバーを構成するには

1.  スタート ページで、[**リモート アクセス管理**] を開きます。

2.  リモート アクセス管理コンソールで [**構成**] をクリックし、[**リモート アクセスのセットアップ**] 詳細ウィンドウの [**ステップ 3**] で、[**編集**] をクリックします。

3.  リモート アクセス サーバーのセットアップ ウィザードの **[ネットワーク ロケーション サーバー]** タブで、 **[ネットワーク ロケーション サーバーをリモート アクセス サーバー上に展開する]** を選択します。次に、事前に発行した証明書を選択します ( [Step 3: Prepare a certificate and DNS record for the network location server](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS))。

4.  指示に従ってウィザードを完了し、**[完了]** をクリックします。

###  <a name="step-5e-add-a-registry-key-to-bypass-ca-certification-when-you-establish-an-ipsec-channel"></a><a name="BKMK_CA"></a>手順 5e: IPsec チャネルを確立するときに CA 証明書をバイパスするレジストリキーを追加する
 次の手順では、IPsec チャネルが確立されたときに CA 証明書をバイパスするようサーバーを構成します。

##### <a name="to-add-a-registry-key-to-bypass-the-ca-certification"></a>CA 証明書をバイパスするレジストリ キーを追加するには

1.  スタート ページで、[**regedit**] (レジストリ エディター) を開きます。

2.  レジストリ エディターで、[**HKEY_LOCAL_MACHINE**] を展開し、[**システム**] を展開し、[**CurrentControlSet**] を展開し、[**サービス**] を展開し、[**IKEEXT**] を展開します。

3.  [**IKEEXT**] で [**パラメーター**] を右クリックし、[**新規**] をクリックし、[**DWORD (32 ビット) 値**] をクリックします。

4.  新しく追加された値の名前を「**ikeflags**」に変更します。

5.  [**ikeflags**] をダブルクリックして、[**種類**] に [**Hexadecimal**] を設定し、値に「**8000**」を設定して [**OK**] をクリックします。

> [!NOTE]
>  管理者特権モードで次の Windows PowerShell コマンドを使用し、このレジストリ キーを追加できます。
>
>  `Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Services\IKEEXT\Parameters -Name ikeflags -Type DWORD -Value 0x8000`

##  <a name="step-6-configure-name-resolution-policy-table-settings-for-the-directaccess-server"></a><a name="BKMK_NRPT"></a>手順 6: DirectAccess サーバーの名前解決ポリシーテーブル設定を構成する
 ここでは、DirectAccess クライアント GPO で内部アドレス (たとえば contoso.local サフィックスを持つエントリ) の名前解決ポリシー テーブル (NPRT) エントリを編集し、IPHTTPS インターフェイス アドレスを設定する手順について説明します。

#### <a name="to-configure-name-resolution-policy-table-entries"></a>名前解決ポリシー テーブル エントリを構成するには

1.  スタート ページで、[**グループ ポリシーの管理**] を開きます。

2.  グループ ポリシーの管理コンソールで、既定のフォレストとドメインをクリックし、[**DirectAccess クライアントの設定**] を右クリックして、[**編集**] をクリックします。

3.  [**コンピューターの構成**] をクリックし、[**ポリシー**]、[**Windows の設定**]、[**名前解決ポリシー**] の順にクリックします。 DNS サフィックスに一致する名前空間のエントリを選択し、**[規則の編集]** をクリックします。

4.  [**DirectAccess の DNS 設定**] タブをクリックし、[**この規則で DirectAccess の DNS 設定を有効にする**] をオンにします。 DNS サーバーの一覧に IP-HTTPS インターフェイスの IPv6 アドレスを追加します。

    > [!NOTE]
    >  IPv6 アドレスを取得するには、次の Windows PowerShell コマンドを使用できます。
    >
    >  `(Get-NetIPInterface -InterfaceAlias IPHTTPSInterface | Get-NetIPAddress -PrefixLength 128)[1].IPAddress`

##  <a name="step-7-configure-tcp-and-udp-firewall-rules-for-the-directaccess-server-gpos"></a><a name="BKMK_TCPUDP"></a>手順 7: DirectAccess サーバー Gpo の TCP および UDP ファイアウォール規則を構成する
 ここでは、DirectAccess サーバーの GPO で TCP および UDP のファイアウォール規則を構成する手順について詳しく説明します。

#### <a name="to-configure-firewall-rules"></a>ファイアウォール規則を構成するには

1.  スタート ページで、[**グループ ポリシーの管理**] を開きます。

2.  グループ ポリシーの管理コンソールで、既定のフォレストとドメインをクリックし、[**DirectAccess サーバーの設定**] を右クリックして、[**編集** ]をクリックします。

3.  [**コンピューターの構成**] をクリックし、[**ポリシー**]、[**Windows の設定**]、[**セキュリティの設定**]、[**セキュリティが強化された Windows ファイアウォール**] の順にクリックし、次のレベルの [**セキュリティが強化された Windows ファイアウォール**] をクリックして、[**受信の規則**] をクリックします。 **[ドメイン ネーム サーバー (TCP 受信)]** を右クリックし、**[プロパティ]** をクリックします。

4.  **[スコープ]** タブをクリックし、**[ローカル IP アドレス]** の一覧で、IP-HTTPS インターフェイスの IPv6 アドレスを追加します。

5.  **[ドメイン ネーム サーバー (UDP 受信)]** についても同じ手順を繰り返します。

##  <a name="step-8-change-the-dns64-configuration-to-listen-to-the-ip-https-interface"></a><a name="BKMK_DNS64"></a>手順 8: IP-HTTPS インターフェイスをリッスンするように DNS64 の構成を変更する
 DNS64 の構成を変更して、IP-HTTPS インターフェイスをリッスンするように設定する必要があります。これには、次の Windows PowerShell コマンドを使用します。

```powershell
Set-NetDnsTransitionConfiguration -AcceptInterface IPHTTPSInterface
```

##  <a name="step-9-reserve-ports-for-the-winnat-service"></a><a name="BKMK_ExemptPort"></a>手順 9: WinNat サービス用にポートを予約する
 次の Windows PowerShell コマンドを使用して、WinNat サービスのポートを予約します。 "192.168.1.100" を Windows Server Essentials サーバーの実際の IPv4 アドレスに置き換えます。

```powershell
Set-NetNatTransitionConfiguration -IPv4AddressPortPool @("192.168.1.100, 10000-47000")
```

> [!IMPORTANT]
>  アプリケーションとのポートの競合を回避するために、WinNat サービス用に予約するポートの範囲にポート 6602 が含まれていないことを確認します。

##  <a name="step-10-restart-the-winnat-service"></a><a name="BKMK_WinNAT"></a>手順 10: WinNat サービスを再起動する
 次の Windows PowerShell コマンドを使用して、Windows NAT ドライバー (WinNat) サービスを再起動します。

```powershell
Restart-Service winnat
```

##  <a name="appendix-set-up-directaccess-by-using-windows-powershell"></a><a name="BKMK_AppendixBPowerShellScript"></a>付録: Windows PowerShell を使用して DirectAccess をセットアップする
 ここでは、Windows PowerShell を使用して DirectAccess のセットアップと構成を行う方法について説明します。

### <a name="preparation"></a>準備
 DirectAccess 用にサーバーの構成を開始する前に、次の操作を完了する必要があります。

1.  [「手順 3: ネットワークロケーションサーバーの証明書と DNS レコードを準備](Configure-DirectAccess-in-Windows-Server-Essentials.md#BKMK_DNS)する」の手順に従って、 **DirectAccess-NLS.contoso.com**という名前の証明書を登録します ( **contoso.com**は実際の内部ドメイン名に置き換えられます)。また、ネットワークロケーションサーバー (NLS) の dns レコードを追加します。

2.  Active Directory に **DirectAccessClients** という名前のセキュリティ グループを追加し、DirectAccess 機能を使用できるようにするクライアント コンピューターを追加します。 詳細については、「[手順 4: DirectAccess クライアントコンピューターのセキュリティグループを作成する](#BKMK_AddSecurityGroup)」を参照してください。

### <a name="commands"></a>コマンド

> [!IMPORTANT]
>  Windows Server Essentials では、不要な IPv6 プレフィックスの GPO を削除する必要はありません。 次のラベルのコード セクションを削除します。 `# [WINDOWS SERVER 2012 ESSENTIALS ONLY] Remove the unnecessary IPv6 prefix GPO`

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
Set-DAServer -IPSecRootCertificate $rootcert[0]
Set -DAClient -OnlyRemoteComputers Disabled -Downlevel Enabled

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
Set-NetNatTransitionConfiguration -IPv4AddressPortPool @("192.168.1.100, 10000-47000")

# Restart the WinNat service
Restart-Service winnat
```

## <a name="additional-references"></a>その他のリファレンス

-   [Anywhere Access の管理](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)

-   [Windows Server Essentials の管理](Manage-Windows-Server-Essentials.md)
