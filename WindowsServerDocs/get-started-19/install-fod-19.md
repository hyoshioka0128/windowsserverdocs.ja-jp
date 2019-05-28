---
title: Server Core アプリ互換性オンデマンド機能 (FOD)
description: Windows Server の機能をオンデマンドでインストールする方法
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
ms.assetid: 99f7daa4-30ce-4d13-be65-0a4d55cca754
author: jasongerend
ms.author: jgerend
manager: jasgroce
ms.localizationpriority: medium
ms.date: 05/24/2019
ms.openlocfilehash: c9af38720df79918bed3404995e81a7f93a10744
ms.sourcegitcommit: 8ba2c4de3bafa487a46c13c40e4a488bf95b6c33
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/25/2019
ms.locfileid: "66222896"
---
# <a name="server-core-app-compatibility-feature-on-demand-fod"></a>Server Core アプリ互換性オンデマンド機能 (FOD)

> 適用対象:Windows Server 2019、Windows Server 半期チャネル

**オンデマンドで Server Core アプリの互換性機能**はいつでも、Windows Server 2019 の Server Core インストールまたは Windows Server 半期チャネルに追加できるオプションの機能パッケージです。

必要に応じて (FOD) での機能の詳細については、次を参照してください。[オンデマンド機能](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities)します。

## <a name="why-install-the-app-compatibility-fod"></a>アプリの互換性 FOD をインストールする理由

アプリケーションの互換性、Server core では、オンデマンドでの機能が追加せず、一部のバイナリとデスクトップ エクスペリエンス、Windows Server からパッケージを含めることによって、Windows Server Core インストール オプションのアプリケーションの互換性を大幅に向上しますWindows Server Desktop Experience のグラフィカルな環境です。 この省略可能なパッケージが Windows update、または、別の ISO で使用できますが、Windows Server Core インストール、および画像にのみ追加できます。

アプリの互換性 FOD を提供する 2 つのプライマリ値は次のとおりです。

- サーバー アプリケーションが既に市場または組織で開発およびデプロイされた既にの Server Core の互換性が向上します。
- OS のコンポーネントと深刻のトラブルシューティングとデバッグ シナリオで使用されるソフトウェア ツールのアプリの互換性を提供することを支援します。

Server Core のアプリケーション互換性 FOD の一部が含まれるので、利用できるオペレーティング システムのコンポーネント:

-   Microsoft 管理コンソール (mmc.exe)

-   イベント ビューアー (Eventvwr.msc)

-   パフォーマンス モニター (PerfMon.exe)

-   リソース モニター (Resmon.exe)

-   デバイス マネージャー (Devmgmt.msc)

-   ファイル エクスプ ローラー (Explorer.exe)

-   Windows PowerShell (Powershell_ISE.exe)

-   ディスクの管理 (Diskmgmt.msc)

-   フェールオーバー クラスター マネージャー (CluAdmin.msc)

    -   まず、フェールオーバー クラスタ リングの Windows Server 機能の追加が必要です。

        -   管理者特権の PowerShell セッション: から 

            ```PowerShell
            Install-WindowsFeature -NameFailover-Clustering -IncludeManagementTools
            ```

        -   フェールオーバー クラスター マネージャーを実行する入力**cluadmin**コマンド プロンプトでします。

Windows Server を実行しているサーバー、1903 およびそれ以降のバージョンは、次のコンポーネントもサポートします。

- Hyper V マネージャー (virtmgmt.msc)
- タスク スケジューラ (taskschd.msc)

## <a name="installing-the-app-compatibility-fod"></a>アプリケーションの互換性 FOD をインストールします。

アプリの互換性 FOD は、Server Core でのみインストールできます。 デスクトップ エクスペリエンス搭載の Windows Server の Windows Server のインストールを Server Core のアプリケーション互換性 FOD を追加しないようにします。 同じ FOD 省略可能なパッケージ ISO は、Windows Server 2019 の Server Core インストールまたは Windows Server 半期チャネルのインストールに使用できます。

1. 場合は、サーバーは、Windows Update に接続できる、管理者特権の PowerShell セッションから次のコマンドを実行し、コマンドの実行が完了した後、Windows サーバーを再起動して行う必要があるすべては。

    ```PowerShell
    Add-WindowsCapability -Online -Name ServerCore.AppCompatibility~~~~0.0.1.0
    ```

2. サーバーが Windows Update に接続できない場合代わりにサーバー FOD 省略可能なパッケージ、ISO をダウンロードし、ISO をローカル ネットワーク上の共有フォルダーにコピーします。

   - ボリューム ライセンスがある場合は、OS の ISO イメージ ファイルが取得される同じポータルからサーバー FOD ISO イメージ ファイルをダウンロードできます。[ボリューム ライセンス サービス センター](https://www.microsoft.com/Licensing/servicecenter/default.aspx)します。
   - Server FOD ISO イメージ ファイルはできるも、 [Microsoft Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server)か、または、 [Visual Studio ポータル](https://visualstudio.microsoft.com)サブスクライバー。

3. ローカル ネットワークに接続されていること、およびに FOD を追加する、Server Core コンピューターの管理者アカウントでサインインします。

4. 使用して、 **net**、または FOD ISO の場所に接続するため、他の方法です。

5. FOD ISO を独自のローカル フォルダーにコピーします。

6. 管理者特権の PowerShell セッションで、次のコマンドを使用して、FOD ISO をマウントします。

    ```PowerShell
    Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso
    ```

7. 次のコマンドを実行します。

    ```PowerShell
    Add-WindowsCapability -Online -Name ServerCore.AppCompatibility~~~~0.0.1.0 -Source <Mounted_Server_FOD_Drive> -LimitAccess
     ```

8. 進行状況バーが完了したら後、は、オペレーティング システムを再起動します。

 DISM コマンドの詳細については、次を参照してください[Windows PowerShell の DISM の使用。](https://docs.microsoft.com/windows-hardware/manufacture/desktop/use-dism-in-windows-powershell-s14)

## <a name="to-optionally-add-internet-explorer-11-to-server-core-after-adding-the-server-core-app-compatibility-fod"></a>(Server Core のアプリケーション互換性 FOD の追加) した後、Internet Explorer 11 を Server Core 必要に応じて追加するには

 >[!NOTE]  
   > Server Core のアプリケーション互換性 FOD は Internet Explorer 11 の追加に必要ですが、Internet Explorer 11 は、Server Core のアプリケーション互換性 FOD を追加する必要はありません。

1. 既に追加されて、アプリ互換性 FOD を持つ、Server Core コンピューターと ISO がローカルにコピーされるサーバー FOD 省略可能なパッケージで管理者としてサインインします。

2. 入力して PowerShell を起動**powershell.exe**コマンド プロンプトでします。

3. 次のコマンドを使用して FOD ISO をマウントします。

    ```PowerShell
    Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso
    ```

4. 次の実行コマンドを使用して、 `$package_path` Internet Explorer の cab ファイルのパスを入力する変数。

    ```PowerShell
    $package_path = "D:\Microsoft-Windows-InternetExplorer-Optional-Package~31bf3856ad364e35~amd64~~.cab"

    Add-WindowsPackage -Online -PackagePath $package_path
    ```

5. 進行状況バーが完了したら後、は、オペレーティング システムを再起動します。

## <a name="release-notes-and-suggestions-for-the-server-core-app-compatibility-fod-and-internet-explorer-11-optional-package"></a>リリース ノートと Server Core アプリの互換性 FOD および Internet Explorer 11 の省略可能なパッケージに関する推奨事項

> [!IMPORTANT]
> Windows Server にインストールされている FODs、バージョンは 1809 しませんに残しておく Windows Server バージョンが 1903 年へのインプレース アップグレード後ため、それらをアップグレード後にもう一度インストールする必要があります。 またはにアップグレードする前に新しい Windows Server のインストール ソースに FODs を追加することができます。 これにより、任意の FODs の新しいバージョンがアップグレードの完了後にあります。 詳細については、次を参照してください。、[機能とオプションのパッケージをオフラインの WIM の Server Core イメージに追加する](install-fod-19.md#add-capabilities)します。

- **重要:** Windows Server 2019 のリリース ノートの問題、考慮事項、またはインストールと Server Core アプリの互換性 FOD および Internet Explorer 11 の省略可能なパッケージの使用を続行する前にガイダンスを読み取る。

- Windows Update を使用して、累積的更新プログラムをインストールした後、アプリ互換性 FOD を追加するときに、Server Core のコンソールのエクスペリエンスでちらつきが発生することになります。  この問題は、2018 年 12 月で解決を更新します。  詳細情報と解決手順は、次を参照してください。[サポート技術情報記事 4481610。Windows Server 2019 の Server Core で Server Core アプリの互換性 FOD をインストールした後に画面がちらつき](https://support.microsoft.com/help/4481610/screen-flickers-after-fod-installation-windows2019-server-core)します。

- アプリケーション互換性 FOD と、サーバーの再起動のインストール後、コマンド コンソールのウィンドウ フレームの色は、青色のさまざまな網掛けに変更されます。

- Internet Explorer 11 の省略可能なパッケージをインストールする場合は、ダブルクリックするとローカルに保存した .htm ファイルを開くには、サポートされていないことに注意してください。 ただし、**を右クリックして**選択**IE で開く**、または Internet Explorer から直接開くことができます**ファイル** -> **を開く**.

- アプリの互換性 FOD と Server Core のアプリケーションの互換性をさらに強化するには、IIS 管理コンソールが追加されました Server core オプション コンポーネントとして。  ただし、最初に追加の IIS 管理コンソールを使用するアプリの互換性 FOD どうしても必要なは。 IIS 管理コンソールは、Server Core のアプリケーションの互換性 FOD 追加収録されてのみを Microsoft 管理コンソール (mmc.exe) に依存します。  Powershell を使用して[ **Install-windowsfeature** ](https://docs.microsoft.com/powershell/module/microsoft.windows.servermanager.migration/install-windowsfeature?view=win10-ps) IIS 管理コンソールを追加します。

- ガイダンスについては、サーバー上のアプリのインストールのコア (これらの省略可能なパッケージの有無にかかわらず)、時の一般的なポイントでは、サイレント インストール オプションと手順を使用する必要な場合があります。 
    
 - 例として、SQL Server 2016 および SQL Server 2017 の SQL Server Management Studio は Server Core にインストールすることができ、アプリの互換性 FOD が存在する場合は、完全に機能します。  参照してください、[コマンド プロンプトから SQL Server インストール](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-from-the-command-prompt?view=sql-server-2017)します。
 - SQL Server Management Studio が望ましくない場合、必要はありませんサーバー コア アプリ互換性 FOD をインストールします。  参照してください、 [Server Core での SQL Server のインストール](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-on-server-core?view=sql-server-2017)します。

## <a name="a-idadd-capabilities-adding-capabilities-and-optional-packages-to-an-offline-wim-server-core-image"></a><a id="add-capabilities"> オフラインの Server Core の WIM イメージへの機能とオプションのパッケージの追加

1. Windows コンピューター上のローカル フォルダーには、Windows Server および Server FOD ISO イメージ ファイルをダウンロードします。

   - ボリューム ライセンスがある場合から Windows Server および Server FOD ISO イメージ ファイルをダウンロードすることができます、[ボリューム ライセンス サービス センター](https://www.microsoft.com/Licensing/servicecenter/default.aspx)します。
   - Server FOD ISO イメージ ファイルはできるも、 [Microsoft Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server)か、または、 [Visual Studio ポータル](https://visualstudio.microsoft.com)サブスクライバー。

2. 管理者として PowerShell セッションを開き、ドライブとしてイメージ ファイルをマウントし、次のコマンドを使用します。

   ```PowerShell
   Mount-DiskImage -ImagePath Path_To_ServerFOD_ISO
   Mount-DiskImage -ImagePath Path_To_Windows_Server_ISO
   ```

3. コピー、ローカル フォルダーに Windows Server の ISO ファイルの内容 (たとえば、 *C:\SetupFiles\WindowsServer*)。

4. 次のコマンドを使用して、Install.wim ファイル内で変更するイメージの名前を取得します。<br>
使用して、 `$install_wim_path` ISO ファイルの \Sources フォルダー内にある、Install.wim ファイルのパスを入力する変数。

   ```PowerShell
   $install_wim_path = "C:\SetupFiles\WindowsServer\sources\install.wim"

   Get-WindowsImage -ImagePath $install_wim_path
   ```

5. 次を使用して新しいフォルダーに、Install.wim ファイルをマウント コマンドを独自のサンプルの変数の値を置き換えると、再利用、`$install_wim_path`前のコマンドから変数。<br>

   - `$image_name` -マウントするイメージの名前を入力します。
   - `$mount_folder variable` Install.wim ファイルの内容にアクセスするときに使用するフォルダーを指定します。

   ```PowerShell
   $image_name = "Windows Server Datacenter"
   $mount_folder = "c:\test\offline"

   Mount-WindowsImage -ImagePath $install_wim_path -Name $image_name -path $mount_folder
   ```

6. 独自のサンプルの変数の値を置き換えて、次のコマンドを使用してマウントの Install.wim イメージに機能とパッケージを追加します。<br>

   - `$capability_name` -(この場合は、AppCompatibility 機能) をインストールする機能の名前を指定します。
   - `$package_path` -(この場合、Internet Explorer) をインストールするパッケージへのパスを指定します。
   - `$fod_drive` -サーバー FOD のマウントされたイメージのドライブ文字を指定します。

   ```PowerShell
   $capability_name = "ServerCore.AppCompatibility~~~~0.0.1.0"
   $package_path = "D:\Microsoft-Windows-InternetExplorer-Optional-Package~31bf3856ad364e35~amd64~~.cab"
   $fod_drive = "d:\"

   Add-WindowsCapability -Path $mount_folder -Name $capability_name -Source $fod_drive -LimitAccess
   Add-WindowsPackage -Path $mount_folder -PackagePath $package_path
   ```

7. マウントを解除し、次のコマンドを使用してを使用して、Install.wim ファイルに変更をコミット、`$mount_folder`前のコマンドから変数。

   ```PowerShell
   Dismount-WindowsImage -Path $mount_folder -Save
   ```

Windows Server インストール ファイル用に作成したフォルダーから setup.exe を実行して、サーバーをアップグレードできるようになりました (この例では。*C:\SetupFiles\WindowsServer*)。 これで、このフォルダーには、追加機能とオプションのパッケージに含まれる Windows Server のインストール ファイルが含まれます。