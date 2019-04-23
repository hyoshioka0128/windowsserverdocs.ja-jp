---
title: Server Core アプリ互換性オンデマンド機能 (FOD)
description: Windows Server の機能をオンデマンドでインストールする方法
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866113"
---
# <a name="server-core-app-compatibility-feature-on-demand-fod"></a>Server Core アプリ互換性オンデマンド機能 (FOD)

> Windows Server 2019 および Windows Server バージョンは 1809 に適用されます。

**オンデマンドで Server Core アプリの互換性機能**は Windows Server 2019 の Server Core インストールでは、または Windows Server バージョン 1809、いつでも追加できるオプションの機能パッケージです。

必要に応じて (FOD) での機能の詳細については、次を参照してください。[オンデマンド機能](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities)します。


## <a name="why-install-the-app-compatibility-fod"></a>アプリの互換性 FOD をインストールする理由 

アプリケーションの互換性、Server core では、オンデマンドでの機能が追加せず、一部のバイナリとデスクトップ エクスペリエンス、Windows Server からパッケージを含めることによって、Windows Server Core インストール オプションのアプリケーションの互換性を大幅に向上しますWindows Server Desktop Experience のグラフィカルな環境です。 この省略可能なパッケージが Windows update、または、別の ISO で使用できますが、Windows Server Core インストール、および画像にのみ追加できます。

アプリの互換性 FOD を提供する 2 つのプライマリ値は次のとおりです。

1.  サーバー アプリケーションが既に市場または組織で開発およびデプロイされた既にの Server Core の互換性が向上します。

2.  OS のコンポーネントと深刻のトラブルシューティングとデバッグ シナリオで使用されるソフトウェア ツールのアプリの互換性を提供することを支援します。

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

        -   Powershell コマンドレットを使用して、追加します。 `Install-WindowsFeature -NameFailover-Clustering -IncludeManagementTools`

        -   フェールオーバー クラスター マネージャーを実行する入力**cluadmin**コマンド プロンプトでします。

## <a name="installing-the-app-compatibility-fod"></a>アプリケーションの互換性 FOD をインストールします。

 >[!IMPORTANT] 
   >アプリの互換性 FOD は、Server Core でのみインストールできます。 デスクトップ エクスペリエンス搭載の Windows Server の Windows Server のインストールを Server Core のアプリケーション互換性 FOD を追加しようとしないでください。

### <a name="to-add-the-server-core-app-compatibility-feature-on-demand-fod-to-a-running-instance-of-server-core"></a>Server Core の実行中のインスタンスにオンデマンド (FOD) サーバー コア アプリケーションの互換性機能を追加するには

 >[!NOTE] 
   > この手順では、Deployment Image Servicing and Management (DISM.exe) コマンド ライン ツールを使用します。 DISM コマンドの詳細については、次を参照してください。 [DISM 機能パッケージ Servicing コマンド ライン オプション](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-capabilities-package-servicing-command-line-options)します。

>[!NOTE] 
   > 同じ FOD 省略可能なパッケージ ISO は、Windows Server 2019 の Server Core インストールまたは Windows Server、バージョンは 1809 のインストールに使用できます。

>[!NOTE] 
   > コンピューターまたは Server Core を実行している仮想マシンが Windows Update に接続できない場合、以下の手順 1-7 を省略できます。 手順 8 の DISM コマンドから/Source と/LimitAccess をオフのままにしてください。

1. Server FOD 省略可能なパッケージ、ISO をダウンロードし、ISO をローカル ネットワーク上の共有フォルダーにコピーします。

 - ボリューム ライセンスがある場合は、OS の ISO イメージ ファイルが取得される同じポータルからサーバー FOD ISO イメージ ファイルをダウンロードできます。[ボリューム ライセンス サービス センター](https://www.microsoft.com/Licensing/servicecenter/default.aspx)します。
 - Server FOD ISO イメージ ファイルはできるも、 [Microsoft Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019)か、または、 [Visual Studio ポータル](https://visualstudio.microsoft.com)サブスクライバー。


2. ローカル ネットワークに接続されていること、およびに FOD を追加する Server Core コンピューターに管理者としてサインインします。

3. 使用して、 **net**、または FOD ISO の場所に接続するため、他の方法です。

4. FOD ISO を独自のローカル フォルダーにコピーします。

5. 入力して PowerShell を起動**powershell.exe**コマンド プロンプトでします。

6. 次のコマンドを使用して FoD ISO をマウントします。

        Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso

7. 型**終了**を PowerShell を終了します。

8.  次のコマンドを実行します。

        DISM /Online /Add-Capability /CapabilityName:"ServerCore.AppCompatibility~~~~0.0.1.0" /Source:drive_letter_of_mounted_ISO: /LimitAccess

9.  進行状況バーが完了したら後、は、オペレーティング システムを再起動します。

### <a name="to-optionally-add-internet-explorer-11-to-server-core-after-adding-the-server-core-app-compatibility-fod"></a>(Server Core のアプリケーション互換性 FOD の追加) した後、Internet Explorer 11 を Server Core 必要に応じて追加するには

 >[!NOTE]  
   > Server Core のアプリケーション互換性 FOD は Internet Explorer 11 の追加に必要ですが、Internet Explorer 11 は、Server Core のアプリケーション互換性 FOD を追加する必要はありません。

1.  既に追加されて、アプリ互換性 FOD を持つ、Server Core コンピューターと ISO がローカルにコピーされるサーバー FOD 省略可能なパッケージで管理者としてサインインします。

2.  入力して PowerShell を起動**powershell.exe**コマンド プロンプトでします。

3.  次のコマンドを使用して FoD ISO をマウントします。

         Mount-DiskImage -ImagePath drive_letter:\folder_where_ISO_is_saved\ISO_filename.iso

4.  型**終了**を PowerShell を終了します。


5.  次のコマンドを実行します。

        Dism /online /add-package:drive_letter_of_mounted_iso:"Microsoft-Windows-InternetExplorer-Optional-Package~31bf3856ad364e35~amd64~~.cab"

6.  進行状況バーが完了したら後、は、オペレーティング システムを再起動します。

 
#### <a name="release-notes-and-suggestions-for-the-server-core-app-compatibility-fod-and-internet-explorer-11-optional-package"></a>リリース ノートと Server Core アプリの互換性 FOD および Internet Explorer 11 の省略可能なパッケージに関する推奨事項

- **重要:** 懸案事項、考慮事項、またはインストールと Server Core アプリの互換性 FOD および Internet Explorer 11 の省略可能なパッケージの使用を続行する前にガイダンスの Windows Server 2019 リリース ノートをお読みください。
 
 >[!NOTE] 
   > Windows Update を使用して、累積的更新プログラムをインストールした後、アプリ互換性 FOD を追加するときに、Server Core のコンソールのエクスペリエンスでちらつきが発生することになります。  この問題は、2018 年 12 月で解決を更新します。  詳細情報と解決手順は、次を参照してください。[サポート技術情報記事 4481610。Windows Server 2019 の Server Core で Server Core アプリの互換性 FOD をインストールした後に画面がちらつき](https://support.microsoft.com/help/4481610/screen-flickers-after-fod-installation-windows2019-server-core)します。

- アプリケーション互換性 FOD と、サーバーの再起動のインストール後、コマンド コンソールのウィンドウ フレームの色は、青色のさまざまな網掛けに変更されます。

- Internet Explorer 11 の省略可能なパッケージをインストールする場合は、ダブルクリックするとローカルに保存した .htm ファイルを開くには、サポートされていないことに注意してください。 ただし、**を右クリックして**選択**IE で開く**、または Internet Explorer から直接開くことができます**ファイル** -> **を開く**. 

- アプリの互換性 FOD と Server Core のアプリケーションの互換性をさらに強化するには、IIS 管理コンソールが追加されました Server core オプション コンポーネントとして。  ただし、最初に追加の IIS 管理コンソールを使用するアプリの互換性 FOD どうしても必要なは。 IIS 管理コンソールは、Server Core のアプリケーションの互換性 FOD 追加収録されてのみを Microsoft 管理コンソール (mmc.exe) に依存します。  Powershell を使用して[ **Install-windowsfeature** ](https://docs.microsoft.com/powershell/module/microsoft.windows.servermanager.migration/install-windowsfeature?view=win10-ps) IIS 管理コンソールを追加します。

- ガイダンスについては、サーバー上のアプリのインストールのコア (これらの省略可能なパッケージの有無にかかわらず)、時の一般的なポイントでは、サイレント インストール オプションと手順を使用する必要な場合があります。 
    
 - 例として、SQL Server 2016 および SQL Server 2017 の SQL Server Management Studio は Server Core にインストールすることができ、アプリの互換性 FOD が存在する場合は、完全に機能します。  参照してください、[コマンド プロンプトから SQL Server インストール](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-from-the-command-prompt?view=sql-server-2017)します。
 - SQL Server Management Studio が望ましくない場合、必要はありませんサーバー コア アプリ互換性 FOD をインストールします。  参照してください、 [Server Core での SQL Server のインストール](https://docs.microsoft.com/sql/database-engine/install-windows/install-sql-server-on-server-core?view=sql-server-2017)します。

