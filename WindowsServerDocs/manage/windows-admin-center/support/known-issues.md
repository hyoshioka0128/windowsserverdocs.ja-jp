---
title: Windows Admin Center の既知の問題
description: Windows Admin Center の既知の問題 (Project Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 06/07/2019
ms.openlocfilehash: e7cf6fc6a4fae2eee76409bd6af4ef2ff6ed35a3
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811782"
---
# <a name="windows-admin-center-known-issues"></a>Windows Admin Center の既知の問題

> 適用対象:Windows Admin Center、Windows Admin Center プレビュー

このページで説明されている問題が発生した場合は、[お知らせください](http://aka.ms/WACfeedback)。

## <a name="lenovo-xclarity-integrator"></a>Lenovo XClarity インテグレーター

Windows Admin Center 1904.1 のバージョンでは、Windows Admin Center バージョン 1904、Lenovo XClarity インテグレーターの拡張機能の公開された以前の非互換性の問題は解決されています。 Windows Admin Center のサポートされている最新のバージョンに更新することを強くお勧めします。

- Lenovo XClarity インテグレーター拡張機能のバージョン 1.1 は Windows Admin Center 1904.1 と完全な互換性です。 Windows Admin Center および Lenovo の拡張機能の最新バージョンに更新することを強くお勧めします。
- 何らかの理由で、時間の Windows Admin Center 1809.5 の使用を続行する必要がある場合可能性がありますを使用する Windows Admin Center 1809.5 はに基づいてサポートされなくなるまでに、Windows Admin Center 拡張子フィードで使用できますが XClarity インテグレーター 1.0.4この[サポート ポリシー](../support/index.md)します。

## <a name="installer"></a>インストーラー

- 独自の証明書を使用して Windows Admin Center をインストールする場合は、証明書マネージャー MMC ツールから拇印をコピーすると、[先頭に無効な文字が含まれる](https://support.microsoft.com/help/2023835/certificate-thumbprint-displayed-in-mmc-certificate-snap-in-has-extra)ことに留意してください。 この問題を回避するには、拇印の最初の文字を入力し、残りをコピー/貼り付けします。

- 1024 未満のポートを使用することはサポートされていません。 サービスのモードでポート 80 を指定されたポートにリダイレクトを構成する場合があります。

- Windows Update service (wuauserv) が停止して無効になっている場合、インストーラーは失敗します。 [19100629]

### <a name="upgrade"></a>アップグレード

- Quiet モードで msiexec を使用する場合は、以前のバージョンからのサービスのモードで Windows Admin Center をアップグレードする場合は、Windows Admin Center ポートの受信ファイアウォール規則の削除で問題があります。
  - ルールを再作成して、管理者特権の PowerShell コンソールから、次のコマンドを実行して交換\<ポート > Windows Admin Center (既定値の 443) 用に構成されたポート。

    ```powershell
    New-NetFirewallRule -DisplayName "SmeInboundOpenException" -Description "Windows Admin Center inbound port exception" -LocalPort <port> -RemoteAddress Any -Protocol TCP
    ```

## <a name="general"></a>全般的な情報

- ゲートウェイとしてインストールされている Windows Admin Center があれば**Windows Server 2016**含むイベント ログ エラーで、サービスがクラッシュする、頻繁に使用```Faulting application name: sme.exe```と```Faulting module name: WsmSvc.dll```。 これは、Windows Server 2019 で修正されたバグがあるためです。 Windows Server 2016 の修正プログラムが含まれている年 2019年 2 月累積更新プログラム、 [KB4480977](https://www.catalog.update.microsoft.com/Search.aspx?q=4480977)します。

- ゲートウェイとしてインストールされている Windows Admin Center がありが破損していた接続一覧が表示される場合は、次の手順を実行します。

   > [!WARNING]
   >これは、接続の一覧と、ゲートウェイ上のすべての Windows Admin Center ユーザーの設定に削除されます。

  1. Windows Admin Center をアンインストールします
  2. **C:\Windows\ServiceProfiles\NetworkService\AppData\Roaming\Microsoft** にある **Server Management Experience** フォルダーを削除します
  3. Windows Admin Center を再インストールします

- 場合は、ツールを開いたままにして、長期間アイドル状態、発生してしまういくつか**エラー。実行空間の状態がこの操作に対して無効**エラー。 この問題が発生した場合は、お使いのブラウザーを更新してください。 これが発生した場合[フィードバックの送信](http://aka.ms/WACfeedback)します。

- 非常に長い URL を含むページを更新するときに **500 エラー**が発生する場合があります。 [12443710]

- 一部のツールでは、ブラウザーのスペル チェックは、特定のフィールド値をスペルミスとしてマークする可能性があります。 [12425477]

- 一部のツールでは、コマンド ボタンがクリックされた直後に状態変更が反映されない場合があります。また、ツール UI に特定のプロパティへの変更が自動的に反映されない場合があります。 **[更新]** をクリックして、対象サーバーから最新の状態を取得することができます。 [11445790]

- タグのタグのフィルター - 接続の一覧で複数選択のチェック ボックスを使用して接続を選択し、接続の一覧でフィルター処理する場合は、選択した任意のアクションは、以前に選択したすべてのマシンに適用されますので、元の選択が解決しません。 [18099259]

- サード パーティ ソフトウェアに関する通知内で表示されている、Windows Admin Center モジュールで実行されている OS のバージョン番号とマイナーの差異である可能性があります。

### <a name="extension-manager"></a>拡張機能マネージャー

- Windows Admin Center を更新するときに、拡張機能を再インストールする必要があります。
- アクセスされるフィード拡張機能を追加する場合、警告はありません。 [14412861]

## <a name="browser-specific-issues"></a>ブラウザーに固有の問題

### <a name="microsoft-edge"></a>Microsoft Edge

- 場合によっては、Microsoft Edge を使用してインターネット経由で Windows Admin Center ゲートウェイにアクセスする場合に、読み込み時間が長くなることがあります。 これは、Windows Admin Center ゲートウェイが自己署名証明書を使用している Azure VM で発生することがあります。 [13819912]

- Azure Active Directory を ID プロバイダーとして使用していて、Windows Admin Center が自己署名証明書またはその他の信頼されていない証明書で構成されている場合は、Microsoft Edge で AAD 認証を完了することはできません。  [15968377]

- サービスとしてデプロイされている Windows Admin Center があり、お使いのブラウザーとして Microsoft Edge を使用している場合、ゲートウェイを Azure に接続する、新しいブラウザー ウィンドウを起動した後は失敗します。 追加することで、この問題を回避しようとしています。 https://login.microsoftonline.com 、 https://login.live.com 、として、ゲートウェイの URL が信頼済みサイトとクライアント側のブラウザーでポップアップ ブロックの設定のサイトを許可されているとします。 この問題の修正の詳細について、[トラブルシューティング ガイド](troubleshooting.md#azure-features-dont-work-properly-in-edge)します。 [17990376]

- デスクトップ モードでインストールされている Windows Admin Center があれば、Microsoft edge ブラウザーのタブは、favicon に表示されません。 [17665801]

### <a name="google-chrome"></a>Google Chrome

- 前のバージョン 70 (年 10 月、2018 年後半にリリース) Chrome が、[バグ](https://bugs.chromium.org/p/chromium/issues/detail?id=423609)websockets プロトコルと NTLM 認証に関連します。 これにより、次のツールが影響します。イベント、PowerShell、リモート デスクトップ接続します。

- Chrome では、特に**ワークグループ** (非ドメイン) 環境での接続の追加エクスペリエンスの実行中に、複数の資格情報プロンプトが表示される場合があります。

- Windows Admin Center が、サービスとしてデプロイした場合、ゲートウェイの URL からのポップアップは、Azure との統合機能を使用するのに有効にする必要があります。 これらのサービスには、Azure のネットワーク アダプター、Azure の更新プログラム管理および Azure Site Recovery が含まれます。

### <a name="mozilla-firefox"></a>Mozilla Firefox

Windows Admin Center は、Mozilla Firefox でテストされていませんが、ほとんどの機能は機能します。

- Windows 10 のインストール:インポートする必要がありますので、Mozilla Firefox は、独自の証明書ストア、```Windows Admin Center Client```証明書を Firefox では Windows 10、Windows Admin Center を使用します。

## <a name="websocket-compatibility-when-using-a-proxy-service"></a>プロキシ サービスを使用するときに WebSocket 互換性

Windows Admin Center のリモート デスクトップ、PowerShell、およびイベント モジュールでは、WebSocket プロトコルを利用します。多くの場合、このプロトコルはプロキシ サービスを使用するときにサポートされていません。 Azure AD アプリケーション プロキシの互換性における WebSocket サポートは[プレビュー](https://blogs.technet.microsoft.com/applicationproxyblog/2018/03/28/limited-websocket-support-now-in-public-preview/)の段階であり、互換性に関するフィードバックを必要としています。

## <a name="support-for-windows-server-versions-before-2016-2012-r2-2012-2008-r2"></a>(2012 R2、2012、2008 R2) の 2016年より前に Windows Server のバージョンのサポート

> [!NOTE]
> Windows Admin Center では、PowerShell の機能は、Windows Server 2012 R2、2012、または 2008 R2 には含まれていない必要があります。 Windows Server は、Windows Admin Center で管理するが場合、は、それらのサーバーに WMF 5.1 以降のバージョンをインストールする必要があります。

PowerShell で `$PSVersiontable` を入力して、WMF がインストールされていること、またバージョンが 5.1 以上であることを確認します。

インストールされていない場合は、[WMF 5.1 をダウンロードしてインストール](https://www.microsoft.com/en-us/download/details.aspx?id=54616)できます。

## <a name="role-based-access-control-rbac"></a>ロールベースのアクセス制御 (RBAC)

- Windows Defender アプリケーション制御 (WDAC、旧称はコードの整合性) を使用するように構成されているコンピューターでは、RBAC 展開は成功しません。[16568455]

- クラスターで RBAC を使用するには、各メンバー ノードに個別に構成を展開する必要があります。

- RBAC が展開されたときに、RBAC 構成に誤って起因する不正なエラーが表示される場合があります。 [16369238]

## <a name="server-manager-solution"></a>サーバー マネージャー ソリューション

### <a name="server-settings"></a>サーバーの設定

- 設定を変更しようと保存せずに移動した場合、ページが未保存の変更に関する警告しますが、移動を続行します。 [設定] タブが選択されているが、ページのコンテンツと一致しません状態で最終的に可能性があります。 [19905798] [19905787]

### <a name="certificates"></a>証明書

- .PFX の暗号化された証明書を現在のユーザー ストアにインポートすることはできません。 [11818622]

### <a name="devices"></a>デバイス

- キーボードでテーブル間の移動、ときに、選択可能性があります、テーブル グループの先頭にジャンプします。 [16646059]

### <a name="events"></a>イベント

- イベントは、[プロキシ サービスを使用する場合に WebSocket の互換性](#websocket-compatibility-when-using-a-proxy-service)に影響を受けます。

- 大きいログ ファイルをエクスポートするときに、“パケット サイズ” を参照するエラーが表示される場合があります。 [16630279]

  - これを解決するには、ゲートウェイ コンピューターで管理者特権でコマンド プロンプトで、次のコマンドを使用します。 ```winrm set winrm/config @{MaxEnvelopeSizekb="8192"}```

### <a name="files"></a>ファイル

- 大きいファイルのアップロードまたはダウンロードはまだサポートされていません。 (\~100 mb の制限) [12524234]

### <a name="powershell"></a>PowerShell

- PowerShell は、[プロキシ サービスを使用する場合に WebSocket の互換性](#websocket-compatibility-when-using-a-proxy-service)に影響を受けます。

- デスクトップの PowerShell コンソールと同じように 1 回の右クリックで貼り付けしても機能しません。 代わりに、ブラウザーのコンテキスト メニューが表示され、ここで貼り付けを選択できます。 Ctrl + V も機能します。

- Ctrl + C によるコピーは機能しません。常に Ctrl-C Break コマンドがコンソールに送信されます。 右クリックすると表示されるコンテキスト メニューからのコピーは機能します。

- Windows Admin Center のウィンドウを縮小する場合は、端のコンテンツは再配置されますが、もう一度拡大すると、コンテンツは前の状態に戻らないことがあります。 項目が乱雑になる場合は、Clear-Host を試すか、端末上にあるボタンを使用して切断および再接続することができます。

### <a name="registry-editor"></a>レジストリ エディター

- 検索機能が実装されていません。 [13820009]

### <a name="remote-desktop"></a>リモート デスクトップ

- Windows Server 2012 を管理するときに接続するリモート デスクトップ ツールがあります。 [20258278]

- ドメインに参加していないマシンに接続するには、リモート デスクトップを使用する場合で自分のアカウントを入力する必要があります、```MACHINENAME\USERNAME```形式。

- いくつかの構成には、グループ ポリシーを使用してリモート デスクトップ クライアントを Windows Admin Center をブロックできます。 これが発生した場合に有効にする```Allow users to connect remotely by using Remote Desktop Services```下 ```Computer Configuration/Policies/Administrative Templates/Windows Components/Remote Desktop Services/Remote Desktop Session Host/Connections```

- リモート デスクトップによって影響を受ける[websocket 互換性。](#websocket-compatibility-when-using-a-proxy-service)

- リモート デスクトップ ツールは現在、ローカル デスクトップとリモート セッションの間のテキスト、イメージ、またはファイルのコピー/貼り付けをサポートしていません。

- リモート セッション内でコピー/貼り付けを行うには、通常どおりコピーできます (右クリックによるコピーまたは Ctrl+C) が、貼り付けは、右クリックによる貼り付けをする必要があります (Ctrl+V は機能しません)。

- 次のキーコマンドをリモート セッションに送信することはできません。
  - Alt + Tab
  - ファンクション キー
  - Windows キー
  - PrtScn

- リモート アプリ – からリモート デスクトップ設定、アプリのリモート ツールを有効にした後、ツールされない可能性がありますツールの一覧にデスクトップ エクスペリエンス搭載サーバーを管理するときにします。 [18906904]

### <a name="roles-and-features"></a>役割と機能

- インストールに使用できないソースを含む役割や機能を選択すると、スキップされます。 [12946914]

- 役割のインストール後に自動的に再起動しないように選択すると、今後メッセージは表示されません。 [13098852]

- 自動的に再起動するように選択した場合、状態が 100% に更新される前に、再起動が行われます。 [13098852]

### <a name="storage"></a>ストレージ

- エラー通知なくが失敗するクォータ情報をフェッチしています (されますが、エラー、ブラウザーのコンソールで) [18962274]

- 下位レベル。DVD または CD/フロッピー ドライブは、下位レベル上のボリュームとしては表示されません。

- 下位レベル。不明または空白の詳細 パネルに表示されるため、ボリュームとディスクで一部のプロパティが使用可能な下位レベルです。

- 下位レベル。新しいボリュームを作成するには、ReFS はのみ Windows 2012 および 2012 R2 コンピューターで 64 K のアロケーション ユニット サイズをサポートします。 ReFS ボリュームがダウンレベル ターゲットの小さいアロケーション ユニット サイズで作成された場合は、ファイル システムの書式設定が失敗します。 新しいボリュームは使用できません。 解決策は、ボリュームを削除し、64 K のアロケーション ユニット サイズを使用することです。

### <a name="updates"></a>更新プログラム

- 更新プログラムをインストールすると、インストールの状態がキャッシュしてブラウザーの更新が必要です。

- エラーが発生する可能性があります。「キーセットが存在しません」Azure の更新プログラム管理を設定しようとしています。 この場合は、管理対象ノードで次の修復手順をお試しください。
    1. ' Cryptographic Services' サービスを停止します。
    2. フォルダー オプションの変更を表示するにはファイルが非表示 (必要な場合)。
    3. "%Allusersprofile%\microsoft\crypto\rsa\s-1-5-18"フォルダーにあり、その内容をすべて削除します。
    4. ' Cryptographic Services' サービスを再起動します。
    5. Windows Admin Center での更新管理のセットアップを繰り返します

### <a name="virtual-machines"></a>仮想マシン

- Windows Server 2012 ホスト上のバーチャル マシンを管理する場合、ブラウザーで VM が接続ツールは、VM への接続に失敗します。 VM に接続するための .rdp ファイルをダウンロードして動作するはずです。 [20258278]

- Azure Site Recovery – ASR が WAC、外部ホストのセットアップの場合はできないことから WAC [18972276] 内の VM を保護するには

- 仮想 SAN マネージャー、Move VM、Export VM、VM レプリケーションなどの Hyper-V マネージャーで利用可能な高度な機能は、現在サポートされていません。

### <a name="virtual-switches"></a>仮想スイッチ

- スイッチ埋め込みチーミング (SET) をします。Nic チームを追加する場合は、同じサブネット上があります。

## <a name="computer-management-solution"></a>コンピューターの管理ソリューション

コンピューターの管理ソリューションには、サーバー マネージャー ソリューションのツールのサブセットが含まれているため、同じ既知の問題と共に、次のコンピューターの管理ソリューション特有の問題が該当します。

- Microsoft アカウントを使用する場合 ([MSA](https://account.microsoft.com/account/)) する必要がありますを指定する Windows 10 コンピューターにログオンするために Azure Active Directory (AAD) を使用する場合、または"管理-として"ローカル マシン [16568455] を管理する資格情報

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