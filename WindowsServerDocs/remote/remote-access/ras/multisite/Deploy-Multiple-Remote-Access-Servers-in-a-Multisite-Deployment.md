---
title: マルチサイト展開での複数のリモート アクセス サーバーの展開
description: このトピックは、ガイドの一部複数リモート アクセス サーバーの展開で Windows Server 2016 の Multisite 展開します。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ac2f6015-50a5-4909-8f67-8565f9d332a2
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 607e3f5b2aa7e4c81e507a3d551d3d56e1f0b347
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282592"
---
# <a name="deploy-multiple-remote-access-servers-in-a-multisite-deployment"></a>マルチサイト展開での複数のリモート アクセス サーバーの展開

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

 Windows Server 2016 および Windows Server 2012 は、DirectAccess およびリモート アクセス サービス (RAS) VPN を 1 つのリモート アクセス役割に結合します。 リモート アクセスは、さまざまなエンタープライズ シナリオで展開できます。 この概要では、マルチサイト構成でのリモート アクセス サーバーを展開するためのエンタープライズ シナリオを紹介します。  
  
## <a name="BKMK_OVER"></a>シナリオの説明  
マルチサイト展開で 2 つ以上のリモート アクセス サーバーまたはサーバー クラスターが展開されているし、1 つの場所または地理的な場所にいる別のエントリ ポイントとして構成されています。 サーバーの冗長性、または既存のネットワーク アーキテクチャでのリモート アクセス サーバーの配置は、1 つの場所で複数のエントリ ポイントを展開できます。 地理的な場所での展開により、リモート クライアント コンピューターがそれらに最も近いエントリ ポイントを使用して内部ネットワーク リソースに接続できるよう、リソースの効率的な使用。 マルチサイト展開内のトラフィックを分散し、外部のグローバル ロード バランサーに分散できます。  
  
マルチサイト展開では、Windows 10、Windows 8 または Windows 7 を実行しているクライアント コンピューターをサポートします。 自動的に Windows 10 または Windows 8 を実行しているクライアント コンピューターが、エントリ ポイントを識別するか、ユーザーがエントリ ポイントを手動で選択できます。 次の優先順位での自動割り当てが行われます。  
  
1.  ユーザーが手動で選択したエントリ ポイントを使用します。  
  
2.  展開されている場合、外部のグローバル ロード バランサーによって識別されたエントリ ポイントを使用します。  
  
3.  自動プローブの機構を使用してクライアント コンピューターで識別される最も近いエントリ ポイントを使用します。  
  
各エントリ ポイントで Windows 7 を実行しているクライアントのサポートが手動で有効にする必要があるし、これらのクライアントでエントリ ポイントの選択がサポートされていません。  
  
## <a name="prerequisites"></a>前提条件  
このシナリオの展開を開始する前に、重要な要件の一覧を確認してください。  
  
-   [詳細設定を単一の DirectAccess サーバーをデプロイ](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)マルチサイト展開する前にデプロイする必要があります。  
  
-   Windows 7 クライアントは常に、特定のサイトに接続します。 (Windows 10、8、または 8.1 クライアント) とは異なり、クライアントの場所に基づいて、最も近いサイトに接続することはできません。  
  
-   DirectAccess 管理コンソールまたは Windows PowerShell コマンドレットを使用しないポリシーの変更はサポートされていません。  
  
-   公開キー基盤を展開する必要があります。  
  
    詳しくは、次のトピックをご覧ください。[テスト ラボ ガイド ミニ モジュール:Windows Server 2012 の基本 PKI。](https://social.technet.microsoft.com/wiki/contents/articles/7862.test-lab-guide-mini-module-basic-pki-for-windows-server-2012.aspx)  
  
-   企業ネットワークには、IPv6 が有効なをする必要があります。 ISATAP を使用している場合は、これを削除し、ネイティブ IPv6 を使用する必要があります。  
  
## <a name="in-this-scenario"></a>このシナリオの内容  
マルチサイト展開シナリオには、いくつかの手順が含まれます。  
  
1. [高度な設定で単一の DirectAccess サーバーをデプロイ](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)します。 高度な設定で単一のリモート アクセス サーバーをマルチサイト展開をセットアップする前にデプロイする必要があります。  
  
2. [マルチサイト展開の計画](plan/Plan-a-Multisite-Deployment.md)します。 1 台のサーバーをマルチサイト展開の追加の計画の数をビルドするには、手順が必要ですがマルチサイトの前提条件のコンプライアンスを含む、Active Directory セキュリティ グループ、グループ ポリシー オブジェクト (Gpo)、DNS、およびクライアント設定の計画。  
  
3. [マルチサイト展開を構成する](configure/Configure-a-Multisite-Deployment.md)します。 これは、多数の Active Directory インフラストラクチャ、既存のリモート アクセス サーバーの構成とマルチサイト展開へのエントリ ポイントとして複数のリモート アクセス サーバーの追加の準備を含め、構成の手順で構成されます。  
  
4. [マルチサイト展開のトラブルシューティングを行う](troubleshoot/Troubleshoot-a-Multisite-Deployment.md)します。 このトラブルシューティングのセクションでは、さまざまなマルチサイト展開でリモート アクセスを展開するときに発生する最も一般的なエラーについて説明します。
  
## <a name="BKMK_APP"></a>実際の適用  
マルチサイト展開には、次のものが用意されています。  
  
-   強化されたパフォーマンスには、マルチサイト展開により、最も近いと最も適切なエントリ ポイントを使用して接続するリモート アクセスを使用して内部リソースにアクセスするコンピューターをクライアントにできます。 クライアントが効率的に、内部リソースにアクセスし、DirectAccess 経由でルーティング インターネット要求のクライアントの速度が向上します。 エントリ ポイント間のトラフィックを分散するには、外部のグローバル ロード バランサーを使用します。  
  
-   管理 Multisite 簡単では、簡素化されたアーキテクチャを提供する、Active Directory サイトの展開へのリモート アクセスの展開を配置することができます。 共有の設定は、エントリ ポイントのサーバーまたはクラスター間で簡単に設定できます。 リモート アクセスの設定は、任意の展開、またはリモート サーバー管理ツール (RSAT) を使用してリモート サーバーから管理できます。 さらに、マルチサイト展開全体を単一のリモート アクセス管理コンソールから監視できます。  
  
## <a name="BKMK_NEW"></a>役割と機能がこのシナリオに含まれる  
次の表は、役割と機能がこのシナリオで使用します。  
  
|役割/機能|このシナリオのサポート方法|  
|---------|-----------------|  
|リモート アクセスの役割|この役割をインストールまたはアンインストールするには、サーバー マネージャー コンソールを使用します。 この役割には、以前は Windows Server 2008 R2 の機能であった DirectAccess と、以前はネットワーク ポリシーとアクセス サービス (NPAS) サーバーの役割の役割サービスであったリモート アクセス サービス (RRAS) の両方が含まれています。 リモート アクセスの役割は、次の 2 つのコンポーネントで構成されています。<br /><br />-DirectAccess およびルーティングとリモート アクセス サービス (RRAS) VPN DirectAccess と VPN は、リモート アクセス管理コンソールでまとめて管理します。<br />RRAS ルーティング RRAS ルーティング機能は、従来のルーティングとリモート アクセス コンソールで管理されます。<br /><br />依存関係は次のとおりです。<br /><br />-インターネット インフォメーション サービス (IIS) Web サーバー - この機能は、ネットワーク ロケーション サーバーおよび既定の web プローブを構成するために必要です。<br />-リモート アクセス サーバー上のローカル アカウンティング Windows 内部 Database-Used します。|  
|リモート アクセス管理ツールの機能|この機能は、次のようにインストールされます。<br /><br />-は、リモート アクセスの役割がインストールされているし、リモート管理コンソールのユーザー インターフェイスをサポートしているときに、既定でリモート アクセス サーバーにインストールされます。<br />-は、リモート アクセス サーバーの役割が実行されていないサーバーで必要に応じてインストールすることができます。 この場合は、DirectAccess および VPN が実行されているリモート アクセス コンピューターのリモート管理に使用されます。<br /><br />リモート アクセス管理ツールの機能は、次の要素で構成されています。<br /><br />-リモート アクセス GUI およびコマンド ライン ツール<br />の Windows PowerShell 用リモート アクセス モジュール<br /><br />次の要素と依存関係があります。<br /><br />グループ ポリシー管理コンソール<br />RAS 接続マネージャー管理キット (CMAK)<br />-   Windows PowerShell 3.0<br />グラフィカル管理ツールとインフラストラクチャ|  
  
## <a name="BKMK_HARD"></a>ハードウェア要件  
このシナリオのハードウェア要件は次のとおりです。  
  
-   マルチサイト展開に収集するには少なくとも 2 つのリモート アクセス コンピューター。   
  
-   シナリオをテストするには、Windows 8 を実行している DirectAccess クライアントとして構成されている少なくとも 1 つのコンピューターが必要です。 Windows 7 を実行しているクライアントのシナリオをテストするには、Windows 7 を実行している少なくとも 1 つのコンピューターが必要です。  
  
-   トラフィックを負荷分散のエントリ ポイントのサーバー間で、サードパーティの外部のグローバル ロード バランサーが必要です。  
  
## <a name="BKMK_SOFT"></a>ソフトウェアの要件  
このシナリオのソフトウェア要件は次のとおりです。  
  
-   単一サーバーの展開のソフトウェア要件。  
  
-   1 台のサーバーのソフトウェア要件に加えてには、さまざまな multisite-特定の要件があります。  
  
    -   IPsec 認証の要件で DirectAccess のマルチサイト展開は、IPsec コンピューター証明書認証を使用してデプロイする必要があります。 Kerberos プロキシとして、リモート アクセス サーバーを使用する IPsec 認証を実行するオプションがサポートされていません。 IPsec 証明書を展開するには、内部 CA が必要です。  
  
    -   IP-HTTPS およびネットワークの場所サーバー要件-必要な証明書、IP-HTTPS およびネットワーク ロケーション サーバーは、CA から発行する必要があります。 自動的に発行され、リモート アクセス サーバーによって自己署名証明書を使用するオプションがサポートされていません。 内部 CA またはサード パーティの外部 CA、証明書を発行できます。  
  
    -   Active Directory の要件の少なくとも 1 つの Active Directory サイトが必要です。 リモート アクセス サーバーは、サイトに配置する必要があります。 更新時間の短縮、お勧めする各サイトでは、書き込み可能なドメイン コント ローラーが、これは必須ではありません。  
  
    -   セキュリティ グループの要件は次のとおりです。  
  
        -   1 つのセキュリティ グループは、すべてのドメインからのすべての Windows 8 クライアント コンピューターに必要です。 ドメインごとにこれらのクライアントの一意なセキュリティ グループを作成することをお勧めします。  
  
        -   Windows 7 コンピューターを含む一意のセキュリティ グループは、各エントリ ポイントを Windows 7 クライアントをサポートするために構成されている必要があります。 各ドメインのエントリ ポイントごとの一意のセキュリティ グループを作成することをお勧めします。  
  
        -   DirectAccess クライアントが含まれている複数のセキュリティ グループに、コンピューターを含めないようにする必要があります。 クライアントを複数のグループに含めると、クライアント要求の名前解決が期待どおりに動作しなくなります。  
  
    -   GPO の要件の Gpo は、リモート アクセスを構成する前に手動で作成またはリモート アクセスの展開中に自動的に作成できます。 要件は次のとおりです。  
  
        -   一意のクライアント GPO は、各ドメインに必要です。  
  
        -   サーバー GPO は、エントリ ポイントが配置されているドメイン内のエントリ ポイントごとに必要です。 このため、複数のエントリ ポイントは、同じドメインに存在する場合は、複数のサーバー、ドメインの Gpo (エントリ ポイントごとに 1 つ) があります。  
  
        -   Windows 7 クライアントの一意の GPO は、各エントリ ポイントをドメインごとに、Windows 7 クライアントのサポートを有効になっている必要があります。  
  
## <a name="KnownIssues"></a>既知の問題  
次は既知の問題、マルチサイトのシナリオを構成する場合。  
  
-   **同じ IPv4 サブネット内の複数のエントリ ポイント**します。 同じ IPv4 サブネット内の複数のエントリ ポイントを追加すると、IP アドレスの競合メッセージ、およびエントリ ポイントの DNS64 アドレスは構成されません。 この問題は、企業ネットワーク上のサーバーの内部インターフェイスに IPv6 が展開されていないときに発生します。 防ぐためには、この問題は、現在および将来のすべてのリモート アクセス サーバー上で、次の Windows PowerShell コマンドを実行します。  
  
    ```  
    Set-NetIPInterface -InterfaceAlias <InternalInterfaceName> -AddressFamily IPv6 -DadTransmits 0  
    ```  
  
-   DirectAccess クライアントのリモート アクセス サーバーへの接続に指定されたパブリック アドレスに、サフィックスを NRPT に含まれる場合は、DirectAccess はどおりに動作しない可能性があります。 NRPT にパブリック名を除外してください。 マルチサイト展開では、すべてのエントリ ポイントのパブリック名の除外対象を追加する必要があります。 注場合に強制トンネリングが有効になっているこれらの例外が自動的に追加されます。 これらは、強制トンネリングは無効になっている場合に削除されます。  
  
-   Windows PowerShell コマンドレットを使用する場合**無効 DAMultiSite**WhatIf、Confirm パラメーターがある影響しない、およびマルチサイトは無効になりますと Windows 7 の Gpo が削除されます。  
  
-   DCA をマルチサイト展開で使用して Windows 7 クライアントは Windows 8 にアップグレードするとき、Network Connectivity Assistant は機能しません。 次の Windows PowerShell コマンドレットを使用して Windows 7 の Gpo を変更することでクライアントのアップグレードの前にこの問題を解決できます。  
  
    ```  
    Set-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant" -ValueName "TemporaryValue" -Type Dword -Value 1  
    Remove-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant"  
    ```  
  
    クライアントがアップグレードされていることは、Windows 8 のセキュリティ グループに、クライアント コンピューターを移動します。  
  
-   Windows PowerShell コマンドレットを使用してドメイン コント ローラーの設定を変更するときに**Set-daentrypointdc**ComputerName パラメーターを指定、マルチサイトに追加された最後の 1 つ以外のエントリ ポイントのリモート アクセス サーバーである場合は、警告がありますが、展開を指定されたサーバーは次のポリシー更新するまで更新されませんを示す表示されます。 更新された実際のサーバーを使用して表示することができます、**構成状態**で、**ダッシュ ボード**の**リモート アクセス管理コンソール**します。 機能上の問題は発生しません、ただし、実行**gpupdate/force**サーバーをすぐに更新された構成状態を取得するには更新されませんでした。  
  
-   IPv4 専用企業ネットワークで、内部を変更するマルチサイトを展開するときにも変更、DNS64 アドレス、IPv6 プレフィックスのネットワークが、DNS クエリを DNS64 サービスを許可するファイアウォール規則でアドレスを更新できません。 この問題を解決するには、内部ネットワークの IPv6 プレフィックスを変更した後、次の Windows PowerShell コマンドを実行します。  
  
    ```  
    $dns64Address = (Get-DAClientDnsConfiguration).NrptEntry | ?{ $_.DirectAccessDnsServers -match ':3333::1' } | Select-Object -First 1 -ExpandProperty DirectAccessDnsServers  
  
    $serverGpoName = (Get-RemoteAccess).ServerGpoName  
  
    $serverGpoDc = (Get-DAEntryPointDC).DomainControllerName  
  
    $gpoSession = Open-NetGPO -PolicyStore $serverGpoName -DomainController $serverGpoDc  
  
    Get-NetFirewallRule -GPOSession $gpoSession | ? {$_.Name -in @('0FDEEC95-1EA6-4042-8BA6-6EF5336DE91A', '24FD98AA-178E-4B01-9220-D0DADA9C8503')} |  Set-NetFirewallRule -LocalAddress $dns64Address  
  
    Save-NetGPO -GPOSession $gpoSession  
    ```  
  
-   既存の ISATAP インフラストラクチャが、ISATAP ホストされたエントリ ポイントを削除するときに存在していたときに、DirectAccess が展開された場合、DNS64 サービスの IPv6 アドレスが NRPT 内のすべての DNS サフィックスの DNS サーバーのアドレスから削除されます。  
  
    この問題を解決するのには、**インフラストラクチャ サーバーのセットアップ**ウィザードの**DNS**  ページで変更された DNS サフィックスを削除してもう一度正しい DNS サーバーのアドレスを使用してをクリックして追加**検出**上、 **DNS サーバーのアドレス** ダイアログ ボックス。  
  


