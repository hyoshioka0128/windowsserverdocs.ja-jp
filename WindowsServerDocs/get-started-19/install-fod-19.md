---
title: Server Core アプリ互換性オンデマンド機能 (FOD)
description: Windows Server 機能をオンデマンドでインストールする方法
ms.prod: windows-server-threshold
ms.technology: server-general
ms.topic: article
ms.assetid: 99f7daa4-30ce-4d13-be65-0a4d55cca754
author: jasongerend
ms.author: jgerend
manager: jasgroce
ms.localizationpriority: medium
ms.date: 06/07/2019
ms.openlocfilehash: 441cd9593371cb7e5018a61c3d7a6af991ce8fed
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280168"
---
# <a name="server-core-app-compatibility-feature-on-demand-fod"></a>Server Core アプリ互換性オンデマンド機能 (FOD)

> 適用対象:Windows Server 2019、Windows Server 半期チャネル

**Server Core アプリ互換性オンデマンド機能**は、Windows Server 2019 の Server Core インストール、または Windows Server 半期チャネルにいつでも追加できるオプションの機能パッケージです。

オンデマンド機能 (FOD) の詳細については、「[オンデマンド機能](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities)」を参照してください。

## <a name="why-install-the-app-compatibility-fod"></a>アプリ互換性 FOD をインストールする理由

Server Core のオンデマンド機能であるアプリ互換性により、デスクトップ エクスペリエンスがインストールされている Windows Server からバイナリとパッケージのサブセットを含めることで、Windows Server デスクトップ エクスペリエンス グラフィカル環境を追加しなくても、Windows Server Core インストール オプションのアプリ互換性が大幅に向上します。 このオプション パッケージは、独立した ISO で、または Windows Update から入手できますが、追加できるのは Windows Server Core インストールとイメージだけです。

アプリ互換性 FOD が提供する 2 つの主要な価値は次のとおりです。

- 既に市場に出回っているか既に組織によって開発され展開されているサーバー アプリケーション向けに Server Core の互換性を向上させます。
- OS コンポーネントと重大なトラブルシューティングとデバッグ シナリオで使用されるソフトウェア ツールの向上したアプリ互換性を提供することを支援します。

Server Core アプリ互換性 FOD の一部として利用できるオペレーティング システムのコンポーネントには、次のものが含まれます。

-   Microsoft 管理コンソール (mmc.exe)

-   イベント ビューアー (Eventvwr.msc)

-   パフォーマンス モニター (PerfMon.exe)

-   リソース モニター (Resmon.exe)

-   デバイス マネージャー (Devmgmt.msc)

-   ファイル エクスプローラー (Explorer.exe)

-   Windows PowerShell (Powershell_ISE.exe)

-   ディスク管理 (Diskmgmt.msc)

-   フェールオーバー クラスター マネージャー (CluAdmin.msc)

    -   最初にフェールオーバー クラスタリングの Windows Server 機能を追加する必要があります。

        -   管理者特権の PowerShell セッションから次を実行します。 

            ```PowerShell
            Install-WindowsFeature -NameFailover-Clustering -IncludeManagementTools
            ```

        -   フェールオーバー クラスター マネージャーを実行するには、コマンド プロンプトに「**cluadmin**」と入力します。

Windows Server バージョン 1903 以降を実行しているサーバーでは、次のコンポーネントもサポートされています (アプリ互換性 FOD と同じバージョンを使用している場合)。

- Hyper-V マネージャー (virtmgmt.msc)
- タスク スケジューラ (taskschd.msc)

## <a name="installing-the-app-compatibility-fod"></a>アプリ互換性 FOD をインストールする

アプリ互換性 FOD は、Server Core にのみインストールできます。 Server Core アプリ互換性 FOD をデスクトップ エクスペリエンスがインストールされた Windows Server の Windows Server インストールに追加しないようにしてください。 同じ FOD のオプション パッケージ ISO は、Windows Server 2019 の Server Core インストールまたは Windows Server 半期チャネルのインストールに使用できます。

1. サーバーが Windows Update に接続できる場合は、管理者特権の PowerShell セッションから次のコマンドを実行し、コマンドの実行が完了したら Windows サーバーを再起動するだけです。

    ```PowerShell
    Add-WindowsCapability -Online -Name ServerCore.AppCompatibility~~~~0.0.1.0
    ```

2. サーバーが Windows Update に接続できない場合は、代わりに Server FOD のオプション パッケージ ISO をダウンロードして、ISO をローカル ネットワーク上の共有フォルダーにコピーします。

   - ボリューム ライセンスをお持ちの場合は、Server FOD ISO イメージ ファイルは、OS の ISO イメージ ファイルを取得するのと同じポータルの[ボリューム ライセンス サービス センター](https://www.microsoft.com/Licensing/servicecenter/default.aspx)からダウンロードできます。
   - Server FOD ISO イメージ ファイルは、[Microsoft Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server) またはサブスクライバー向けの [Visual Studio ポータル](https://visualstudio.microsoft.com)でも入手できます。

3. ローカル ネットワークに接続されていて、FOD を追加したい Server Core コンピューターで、管理者アカウントを使ってサインインします。

4. **net use** またはその他の方法を使用して、FOD ISO の場所に接続します。

5. FOD ISO を任意のローカル フォルダーにコピーします。

6. 管理者特権の PowerShell セッションで次のコマンドを使用して FOD ISO をマウントします。

    ```PowerShell
    Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso
    ```

7. 次のコマンドを実行します。

    ```PowerShell
    Add-WindowsCapability -Online -Name ServerCore.AppCompatibility~~~~0.0.1.0 -Source <Mounted_Server_FOD_Drive> -LimitAccess
     ```

8. 進行状況バーが完了したら、オペレーティング システムを再起動します。

   DISM コマンドの詳細については、「[Windows PowerShell での DISM の使用](https://docs.microsoft.com/windows-hardware/manufacture/desktop/use-dism-in-windows-powershell-s14)」を参照してください。

## <a name="to-optionally-add-internet-explorer-11-to-server-core-after-adding-the-server-core-app-compatibility-fod"></a>(Server Core アプリ互換性 FOD を追加した後) オプションで Internet Explorer 11 を Server Core に追加するには

 >[!NOTE]  
   > Server Core アプリ互換性 FOD は、Internet Explorer 11 の追加に必要ですが、Internet Explorer 11 は Server Core アプリ互換性 FOD を追加するのには必要ありません。

1. アプリ互換性 FOD が既に追加されていて、Server FOD のオプション パッケージ ISO がローカルにコピーされている Server Core コンピューターで、管理者としてサインインします。

2. コマンド プロンプトに「**powershell.exe**」と入力して PowerShell を起動します。

3. 次のコマンドを使用して、FOD ISO をマウントします。

    ```PowerShell
    Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso
    ```

4. Internet Explorer の cab ファイルへのパスを入力する `$package_path` 変数を使用して、次のコマンドを実行します。

    ```PowerShell
    $package_path = "D:\Microsoft-Windows-InternetExplorer-Optional-Package~31bf3856ad364e35~amd64~~.cab"

    Add-WindowsPackage -Online -PackagePath $package_path
    ```

5. 進行状況バーが完了したら、オペレーティング システムを再起動します。

## <a name="release-notes-and-suggestions-for-the-server-core-app-compatibility-fod-and-internet-explorer-11-optional-package"></a>Server Core アプリ互換性 FOD と Internet Explorer 11 オプション パッケージに関するリリース ノートと推奨事項

> [!IMPORTANT]
> Windows Server バージョン 1809 にインストールされている FOD は、Windows Server バージョン 1903 へのインプレース アップグレード後には残らないため、アップグレード後にもう一度インストールする必要はありません。 代わりに、アップグレードする前に新しい Windows Server のインストール ソースに FOD を追加することができます。 これにより、アップグレードの完了後も任意の FOD の新しいバージョンが確実に存在します。 詳細については、「[オフラインの WIM Server Core イメージに機能とオプション パッケージを追加する](install-fod-19.md#add-capabilities)」を参照してください。

- **重要:** Server Core アプリ互換性 FOD と Internet Explorer 11 オプション パッケージのインストールと使用に進む前に、問題、考慮事項、またはガイダンスについて Windows Server 2019 のリリース ノートをお読みください。

- Windows Update を使用して、累積的な更新プログラムをインストールした後、アプリ互換性 FOD を追加するときに、Server Core コンソール エクスペリエンスでちらつきが発生する可能性があります。  この問題は、2018 年 12 月の更新プログラムで解決されます。  詳細情報と解決手順については、[サポート技術情報の記事 4481610:Windows Server 2019 Server Core に Server Core アプリ互換性 FOD をインストールした後に画面がちらつく](https://support.microsoft.com/help/4481610/screen-flickers-after-fod-installation-windows2019-server-core)を参照してください。

- アプリ互換性 FOD をインストールしてサーバーを再起動すると、コマンド コンソールのウィンドウ フレームの色が異なる色調の青に変わります。

- Internet Explorer 11 のオプション パッケージのインストールも選択する場合は、ローカルに保存した .htm ファイルをダブルクリックして開くことはサポートされていないことに注意してください。 ただし、**右クリック**して **[IE で開く]** を選択するか、Internet Explorer から **[ファイル]**  ->  **[開く]** で直接開くことができます。

- アプリ互換性 FOD を使用して Server Core のアプリ互換性をさらに強化するため、IIS 管理コンソールがオプション コンポーネントとして Server Core に追加されています。  ただし、IIS 管理コンソールを使用するには、必ず最初にアプリ互換性 FOD を追加する必要があります。 IIS 管理コンソールは、Microsoft 管理コンソール (mmc.exe) に依存します。これはアプリ互換性 FOD を追加することで Server Core でのみ使用できます。  IIS 管理コンソールを追加するには、PowerShell の [**Install-WindowsFeature**](https://docs.microsoft.com/powershell/module/microsoft.windows.servermanager.migration/install-windowsfeature?view=win10-ps) を使用します。

- 一般的なガイダンスとして、Server Core にアプリをインストールするときに (これらのオプション パッケージの有無にかかわらず)、サイレント インストールのオプションと手順を使用する必要がある場合があります。 
    
  - 例として、SQL Server 2016 および SQL Server 2017 の SQL Server Management Studio は、Server Core にインストールすることができ、アプリ互換性 FOD が存在する場合は、完全に機能します。  「[コマンド プロンプトからの SQL Server のインストール](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-from-the-command-prompt?view=sql-server-2017)」を参照してください。
  - SQL Server Management Studio が必要ない場合は、Server Core アプリ互換性 FOD をインストールする必要はありません。  「[Server Core への SQL Server のインストール](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-on-server-core?view=sql-server-2017)」を参照してください。

## <a name="a-idadd-capabilities-adding-capabilities-and-optional-packages-to-an-offline-wim-server-core-image"></a><a id="add-capabilities"> オフラインの WIM Server Core イメージに機能とオプション パッケージを追加する

1. Windows Server と Server FOD ISO イメージ ファイルを Windows コンピューター上のローカル フォルダーにダウンロードします。

   - ボリューム ライセンスをお持ちの場合は、[ボリューム ライセンス サービス センター](https://www.microsoft.com/Licensing/servicecenter/default.aspx)から Windows Server と Server FOD ISO イメージ ファイルをダウンロードすることができます。
   - Server FOD ISO イメージ ファイルは、[Microsoft Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server) またはサブスクライバー向けの [Visual Studio ポータル](https://visualstudio.microsoft.com)での長期的なサービス チャネルのリリースにも使用できます。

2. 管理者として PowerShell セッションを開き、次のコマンドを使用してイメージ ファイルをドライブとしてマウントします。

   ```PowerShell
   Mount-DiskImage -ImagePath Path_To_ServerFOD_ISO
   Mount-DiskImage -ImagePath Path_To_Windows_Server_ISO
   ```

3. Windows Server ISO ファイルの内容をローカル フォルダー (例: *C:\SetupFiles\WindowsServer*) にコピーします。

4. 次のコマンドを使用して、Install.wim ファイル内で変更するイメージ名を取得します。<br>
`$install_wim_path` 変数を使用して、ISO ファイルの \Sources フォルダー内にある Install.wim ファイルへのパスを入力します。

   ```PowerShell
   $install_wim_path = "C:\SetupFiles\WindowsServer\sources\install.wim"

   Get-WindowsImage -ImagePath $install_wim_path
   ```

5. 次のコマンドを使用 (サンプルの変数値は独自の値に置き換えて、前のコマンドから `$install_wim_path` 変数を再利用します) して、Install.wim ファイルを新しいフォルダーにマウントします。<br>

   - `$image_name` - マウントするイメージの名前を入力します。
   - `$mount_folder variable` - Install.wim ファイルの内容にアクセスするときに使用するフォルダーを指定します。

   ```PowerShell
   $image_name = "Windows Server Datacenter"
   $mount_folder = "c:\test\offline"

   Mount-WindowsImage -ImagePath $install_wim_path -Name $image_name -path $mount_folder
   ```

6. 次のコマンドを使用 (サンプルの変数値は独自の値に置き換えます) して、マウントした Install.wim イメージに機能とパッケージを追加します。<br>

   - `$capability_name` - インストールする機能の名前を指定します (この場合は AppCompatibility 機能)。
   - `$package_path` - インストールするパッケージへのパスを指定します (この場合は Internet Explorer)。
   - `$fod_drive` - マウントした Server FOD イメージのドライブ文字を指定します。

   ```PowerShell
   $capability_name = "ServerCore.AppCompatibility~~~~0.0.1.0"
   $package_path = "D:\Microsoft-Windows-InternetExplorer-Optional-Package~31bf3856ad364e35~amd64~~.cab"
   $fod_drive = "d:\"

   Add-WindowsCapability -Path $mount_folder -Name $capability_name -Source $fod_drive -LimitAccess
   Add-WindowsPackage -Path $mount_folder -PackagePath $package_path
   ```

7. 前のコマンドから `$mount_folder` 変数を使用する次のコマンドを使用して、Install.wim ファイルをマウント解除して変更をコミットします。

   ```PowerShell
   Dismount-WindowsImage -Path $mount_folder -Save
   ```

これで、Windows Server インストール ファイル用に作成したフォルダーから setup.exe を実行して、サーバーをアップグレードできるようになりました (この例では*C:\SetupFiles\WindowsServer*)。 これでこのフォルダーに、追加機能とオプション パッケージが含まれた Windows Server のインストール ファイルが含まれるようになりました。