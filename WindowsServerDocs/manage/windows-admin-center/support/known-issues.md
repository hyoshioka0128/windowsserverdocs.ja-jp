---
title: Windows Admin Center の既知の問題
description: Windows Admin Center の既知の問題 (Project Honolulu)
ms.technology: manage
ms.topic: article
author: jwwool
ms.author: jeffrew
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 04/12/2019
ms.openlocfilehash: b0159d88251c7f4f6422dffd8f1e1414e1f30f33
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9297046"
---
# Windows Admin Center の既知の問題

>適用対象: Windows Admin Center、Windows Admin Center Preview

このページで説明されている問題が発生した場合は、[お知らせください](http://aka.ms/WACfeedback)。

## Lenovo XClarity インテグレーター
Lenovo XClarity インテグレーターの特定のバージョンの組み合わせと Windows Admin Center の間での非互換性が存在しています。 場合は、現在使用したり、Windows Admin Center で Lenovo XClarity インテグレーター拡張機能を使用する、知っておく必要がある次に示します。

- Lenovo XClarity インテグレーター 1.0.4 拡張機能のバージョンは、Windows Admin Center 1809.5 と完全に互換性が。
- Lenovo XClarity インテグレーター 1.0.4 拡張機能のバージョンには、Windows Admin Center 1904 で互換性の問題が公開されます。 Microsoft と Lenovo のエンジニアは同時に、積極的に調査し、できるだけ早くソリューションを提供することを願っています。 すべての更新プログラムは、Windows Admin Center ドキュメント サイトでは、ここ転記し、参照用[Lenovo のサポート ページ](https://support.lenovo.com/solutions/ht507549)を参照することもできます。
- Lenovo の XClarity 機能の頻繁にユーザーの場合は、引き続き XClarity インテグレーター 1.0.4 を使用する Windows Admin Center 1809.5 のいずれかのままにすることができます。 か、Windows Admin Center 1904 にアップグレードして、個別にスタンドアロン XClarity 管理者を使用することができます。ここでは、回避策としてのソフトウェア。


## インストーラー

- 独自の証明書を使用して Windows Admin Center をインストールする場合は、証明書マネージャー MMC ツールから拇印をコピーすると、[先頭に無効な文字が含まれる](https://support.microsoft.com/help/2023835/certificate-thumbprint-displayed-in-mmc-certificate-snap-in-has-extra)ことに留意してください。 この問題を回避するには、拇印の最初の文字を入力し、残りをコピー/貼り付けします。

- 1024 以下のポートを使用することはサポートされていません。 サービス モードでは、必要に応じてポート 80 に指定したポートにリダイレクトを構成する場合があります。

- Windows Update サービス (wuauserv) が停止し、無効になっている場合は、インストーラーは失敗します。 [19100629]

### アップグレード パッケージ、アップグレード

- Quiet モードで msiexec を使用する場合は、以前のバージョンからサービス モードで Windows Admin Center をアップグレード、Windows Admin Center のポートの受信ファイアウォール規則を削除する場所問題が発生した可能性があります。
  - ルールを再作成するには、Windows Admin Center (既定 443) 用に構成されたポートを持つ \<port> を置き換えて、管理者特権の PowerShell コンソールから、次のコマンドを実行します。

    ```powershell
    New-NetFirewallRule -DisplayName "SmeInboundOpenException" -Description "Windows Admin Center inbound port exception" -LocalPort <port> -RemoteAddress Any -Protocol TCP
    ```

## 全般

- 使用率で**Windows Server 2016**でのゲートウェイとしてインストールされている Windows Admin Center を使っている場合、サービスが含まれているイベント ログにエラーがクラッシュ```Faulting application name: sme.exe```と```Faulting module name: WsmSvc.dll```します。 というバグが Windows Server 2019 で修正されましたが原因です。 Windows Server 2016 の更新プログラムが含まれている年 2019年 2 月の累積的な更新、 [KB4480977](https://www.catalog.update.microsoft.com/Search.aspx?q=4480977)します。

- Windows Admin Center のゲートウェイとしてインストールされているがあり、壊れているように、接続の一覧が表示されますがある場合は、次の手順を実行します。

>[!WARNING]
>接続の一覧およびゲートウェイ上のすべての Windows Admin Center ユーザーの設定は削除されます。

  1. Windows Admin Center をアンインストールします
  2. **C:\Windows\ServiceProfiles\NetworkService\AppData\Roaming\Microsoft** にある **Server Management Experience** フォルダーを削除します
  3. Windows Admin Center を再インストールします

- ツールを開いたまま長時間アイドル状態にすると、**Error: The runspace state is not valid for this operation** (エラー: この操作の実行空間の状態が有効ではありません) というエラーが何度か表示されることがあります。 この問題が発生した場合は、お使いのブラウザーを更新してください。 これは、[フィードバックの送信](http://aka.ms/WACfeedback)が発生した場合。

- 非常に長い URL を含むページを更新するときに **500 エラー**が発生する場合があります。 [12443710]

- 一部のツールでは、ブラウザーのスペル チェックは、特定のフィールド値をスペルミスとしてマークする可能性があります。 [12425477]

- 一部のツールでは、コマンド ボタンがクリックされた直後に状態変更が反映されない場合があります。また、ツール UI に特定のプロパティへの変更が自動的に反映されない場合があります。 **[更新]** をクリックして、対象サーバーから最新の状態を取得することができます。 [11445790]

- タグのタグは、複数選択のチェック ボックスを使用して接続を選択し、接続一覧によってフィルター処理する場合 - 接続の一覧にフィルターは、選択したすべてのアクションは、以前に選択したすべてのコンピューターに適用されますので、元の選択範囲が引き続き発生します。 [18099259]

- サード パーティのソフトウェアに関する内で表示されている、Windows Admin Center モジュールで実行されている OS のバージョン番号とマイナーの差異が可能性があります。

### 拡張機能マネージャー

- Windows Admin Center を更新すると、拡張機能を再インストールする必要があります。
- アクセス可能なフィード拡張機能を追加する場合、警告はありません。 [14412861]

## ブラウザーに固有の問題

### Microsoft Edge

- 場合によっては、Microsoft Edge を使用してインターネット経由で Windows Admin Center ゲートウェイにアクセスする場合に、読み込み時間が長くなることがあります。 これは、Windows Admin Center ゲートウェイが自己署名証明書を使用している Azure VM で発生することがあります。 [13819912]

- Azure Active Directory を ID プロバイダーとして使用していて、Windows Admin Center が自己署名証明書またはその他の信頼されていない証明書で構成されている場合は、Microsoft Edge で AAD 認証を完了することはできません。  [15968377]

- Windows Admin Center をサービスとして展開があり、お使いのブラウザーとして Microsoft Edge を使用している場合は、新しいブラウザー ウィンドウを起動した後は失敗、ゲートウェイを Azure に接続があります。 追加することで、この問題を回避しようとしています。 https://login.microsoftonline.com、 https://login.live.com、として、ゲートウェイの URL が信頼済みサイトとクライアント側のブラウザーでのポップアップ ブロックの設定のサイトに許可されているとします。 [トラブルシューティング ガイド](troubleshooting.md#azlogin)でこれを修正するに関する詳細なガイダンスについてはします。 [17990376]

- デスクトップ モードでインストールされている Windows Admin Center を使っている場合、Microsoft Edge でブラウザー タブは、お気に入りアイコンを表示されません。 [17665801]

### Google Chrome

- 前のバージョン 70 (遅延の 2018 年 10 月にリリース) Chrome には、websocket プロトコルおよび NTLM 認証に関する[バグ](https://bugs.chromium.org/p/chromium/issues/detail?id=423609)が必要があります。 これは、イベント、PowerShell、リモート デスクトップのツールに影響します。

- Chrome では、特に**ワークグループ** (非ドメイン) 環境での接続の追加エクスペリエンスの実行中に、複数の資格情報プロンプトが表示される場合があります。

- Windows Admin Center をサービスとしての展開を使っている場合ゲートウェイ URL からのポップアップは、Azure の統合機能を使用するが有効にする必要があります。 これらのサービスには、Azure ネットワーク アダプター、Azure の更新プログラムの管理、および Azure Site Recovery が含まれます。

### Mozilla Firefox

Windows Admin Center は、Mozilla Firefox でテストされていませんが、ほとんどの機能は機能します。

- Windows 10 インストール: Mozilla Firefox には独自の証明書ストアがあるため、Windows 10 で Windows Admin Center を使用するには、```Windows Admin Center Client``` 証明書を Firefox にインポートする必要があります。

<a id="websockets"></a>

## プロキシ サービスを使用する場合の WebSocket の互換性

Windows Admin Center のリモート デスクトップ、PowerShell、およびイベント モジュールでは、WebSocket プロトコルを利用します。多くの場合、このプロトコルはプロキシ サービスを使用するときにサポートされていません。 Azure AD アプリケーション プロキシの互換性における WebSocket サポートは[プレビュー](https://blogs.technet.microsoft.com/applicationproxyblog/2018/03/28/limited-websocket-support-now-in-public-preview/)の段階であり、互換性に関するフィードバックを必要としています。

## 2016 (2012 R2、2012、2008 R2) 前に、のバージョンの Windows Server のサポート

> [!NOTE]
> Windows Admin Center には、Windows Server 2012 R2、2012、または 2008 R2 に含まれていない PowerShell 機能が必要です。 Windows Server は、Windows Admin Center でこれらを管理するが場合、は、それらのサーバーに WMF バージョン 5.1 以上をインストールする必要があります。

PowerShell で `$PSVersiontable` を入力して、WMF がインストールされていること、またバージョンが 5.1 以上であることを確認します。

インストールされていない場合は、[WMF 5.1 をダウンロードしてインストール](https://www.microsoft.com/en-us/download/details.aspx?id=54616)できます。

<a id="rbacknownissues"></a>

## 役割ベースのアクセス制御 (RBAC)

- Windows Defender アプリケーション制御 (WDAC、旧称はコードの整合性) を使用するように構成されているコンピューターでは、RBAC 展開は成功しません。[16568455]

- クラスターで RBAC を使用するには、各メンバー ノードに個別に構成を展開する必要があります。

- RBAC が展開されたときに、RBAC 構成に誤って起因する不正なエラーが表示される場合があります。 [16369238]

## サーバー マネージャー ソリューション

### サーバーの設定

- 設定にセーブせず移動しようとした場合、ページが未保存の変更に関する警告を表示するが、引き続きに移動します。 設定] タブを選択すると、ページのコンテンツが一致しません状態終了する可能性があります。 [19905798] [19905787]

### 証明書

- .PFX の暗号化された証明書を現在のユーザー ストアにインポートすることはできません。 [11818622]

### デバイス

- キーボードを使用してテーブル間を移動する、する場合は、選択範囲がテーブル グループの上部にジャンプ可能性があります。 [16646059]

### イベント

- イベントは、[プロキシ サービスを使用する場合に WebSocket の互換性](#websockets)に影響を受けます。

- 大きいログ ファイルをエクスポートするときに、“パケット サイズ” を参照するエラーが表示される場合があります。 [16630279]

  - この問題を解決するには、ゲートウェイ マシンで管理者特権のコマンド プロンプトで、次のコマンドを使用します。 ```winrm set winrm/config @{MaxEnvelopeSizekb="8192"}```

### ファイル

- 大きいファイルのアップロードまたはダウンロードはまだサポートされていません。 (100 MB までの制限) [12524234]

### PowerShell

- PowerShell は、[プロキシ サービスを使用する場合に WebSocket の互換性](#websockets)に影響を受けます。

- デスクトップの PowerShell コンソールと同じように 1 回の右クリックで貼り付けしても機能しません。 代わりに、ブラウザーのコンテキスト メニューが表示され、ここで貼り付けを選択できます。 Ctrl + V も機能します。

- Ctrl + C によるコピーは機能しません。常に Ctrl-C Break コマンドがコンソールに送信されます。 右クリックすると表示されるコンテキスト メニューからのコピーは機能します。

- Windows Admin Center のウィンドウを縮小する場合は、端のコンテンツは再配置されますが、もう一度拡大すると、コンテンツは前の状態に戻らないことがあります。 項目が乱雑になる場合は、Clear-Host を試すか、端末上にあるボタンを使用して切断および再接続することができます。

### レジストリ エディター

- 検索機能が実装されていません。 [13820009]

### リモート デスクトップ

- リモート デスクトップ ツールは、Windows Server 2012 を管理するときの接続に失敗する可能性があります。 [20258278]

- いないドメインに参加しているコンピューターに接続するには、リモート デスクトップを使用する場合は、[自分のアカウントを入力する必要があります、```MACHINENAME\USERNAME```形式です。

- 一部の構成には、グループ ポリシーを使った Windows Admin Center のリモート デスクトップ クライアントをブロックできます。 これが発生した場合に有効にする```Allow users to connect remotely by using Remote Desktop Services```下 ```Computer Configuration/Policies/Administrative Templates/Windows Components/Remote Desktop Services/Remote Desktop Session Host/Connections```

- リモート デスクトップによって影響を受ける[に websocket の互換性](#websockets)。

- リモート デスクトップ ツールは現在、ローカル デスクトップとリモート セッションの間のテキスト、イメージ、またはファイルのコピー/貼り付けをサポートしていません。

- リモート セッション内でコピー/貼り付けを行うには、通常どおりコピーできます (右クリックによるコピーまたは Ctrl+C) が、貼り付けは、右クリックによる貼り付けをする必要があります (Ctrl+V は機能しません)。

- 次のキーコマンドをリモート セッションに送信することはできません。
  - Alt + Tab
  - ファンクション キー
  - Windows キー
  - PrtScn

- リモート アプリ: リモート アプリ ツールは、リモート デスクトップの設定を有効にした後、ツールされない可能性がありますツールの一覧でデスクトップ エクスペリエンス搭載サーバーを管理する場合。 [18906904]

### 役割と機能

- インストールに使用できないソースを含む役割や機能を選択すると、スキップされます。 [12946914]

- 役割のインストール後に自動的に再起動しないように選択すると、今後メッセージは表示されません。 [13098852]

- 自動的に再起動するように選択した場合、状態が 100% に更新される前に、再起動が行われます。 [13098852]

### 記憶域

- エラー通知することがなく失敗する可能性がクォータ情報をフェッチ (されますが、エラー、ブラウザーのコンソールで) [18962274]

- ダウンレベル: DVD/CD/フロッピー ドライブは、ダウンレベルのボリュームとして表示されません。

- ダウンレベル: ボリュームとディスクの一部のプロパティはダウンレベルで利用できないため、詳細パネルで不明または空白で表示されます。

- ダウンレベル: 新しいボリュームを作成する場合、ReFS では、Windows 2012 および 2012 R2 コンピューターでの 64K のアロケーション ユニット サイズのみがサポートされます。 ReFS ボリュームがダウンレベル ターゲットの小さいアロケーション ユニット サイズで作成された場合は、ファイル システムの書式設定が失敗します。 新しいボリュームは使用できません。 解決策は、ボリュームを削除し、64 K のアロケーション ユニット サイズを使用することです。

### 更新プログラム

- 更新プログラムをインストールすると、インストール ステータスがキャッシュして、ブラウザーの更新が必要です。

- エラーが発生した可能性があります:「キーセットが存在しない」Azure の更新プログラムの管理を設定しようとしています。 この例では、管理ノードのでは、次の修復手順をやり直してください。
    1. '暗号化サービス' サービスを停止します。
    2. 表示するフォルダーのオプションを変更するでは、(必要な場合) にファイルが表示されません。
    3. "%Allusersprofile%\microsoft\crypto\rsa\s-1-5-18"フォルダーにあり、その内容をすべて削除します。
    4. '暗号化サービス' サービスを再起動します。
    5. Windows Admin Center で更新プログラムの管理の設定を繰り返す

### 仮想マシン

- Windows Server 2012 ホスト上の仮想マシンを管理するときに、ブラウザーで VM が接続ツールは、VM への接続に失敗します。 仮想マシンに接続して .rdp ファイルをダウンロードして動作する必要があります。 [20258278]

- Azure Site Recovery – ASR が WAC、外部ホスト上のセットアップである場合はできないことから WAC [18972276] 内の VM を保護するには

- 仮想 SAN マネージャー、Move VM、Export VM、VM レプリケーションなどの Hyper-V マネージャーで利用可能な高度な機能は、現在サポートされていません。

### 仮想スイッチ

- スイッチ埋め込みチーミング (SET): NIC をチームに追加する場合は、NIC が同じサブネット上にある必要があります。

## コンピューターの管理ソリューション

コンピューターの管理ソリューションには、サーバー マネージャー ソリューションのツールのサブセットが含まれているため、同じ既知の問題と共に、次のコンピューターの管理ソリューション特有の問題が該当します。

- Microsoft アカウント ([MSA](https://account.microsoft.com/account/)) を使用するか、Azure Active Directory (AAD) を使用して Windows 10 のコンピューターにログオンするためを指定する場合"管理-として"ローカル マシン [16568455] を管理する資格情報

- ローカル ホストを管理しようとすると、ゲートウェイ プロセスを昇格するように求められます。 続いて表示される [ユーザー アカウント制御] ポップアップで **[いいえ]** をクリックすると、Windows Admin Center でそれを表示することができなくなります。 この場合、システム トレイの Windows Admin Center アイコンを右クリックし、[終了] を選択することでゲートウェイ プロセスを終了し、[スタート] メニューから Windows Admin Center を再起動します。

- Windows 10 では既定で WinRM/PowerShell リモート処理が有効になっていません。
  
  - Windows 10 クライアントの管理を有効にするには、管理者特権の PowerShell プロンプトから ```Enable-PSRemoting``` コマンドを実行する必要があります。

  - また、```Set-NetFirewallRule -Name WINRM-HTTP-In-TCP -RemoteAddress Any``` を使用して、ローカル サブネットの外部から接続を許可できるようにファイアウォールを更新する必要があります。 より制限の厳しいネットワーク シナリオでは、[このドキュメント](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/enable-psremoting?view=powershell-5.1)を参照してください。

## フェールオーバー クラスター マネージャー ソリューション

- クラスター (ハイパーコンバージドまたは従来のクラスターのいずれか) を管理するときに、**shell was not found** (シェルが見つかりませんでした) というエラーが発生する場合があります。 この問題が発生した場合は、お使いのブラウザーを再読み込みするか、別のツールに移動して戻ります。 [13882442]

- 完全に構成されていない下位バージョン (Windows Server 2012 または 2012 R2) のクラスターを管理するときに問題が発生することがあります。 この問題の解決方法は、Windows の機能**RSAT クラスタ リング PowerShell**がインストールされ、クラスターの**各メンバー ノード**で有効になっていることを確認することです。 PowerShell でこれを行うには、すべてのクラスター ノードで `Install-WindowsFeature -Name RSAT-Windows-PowerShell` コマンドを入力します。 [12524664]

- クラスターは正しく検出されるように全 FQDN を指定して追加する必要があります。

- ゲートウェイとしてインストールされた Windows Admin Center を使用してクラスターに接続する場合は、メンバー ノードを照会するために資格情報を利用できるように、**Use these credentials for all connections** (これらの資格情報をすべての接続に使用する) を選択する必要があります。

## ハイパーコンバージド クラスター マネージャー ソリューション

- **Drives - Update firmware**、**Servers - Remove**、および **Volumes - Open** などの一部のコマンドは無効になっていて現在サポートされていません。