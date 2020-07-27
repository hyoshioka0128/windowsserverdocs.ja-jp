---
title: Nano Server を展開します。
description: カスタム イメージ、パッケージ、ドライバー、ドメイン、役割、機能を作成および展開する方法について説明します。
ms.prod: windows-server
manager: DonGill
ms.technology: server-nano
ms.date: 09/06/2017
ms.topic: conceptual
ms.assetid: 9f109c91-7c2e-4065-856c-ce9e2e9ce558
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: e3d710a8c701b52bda62c5cd0616a44f37fe2e7b
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86962034"
---
# <a name="deploy-nano-server"></a>Nano Server を展開します。

> 適用先:Windows Server 2016

> [!IMPORTANT]
> Windows Server バージョン 1709 以降では、Nano Server は[コンテナーの基本 OS イメージ](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)としてのみ提供されます。 その意味については、[Nano Server に加えられる変更](nano-in-semi-annual-channel.md)に関する記事をご覧ください。

このトピックでは、Nano Server のクイック スタート トピックに示されている簡単な例と比較して、ニーズに合わせてより多くのカスタマイズが加えられた Nano Server のイメージを展開するのに必要な情報を取り上げます。 必要な機能のみを備えたカスタム Nano Server イメージの作成、VHD または WIM からの Nano Server イメージのインストール、ファイルの編集、ドメインの操作、さまざまな方法によるパッケージの操作、およびサーバーの役割の操作に関する情報が含まれています。

## <a name="nano-server-image-builder"></a>Nano Server Image Builder

Nano Server Image Builder は、グラフィカル インターフェイスを使用してカスタム Nano Server イメージと起動可能な USB メディアの作成を支援するツールです。 指定した入力に基づいて、Windows Server 2016 Datacenter Edition または Standard Edition を実行する Nano Server の一貫したインストールを簡単に自動化できる、再利用可能な PowerShell スクリプトを生成します。

[ダウンロード センター](https://www.microsoft.com/download/details.aspx?id=54065)からツールを入手します。

このツールを使用するには、[Windows アセスメント & デプロイメント キット (ADK)](https://developer.microsoft.comwindows/hardware/windows-assessment-deployment-kit) も必要になります。


Nano Server Image Builder では、カスタマイズされた Nano Server イメージを VHD、VHDX、または ISO 形式で作成することや、Nano Server を展開したりサーバーのハードウェア構成を検出したりするための起動可能な USB メディアを作成することができます。 次の操作を行うこともできます。

- ライセンス条項に同意する。
- イメージを VHD、VHDX、または ISO 形式で作成する。
- サーバーの役割を追加する。
- デバイス ドライバーを追加する。
- コンピューター名、管理者のパスワード、ログ ファイルのパス、およびタイムゾーンを設定する。
- 既存の Active Directory アカウントまたは取得されたドメイン参加 BLOB を使用して、ドメインに参加する。
- ローカル サブネットの外部の通信用に WinRM を有効にする。
- 仮想 LAN ID を有効にし、静的 IP アドレスを構成する。
- 実行時に新しいサービス パッケージを挿入する。
- unattend.xml が処理された後に実行する setupcomplete.cmd またはその他のカスタマー スクリプトを追加する。
- 緊急管理サービス (EMS) を有効にして、シリアル ポート コンソールにアクセスできるようにする。
- 開発サービスを有効にして、テスト署名されたドライバー、署名されていないアプリケーション、および PowerShell の既定のシェルを有効にする。
- シリアル、USB、TCP/IP、または IEEE 1394 プロトコルでのデバッグを有効にする。
- WinPE を使用して、サーバーをパーティション分割し、Nano イメージをインストールする USB メディアを作成する。
- WinPE を使用して、既存の Nano Server のハードウェア構成を検出し、すべての詳細レポートをログと画面に出力する USB メディアを作成する。 報告される情報には、ネットワーク アダプター、MAC アドレス、およびファームウェアの種類 (BIOS または UEFI) が含まれます。 検出プロセスにより、システムのすべてのボリュームと、Server Core のドライバー パッケージにドライバーが含まれていないデバイスの一覧も出力されます。

これらを初めて取り扱う場合は、このトピックの残りの部分と Nano Server に関する他のトピックを読むと、ツールに必要な情報を準備できるようになります。

## <a name="creating-a-custom-nano-server-image"></a><a name=BKMK_CreateImage></a>カスタム Nano Server イメージの作成

Windows Server 2016 の場合、Nano Server は物理メディアで配布されます。物理メディア内には、**NanoServer** フォルダーに .wim イメージと **Packages** という名前のサブフォルダーが含まれています。 これらのパッケージ ファイルを使用して、サーバーの役割や機能を VHD イメージに追加し、そのイメージから起動します。

これらのパッケージは、PackageManagement (OneGet) PowerShell モジュールの NanoServerPackage プロバイダーを使って検索およびインストールすることもできます。 このトピックの「オンラインでの役割と機能のインストール」を参照してください。

次の表に、Nano Server のこのリリースで利用できる役割と機能、およびそれに対応するパッケージをインストールするための Windows PowerShell オプションを示します。 一部のパッケージは、Windows PowerShell スイッチ (たとえば、-Compute) を指定することで直接インストールされます。その他のパッケージについては、-Package パラメーターにパッケージ名を渡してインストールします。この場合は、コンマ区切り形式で複数の名前を指定できます。 Get-NanoServerPackage コマンドレットを使用すると、利用可能なパッケージを動的に一覧表示できます。

|| 役割または機能 | オプション |
|--|--|
| Hyper-V の役割 (NetQoS を含む) | -Compute |
| フェールオーバー クラスタリングとその他のコンポーネント (詳細はこの表の後に示す) | -Clustering |
| 各種ネットワーク アダプターと記憶域コントローラーの基本的なドライバー。 これは、Windows Server 2016 の Server Core インストールに含まれるドライバーのセットと同じです。 | -OEMDrivers |
| ファイル サーバーの役割とその他の記憶域コンポーネント (詳細はこの表の後に示す) | -Storage |
| 既定の署名ファイルを含む Windows Defender | -Defender |
| Ruby、Node.js などの一般的なアプリケーション フレームワークのアプリケーションの互換性を保つための Reverse Forwarder | 既定で含まれるようになりました |
| DNS サーバーの役割 | -Package Microsoft-NanoServer-DNS-Package |
| PowerShell Desired State Configuration (DSC) | -Package Microsoft-NanoServer-DSC-Package<p>**注:** 詳細については、「[DSC on Nano Server の使用](/archive/blogs/askcore/kms-host-client-count-not-increasing-due-to-duplicate-cmids)」を参照してください。 |
| Internet Information Server (IIS) | -Package Microsoft-NanoServer-IIS-Package<p>**注:** IIS の操作の詳細については、「[Nano Server の IIS](IIS-on-Nano-Server.md)」を参照してください。 |
| Windows コンテナーのホストのサポート | -Containers |
| System Center Virtual Machine Manager エージェント | -Package Microsoft-NanoServer-SCVMM-Package<p>-Package Microsoft-NanoServer-SCVMM-Compute-Package<p>**注:** Hyper-V を監視する場合にのみ SCVMM Compute パッケージを使用します。 VMM でのハイパーコンバージドの展開には、-Storage パラメーターも指定してください。 詳しくは、[VMM のマニュアル](/system-center/vmm/hyper-v-nano?view=sc-vmm-2016&viewFallbackFrom=sc-vmm-2019)をご覧ください。 |
| System Center Operations Manager エージェント | 個別にインストールされます。 詳細については、 https://technet.microsoft.com/system-center-docs/om/manage/install-agent-on-nano-server の System Center Operations Manager のドキュメントをご覧ください。 |
| データ センター ブリッジング (DCBQoS を含む) | -Package Microsoft-NanoServer-DCB-Package |
| 仮想マシンでの展開 | -Package Microsoft-NanoServer-Guest-Package |
| 物理マシンでの展開 | - Package Microsoft-NanoServer-Host-Package |
| BitLocker、トラステッド プラットフォーム モジュール (TPM)、ボリュームの暗号化、プラットフォームの識別、暗号化プロバイダー、およびセキュア スタートアップに関連するその他の機能 | -Package Microsoft-NanoServer-SecureStartup-Package |
| Hyper-V によるシールドされた VM のサポート | -Package Microsoft-NanoServer-ShieldedVM-Package<p>**注:** このパッケージは、Nano Server の Datacenter Edition でのみ利用できます。 |
| 簡易ネットワーク管理プロトコル (SNMP) エージェント | -Package Microsoft-NanoServer-SNMP-Agent-Package.cab<p>**注:** Windows Server 2016 インストール メディアには含まれていません。 オンラインでのみ入手できます。 詳しくは、「[オンラインでの役割と機能のインストール](#BKMK_online)」をご覧ください。 |
| IPv6 移行テクノロジ (6to4、ISATAP、Port Proxy、Teredo) を使用してトンネル接続を提供する IPHelper サービスと、IP-HTTPS | -Package Microsoft-NanoServer-IPHelper-Service-Package.cab<p>**注:** Windows Server 2016 インストール メディアには含まれていません。 オンラインでのみ入手できます。 詳しくは、「[オンラインでの役割と機能のインストール](#BKMK_online)」をご覧ください。 ||

> [!NOTE]
> これらのオプションを使ってパッケージをインストールすると、選択したサーバー メディアのロケールに基づいて対応する言語パックもインストールされます。 利用可能な言語パックとそのロケールの省略形は、インストール メディア内のイメージのロケールの名前が付いたサブフォルダーを見るとわかります。

> [!NOTE]
> -Storage パラメーターを使用してファイル サービスをインストールしても、ファイル サービスは実際には有効になりません。 この機能は、サーバー マネージャーを使用してリモート コンピューターから有効にします。

### <a name="failover-clustering-items-installed-by-the--clustering-parameter"></a>-Clustering パラメーターによってインストールされるフェールオーバー クラスタリング項目

- フェールオーバー クラスタリングの役割
- VM フェールオーバー クラスタリング
- 記憶域スペース ダイレクト (S2D)
- 記憶域のサービスの品質 (QoS)
- ボリューム レプリケーション クラスタリング
- SMB 監視サービス

### <a name="file-and-storage-items-installed-by-the--storage-parameter"></a>-Storage パラメーターによってインストールされるファイルとストレージの項目

- ファイル サーバーの管理
- データ重複除去
- Microsoft デバイス固有モジュール (MSDSM) 用のドライバーを含むマルチパス I/O
- ReFS (v1 および v2)
- iSCSI イニシエーター (ただし iSCSI ターゲットではない)
- 記憶域レプリカ
- SMI-S のサポートを含む記憶域管理サービス
- SMB 監視サービス
- ダイナミック ボリューム
- 基本的な Windows 記憶域プロバイダー (Windows 記憶域管理用)

### <a name="installing-a-nano-server-vhd"></a>Nano Server VHD のインストール

この例では、ネットワーク共有上の Nano Server インストール メディアから、Hyper-V ゲスト ドライバーを含む、指定したコンピューター名の GPT ベースの VHDX イメージを作成します。 管理者特権での Windows PowerShell プロンプトで、次のコマンドレットを入力します。

`Import-Module <Server media location>\NanoServer\NanoServerImageGenerator; New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\server_en-us -BasePath .\Base -TargetPath .\FirstStepsNano.vhdx -ComputerName FirstStepsNano`

このコマンドレットは、次のすべてのタスクを実行します。

1. 基本エディションとして Standard を選択する。

2. 管理者パスワードを要求する。

3. インストール メディアを \\\Path\To\Media\server_en-us から .\Base にコピーする。

4. WIM イメージを VHD に変換する (ターゲット パス引数のファイル拡張子によって、第 1 世代仮想マシン用の MBR ベースの VHD と第 2 世代仮想マシン用の GPT ベースの VHDX のどちらを作成するかが決まります)。

5. 作成された VHD を .\FirstStepsNano.vhdx にコピーする。

6. イメージの管理者パスワードを指定されたパスワードに設定する。

7. イメージのコンピューター名を FirstStepsNano に設定する。

8. Hyper-V ゲスト ドライバーをインストールする。

上記の操作により、.\FirstStepsNano.vhdx イメージが作成されます。

このコマンドレットの実行に伴ってログが生成され、処理が終了するとログの場所が通知されます。 コンパニオン スクリプトによって実行される WIM から VHD への変換では、%TEMP%\Convert-WindowsImage\\\<GUID> に独自のログが生成されます (ここで、\<GUID> は、変換セッションごとの一意の識別子です)。

基本パスからキャッシュされたファイルが使用されるため、同じ基本パスを使用する限り、このコマンドレットを実行するたびにメディア パス パラメーターを指定する必要はありません。 基本パスを指定しない場合、TEMP フォルダーに既定のパスが生成されます。 ただし、別のソース メディアで同じ基本パスを使用する場合は、メディア パス パラメーターを指定する必要があります。

> [!NOTE]
> Nano Server エディションを指定して、Standard Edition または Datacenter Edition を作成できるようになりました。 *Standard* Edition または *Datacenter* Edition を指定するには、-Edition パラメーターを使用します。

既存のイメージがある場合は、必要に応じて *Edit-NanoServerImage* コマンドレットを使用してイメージを変更できます。

コンピューター名を指定しない場合、ランダムな名前が生成されます。

### <a name="installing-a-nano-server-wim"></a>Nano Server WIM のインストール

1. Windows Server 2016 ISO の \NanoServer フォルダーにある *NanoServerImageGenerator* フォルダーを、お使いのコンピューターのローカル フォルダーにコピーします。
2. 管理者として Windows PowerShell を起動します。NanoServerImageGenerator フォルダーを配置したフォルダーに移動し、`Import-Module .\NanoServerImageGenerator -Verbose` を使ってモジュールをインポートします。

   >[!NOTE]
   >場合によっては Windows PowerShell 実行ポリシーを調整する必要があります。その場合は、 `Set-ExecutionPolicy RemoteSigned` を使います。

Hyper-V ホストとして機能する Nano Server イメージを作成するには、以下を実行します。

`New-NanoServerImage -Edition Standard -DeploymentType Host -MediaPath <path to root of media> -BasePath .\Base -TargetPath .\NanoServerPhysical\NanoServer.wim -ComputerName <computer name> -OEMDrivers -Compute -Clustering`

[場所]
- MediaPath は、Windows Server 2016 を含む DVD メディアまたは ISO イメージのルートです。
- `-BasePath` には Nano Server のバイナリのコピーが格納されます。したがって、将来の実行で -MediaPath を指定する必要なく New-NanoServerImage -BasePath を使用できます。
- `-TargetPath` には、選択した役割と機能を含む、作成された .wim ファイルが格納されます。 拡張子 .wim を必ず指定してください。
- `-Compute` は、Hyper-V の役割を追加します。
- `-OemDrivers` は、いくつかの一般的なドライバーを追加します。

管理者パスワードの入力を求められます。

詳細を確認するには、`Get-Help New-NanoServerImage -Full` を実行してください。

WinPE で起動し、先ほど作成した .wim ファイルが WinPE からアクセスできることを確認します (たとえば、.wim ファイルを USB フラッシュ ドライブ上の起動可能な WinPE イメージにコピーします)。

WinPE が起動したら、Diskpart.exe を使用してターゲット コンピューターのハード ドライブを準備します。 次の Diskpart コマンドを実行します (UEFI と GPT を使用していない場合は適宜変更してください)。

> [!WARNING]
> 以下のコマンドを実行すると、ハード ドライブ上のすべてのデータが削除されます。

  ```
  Diskpart.exe
  Select disk 0
  Clean
  Convert GPT
  Create partition efi size=100
  Format quick FS=FAT32 label=System
  Assign letter=s
  Create partition msr size=128
  Create partition primary
  Format quick FS=NTFS label=NanoServer
  Assign letter=n
  List volume
  Exit
  ```

Nano Server イメージを適用します (.wim ファイルのパスを調整してください)。

```
Dism.exe /apply-image /imagefile:.\NanoServer.wim /index:1 /applydir:n:\
Bcdboot.exe n:\Windows /s s:
```

DVD メディアまたは USB ドライブを取り外し、**Wpeutil.exe reboot** を使用してシステムを再起動します。

### <a name="editing-files-on-nano-server-locally-and-remotely"></a>ローカルおよびリモートでの Nano Server 上のファイルの編集

どちらの場合でも、Windows PowerShell リモート処理などを使って Nano Server に接続します。

Nano Server に接続した後は、psEdit コマンドにファイルの相対パスまたは絶対パスを渡すことによって、ローカル コンピューター上にあるファイルを編集できます。例: `psEdit C:\Windows\Logs\DISM\dism.log` または `psEdit .\myScript.ps1`

`Enter-PSSession -ComputerName 192.168.0.100 -Credential ~\Administrator` を使用してリモート セッションを開始した後、次のように psEdit コマンドにファイルの相対パスまたは絶対パスを渡して、リモート Nano Server 上にあるファイルを編集します。`psEdit C:\Windows\Logs\DISM\dism.log`

## <a name="installing-roles-and-features-online"></a><a name=BKMK_online></a>オンラインでの役割と機能のインストール

> [!NOTE]
> オプションの Nano Server パッケージをメディアやオンライン リポジトリからインストールした場合、最近のセキュリティ修正プログラムは含まれていません。 オプションのパッケージとベースとなるオペレーティング システム間のバージョンの不一致を避けるためには、オプションのパッケージをインストールした直後かつサーバーを再起動する**前に**、[最新の累積的な更新プログラム](./update-nano-server.md)をインストールする必要があります。

### <a name="installing-roles-and-features-from-a-package-repository"></a>パッケージ リポジトリからの役割と機能のインストール

PackageManagement PowerShell モジュールの NanoServerPackage プロバイダーを使用して、オンライン パッケージ リポジトリから Nano Server パッケージを検索してインストールできます。 このプロバイダーをインストールするには、次のコマンドレットを使用します。

```powershell
Install-PackageProvider NanoServerPackage
Import-PackageProvider NanoServerPackage
```

>[!NOTE]
>Install-PackageProvider の実行時にエラーが発生した場合、[最新の累積的な更新プログラム](./update-nano-server.md) ([KB3206632](https://support.microsoft.com/kb/3206632) 以降) をインストールしたことを確認するか、次のように Save-Module を使います。

```powershell
Save-Module -Path $Env:ProgramFiles\WindowsPowerShell\Modules\ -Name NanoServerPackage -MinimumVersion 1.0.1.0
Import-PackageProvider NanoServerPackage
```

このプロバイダーをインストールしてインポートした後は、Nano Server パッケージの操作用に設計されたコマンドレットを使用して、Nano Server パッケージを検索、ダウンロード、インストールできます。

```powershell
Find-NanoServerPackage
Save-NanoServerPackage
Install-NanoServerPackage
```

汎用の PackageManagement コマンドレットを使用して、NanoServerPackage プロバイダーを指定することもできます。

```powershell
Find-Package -ProviderName NanoServerPackage
Save-Package -ProviderName NanoServerPackage
Install-Package -ProviderName NanoServerPackage
Get-Package -ProviderName NanoServerPackage
```

Nano Server 上の Nano Server パッケージにこれらのコマンドレットのいずれかを使用するには、`-ProviderName NanoServerPackage` を追加します。 -ProviderName パラメーターを追加しない場合、PackageManagement はすべてのプロバイダーに対して処理を繰り返し実行します。 これらのコマンドレットの詳細を確認するには、`Get-Help <cmdlet>` を実行します。 以下に一般的な使用例を示します。

### <a name="searching-for-nano-server-packages"></a>Nano Server パッケージの検索

`Find-NanoServerPackage` または `Find-Package -ProviderName NanoServerPackage` のどちらかを使用すると、オンライン リポジトリで使用できる Nano Server パッケージを検索して、その一覧を取得できます。 たとえば、以下を使用して、最新のパッケージの全一覧を取得できます。

```powershell
Find-NanoServerPackage
```

`Find-Package -ProviderName NanoServerPackage -DisplayCulture` を実行すると、使用可能なすべてのカルチャが表示されます。

米国英語などの特定のロケール バージョンが必要な場合は、`Find-NanoServerPackage -Culture en-us`、`Find-Package -ProviderName NanoServerPackage -Culture en-us`、または `Find-Package -Culture en-us -DisplayCulture` を使用できます。

パッケージ名で特定のパッケージを検索するには、-Name パラメーターを使用します。 このパラメーターでは、ワイルドカードも許可されます。 たとえば、名前に VMM が含まれるパッケージをすべて検索するには、`Find-NanoServerPackage -Name *VMM*` または `Find-Package -ProviderName NanoServerPackage -Name *VMM*` を使用します。

-RequiredVersion、-MinimumVersion、または -MaximumVersion パラメーターを使用すると、特定のバージョンを検索できます。 使用可能なすべてのバージョンを検索するには、-AllVersions を使用します。 それ以外の場合は、最新バージョンのみが返されます。 たとえば、 `Find-NanoServerPackage -Name *VMM* -RequiredVersion 10.0.14393.0`と指定します。 すべてのバージョンの場合は、次のようになります。`Find-Package -ProviderName NanoServerPackage -Name *VMM* -AllVersions`

### <a name="installing-nano-server-packages"></a>Nano Server パッケージのインストール

`Install-NanoServerPackage` または `Install-Package -ProviderName NanoServerPackage` のどちらかを使用して、Nano Server パッケージ (存在する場合はその依存関係パッケージを含む) を Nano Server にローカルに、またはオフライン イメージにインストールできます。 これらはどちらも、パイプラインから入力を受け取ります。

最新バージョンの Nano Server パッケージをオンラインの Nano Server にインストールするには、`Install-NanoServerPackage -Name Microsoft-NanoServer-Containers-Package` または `Install-Package -Name Microsoft-NanoServer-Containers-Package` のどちらかを使用します。 PackageManagement は Nano Server のカルチャを使用します。

次のように特定のバージョンとカルチャを指定して、Nano Server パッケージをオフライン イメージにインストールすることができます。

`Install-NanoServerPackage -Name Microsoft-NanoServer-DCB-Package -Culture de-de -RequiredVersion 10.0.14393.0 -ToVhd C:\MyNanoVhd.vhd`

または

`Install-Package -Name Microsoft-NanoServer-DCB-Package -Culture de-de -RequiredVersion 10.0.14393.0 -ToVhd C:\MyNanoVhd.vhd`

パッケージの検索結果をパイプラインでインストール コマンドレットに渡す例を次に示します。

`Find-NanoServerPackage *dcb* | Install-NanoServerPackage` を実行すると、名前に dcb が含まれるパッケージがすべて検索され、それらがインストールされます。

`Find-Package *nanoserver-compute-* | Install-Package` を実行すると、名前に nanoserver-compute- が含まれるパッケージが検索され、それらがインストールされます。

`Find-NanoServerPackage -Name *nanoserver-compute* | Install-NanoServerPackage -ToVhd C:\MyNanoVhd.vhd` を実行すると、名前に compute が含まれるパッケージが検索され、それらがオフライン イメージにインストールされます。

`Find-Package -ProviderName NanoserverPackage *nanoserver-compute-* | Install-Package -ToVhd C:\MyNanoVhd.vhd` を実行すると、名前に nanoserver-compute- が含まれるすべてのパッケージに対して同じ操作が実行されます。

### <a name="downloading-nano-server-packages"></a>Nano Server パッケージのダウンロード

`Save-NanoServerPackage` または `Save-Package` を使用すると、パッケージをインストールすることなくダウンロードして保存できます。 どちらのコマンドレットも、パイプラインから入力を受け取ります。

たとえば、Nano Server パッケージをダウンロードして、ワイルドカード パスと一致するディレクトリに保存するには、`Save-NanoServerPackage -Name Microsoft-NanoServer-DNS-Package -Path C:\` を使用します。この例では、-Culture が指定されていないため、ローカル コンピューターのカルチャが使用されます。 また、バージョンも指定されていないため、最新のバージョンが保存されます。

`Save-Package -ProviderName NanoServerPackage -Name Microsoft-NanoServer-IIS-Package -Path C:\ -Culture it-IT -MinimumVersion 10.0.14393.0` は、特定のバージョンの、言語とロケールがイタリア語のパッケージを保存します。

次の例に示すように、パイプラインによって検索結果を送信できます。

`Find-NanoServerPackage -Name *containers* -MaximumVersion 10.2 -MinimumVersion 1.0 -Culture es-ES | Save-NanoServerPackage -Path C:\`

または

`Find-Package -ProviderName NanoServerPackage -Name *shield* -Culture es-ES | Save-Package -Path`

### <a name="inventory-installed-packages"></a>インストール済みパッケージの一覧の取得

`Get-Package` を使用すると、インストール済みの Nano Server パッケージを検出できます。 たとえば、Nano Server 上にあるパッケージを表示するには、`Get-Package -ProviderName NanoserverPackage` を使用します。

オフライン イメージにインストールされている Nano Server パッケージを確認するには、`Get-Package -ProviderName NanoserverPackage -FromVhd C:\MyNanoVhd.vhd` を実行します。

### <a name="installing-roles-and-features-from-local-source"></a>ローカル ソースからの役割と機能のインストール

サーバーの役割と他のパッケージのインストールはオフラインで実行することをお勧めしますが、コンテナー シナリオでは (Nano Server の実行中に) オンラインでインストールすることが必要になる場合があります。 これを行うには、次の手順に従います。

1. Packages フォルダーをインストール メディアから実行中の Nano Server (たとえば、C:\packages) にローカルにコピーします。

2. 別のコンピューター上に新しい Unattend.xml ファイルを作成し、Nano Server にコピーします。 この XML コンテンツをコピーし、作成した XML ファイルに貼り付けてもかまいません (この例では、IIS パッケージをインストールします)。

  ```
  <?xml version=1.0 encoding=utf-8?>
      <unattend xmlns=urn:schemas-microsoft-com:unattend>
      <servicing>
          <package action=install>
              <assemblyIdentity name=Microsoft-NanoServer-IIS-Feature-Package version=10.0.14393.0 processorArchitecture=amd64 publicKeyToken=31bf3856ad364e35 language=neutral />
              <source location=c:\packages\Microsoft-NanoServer-IIS-Package.cab />
          </package>
          <package action=install>
              <assemblyIdentity name=Microsoft-NanoServer-IIS-Feature-Package version=10.0.14393.0 processorArchitecture=amd64 publicKeyToken=31bf3856ad364e35 language=en-US />
              <source location=c:\packages\en-us\Microsoft-NanoServer-IIS-Package_en-us.cab />
          </package>
      </servicing>
      <cpi:offlineImage cpi:source= xmlns:cpi=urn:schemas-microsoft-com:cpi />
  </unattend>
  ```

3. 作成 (またはコピー) した新しい XML ファイルを編集して、"C:\packages" を、Packages の内容をコピーしたディレクトリに変更します。

4. 新しく作成した XML ファイルがあるディレクトリに移動し、以下を実行します。`dism /online /apply-unattend:.\unattend.xml`

5. 以下を実行して、パッケージとその関連する言語パックが正しくインストールされていることを確認します。`dism /online /get-packages`

   Package Identity : Microsoft-NanoServer-IIS-Package~31bf3856ad364e35~amd64~en-US~10.0.10586.0 が 2 か所に表示されます。1 つは Release Type : "Package Identity : Microsoft-NanoServer-IIS-Package~31bf3856ad364e35~amd64~~10.0.14393.1000"が表示されます。

## <a name="customizing-an-existing-nano-server-vhd"></a>既存の Nano Server VHD のカスタマイズ

次の例に示すように、Edit-NanoServerImage コマンドレットを使用して既存の VHD の詳細を変更できます。`Edit-NanoServerImage   -BasePath .\Base   -TargetPath .\BYOVHD.vhd`

このコマンドレットは New-NanoServerImage と同じ効果を持ちますが、WIM を VHD に変換する代わりに既存のイメージを変更します。 Edit-NanoServerImage では、-MediaPath と -MaxSize を除いて New-NanoServerImage と同じパラメーターをサポートしています。したがって、Edit-NanoServerImage で変更を加える前に、これらのパラメーターを使用して初期の VHD が作成されている必要があります。

## <a name="additional-tasks-you-can-accomplish-with-new-nanoserverimage-and-edit-nanoserverimage"></a>New-NanoServerImage と Edit-NanoServerImage を使用して実行できるその他のタスク

### <a name="joining-domains"></a>ドメインへの参加

New-NanoServerImage は、ドメインに参加するための 2 つの方法を提供します。どちらもオフラインのドメイン プロビジョニングに依存しますが、1 つ目の方法では BLOB を取得して参加を実現します。 この例のコマンドレットでは、Contoso ドメインのドメイン BLOB をローカル コンピューター (このコンピューターは当然 Contoso ドメインの一部である必要があります) から取得し、BLOB を使用してイメージのオフライン プロビジョニングを実行します。

`New-NanoServerImage -Edition Standard -DeploymentType Host -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\JoinDomHarvest.vhdx -ComputerName JoinDomHarvest -DomainName Contoso`

このコマンドレットが完了すると、Active Directory のコンピューターの一覧に JoinDomHarvest という名前のコンピューターが表示されます。

このコマンドレットは、ドメインに参加していないコンピューターで使用することもできます。 そのためには、ドメインに参加している任意のコンピューターから BLOB を取得し、手動でその BLOB をコマンドレットに渡します。 他のコンピューターからこのような BLOB を取得すると、BLOB にはそのコンピューターの名前が既に含まれています。したがって、 *-ComputerName* パラメーターを追加しようとするとエラーが発生します。

次のコマンドを使用して BLOB を取得できます。

```
djoin
/Provision
/Domain Contoso
/Machine JoiningDomainsNoHarvest
/SaveFile JoiningDomainsNoHarvest.djoin
```

取得した BLOB を使用して New-NanoServerImage を実行します。

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\JoinDomNoHrvest.vhd -DomainBlobPath .\Path\To\Domain\Blob\JoinDomNoHrvestContoso.djoin`

将来の Nano Server と同じコンピューター名を持つノードが既にドメインにある場合、`-ReuseDomainNode` パラメーターを追加することでそのコンピューター名を再利用できます。

### <a name="adding-additional-drivers"></a>ドライバーの追加

Nano Server には、各種のネットワーク アダプターと記憶域コントローラー用の基本的なドライバーのセットを含むパッケージが用意されていますが、お使いのネットワーク アダプターのドライバーが含まれていない場合もあります。 次の手順を使用すると、動作中のシステム内でドライバーを検索および抽出し、それを Nano Server イメージに追加できます。

1. Nano Server を実行する物理コンピューターに Windows Server 2016 をインストールします。
2. デバイス マネージャーを開き、次のカテゴリのデバイスを確認します。
3. ネットワーク アダプター
4. 記憶域コントローラー
5. ディスク ドライブ
6. これらのカテゴリのデバイスごとに、デバイス名を右クリックし、 **[プロパティ]** をクリックします。 表示されたダイアログ ボックスで、 **[ドライバー]** タブをクリックし、 **[ドライバーの詳細]** をクリックします。
7. 表示されたドライバー ファイルのパスとファイル名をメモします。 たとえば、ドライバー ファイルが e1i63x64.sys で、C:\Windows\System32\Drivers にあると示されているとします。
8. コマンド プロンプトで「dir e1i*.sys /s /b」と入力して、このドライバー ファイルとすべてのインスタンスを検索します。 この例では、ドライバー ファイルがパス C:\Windows\System32\DriverStore\FileRepository\net1ic64.inf_amd64_fafa7441408bbecd\e1i63x64.sys にも存在します。
9. 管理者特権でのコマンド プロンプトで、Nano Server VHD があるディレクトリに移動し、次のコマンドを実行します。

  ```
  md mountdir
  dism\dism /Mount-Image /ImageFile:.\NanoServer.vhd /Index:1 /MountDir:.\mountdir
  dism\dism /Add-Driver /image:.\mountdir /driver: C:\Windows\System32\DriverStore\FileRepository\net1ic64.inf_amd64_fafa7441408bbecd
  dism\dism /Unmount-Image /MountDir:.\MountDir /Commit
  ```

10. 必要なそれぞれのドライバー ファイルに対してこの手順を繰り返します。

> [!NOTE]
> ドライバーを保存するフォルダーには、SYS ファイルと対応する INF ファイルの両方が存在している必要があります。 また、Nano Server では、署名済みの 64 ビット ドライバーのみがサポートされます。

### <a name="injecting-drivers"></a>ドライバーの挿入

Nano Server には、各種のネットワーク アダプターと記憶域コントローラー用の基本的なドライバーのセットを含むパッケージが用意されていますが、お使いのネットワーク アダプターのドライバーが含まれていない場合もあります。 次の構文を使用すると、New-NanoServerImage でディレクトリ内の使用可能なドライバーを検索して Nano Server イメージに挿入することができます。

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\InjectingDrivers.vhdx -DriverPath .\Extra\Drivers`

> [!NOTE]
> ドライバーを保存するフォルダーには、SYS ファイルと対応する INF ファイルの両方が存在している必要があります。 また、Nano Server では、署名済みの 64 ビット ドライバーのみがサポートされます。

-DriverPath パラメーターを使用して、ドライバーの .inf ファイルへのパスの配列を渡すこともできます。

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\InjectingDrivers.vhdx -DriverPath .\Extra\Drivers\netcard64.inf`

### <a name="connecting-with-winrm"></a>WinRM を使用した接続

(同じサブネット上にない別のコンピューターから) Windows リモート管理 (WinRM) を使用して Nano Server コンピューターに接続するには、着信 TCP トラフィック用に Nano Server イメージのポート 5985 を開きます。 次のコマンドレットを使用します。

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\ConnectingOverWinRM.vhd -EnableRemoteManagementPort`

### <a name="setting-static-ip-addresses"></a>静的 IP アドレスの設定

静的 IP アドレスを使用するように Nano Server イメージを構成するには、まず、Get-NetAdapter、netsh、または Nano Server 回復コンソールを使用して変更するインターフェイスの名前またはインデックスを見つけます。 -Ipv6Address、-Ipv6Dns、-Ipv4Address、-Ipv4SubnetMask、-Ipv4Gateway、および -Ipv4Dns パラメーターを使用して構成を指定します。次に例を示します。

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\StaticIpv4.vhd -InterfaceNameOrIndex Ethernet -Ipv4Address 192.168.1.2 -Ipv4SubnetMask 255.255.255.0 -Ipv4Gateway 192.168.1.1 -Ipv4Dns 192.168.1.1`

### <a name="custom-image-size"></a>カスタム イメージのサイズ

-MaxSize パラメーターを使用すると、Nano Server イメージを動的に拡張される VHD または VHDX として構成できます。次に例を示します。

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\BigBoss.vhd -MaxSize 100GB`

### <a name="embedding-custom-data"></a>カスタム データの埋め込み

独自のスクリプトまたはバイナリを Nano Server イメージに埋め込むには、-CopyPath パラメーターを使用して、コピーするファイルおよびディレクトリの配列を渡します。 また、-CopyPath パラメーターでは、ファイルとディレクトリの宛先パスを指定するハッシュテーブルを受け取ることもできます。

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\BigBoss.vhd -CopyPath .\tools`

### <a name="running-custom-commands-after-the-first-boot"></a>初回起動後のカスタム コマンドの実行

setupcomplete.cmd の一部としてカスタム コマンドを実行するには、-SetupCompleteCommand パラメーターを使用して、コマンドの配列を渡します。

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -SetupCompleteCommand @(echo foo, echo bar)`

### <a name="running-custom-powershell-scripts-as-part-of-image-creation"></a>イメージ作成の一環としてのカスタム PowerShell スクリプトの実行

イメージ作成プロセスの一環としてカスタム PowerShell スクリプトを実行するには、-OfflineScriptPathパラメーターを使用して、.ps1 スクリプトへのパスの配列を渡します。 それらのスクリプトが引数を取る場合は、-OfflineScriptArgument を使用して、スクリプトに追加の引数のハッシュテーブルを渡します。

`New-NanoServerImage -DeploymentType Host -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -OfflineScriptPath C:\MyScripts\custom.ps1 -OfflineScriptArgument @{Param1=Value1; Param2=Value2}`

### <a name="support-for-development-scenarios"></a>開発シナリオのサポート

Nano Server 上で開発およびテストを行う場合は、-Development パラメーターを使用することができます。 これにより、既定のローカル シェルとして PowerShell が有効になり、署名されていないドライバーのインストール、デバッガー バイナリのコピー、デバッグ用にポートを開く操作、テスト署名、開発者用ライセンスなしでの AppX パッケージのインストールを行うことができるようになります。

`New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -Development`

### <a name="custom-unattend-file"></a>カスタムの無人セットアップ ファイル

自分で用意した無人セットアップ ファイルを使用する場合は、-UnattendPath パラメーターを使用します。

`New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -UnattendPath \\path\to\unattend.xml`

この無人セットアップ ファイルで管理者パスワードまたはコンピューター名を指定すると、-AdministratorPassword と -ComputerName によって設定された値がオーバーライドされます。

> [!NOTE]
> Nano Server では、無人ファイルを使って TCP/IP 設定を行うことはサポートされていません。 Setupcomplete.cmd を使って TCP/IP 設定を構成できます。

### <a name="collecting-log-files"></a>ログ ファイルの収集

イメージの作成中にログ ファイルを収集する場合は、-LogPath パラメーターを使用して、すべてのログ ファイルがコピーされるディレクトリを指定します。

`New-NanoServerImage -DeploymentType Guest -Edition Standard -MediaPath \\Path\To\Media\en_us -BasePath .\Base -TargetPath .\NanoServer.wim -LogPath C:\Logs`

> [!NOTE]
> New-NanoServerImage および Edit-NanoServerImage の一部のパラメーターは、内部使用のみを目的としており、無視してかまいません。 これには、-SetupUI パラメーターと -Internal パラメーターが含まれます。

### <a name="windows-server-app-installer"></a>Windows Server App インストーラー

Windows Server App (WSA) インストーラーは、Nano Server 向けの信頼性の高いインストール オプションを提供します。 Nano Server では Windows インストーラー (MSI) がサポートされていないため、Microsoft 以外の製品においても WSA が唯一使用可能なインストール テクノロジとなります。 WSA では、宣言型のマニフェストを使用してアプリケーションを安全かつ確実にインストールし、サービスを提供するように設計された Windows アプリ パッケージ テクノロジを利用しています。 WSA は Windows Server に固有の拡張機能をサポートするように Windows アプリ パッケージ インストーラーを拡張したものですが、ドライバーのインストールがサポートされないという制限があります。

Nano Server で WSA パッケージを作成してインストールするには、パッケージの発行者とコンシューマーの双方で特定の手順を実行する必要があります。

パッケージの発行者は、次の手順を実行する必要があります。

1. [Windows 10 SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk) をインストールします。これには、WSA パッケージを作成するために必要なツールであるMakeAppx、MakeCert、Pvk2Pfx、SignTool が含まれています。
2. マニフェストを宣言します。[WSA マニフェスト拡張スキーマ](/uwp/schemas/appxpackage/uapmanifestschema/element-serverpreview-extension-manual)に従って、AppxManifest.xml マニフェスト ファイルを作成します。
3. **MakeAppx** ツールを使用して WSA パッケージを作成します。
4. **MakeCert** ツールと **Pvk2Pfx** ツールを使用して証明書を作成し、**Signtool** ツールを使用してパッケージに署名します。

次に、パッケージのコンシューマーは、次の手順を実行する必要があります。

1. certStoreLocation に Cert:\LocalMachine\TrustedPeople を指定して [*Import-Certificate*](/uwp/schemas/appxpackage/uapmanifestschema/element-serverpreview-extension-manual) PowerShell コマンドレットを実行して、発行者が上記の手順 4. で作成した証明書を Nano Server にインポートします。 たとえば次のようになります。`Import-Certificate -FilePath .\xyz.cer -CertStoreLocation Cert:\LocalMachine\TrustedPeople`
2. [**Add-AppxPackage**](/uwp/schemas/appxpackage/uapmanifestschema/element-serverpreview-extension-manual) PowerShell コマンドレットを実行して、WSA パッケージを Nano Server にインストールすることで、アプリを Nano Server にインストールします。 たとえば次のようになります。`Add-AppxPackage wsaSample.appx`

#### <a name="additional-resources-for-creating-apps"></a>アプリの作成に関連するその他のリソース

WSA は、Windows アプリ パッケージ テクノロジのサーバー拡張機能です (ただし、Microsoft Store ではホストされません)。 WSA を使用したアプリを発行する場合は、アプリ パッケージのパイプラインについて理解するうえで、次のトピックが役に立ちます。

- [基本的なパッケージ マニフェストを作成する方法](/uwp/schemas/appxpackage/how-to-create-a-basic-package-manifest)
- [アプリ パッケージ ツール (MakeAppx.exe)](/windows/win32/appxpkg/make-appx-package--makeappx-exe-)
- [アプリ パッケージの署名証明書を作成する方法](/windows/win32/appxpkg/how-to-create-a-package-signing-certificate)
- [SignTool](/windows/win32/seccrypto/signtool)

### <a name="installing-drivers-on-nano-server"></a>Nano Server へのドライバーのインストール

Microsoft 以外のドライバーは、INF ドライバー パッケージを使用して Nano Server にインストールできます。 これには、プラグ アンド プレイ (PnP) ドライバー パッケージとファイル システム フィルター ドライバー パッケージの両方が含まれます。 ネットワーク フィルター ドライバーは、現在 Nano Server でサポートされていません。

PnP ドライバー パッケージとファイル システム フィルター ドライバー パッケージのどちらも、署名などの一般的なドライバー パッケージ ガイドラインだけでなく、ユニバーサル ドライバーの要件とインストール プロセスに従う必要があります。 これについては、次のトピックで説明されています。

- [ドライバーの署名](/windows-hardware/drivers/install/driver-signing)
- [ユニバーサル INF ファイルの使用](/windows-hardware/drivers/install/using-a-universal-inf-file)

#### <a name="installing-driver-packages-offline"></a>オフラインでのドライバー パッケージのインストール

サポートされているドライバー パッケージは、[DISM.exe](/windows-hardware/manufacture/desktop/dism-driver-servicing-command-line-options-s14) または [DISM PowerShell](/powershell/module/dism/add-windowsdriver?view=win10-ps) コマンドレットを使用してオフラインで Nano Server にインストールできます。

#### <a name="installing-driver-packages-online"></a>オンラインでのドライバー パッケージのインストール
PnP ドライバー パッケージは、[PnpUtil](/windows-hardware/drivers/devtest/pnputil) を使用してオンラインで Nano Server にインストールできます。 Nano Server では、現在、非 PnP ドライバー パッケージのオンラインでのドライバーのインストールはサポートされていません。

## <a name="joining-nano-server-to-a-domain"></a><a name=BKMK_JoinDomain></a>Nano Server のドメインへの参加

### <a name="to-add-nano-server-to-a-domain-online"></a>Nano Server をオンラインでドメインに追加するには

1. 次のコマンドを使用して、Windows Threshold Server を既に実行しているドメインのコンピューターからデータ BLOB を取得します。

    `djoin.exe /provision /domain <domain-name> /machine <machine-name> /savefile .\odjblob`

    このコマンドを実行すると、データ BLOB が odjblob という名前のファイルに保存されます。

2. 次のコマンドを使用して、odjblob ファイルを Nano Server コンピューターにコピーします。

    **net use z: \\\\\<ip address of Nano Server>\c$**

    > [!NOTE]
    > net use コマンドが失敗する場合は、おそらく Windows ファイアウォール規則を調整する必要があります。 そのためには、最初に管理者特権でコマンド プロンプトを開き、Windows PowerShell を起動します。次に、次のコマンドを使用して、Windows PowerShell リモート処理で Nano Server コンピューターに接続します。
    >
    > `Set-Item WSMan:\localhost\Client\TrustedHosts <IP address of Nano Server>`
    >
    > `$ip = <ip address of Nano Server>`
    >
    > `Enter-PSSession -ComputerName $ip -Credential $ip\Administrator`
    >
    > メッセージに従って管理者パスワードを入力し、次のコマンドを実行してファイアウォール規則を設定します。
    >
    > **netsh advfirewall firewall set rule group=File and Printer Sharing new enable=yes**
    >
    > `Exit-PSSession` を使用して Windows PowerShell を終了した後、再度 net use コマンドを実行します。 コマンドが正常に実行された場合は、続いて odjblob ファイルを Nano Server にコピーします。

    **md z:\Temp**

    **copy odjblob z:\Temp**

3. Nano Server を参加させるドメインを確認し、DNS が構成されていることを確認します。 さらに、ドメインまたはドメイン コントローラーの名前解決が正常に動作することを確認します。 そのためには、管理者特権でコマンド プロンプトを開き、Windows PowerShell を起動します。次に、次のコマンドを使用して、Windows PowerShell リモート処理で Nano Server コンピューターに接続します。

    `Set-Item WSMan:\localhost\Client\TrustedHosts <IP address of Nano Server>`

    `$ip = <ip address of Nano Server>`

    `Enter-PSSession -ComputerName $ip -Credential $ip\Administrator`

    メッセージに従って管理者パスワードを入力します。 Nano Server 上では Nslookup を使用できないため、Resolve-DNSName を使用して名前解決を確認します。

4. 名前解決が成功した場合は、同じ Windows PowerShell セッションで次のコマンドを実行して、ドメインに参加します。

    `djoin /requestodj /loadfile c:\Temp\odjblob /windowspath c:\windows /localos`

5. Nano Server コンピューターを再起動した後、Windows PowerShell セッションを終了します。

    `shutdown /r /t 5`

    `Exit-PSSession`

6. Nano Server をドメインに参加させたら、Nano Server の管理者グループにドメイン ユーザー アカウントを追加します。

7. セキュリティ上の理由から、次のコマンドを使用して、信頼されたホストの一覧から Nano Server を削除します。`Set-Item WSMan:\localhost\client\TrustedHosts `

**1 回の操作でドメインに参加する別の方法**

まず、次のコマンドを使用して、Windows Threshold Server を実行している、既にドメインに参加している別のコンピューターからデータ BLOB を取得します。

`djoin.exe /provision /domain <domain-name> /machine <machine-name> /savefile .\odjblob`

(メモ帳などを使って) odjblob ファイルを開き、その内容をコピーし、以下に示す Unattend.xml ファイルの \<AccountData> セクションに貼り付けます。

C:\NanoServer フォルダーにこの Unattend.xml ファイルを配置し、次のコマンドを使用して VHD をマウントし、`offlineServicing` セクションの設定を適用します。

```
dism\dism /Mount-ImagemediaFile:.\NanoServer.vhd /Index:1 /MountDir:.\mountdir
dism\dismmedia:.\mountdir /Apply-Unattend:.\unattend.xml
```

Panther フォルダーを作成します (このフォルダーはセットアップ中にファイルを格納するために Windows システムによって使用されます。詳細については、「[Windows 7、Windows Server 2008 R2、および Windows Vista のセットアップ ログ ファイルの場所](https://support.microsoft.com/kb/927521)」を参照してください)。次に、Unattend.xml ファイルをこのフォルダーにコピーし、VHD のマウントを解除します。そのためには、次のコマンドを使用します。

```
md .\mountdir\windows\panther
copy .\unattend.xml .\mountdir\windows\panther
dism\dism /Unmount-Image /MountDir:.\mountdir /Commit
```

この VHD から初めて Nano Server を起動するとき、その他の設定が適用されます。

Nano Server をドメインに参加させたら、Nano Server の管理者グループにドメイン ユーザー アカウントを追加します。

## <a name="working-with-server-roles-on-nano-server"></a>Nano Server 上のサーバーの役割の操作

### <a name="using-hyper-v-on-nano-server"></a>Nano Server での Hyper-V の使用

Nano Server 上の Hyper-V は、Server Core モードの Windows Server 上の Hyper-V と同じように動作しますが、次の 2 つの例外があります。

- すべての管理操作をリモートで実行する必要があります。管理コンピューターでは、Nano Server と同じビルドの Windows Server が実行されている必要があります。 以前のバージョンの Hyper-V マネージャーおよび Hyper-V Windows PowerShell コマンドレットは動作しません。

- RemoteFX は使用できません。

このリリースでは、Hyper-V の次の機能が検証されています。

- Hyper-V の有効化

- 第 1 世代と第 2 世代の仮想マシンの作成

- 仮想スイッチの作成

- 仮想マシンの起動と Windows ゲスト オペレーティング システムの実行

- Hyper-V レプリカ

仮想マシンのライブ マイグレーションを行う場合、SMB 共有に仮想マシンを作成する場合、または既存の SMB 共有上のリソースを既存の仮想マシンに接続する場合は、認証を正しく構成することが不可欠です。 そのためには、次の 2 つのオプションを使用できます。

**制約付き委任**

制約付き委任は、以前のリリースとまったく同じように動作します。 詳細については、次の記事を参照してください。

- [Hyper-V のリモート管理を有効にする - SMB と高可用性 SMB のための制約付き委任の構成](https://blogs.msdn.com/b/taylorb/archive/2012/03/20/enabling-hyper-v-remote-management-configuring-constrained-delegation-for-smb-and-highly-available-smb.aspx)

- [Hyper-V のリモート管理を有効にする - 非クラスター化ライブ マイグレーションのための制約付き委任の構成](https://blogs.msdn.com/b/taylorb/archive/2012/03/20/enabling-hyper-v-remote-management-configuring-constrained-delegation-for-non-clustered-live-migration.aspx)

**CredSSP**

最初に、このトピックの「Windows PowerShell リモート処理を使用する」を参照して、CredSSP を有効にし、テストします。 次に、管理コンピューターで Hyper-V マネージャーを使用して、[別のユーザーとして接続する] オプションを選択します。 Hyper-V マネージャーは CredSSP を使用します。 この操作は、現在のアカウントを使用している場合でも行う必要があります。

Hyper-V 用の Windows PowerShell コマンドレットでは CimSession または Credential パラメーターを使うことができ、どちらの場合でも CredSSP に対応します。

### <a name="using-failover-clustering-on-nano-server"></a><a name=BKMK_Failover></a>Nano Server でのフェールオーバー クラスタリングの使用

フェールオーバー クラスタリングは Server Core モードの Windows Server 上と Nano Server 上で同じように動作しますが、次の点に注意してください。

- クラスターは、フェールオーバー クラスター マネージャーまたは Windows PowerShell を使ってリモートで管理する必要があります。

- Nano Server クラスターのノードは、Windows Server のクラスター ノードと同様に、すべて同じドメインに参加している必要があります。

- ドメイン アカウントは、Windows Server のクラスター ノードの場合と同様に、Nano Server のすべてのノードに対する管理者特権を持っている必要があります。

- すべてのコマンドは、管理者特権でのコマンド プロンプトで実行する必要があります。

> [!NOTE]
> さらに、このリリースでは特定の機能がサポートされていません。
>
> - Windows PowerShell を使用してローカル Nano Server でフェールオーバー クラスタリング コマンドレットを実行することはできません。
> - Hyper-V とファイル サーバーを除くクラスタリング役割。

フェールオーバー クラスターを管理するうえで、次の Windows PowerShell コマンドレットが役に立ちます。

`New-Cluster -Name <clustername> -Node <comma-separated cluster node list>` を実行して、新しいクラスターを作成できます

新しいクラスターを確立した後、すべてのノードで `Set-StorageSetting -NewDiskPolicy OfflineShared` を実行する必要があります。

`Add-ClusterNode -Name <comma-separated cluster node list>  -Cluster <clustername>` を実行して、クラスターにノードを追加します

`Remove-ClusterNode -Name <comma-separated cluster node list>  -Cluster <clustername>` を実行して、クラスターからノードを削除します

`Add-ClusterScaleoutFileServerRole -name <sofsname> -cluster <clustername>` を実行して、スケールアウト ファイル サーバーを作成します

フェールオーバー クラスタリング向けの他のコマンドレットについては、「[Microsoft.FailoverClusters.PowerShell](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee461009(v=technet.10))」を参照してください。

### <a name="using-dns-server-on-nano-server"></a><a name=BKMK_DNS></a>Nano Server での DNS サーバーの使用

Nano Server に DNS サーバーの役割を与えるには、Microsoft-NanoServer-DNS-Package をイメージに追加します (このトピックの「カスタム Nano Server イメージの作成」を参照してください)。 実行中の Nano Server に接続し、管理者特権の Windows PowerShell コンソールから次のコマンドを実行してこの機能を有効にします。

`Enable-WindowsOptionalFeature -Online -FeatureName DNS-Server-Full-Role`

### <a name="using-iis-on-nano-server"></a><a name=BKMK_IIS></a>Nano Server での IIS の使用

インターネット インフォメーション サービス (IIS) 役割を使用するための手順については、「[Nano Server の IIS](IIS-on-Nano-Server.md)」を参照してください。

### <a name="using-mpio-on-nano-server"></a>Nano Server での MPIO の使用

MPIO を使用するための手順については、「[Nano Server の MPIO](MPIO-on-Nano-Server.md)」を参照してください。

### <a name="using-ssh-on-nano-server"></a><a name=BKMK_SSH></a>Nano Server での SSH の使用

Nano Server に SSH をインストールして、OpenSSH プロジェクトで使用する手順については、[Win32-OpenSSH Wiki](https://github.com/PowerShell/Win32-OpenSSH/wiki) を参照してください。

## <a name="appendix-sample-unattendxml-file-that-joins-nano-server-to-a-domain"></a>付録:Nano Server をドメインに参加させるサンプル Unattend.xml ファイル

> [!NOTE]
> odjblob の内容を無人セットアップ ファイルに貼り付けた後、必ず末尾のスペースを削除してください。

```xml
<?xml version='1.0' encoding='utf-8'?>
<unattend xmlns=urn:schemas-microsoft-com:unattend xmlns:wcm=https://schemas.microsoft.com/WMIConfig/2002/State xmlns:xsi=http://www.w3.org/2001/XMLSchema-instance>

  <settings pass=offlineServicing>
    <component name=Microsoft-Windows-UnattendedJoin processorArchitecture=amd64 publicKeyToken=31bf3856ad364e35 language=neutral versionScope=nonSxS>
        <OfflineIdentification>
           <Provisioning>
             <AccountData> AAAAAAARUABLEABLEABAoAAAAAAAMABSUABLEABLEABAwAAAAAAAAABbMAAdYABc8ABYkABLAABbMAAEAAAAMAAA0ABY4ABZ8ABbIABa0AAcIABY4ABb8ABZUABAsAAAAAAAQAAZoABNUABOYABZYAANQABMoAAOEAAMIAAOkAANoAAMAAAXwAAJAAAAYAAA0ABY4ABZ8ABbIABa0AAcIABY4ABb8ABZUABLEAALMABLQABU0AATMABXAAAAAAAKdf/mhfXoAAUAAAQAAAAb8ABLQABbMABcMABb4ABc8ABAIAAAAAAb8ABLQABbMABcMABb4ABc8ABLQABb0ABZIAAGAAAAsAAR4ABTQABUAAAAAAACAAAQwABZMAAZcAAUgABVcAAegAARcABKkABVIAASwAAY4ABbcABW8ABQoAAT0ABN8AAO8ABekAAJMAAVkAAZUABckABXEABJUAAQ8AAJ4AAIsABZMABdoAAOsABIsABKkABQEABUEABIwABKoAAaAABXgABNwAAegAAAkAAAAABAMABLIABdIABc8ABY4AADAAAA4AAZ4ABbQABcAAAAAAACAAkKBW0ID8nJDWYAHnBAXE77j7BAEWEkl+lKB98XC2G0/9+Wd1DJQW4IYAkKBAADhAnKBWEwhiDAAAM2zzDCEAM6IAAAgAAAAAAAQAAAAAAAAAAAABwzzAAA
              </AccountData>
           </Provisioning>
         </OfflineIdentification>
    </component>
  </settings>

  <settings pass=oobeSystem>
    <component name=Microsoft-Windows-Shell-Setup processorArchitecture=amd64 publicKeyToken=31bf3856ad364e35 language=neutral versionScope=nonSxS>
      <UserAccounts>
        <AdministratorPassword>
           <Value>Tuva</Value>
           <PlainText>true</PlainText>
        </AdministratorPassword>
      </UserAccounts>
      <TimeZone>Pacific Standard Time</TimeZone>
    </component>
  </settings>

  <settings pass=specialize>
    <component name=Microsoft-Windows-Shell-Setup processorArchitecture=amd64 publicKeyToken=31bf3856ad364e35 language=neutral versionScope=nonSxS>
      <RegisteredOwner>My Team</RegisteredOwner>
      <RegisteredOrganization>My Corporation</RegisteredOrganization>
    </component>
  </settings>
</unattend>
```
