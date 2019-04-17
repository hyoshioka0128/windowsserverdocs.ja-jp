---
title: "Windows Server Essentials の移行元サーバーを準備する migration1"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5861ae9-77cb-4d37-b4c5-8f0757213385
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 929c7506c78667646e429c4f28df7e5642c575ab
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="prepare-your-source-server-for-windows-server-essentials-migration1"></a>Windows Server Essentials の移行元サーバーを準備する migration1

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

設定と、移行元サーバー上のデータが移行先サーバーに正常に移行することを確認するのには、次の暫定的な手順を完了します。  
  
#### <a name="to-prepare-for-migration"></a>移行を準備するには  
  

1.  [移行元サーバーをバックアップします。](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)  
  
2.  [最新のサービス パックをインストールします。](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)  
  
3.  [移行元サーバーの正常性を評価します。](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_UseWindowsBestPracticeAnalyzer)  
  
4.  [移行元サーバーで移行準備ツールを実行します。](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MPT)  
  
5.  [基幹業務アプリケーションを移行する計画を作成します。](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_PlanToMigrateLineOfBusinessApplications)  

1.  [移行元サーバーをバックアップします。](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)  
  
2.  [最新のサービス パックをインストールします。](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)  
  
3.  [移行元サーバーの正常性を評価します。](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_UseWindowsBestPracticeAnalyzer)  
  
4.  [移行元サーバーで移行準備ツールを実行します。](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MPT)  
  
5.  [基幹業務アプリケーションを移行する計画を作成します。](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_PlanToMigrateLineOfBusinessApplications)  

  
###  <a name="BKMK_BackUpYourSourceServerToPrepareForMigration"></a>移行元サーバーをバックアップします。  
 移行プロセスを開始する前に、移行元サーバーをバックアップします。 バックアップは、移行中に回復不可能なエラーが発生した場合、事故による損失からデータの保護を行っています。  
  
##### <a name="to-back-up-the-source-server"></a>移行元サーバーをバックアップするには  
  
1.  移行元サーバーの完全バックアップを実行します。 Windows Small Business Server 2011 Essentials のバックアップの詳細については、次を参照してください。[サーバー バックアップの設定について詳しく知る](https://technet.microsoft.com/library/server-backup-support-1.aspx)します。  
  
2.  バックアップが正常に実行されたことを確認します。 バックアップの整合性をテストするに、バックアップからランダムにファイルを選択して、それらを別の場所に復元および、復元されたファイルが元のファイルと同じであることを確認します。  
  
###  <a name="BKMK_InstallTheMostRecentServicePacksToPrepareForMigration"></a>最新のサービス パックをインストールします。  
 移行する前に、移行元サーバーで、最新の更新プログラムとサービス パックをインストールする必要があります。  
  
###  <a name="BKMK_UseWindowsBestPracticeAnalyzer"></a>移行元サーバーの正常性を評価します。  
 移行を開始する前に、移行元サーバーの正常性の評価に重要です。 次の手順を使用して、更新プログラムが現在、システム正常性レポートを生成し、Windows Server Solutions ベスト プラクティス アナライザー (BPA) を実行することを確認します。  
  
#### <a name="download-and-install-critical-and-security-updates"></a>ダウンロードとインストールの重要なセキュリティ更新プログラム  
 重要なインストールとセキュリティ更新プログラムを移行元サーバーの移行が成功して、移行プロセス中に、ネットワークを保護するのに役立ちます。  
  
###### <a name="to-check-for-the-latest-updates"></a>最新の更新プログラムを確認するには  
  
1.  移行元サーバーから] をクリックして**開始**、] をクリックして**すべてのプログラム**、] をクリックし、**Windows Update**します。  
  
2.  をクリックして**更新プログラムのチェック**します。  
  
3.  更新プログラムが見つかった場合、] をクリックして**更新プログラムをインストール**します。  
  
#### <a name="check-the-alert-viewer-for-critical-errors"></a>アラート ビューアーで重大なエラーを確認します。  
 アラート ビューアーで重大なエラーのダッシュ ボードを確認することができます。  
  
#### <a name="run-the-windows-server-solutions-best-practices-analyzer"></a>Windows Server Solutions ベスト プラクティス アナライザーを実行します。  
 Windows Server Solutions ベスト プラクティス アナライザー (BPA) がないこと、サーバー、ネットワーク、またはドメイン上の問題の前に、移行プロセスを開始することを確認するを行うことができます。 BPA は、次のソースから構成情報を収集します。  
  
-   アクティブな Directory® Windows Management Instrumentation (WMI)  
  
-   レジストリ  
  
-   インターネット インフォメーション サービス (IIS) メタベース  
  
###### <a name="to-use-the-windows-server-solutions-bpa-to-analyze-your-source-server"></a>移行元サーバーを分析する、Windows Server Solutions BPA を使用するには  
  
1.  ダウンロードしてインストール、[Windows Server Solutions ベスト プラクティス アナライザー](https://www.microsoft.com/en-us/download/details.aspx?id=15556)、Microsoft ダウンロード センターでします。  
  
2.  ダウンロードが完了したら、クリックして**開始**、] をポイント**すべてのプログラム**、] をクリックし、**SBS ベスト プラクティス アナライザー ツール**します。  
  
    > [!NOTE]
    >  サーバーをスキャンする前に、更新プログラムを確認します。  
  
3.  ナビゲーション ウィンドウで、をクリックして**スキャンを開始する**します。  
  
4.  詳細ウィンドウで、スキャンのラベルを入力し、クリックして**スキャンを開始する**します。 スキャンのラベルはスキャン レポートの名前をなどは**SBS BPA Scan 1jul2012**します。  
  
5.  スキャンが完了したら、クリックして**このベスト プラクティス スキャンのレポートを表示**します。  
  
 サーバーの構成に関する情報を収集した後、Windows Server Solutions BPA は情報が正しいとし、重要度で並べ替えた情報と問題の一覧を管理者に対して表示ことを確認します。 一覧は、それぞれの問題について説明し、推奨事項または可能なソリューションを提供します。 3 種類のレポートを使用できます。  
  
|レポートの種類|説明|  
|-----------------|-----------------|  
|レポートを一覧表示|1 次元のリストで、レポートを表示します。|  
|ツリー レポート|階層リストで、レポートを表示します。|  
|その他のレポート|実行時間ログなどのレポートを表示します。|  
  
 説明と問題の解決策を表示するには、レポートで問題をクリックします。 移行に影響しないすべての Windows SBS 2011 Essentials BPA で報告された問題が、移行が成功したことを確認するためにできるだけ多くの問題と解決する必要があります。  
  
####  <a name="BKMK_SynchronizeTheSourceServerTimeWithAnExternalTimeSource"></a>外部のタイム ソースと、移行元サーバーの時刻を同期します。  
 移行先サーバーの時刻から 5 分以内に移行元サーバーの時刻を設定する必要があり、日付とタイム ゾーンは両方のサーバーで同じである必要があります。 移行元サーバーが仮想マシンでを実行している場合、日付、時刻、タイム ゾーンをホスト サーバー必要がありますと一致している移行元サーバーと移行先サーバーのします。 Windows Server Essentials が正常にインストールされていることを確認するには、インターネット上のネットワーク タイム プロトコル (NTP) サーバーに移行元サーバーの時刻を同期する必要があります。  
  
###### <a name="to-synchronize-the-source-server-time-with-the-ntp-server"></a>NTP サーバーと、移行元サーバーの時刻を同期するには  
  
1.  ドメイン管理者アカウントとパスワードで、移行元サーバーにサインオンします。  
  
2.  をクリックして**開始**、] をクリックして**実行**、種類**cmd**テキスト ボックスとし、Enter キーを押します。  
  
3.  コマンド プロンプトで、入力 w32tm /config /syncfromflags: domhier/reliable: ありません/update、し、Enter キーを押します。  
  
4.  コマンド プロンプトでは、net stop w32time を入力し、Enter キーを押します。  
  
5.  コマンド プロンプトで net start w32time を入力し、Enter キーを押します。  
  
> [!IMPORTANT]
>  Windows Server Essentials のインストール中に必要な場合、移行先サーバーの時刻を確認し、変更することがあります。 移行元サーバーで設定されている時刻から 5 分以内に時間があることを確認します。 インストールが完了したら、移行先サーバーが NTP と同期します。 役割のプライマリ ドメイン コントローラ (PDC) エミュレータ マスタを想定して移行先サーバーに、移行元サーバーを含む、すべてのドメインに参加しているコンピューターを同期します。  
  
###  <a name="BKMK_MPT"></a>移行元サーバーで移行準備ツールを実行します。  
 最初に、移行元サーバーで移行準備ツールを実行しない移行モードのインストールを行うことはできません。 Windows Server Essentials に移行するには、移行元サーバーとドメインを準備するのには、このツールは設計されています。  
  
> [!IMPORTANT]
>  移行準備ツールを実行する前に、移行元サーバーをバックアップします。 移行準備ツールがスキーマにいるすべての変更は元に戻せる状態ではありません。 移行中に問題が発生した場合、ツールを実行する前に、移行元サーバーの状態に戻す唯一の方法は、サーバー システムのバックアップから復元するには  
  
 移行準備ツールを実行するには、Enterprise Admins グループ、Schema Admins グループ、および Domain Admins グループのメンバーがあります。  
  
##### <a name="to-verify-that-you-have-the-appropriate-permissions-to-run-the-tool-on-the-source-server"></a>移行元サーバーでツールを実行する適切なアクセス許可があることを確認するには  
  
1.  移行元サーバーで、をクリックして**開始**、] をクリックして**管理ツール**、] をクリックし、**Active Directory ユーザーとコンピューター**します。  
  
2.  コンソール ツリーで、クリックすると、ドメインを展開し、をクリックして**ユーザー**します。  
  
3.  をクリックして、移行を使用している管理者アカウントを右クリックして**プロパティ**します。  
  
4.  をクリックして、**所属するグループ**タブをクリックし、[Enterprise Admins、Schema Admins、および Domain Admins が記載されていることを確認、**のメンバー**テキスト ボックスです。  
  
5.  グループが表示されない場合はクリックして**追加**、し、一覧表示されていない各グループを追加します。  
  
    > [!NOTE]
    >  -   Netlogon サービスが開始されていない場合は、アクセス許可のエラーを受け取る場合があります。  
    > -   ログオフし、変更が反映されるため、サーバーに再度ログオンする必要があります。  
  
     Windows Update エージェントの最新バージョンを使用すると、サーバーの更新プロセスが正常に動作することを確認します。  
  
 Windows Update エージェントの最新バージョンを使用すると、サーバーの更新プロセスが正常に動作することを確認します。  
  
 Windows Update エージェントをインストールするには、移行元サーバーで、前に、最初に Windows PowerShell 2.0 と Microsoft Baseline Configuration Analyzer 2.0 インストールする必要があります。  
  
-   ダウンロードして、Windows PowerShell 2.0 をインストールを参照してください。[記事 968929](https://go.microsoft.com/fwlink/p/?LinkId=241483)、Microsoft サポート技術情報でします。  
  
-   Microsoft Baseline Configuration Analyzer 2.0 のインストールをダウンロードしてを参照してください、[Microsoft Baseline Configuration Analyzer 2.0](https://go.microsoft.com/fwlink/p/?LinkId=241484)、Microsoft ダウンロード センターでします。  
  
-   ダウンロードして、最新バージョンの Windows Update エージェントのインストールを参照してください。[記事 949104](https://go.microsoft.com/fwlink/p/?LinkId=237493)、Microsoft サポート技術情報でします。  
  
##### <a name="to-install-and-run-the-migration-preparation-tool-on-the-source-server"></a>インストールして、移行元サーバーで移行準備ツールを実行します。  
  
1.  移行元サーバーで、DVD ドライブに Windows Server Essentials の DVD1 を挿入します。  
  
2.  Windows エクスプ ローラーを開きを参照してください、**\support\tools**をクリックして、DVD のフォルダー、**sourcetool.msi**ファイル。  
  
    > [!NOTE]
    >  -   移行準備ツールは、サーバーに既にインストールされている場合からツールを実行、**開始**メニュー。  
    > -   考えられる移行の最適なエクスペリエンスの準備がされていることを確認するには、常を選択することを最新の更新プログラムのインストールをお勧めします。  
  
     ウィザードでは、移行元サーバーで移行準備ツールをインストールします。 インストールが完了したら、移行準備ツールが自動的に実行され、最新の更新プログラムをインストールします。  
  
3.  移行準備ツールで、次のように選択します。**バックアップを作成して続行する準備ができました**、] をクリックし、**次**します。  
  
    > [!WARNING]
    >  修正プログラムのインストールに関するエラー メッセージが表示されたら、表示方法 2: Catroot2 フォルダーの名前を変更[記事 822798](https://go.microsoft.com/FWLink/p/?LinkID=118672)、Microsoft サポート技術情報でします。  
  
     移行準備ツールは、Active Directory スキーマを拡張することにより、移行のソース ドメインを準備します。 タスクが完了したら、クリックして**次**を続行します。  
  
4.  移行元ドメインの準備ができたらは、移行準備ツールは、潜在的な問題の 2 つの種類を特定、移行元サーバーをスキャンします。  
  
    -   **エラー**、移行を妨げるまたは移行が失敗する原因になることができますが、移行元サーバーで検出された問題。 クリックして、問題を修正するには、エラー メッセージの指示に従って**再スキャン**します。  
  
    -   **警告**移行中に機能の問題を引き起こす可能性のある、移行元サーバーで検出された問題。 移行を続行する前に問題を修正するエラー メッセージの指示に従うことを強くお勧めします。  
  
     修正するか、またはすべての問題を確認した後にをクリックして**次**します。  
  
5.  移行準備ツールで、をクリックして**完了**します。  
  
6.  移行準備ツールが完了したら、Windows Server Essentials への移行を開始する前に、移行元サーバーの再起動を求めるメッセージが表示します。  
  
> [!NOTE]
>  実行して正常に移行準備ツールの移行元サーバーで移行先サーバーへの Windows Server Essentials のインストールから 2 週間以内に行う必要があります。 それ以外の場合、移行先サーバーで Windows Server Essentials のインストールはブロックされます。 この場合、もう一度移行元サーバーで移行準備ツールを実行する必要があります。  
  
###  <a name="BKMK_PlanToMigrateLineOfBusinessApplications"></a>基幹業務アプリケーションを移行する計画を作成します。  
 基幹業務 (LOB) アプリケーションは、業務の遂行に欠かせない重要なコンピューター アプリケーションです。 LOB アプリケーション含める経理、サプライ チェーン管理、リソース計画アプリケーション。  
  
 LOB アプリケーションの移行を計画するときは、各アプリケーションを移行するための適切な方法を決定する LOB アプリケーションのプロバイダーに問い合わせてください。 移行先サーバーで LOB アプリケーションをインストールするために使用するメディアも検索する必要があります。  
  
> [!NOTE]
>  Windows Small Business Server 2011 Essentials SDK を使用して開発する場合は、カスタマイズしたシステム正常性またはアラート アドインをし、引き続き Windows Server Essentials のアドインを使用するも、アドインを更新して移行先サーバーに展開する必要があります。  
  
