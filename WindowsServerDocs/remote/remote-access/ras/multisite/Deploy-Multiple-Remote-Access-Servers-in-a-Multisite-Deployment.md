---
title: マルチサイト展開では、複数のリモート アクセス サーバーを展開します。
description: このトピックは、「Windows Server 2016 のマルチサイト展開に複数のリモートアクセスサーバーを展開する」の一部です。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: ac2f6015-50a5-4909-8f67-8565f9d332a2
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d8f12839deb1279b9f6c095068a85f528dad4a72
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87181758"
---
# <a name="deploy-multiple-remote-access-servers-in-a-multisite-deployment"></a>マルチサイト展開では、複数のリモート アクセス サーバーを展開します。

>適用先:Windows Server (半期チャネル)、Windows Server 2016

 Windows Server 2016 および Windows Server 2012 は、DirectAccess とリモートアクセスサービス (RAS) VPN を1つのリモートアクセスの役割に結合します。 リモート アクセスは、さまざまなエンタープライズ シナリオで展開できます。 この概要では、マルチサイト構成でリモートアクセスサーバーを展開するエンタープライズシナリオの概要について説明します。

## <a name="scenario-description"></a><a name="BKMK_OVER"></a>シナリオの説明
マルチサイト展開では、2つ以上のリモートアクセスサーバーまたはサーバークラスターが展開され、1つの場所または地理的に分散した場所に異なるエントリポイントとして構成されます。 1つの場所に複数のエントリポイントを展開すると、サーバーの冗長性が確保されます。また、リモートアクセスサーバーを既存のネットワークアーキテクチャに配置することもできます。 地理的な場所別の展開により、リモートクライアントコンピューターは、最も近いエントリポイントを使用して内部ネットワークリソースに接続できるため、リソースを効率的に使用できます。 マルチサイト展開全体のトラフィックは、外部のグローバルロードバランサーと分散して分散することができます。

マルチサイト展開では、Windows 10、Windows 8、または Windows 7 を実行しているクライアントコンピューターがサポートされます。 Windows 10 または Windows 8 を実行するクライアントコンピューターは、エントリポイントを自動的に識別します。または、ユーザーがエントリポイントを手動で選択することもできます。 自動割り当ては、次の優先順位で実行されます。

1.  ユーザーが手動で選択したエントリポイントを使用します。

2.  外部のグローバルロードバランサーがデプロイされている場合は、そのエントリポイントを使用します。

3.  自動プローブメカニズムを使用して、クライアントコンピューターによって識別される最も近いエントリポイントを使用します。

Windows 7 を実行しているクライアントのサポートは、各エントリポイントで手動で有効にする必要があります。これらのクライアントによるエントリポイントの選択はサポートされていません。

## <a name="prerequisites"></a>前提条件
このシナリオの展開を開始する前に、重要な要件の一覧を確認してください。

-   [詳細設定を使用した単一の DirectAccess サーバーの展開](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)は、マルチサイト展開の前に展開する必要があります。

-   Windows 7 クライアントは、常に特定のサイトに接続します。 クライアントの場所 (Windows 10、8、または8.1 クライアントとは異なります) に基づいて、最も近いサイトに接続することはできません。

-   DirectAccess 管理コンソールまたは Windows PowerShell コマンドレットを使用しないポリシーの変更はサポートされていません。

-   公開キー基盤を展開する必要があります。

    詳細については、次のトピックを参照してください。 [Test Lab Guide Mini-Module:Basic PKI for Windows Server 2012 (テスト ラボ ガイド ミニ モジュール: Windows Server 2012 の基本 PKI)](https://docs.microsoft.com/answers/topics/windows-server-2012.html)

-   企業ネットワークは IPv6 が有効になっている必要があります。 ISATAP を使用している場合は、これを削除し、ネイティブ IPv6 を使用する必要があります。

## <a name="in-this-scenario"></a>このシナリオの内容
マルチサイト展開シナリオには、次のようないくつかの手順が含まれます。

1. [詳細設定を使用して単一の DirectAccess サーバーを展開](../../directaccess/single-server-advanced/Deploy-a-Single-DirectAccess-Server-with-Advanced-Settings.md)します。 マルチサイト展開をセットアップする前に、詳細設定のある単一のリモートアクセスサーバーを展開する必要があります。

2. [マルチサイト展開を計画](plan/Plan-a-Multisite-Deployment.md)します。 1台のサーバーからマルチサイト展開を構築するには、マルチサイトの前提条件への対応や、Active Directory セキュリティグループ、グループポリシーオブジェクト (Gpo)、DNS、クライアント設定の計画など、いくつかの追加の計画手順が必要です。

3. [マルチサイト展開を構成](configure/Configure-a-Multisite-Deployment.md)します。 これは、Active Directory インフラストラクチャの準備、既存のリモートアクセスサーバーの構成、マルチサイト展開へのエントリポイントとしての複数のリモートアクセスサーバーの追加など、さまざまな構成手順で構成されています。

4. [マルチサイト展開のトラブルシューティングを](troubleshoot/Troubleshoot-a-Multisite-Deployment.md)行います。 このトラブルシューティングのセクションでは、マルチサイト展開でリモートアクセスを展開するときに発生する可能性のある最も一般的なエラーについて説明します。

## <a name="practical-applications"></a><a name="BKMK_APP"></a>実際の適用例
マルチサイト展開では、次のことが実現されます。

-   パフォーマンスの向上-マルチサイト展開では、クライアントコンピューターがリモートアクセスを使用して内部リソースにアクセスし、最も近い最も適切なエントリポイントを使用して接続できるようにします。 クライアントアクセスの内部リソースが効率的になり、DirectAccess 経由でルーティングされるクライアントのインターネット要求の速度が向上します。 エントリポイント間のトラフィックは、外部のグローバルロードバランサーを使用してバランスを取ることができます。

-   簡単な管理-マルチサイトでは、管理者はリモートアクセスの展開を Active Directory サイトの展開に合わせることができ、簡素化されたアーキテクチャが提供されます。 共有設定は、エントリポイントサーバーまたはクラスター間で簡単に設定できます。 リモートアクセスの設定は、展開内の任意のサーバーから管理することも、リモートサーバー管理ツール (RSAT) を使用してリモートで管理することもできます。 また、単一のリモートアクセス管理コンソールからマルチサイト展開全体を監視できます。

## <a name="roles-and-features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>このシナリオに含まれている役割と機能
次の表に、このシナリオで使用される役割と機能を示します。

|役割/機能|このシナリオのサポート方法|
|---------|-----------------|
|リモート アクセスの役割|この役割をインストールまたはアンインストールするには、サーバー マネージャー コンソールを使用します。 この役割には、以前は Windows Server 2008 R2 の機能であった DirectAccess と、以前はネットワーク ポリシーとアクセス サービス (NPAS) サーバーの役割の役割サービスであったリモート アクセス サービス (RRAS) の両方が含まれています。 リモート アクセスの役割は、次の 2 つのコンポーネントで構成されています。<p>-DirectAccess およびルーティングとリモートアクセスサービス (RRAS) VPN-DirectAccess と VPN は、リモートアクセス管理コンソールで一緒に管理されます。<br />-RRAS ルーティング-RRAS ルーティング機能は、従来のルーティングとリモートアクセスコンソールで管理されます。<p>依存関係は次のとおりです。<p>-インターネットインフォメーションサービス (IIS) Web サーバー-この機能は、ネットワークロケーションサーバーと既定の Web プローブを構成するために必要です。<br />-Windows Internal Database-リモートアクセスサーバーのローカルアカウンティングに使用されます。|
|リモート アクセス管理ツールの機能|この機能は、次のようにインストールされます。<p>-リモートアクセスの役割をインストールするときに、リモートアクセスサーバーに既定でインストールされ、リモート管理コンソールのユーザーインターフェイスをサポートします。<br />-必要に応じて、リモートアクセスサーバーの役割を実行していないサーバーにインストールできます。 この場合は、DirectAccess および VPN が実行されているリモート アクセス コンピューターのリモート管理に使用されます。<p>リモート アクセス管理ツールの機能は、次の要素で構成されています。<p>-リモートアクセス GUI およびコマンドラインツール<br />-Windows PowerShell 用リモートアクセスモジュール<p>次の要素と依存関係があります。<p>-グループポリシー管理コンソール<br />-RAS 接続マネージャー管理キット (CMAK)<br />-Windows PowerShell 3.0<br />-グラフィカル管理ツールとインフラストラクチャ|

## <a name="hardware-requirements"></a><a name="BKMK_HARD"></a>ハードウェア要件
このシナリオのハードウェア要件は次のとおりです。

-   マルチサイト展開に収集される少なくとも2台のリモートアクセスコンピューター。

-   このシナリオをテストするには、Windows 8 を実行し、DirectAccess クライアントとして構成されているコンピューターが少なくとも1台は必要です。 Windows 7 を実行しているクライアントのシナリオをテストするには、Windows 7 を実行しているコンピューターが少なくとも1台必要です。

-   エントリポイントサーバー間でトラフィックの負荷を分散するには、サードパーティの外部グローバルロードバランサーが必要です。

## <a name="software-requirements"></a><a name="BKMK_SOFT"></a>ソフトウェア要件
このシナリオのソフトウェア要件は次のとおりです。

-   単一サーバーの展開のソフトウェア要件。

-   単一サーバーのソフトウェア要件に加えて、複数のマルチサイト固有の要件があります。

    -   IPsec 認証要件-マルチサイト展開では、DirectAccess は IPsec コンピューター証明書認証を使用して展開する必要があります。 リモートアクセスサーバーを Kerberos プロキシとして使用する IPsec 認証を実行するオプションはサポートされていません。 IPsec 証明書を展開するには、内部 CA が必要です。

    -   Ip-https およびネットワークロケーションサーバーの要件-ip-https およびネットワークロケーションサーバーに必要な証明書は、CA によって発行されている必要があります。 自動的に発行され、リモートアクセスサーバーによって自己署名された証明書を使用するオプションはサポートされていません。 証明書は、内部 CA またはサードパーティの外部 CA によって発行できます。

    -   Active Directory の要件-少なくとも1つの Active Directory サイトが必要です。 リモートアクセスサーバーは、サイトに配置されている必要があります。 更新時間を短縮するには、各サイトに書き込み可能なドメインコントローラーを使用することをお勧めします。ただし、これは必須ではありません。

    -   セキュリティグループの要件-要件は次のとおりです。

        -   すべてのドメインのすべての Windows 8 クライアントコンピューターに、1つのセキュリティグループが必要です。 各ドメインに対して、これらのクライアントの一意のセキュリティグループを作成することをお勧めします。

        -   Windows 7 クライアントをサポートするように構成された各エントリポイントには、Windows 7 コンピューターを含む一意のセキュリティグループが必要です。 各ドメインのエントリポイントごとに一意のセキュリティグループを作成することをお勧めします。

        -   DirectAccess クライアントが含まれている複数のセキュリティ グループに、コンピューターを含めないようにする必要があります。 クライアントを複数のグループに含めると、クライアント要求の名前解決が期待どおりに動作しなくなります。

    -   GPO の要件-Gpo は、リモートアクセスを構成する前に手動で作成することも、リモートアクセスの展開中に自動的に作成することもできます。 要件は次のとおりです。

        -   各ドメインには一意のクライアント GPO が必要です。

        -   エントリポイントが配置されているドメイン内の各エントリポイントには、サーバー GPO が必要です。 そのため、同じドメイン内に複数のエントリポイントがある場合は、ドメインに複数のサーバー Gpo (エントリポイントごとに1つ) が存在します。

        -   Windows 7 クライアントのサポートが有効になっている各エントリポイントには、各ドメインに対して一意の Windows 7 クライアント GPO が必要です。

## <a name="known-issues"></a><a name="KnownIssues"></a>既知の問題
マルチサイトシナリオを構成する際の既知の問題は次のとおりです。

-   **同じ IPv4 サブネット内の複数のエントリポイント**。 同じ IPv4 サブネットに複数のエントリポイントを追加すると、IP アドレスの競合メッセージが表示され、エントリポイントの DNS64 アドレスは想定どおりに構成されません。 この問題は、企業ネットワーク上のサーバーの内部インターフェイスに IPv6 が展開されていない場合に発生します。 この問題を回避するには、現在および今後のすべてのリモートアクセスサーバーで次の Windows PowerShell コマンドを実行します。

    ```
    Set-NetIPInterface -InterfaceAlias <InternalInterfaceName> -AddressFamily IPv6 -DadTransmits 0
    ```

-   DirectAccess クライアントに指定されたリモートアクセスサーバーに接続するためのパブリックアドレスに、NRPT に含まれるサフィックスがある場合、DirectAccess は正常に機能しない可能性があります。 NRPT にパブリック名の除外が適用されていることを確認します。 マルチサイト展開では、すべてのエントリポイントのパブリック名に対して除外を追加する必要があります。 強制トンネリングが有効になっている場合、これらの除外は自動的に追加されることに注意してください。 強制トンネリングが無効になっている場合、これらは削除されます。

-   Windows PowerShell コマンドレット**DAMultiSite**を使用すると、WhatIf パラメーターと Confirm パラメーターが無効になり、マルチサイトが無効になり、windows 7 の gpo が削除されます。

-   マルチサイト展開で DCA を使用する Windows 7 クライアントを Windows 8 にアップグレードすると、Network Connectivity Assistant は機能しません。 この問題は、次の Windows PowerShell コマンドレットを使用して Windows 7 の Gpo を変更することで、クライアントのアップグレードの前に解決できます。

    ```
    Set-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant" -ValueName "TemporaryValue" -Type Dword -Value 1
    Remove-GPRegistryValue -Name <Windows7GpoName> -Domain <DomainName> -Key "HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\NetworkConnectivityAssistant"
    ```

    クライアントが既にアップグレードされている場合は、クライアントコンピューターを Windows 8 セキュリティグループに移動します。

-   Windows PowerShell コマンドレット**set-daentrypointdc**を使用してドメインコントローラーの設定を変更するときに、指定した ComputerName パラメーターが、マルチサイト展開に追加されていないエントリポイントのリモートアクセスサーバーである場合、指定されたサーバーが次のポリシー更新まで更新されないことを示す警告が表示されます。 更新されなかった実際のサーバーは、**リモートアクセス管理コンソール**の**ダッシュボード**の**構成ステータス**を使用して確認できます。 これによって機能上の問題が発生することはありませんが、更新されていないサーバーで**gpupdate/force**を実行すると、構成の状態をすぐに更新することができます。

-   マルチサイトが IPv4 専用の企業ネットワークに展開されている場合、内部ネットワークの IPv6 プレフィックスを変更すると、DNS64 のアドレスも変更されますが、DNS64 サービスへの DNS クエリを許可するファイアウォール規則のアドレスは更新されません。 この問題を解決するには、内部ネットワークの IPv6 プレフィックスを変更した後、次の Windows PowerShell コマンドを実行します。

    ```
    $dns64Address = (Get-DAClientDnsConfiguration).NrptEntry | ?{ $_.DirectAccessDnsServers -match ':3333::1' } | Select-Object -First 1 -ExpandProperty DirectAccessDnsServers

    $serverGpoName = (Get-RemoteAccess).ServerGpoName

    $serverGpoDc = (Get-DAEntryPointDC).DomainControllerName

    $gpoSession = Open-NetGPO -PolicyStore $serverGpoName -DomainController $serverGpoDc

    Get-NetFirewallRule -GPOSession $gpoSession | ? {$_.Name -in @('0FDEEC95-1EA6-4042-8BA6-6EF5336DE91A', '24FD98AA-178E-4B01-9220-D0DADA9C8503')} |  Set-NetFirewallRule -LocalAddress $dns64Address

    Save-NetGPO -GPOSession $gpoSession
    ```

-   既存の ISATAP インフラストラクチャが存在するときに DirectAccess を展開した場合、ISATAP ホストであったエントリポイントを削除すると、DNS64 サービスの IPv6 アドレスは、NRPT 内のすべての DNS サフィックスの DNS サーバーアドレスから削除されます。

    この問題を解決するには、**インフラストラクチャサーバーのセットアップ**ウィザードの [ **dns** ] ページで、変更された dns サフィックスを削除し、正しい dns サーバーアドレスを使用して再度追加します。そのためには、[ **dns サーバーアドレス**] ダイアログボックスの [**検出**] をクリックします。



