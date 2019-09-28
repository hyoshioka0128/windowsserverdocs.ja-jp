---
title: Windows Admin Center の既知の問題
description: Windows Admin Center の既知の問題 (Project Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server
ms.date: 06/07/2019
ms.openlocfilehash: a579d0274ff4b53a72c17760a6d53ef796625d3a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356913"
---
# <a name="windows-admin-center-known-issues"></a>Windows Admin Center の既知の問題

> 適用対象:Windows Admin Center、Windows Admin Center Preview

このページで説明されている問題が発生した場合は、[お知らせください](http://aka.ms/WACfeedback)。

## <a name="lenovo-xclarity-integrator"></a>Lenovo XClarity インテグレーター

以前に公開されていた Lenovo XClarity インテグレーター拡張と Windows 管理センターバージョン1904の非互換性の問題は、Windows 管理センターバージョン1904.1 で解決されるようになりました。 サポートされている最新バージョンの Windows 管理センターに更新することを強くお勧めします。

- Lenovo XClarity インテグレーター拡張バージョン1.1 は、Windows 管理センター1904.1 と完全に互換性があります。 最新バージョンの Windows 管理センターと Lenovo 拡張機能を更新することを強くお勧めします。
- 何らかの理由で、Windows 管理センター1809.5 の使用を継続する必要がある場合は、XClarity インテグレーター1.0.4 を使用することができます。これは、windows 管理センターの拡張機能1809.5 フィードでも使用できます。[サポートポリシー](../support/index.md)。

## <a name="installer"></a>インストーラー

- 独自の証明書を使用して Windows Admin Center をインストールする場合は、証明書マネージャー MMC ツールから拇印をコピーすると、[先頭に無効な文字が含まれる](https://support.microsoft.com/help/2023835/certificate-thumbprint-displayed-in-mmc-certificate-snap-in-has-extra)ことに留意してください。 この問題を回避するには、拇印の最初の文字を入力し、残りをコピー/貼り付けします。

- 1024未満のポートの使用はサポートされていません。 サービスモードでは、必要に応じて、指定したポートにリダイレクトするようにポート80を構成できます。

- Windows Update サービス (wuauserv) が停止され、無効になっている場合、インストーラーは失敗します。 [19100629]

### <a name="upgrade"></a>アップグレード

- 以前のバージョンから Windows 管理センターのサービスモードをアップグレードする場合、msiexec を quiet モードで使用すると、Windows 管理センターのポートの受信ファイアウォール規則が削除されるという問題が発生することがあります。
  - ルールを再作成するには、管理者特権の PowerShell コンソールから次\<のコマンドを実行し、ポート > を Windows 管理センター用に構成されたポート (既定では 443) に置き換えます。

    ```powershell
    New-NetFirewallRule -DisplayName "SmeInboundOpenException" -Description "Windows Admin Center inbound port exception" -LocalPort <port> -RemoteAddress Any -Protocol TCP
    ```

## <a name="general"></a>全般

- Windows **Server 2016**にゲートウェイとしてインストールされている windows 管理センターを使用している場合、サービスがとを```Faulting application name: sme.exe``` ```Faulting module name: WsmSvc.dll```含むイベントログのエラーでクラッシュすることがあります。 これは、Windows Server 2019 で修正されたバグが原因です。 Windows Server 2016 の修正プログラムには、2019の累積的な更新プログラム[KB4480977](https://www.catalog.update.microsoft.com/Search.aspx?q=4480977)が含まれています。

- Windows 管理センターがゲートウェイとしてインストールされていて、接続リストが破損していると思われる場合は、次の手順を実行します。

   > [!WARNING]
   >これにより、ゲートウェイのすべての Windows 管理センターユーザーの接続リストと設定が削除されます。

  1. Windows Admin Center をアンインストールします
  2. **C:\Windows\ServiceProfiles\NetworkService\AppData\Roaming\Microsoft** にある **Server Management Experience** フォルダーを削除します
  3. Windows Admin Center を再インストールします

- このツールを長時間開いたままアイドル状態にすると、次のような**エラーが発生する場合があります。実行空間の状態は、この操作**エラーに対して無効です。 この問題が発生した場合は、お使いのブラウザーを更新してください。 この問題が発生した場合は、[フィードバックをお送り](http://aka.ms/WACfeedback)ください。

- 非常に長い URL を含むページを更新するときに **500 エラー**が発生する場合があります。 [12443710]

- 一部のツールでは、ブラウザーのスペル チェックは、特定のフィールド値をスペルミスとしてマークする可能性があります。 [12425477]

- 一部のツールでは、コマンド ボタンがクリックされた直後に状態変更が反映されない場合があります。また、ツール UI に特定のプロパティへの変更が自動的に反映されない場合があります。 **[更新]** をクリックして、対象サーバーから最新の状態を取得することができます。 [11445790]

- [接続一覧でのタグフィルター]-[複数選択] チェックボックスを使用して接続を選択した場合、接続リストをタグでフィルター処理すると、選択したすべてのコンピューターに対して選択した操作が適用されます。 [18099259]

- Windows 管理センターのモジュールで実行されている OSS のバージョン番号と、サードパーティのソフトウェアに関する通知に記載されているものとの間には、若干の差異がある場合があります。

### <a name="extension-manager"></a>拡張機能マネージャー

- Windows 管理センターを更新する場合は、拡張機能を再インストールする必要があります。
- アクセスできない拡張機能フィードを追加すると、警告は表示されません。 [14412861]

## <a name="browser-specific-issues"></a>ブラウザーに固有の問題

### <a name="microsoft-edge"></a>Microsoft Edge

- 場合によっては、Microsoft Edge を使用してインターネット経由で Windows Admin Center ゲートウェイにアクセスする場合に、読み込み時間が長くなることがあります。 これは、Windows Admin Center ゲートウェイが自己署名証明書を使用している Azure VM で発生することがあります。 [13819912]

- Azure Active Directory を ID プロバイダーとして使用していて、Windows Admin Center が自己署名証明書またはその他の信頼されていない証明書で構成されている場合は、Microsoft Edge で AAD 認証を完了することはできません。  [15968377]

- Windows 管理センターがサービスとして展開されていて、ブラウザーとして Microsoft Edge を使用している場合は、新しいブラウザーウィンドウを起動した後にゲートウェイを Azure に接続できないことがあります。 追加することで、この問題を回避しようとしています。 https://login.microsoftonline.com 、 https://login.live.com 、として、ゲートウェイの URL が信頼済みサイトとクライアント側のブラウザーでポップアップ ブロックの設定のサイトを許可されているとします。 この問題を解決する方法については、[トラブルシューティングガイド](troubleshooting.md#azure-features-dont-work-properly-in-edge)を参照してください。 [17990376]

- Windows 管理センターがデスクトップモードでインストールされている場合、Microsoft Edge の [ブラウザー] タブに favicon は表示されません。 [17665801]

### <a name="google-chrome"></a>Google Chrome

- バージョン70より前 (10 月、2018)、Chrome には websocket プロトコルと NTLM 認証に関する[バグ](https://bugs.chromium.org/p/chromium/issues/detail?id=423609)がありました。 これは、次のツールに影響します。イベント、PowerShell、リモートデスクトップ。

- Chrome では、特に**ワークグループ** (非ドメイン) 環境での接続の追加エクスペリエンスの実行中に、複数の資格情報プロンプトが表示される場合があります。

- Windows 管理センターがサービスとしてデプロイされている場合、Azure 統合機能を使用するには、ゲートウェイ URL のポップアップを有効にする必要があります。 これらのサービスには、Azure ネットワークアダプター、Azure Update Management および Azure Site Recovery が含まれます。

### <a name="mozilla-firefox"></a>Mozilla Firefox

Windows Admin Center は、Mozilla Firefox でテストされていませんが、ほとんどの機能は機能します。

- Windows 10 のインストール:Mozilla Firefox には独自の証明書ストアがあるため、windows ```Windows Admin Center Client``` 10 で windows 管理センターを使用するには、Firefox に証明書をインポートする必要があります。

## <a name="websocket-compatibility-when-using-a-proxy-service"></a>プロキシサービスを使用する場合の WebSocket の互換性

Windows Admin Center のリモート デスクトップ、PowerShell、およびイベント モジュールでは、WebSocket プロトコルを利用します。多くの場合、このプロトコルはプロキシ サービスを使用するときにサポートされていません。 Azure AD アプリケーション プロキシの互換性における WebSocket サポートは[プレビュー](https://blogs.technet.microsoft.com/applicationproxyblog/2018/03/28/limited-websocket-support-now-in-public-preview/)の段階であり、互換性に関するフィードバックを必要としています。

## <a name="support-for-windows-server-versions-before-2016-2012-r2-2012-2008-r2"></a>2016より前の Windows Server バージョンのサポート (2012 R2、2012、2008 R2)

> [!NOTE]
> Windows 管理センターには、Windows Server 2012 R2、2012、または 2008 R2 に含まれていない PowerShell 機能が必要です。 Windows 管理センターで Windows Server を管理する場合は、これらのサーバーに WMF バージョン5.1 以上をインストールする必要があります。

PowerShell で `$PSVersiontable` を入力して、WMF がインストールされていること、またバージョンが 5.1 以上であることを確認します。

インストールされていない場合は、[WMF 5.1 をダウンロードしてインストール](https://www.microsoft.com/en-us/download/details.aspx?id=54616)できます。

## <a name="role-based-access-control-rbac"></a>ロールベースの Access Control (RBAC)

- Windows Defender アプリケーション制御 (WDAC、旧称はコードの整合性) を使用するように構成されているコンピューターでは、RBAC 展開は成功しません。[16568455]

- クラスターで RBAC を使用するには、各メンバー ノードに個別に構成を展開する必要があります。

- RBAC が展開されたときに、RBAC 構成に誤って起因する不正なエラーが表示される場合があります。 [16369238]

## <a name="server-manager-solution"></a>サーバー マネージャー ソリューション

### <a name="server-settings"></a>サーバーの設定

- 設定を変更した後、保存せずに移動しようとすると、未保存の変更についての警告が表示されますが、移動は続行されます。 選択した [設定] タブがページの内容と一致しない状態になることがあります。 [19905798] [19905787]

### <a name="certificates"></a>証明書

- .PFX の暗号化された証明書を現在のユーザー ストアにインポートすることはできません。 [11818622]

### <a name="devices"></a>デバイス

- キーボードを使用してテーブル内を移動すると、選択した項目がテーブルグループの一番上に移動する場合があります。 [16646059]

### <a name="events"></a>イベント

- イベントは、[プロキシ サービスを使用する場合に WebSocket の互換性](#websocket-compatibility-when-using-a-proxy-service)に影響を受けます。

- 大きいログ ファイルをエクスポートするときに、“パケット サイズ” を参照するエラーが表示される場合があります。 [16630279]

  - これを解決するには、ゲートウェイコンピューターで管理者特権のコマンドプロンプトで次のコマンドを使用します。```winrm set winrm/config @{MaxEnvelopeSizekb="8192"}```

### <a name="files"></a>ファイル

- 大きいファイルのアップロードまたはダウンロードはまだサポートされていません。 (@no__t 0100mb mb の制限)[12524234]

### <a name="powershell"></a>PowerShell

- PowerShell は、[プロキシ サービスを使用する場合に WebSocket の互換性](#websocket-compatibility-when-using-a-proxy-service)に影響を受けます。

- デスクトップの PowerShell コンソールと同じように 1 回の右クリックで貼り付けしても機能しません。 代わりに、ブラウザーのコンテキスト メニューが表示され、ここで貼り付けを選択できます。 Ctrl + V も機能します。

- Ctrl + C によるコピーは機能しません。常に Ctrl-C Break コマンドがコンソールに送信されます。 右クリックすると表示されるコンテキスト メニューからのコピーは機能します。

- Windows Admin Center のウィンドウを縮小する場合は、端のコンテンツは再配置されますが、もう一度拡大すると、コンテンツは前の状態に戻らないことがあります。 項目が乱雑になる場合は、Clear-Host を試すか、端末上にあるボタンを使用して切断および再接続することができます。

### <a name="registry-editor"></a>レジストリ エディター

- 検索機能が実装されていません。 [13820009]

### <a name="remote-desktop"></a>リモート デスクトップ

- Windows Server 2012 を管理している場合、リモートデスクトップツールが接続に失敗することがあります。 [20258278]

- リモートデスクトップを使用して、ドメインに参加していないコンピューターに接続する場合は、の```MACHINENAME\USERNAME```形式でアカウントを入力する必要があります。

- 一部の構成では、Windows 管理センターのリモートデスクトップクライアントがグループポリシーでブロックされることがあります。 この問題が発生した```Allow users to connect remotely by using Remote Desktop Services```場合は、```Computer Configuration/Policies/Administrative Templates/Windows Components/Remote Desktop Services/Remote Desktop Session Host/Connections```

- リモートデスクトップは websocket 互換性によって影響を受け[ます。](#websocket-compatibility-when-using-a-proxy-service)

- リモート デスクトップ ツールは現在、ローカル デスクトップとリモート セッションの間のテキスト、イメージ、またはファイルのコピー/貼り付けをサポートしていません。

- リモート セッション内でコピー/貼り付けを行うには、通常どおりコピーできます (右クリックによるコピーまたは Ctrl+C) が、貼り付けは、右クリックによる貼り付けをする必要があります (Ctrl+V は機能しません)。

- 次のキーコマンドをリモート セッションに送信することはできません。
  - Alt + Tab
  - ファンクション キー
  - Windows キー
  - PrtScn

- リモートアプリ-リモートデスクトップの設定からリモートアプリツールを有効にした後、デスクトップエクスペリエンスを備えたサーバーを管理するときにツールの一覧にツールが表示されない場合があります。 [18906904]

### <a name="roles-and-features"></a>役割と機能

- インストールに使用できないソースを含む役割や機能を選択すると、スキップされます。 [12946914]

- 役割のインストール後に自動的に再起動しないように選択すると、今後メッセージは表示されません。 [13098852]

- 自動的に再起動するように選択した場合、状態が 100% に更新される前に、再起動が行われます。 [13098852]

### <a name="storage"></a>ストレージ

- クォータ情報の取得がエラー通知なしに失敗する (ブラウザーのコンソールにエラーが表示される) [18962274]

- ダウンレベル:DVD/CD/フロッピードライブは、下位レベルではボリュームとして表示されません。

- ダウンレベル:[ボリュームとディスク] の一部のプロパティは下位レベルでは使用できないため、[詳細] パネルに [不明] または [空白] と表示されます。

- ダウンレベル:新しいボリュームを作成する場合、ReFS でサポートされるのは、Windows 2012 および 2012 R2 コンピューターでのアロケーションユニットサイズが64K です。 ReFS ボリュームがダウンレベル ターゲットの小さいアロケーション ユニット サイズで作成された場合は、ファイル システムの書式設定が失敗します。 新しいボリュームは使用できません。 解決策は、ボリュームを削除し、64 K のアロケーション ユニット サイズを使用することです。

### <a name="updates"></a>更新プログラム

- 更新プログラムをインストールすると、インストールの状態がキャッシュされ、ブラウザーの更新が必要になる場合があります。

- 次のようなエラーが発生する可能性があります。Azure Update management を設定しようとすると、"キーセットが存在しません" が発生します。 この場合は、管理ノードで次の修復手順を試してください。
    1. ' Cryptographic Services ' サービスを停止します。
    2. 隠しファイルを表示するようにフォルダーオプションを変更します (必要な場合)。
    3. "%Allusersprofile%\Microsoft\Crypto\RSA\S-1-5-18" フォルダーを受け取って、その内容をすべて削除します。
    4. ' Cryptographic Services ' サービスを再起動してください。
    5. Windows 管理センターで Update Management のセットアップを繰り返す

### <a name="virtual-machines"></a>仮想マシン

- Windows Server 2012 ホスト上の仮想マシンを管理する場合、ブラウザー内 VM 接続ツールは VM に接続できません。 VM に接続するための .rdp ファイルのダウンロードは引き続き機能します。 [20258278]

- Azure Site Recovery – ASR が WAC の外部のホストにセットアップされている場合、WAC 内から VM を保護することはできません [18972276]

- 仮想 SAN マネージャー、Move VM、Export VM、VM レプリケーションなどの Hyper-V マネージャーで利用可能な高度な機能は、現在サポートされていません。

### <a name="virtual-switches"></a>仮想スイッチ

- スイッチ埋め込みチーミング (SET):Nic をチームに追加する場合は、同じサブネット上にある必要があります。

## <a name="computer-management-solution"></a>コンピューターの管理ソリューション

コンピューターの管理ソリューションには、サーバー マネージャー ソリューションのツールのサブセットが含まれているため、同じ既知の問題と共に、次のコンピューターの管理ソリューション特有の問題が該当します。

- Microsoft アカウント ([MSA](https://account.microsoft.com/account/)) を使用している場合、または AZURE ACTIVE DIRECTORY (AAD) を使用して Windows 10 コンピューターにログオンしている場合、ローカルコンピューターを管理するには、"管理-as" の資格情報を指定する必要があります [16568455]

- ローカル ホストを管理しようとすると、ゲートウェイ プロセスを昇格するように求められます。 続いて表示される [ユーザー アカウント制御] ポップアップで **[いいえ]** をクリックすると、Windows Admin Center でそれを表示することができなくなります。 この場合、システム トレイの Windows Admin Center アイコンを右クリックし、[終了] を選択することでゲートウェイ プロセスを終了し、[スタート] メニューから Windows Admin Center を再起動します。

- Windows 10 では既定で WinRM/PowerShell リモート処理が有効になっていません。
  
  - Windows 10 クライアントの管理を有効にするには、管理者特権の PowerShell プロンプトから ```Enable-PSRemoting``` コマンドを実行する必要があります。

  - また、```Set-NetFirewallRule -Name WINRM-HTTP-In-TCP -RemoteAddress Any``` を使用して、ローカル サブネットの外部から接続を許可できるようにファイアウォールを更新する必要があります。 より制限の厳しいネットワーク シナリオでは、[このドキュメント](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/enable-psremoting?view=powershell-5.1)を参照してください。

## <a name="failover-cluster-manager-solution"></a>フェールオーバー クラスター マネージャー ソリューション

- クラスター (ハイパーコンバージドまたは従来のクラスターのいずれか) を管理するときに、**shell was not found** (シェルが見つかりませんでした) というエラーが発生する場合があります。 この問題が発生した場合は、お使いのブラウザーを再読み込みするか、別のツールに移動して戻ります。 [13882442]

- 完全に構成されていない下位バージョン (Windows Server 2012 または 2012 R2) のクラスターを管理するときに問題が発生することがあります。 この問題の解決方法は、Windows の機能**RSAT クラスタ リング PowerShell**がインストールされ、クラスターの**各メンバー ノード**で有効になっていることを確認することです。 PowerShell でこれを行うには、すべてのクラスター ノードで `Install-WindowsFeature -Name RSAT-Windows-PowerShell` コマンドを入力します。 [12524664]

- クラスターは正しく検出されるように全 FQDN を指定して追加する必要があります。

- ゲートウェイとしてインストールされた Windows Admin Center を使用してクラスターに接続する場合は、メンバー ノードを照会するために資格情報を利用できるように、**Use these credentials for all connections** (これらの資格情報をすべての接続に使用する) を選択する必要があります。

## <a name="hyper-converged-cluster-manager-solution"></a>ハイパーコンバージド クラスター マネージャー ソリューション

- **Drives - Update firmware**、**Servers - Remove**、および **Volumes - Open** などの一部のコマンドは無効になっていて現在サポートされていません。