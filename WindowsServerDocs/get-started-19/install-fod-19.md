---
title: Server Core アプリ互換性オンデマンド機能 (FOD)
description: オンデマンドで Windows Server の機能をインストールする方法
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99f7daa4-30ce-4d13-be65-0a4d55cca754
author: coreyp-at-msft
ms.author: coreyp
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: b8211ace56aa6565295a15adce26a8dfbc98e1e9
ms.sourcegitcommit: dbb4738fdac3b7911952ff11f1eaed9649d6567a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/07/2019
ms.locfileid: "9149902"
---
# Server Core アプリ互換性オンデマンド機能 (FOD)

> Windows Server 2019 と Windows Server version 1809 に適用されます。

**サーバー コア アプリ互換性オンデマンド機能**は、Windows Server 2019 の Server Core インストールでは、または Windows Server version 1809、いつでもでも追加できるオプション機能パッケージです。

オンデマンド (FOD) での機能について詳しくは、[オンデマンド機能](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities)を参照してください。


## インストールのアプリ互換性 FOD はなぜですか。 

アプリの互換性、Server core、オンデマンドでの機能が追加することがなくバイナリとデスクトップ エクスペリエンス搭載 Windows Server からのパッケージのサブセットを含む、Windows Server Core インストール オプションのアプリの互換性を大幅に向上しますWindows Server デスクトップ エクスペリエンス グラフィカル環境です。 このオプションのパッケージでは、または、Windows Update から、独立した ISO で利用可能なですが、Windows Server Core インストールとイメージにのみ追加できます。

アプリの互換性 FOD を提供する 2 つのプライマリ値は次のとおりです。

1.  Server Core の市場では、既にまたは組織によって開発および展開された既にするサーバー アプリケーションの互換性が向上します。

2.  OS コンポーネントと鋭角のトラブルシューティングとデバッグ シナリオで使用されるソフトウェア ツールの向上のアプリの互換性を提供することを支援します。

サーバー コア アプリ互換性 FOD の一部として、利用できるオペレーティング システムのコンポーネント:

-   Microsoft 管理コンソール (mmc.exe)

-   イベント ビューアー (Eventvwr.msc)

-   パフォーマンス モニター (PerfMon.exe)

-   リソース モニター (Resmon.exe)

-   デバイス マネージャー (Devmgmt.msc)

-   ファイル エクスプ ローラー (Explorer.exe)

-   Windows PowerShell (Powershell_ISE.exe)

-   ディスクの管理 (Diskmgmt.msc)

-   フェールオーバー クラスター マネージャー (CluAdmin.msc)

    -   まず、フェールオーバー クラスタ リングの Windows Server の機能の追加が必要です。

        -   Powershell コマンドレットを使用して、追加します。 `Install-WindowsFeature -NameFailover-Clustering -IncludeManagementTools`

        -   フェールオーバー クラスター マネージャーを実行するには、コマンド プロンプトで**cluadmin**を入力します。

## アプリの互換性 FOD をインストールします。

 >[!IMPORTANT] 
   >アプリの互換性 FOD は、Server Core にのみインストールできます。 デスクトップ エクスペリエンス搭載 Windows Server の Windows Server のインストールにサーバー コア アプリ互換性 FOD を追加しないでください。

### Server Core の実行中のインスタンスに、Server Core アプリ互換性オンデマンド機能 (FOD) を追加するには

 >[!NOTE] 
   > この手順では、展開イメージのサービスと管理 (DISM.exe) コマンド ライン ツールを使用します。 DISM コマンドの詳細については、 [DISM 機能パッケージ サービス コマンド ライン オプション](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-capabilities-package-servicing-command-line-options)を参照してください。

>[!NOTE] 
   > 同じ FOD オプション パッケージ ISO を Windows Server 2019 の Server Core インストールでは、または Windows Server version 1809、インストールに使用できます。

>[!NOTE] 
   > コンピューターまたは Server Core を実行している仮想マシンが Windows Update に接続できない場合、以下の手順 1 ~ 7 をスキップできます。 ただし、手順 8 の DISM コマンドから/Source および/LimitAccess オフのままにしてください。

1. サーバー FOD オプション パッケージ、ISO をダウンロードし、ISO をローカル ネットワーク上の共有フォルダーにコピーします。

 - ボリューム ライセンスがある場合は、OS ISO イメージ ファイルが取得される同じポータルからサーバー FOD ISO イメージ ファイルをダウンロードできます。[ボリューム ライセンス サービス センター](https://www.microsoft.com/Licensing/servicecenter/default.aspx)。
 - サーバー FOD ISO イメージ ファイルも[Microsoft Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019)またはのサブスクライバーに対して、 [Visual Studio ポータル](https://visualstudio.microsoft.com)で使用できます。


2. Server Core のコンピューター、ローカル ネットワークに接続されていること、およびに FOD を追加する上で管理者としてサインインします。

3. **正味の使用**、またはその他のいくつかのメソッドを使用して FOD ISO の場所に接続します。

4. FOD ISO を任意のローカル フォルダーにコピーします。

5. コマンド プロンプトで**powershell.exe**を入力して PowerShell を起動します。

6. 次のコマンドを使用して FoD ISO をマウントします。

        Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso

7. PowerShell を終了する**終了**を入力します。

8.  次のコマンドを実行します。

        DISM /Online /Add-Capability /CapabilityName:"ServerCore.AppCompatibility~~~~0.0.1.0" /Source:drive_letter_of_mounted_ISO: /LimitAccess

9.  進行状況バーが完了したら後、は、オペレーティング システムを再起動します。

### 必要に応じて Internet Explorer 11 を追加した後、Server Core アプリ互換性 FOD) Server Core に追加するには

 >[!NOTE]  
   > サーバー コア アプリ互換性 FOD が Internet Explorer 11 を追加するために必要なには、Internet Explorer 11 は、Server Core アプリ互換性 FOD を追加する必要はありません。

1.  Server Core コンピューターが既に追加アプリの互換性 FOD と ISO をローカルにコピー サーバー FOD オプション パッケージに管理者としてサインインします。

2.  コマンド プロンプトで**powershell.exe**を入力して PowerShell を起動します。

3.  次のコマンドを使用して FoD ISO をマウントします。

         Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso

4.  PowerShell を終了する**終了**を入力します。


5.  次のコマンドを実行します。

        Dism /online /add-package:drive_letter_of_mounted_iso:"Microsoft-Windows-InternetExplorer-Optional-Package~31bf3856ad364e35~amd64~~.cab"

6.  進行状況バーが完了したら後、は、オペレーティング システムを再起動します。

 
#### リリース ノートとサーバー コア アプリ互換性 FOD と Internet Explorer 11 のオプション パッケージのための推奨事項

- **重要:** の問題、に関する考慮事項、またはガイダンス サーバー コア アプリ互換性 FOD と Internet Explorer 11 のオプション パッケージのインストールと使用を続行する前に、Windows Server 2019 リリース ノートをお読みください。
 
 >[!NOTE] 
   > それは、Windows Update を使用して、累積的な更新プログラムをインストールした後、アプリの互換性 FOD を追加するときに、Server Core コンソール エクスペリエンスとちらつきが発生することもできます。  この問題が解決、2018 年 12 月に更新します。  詳細情報と解像度の手順を参照してください。[サポート技術情報の記事 4481610: Windows Server 2019 の Server Core で Server Core アプリ互換性 FOD をインストールした後に画面がちらつき](https://support.microsoft.com/help/4481610/screen-flickers-after-fod-installation-windows2019-server-core)します。

- アプリの互換性 FOD とサーバーの再起動のインストール後、コマンドのコンソール ウィンドウのフレームの色は、青のさまざまな網掛けに変更されます。

- また、Internet Explorer 11 のオプション パッケージをインストールする場合は、ローカルに保存されている .htm ファイルを開くをダブルクリックすることはサポートされていません注意してください。 ただし、**右クリック**でき、 **IE で開く**には、選択または Internet Explorer**ファイル**から直接開くことができます -> **を開きます**。 

- Server Core アプリ互換性 FOD と、アプリの互換性をさらに強化するには、IIS 管理コンソールが追加されました Server Core にコンポーネントとして、省略可能です。  ただし、どうしても IIS 管理コンソールを使用してアプリの互換性 FOD を最初に追加する必要は。 IIS 管理コンソールは、これはアプリの互換性 FOD の追加と Server Core で利用可能なのみ Microsoft 管理コンソール (mmc.exe) に依存します。  Powershell[**インストール WindowsFeature**](https://docs.microsoft.com/powershell/module/microsoft.windows.servermanager.migration/install-windowsfeature?view=win10-ps)を使用して、IIS 管理コンソールを追加します。

- ガイダンスについては、サーバー上のアプリのインストールのコア (これらのオプション パッケージの有無にかかわらず) そのときの一般的なポイントは、サイレント インストール オプションと手順を使用する必要があります。 
    
 - 例として、SQL Server 2016 および SQL Server 2017 の SQL Server Management Studio は、Server Core にインストールし、アプリの互換性 FOD が存在する場合は、完全に機能します。  [コマンド プロンプトから、SQL Server のインストール](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-from-the-command-prompt?view=sql-server-2017)をご覧ください。
 - SQL Server Management Studio は望ましくない場合は、必要はありませんサーバー コア アプリ互換性 FOD をインストールします。  [Server Core での SQL Server のインストール](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-on-server-core?view=sql-server-2017)をご覧ください。

