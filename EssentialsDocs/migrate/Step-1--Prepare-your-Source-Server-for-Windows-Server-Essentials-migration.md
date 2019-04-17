---
title: "手順 1: Windows Server Essentials で移行元サーバーの移行を準備します。"
description: "Windows Server Essentials を使用する方法について説明します。"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 244c8a06-04c6-4863-8b52-974786455373
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 2efb1badde6d0ca11bc3b7526fdfb377d9f95d3f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/12/2017
---
# <a name="step-1-prepare-your-source-server-for-windows-server-essentials-migration"></a>手順 1: Windows Server Essentials で移行元サーバーの移行を準備します。

>Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials での Windows Server 2012 Essentials を適用対象:

このトピックは、移行元サーバーをバックアップ、移行元サーバーのシステム正常性を評価、最新の service pack と修正プログラム、インストール、およびネットワーク構成を確認する方法について説明します。  
  
## <a name="to-prepare-for-migration"></a>移行を準備するには  
 設定と、移行元サーバー上のデータが移行先サーバーに正常に移行することを確認するのには、次の暫定的な手順を完了します。  
  
1.  [移行元サーバーをバックアップします。](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)  
  
2.  [最新のサービス パックをインストールします。](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)  
  
3.  [サービス アカウント設定としてログを削除します。](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_DeleteSvcAcctSetting)  
  
4.  [移行元サーバーの正常性を評価します。](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_EvaluateHealth)  
  
5.  [基幹業務アプリケーションを移行する計画を作成します。](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MigrateLOB)  
  
###  <a name="BKMK_BackUpYourSourceServerToPrepareForMigration"></a>移行元サーバーをバックアップします。  
 移行プロセスを開始する前に、移行元サーバーをバックアップします。 バックアップは、移行中に回復不可能なエラーが発生した場合、事故による損失からデータの保護を行っています。  
  
##### <a name="to-back-up-the-source-server"></a>移行元サーバーをバックアップするには  
  
1.  次の表に、移行元サーバーの完全バックアップを実行するのにリソースのいずれかを使用します。  
  
2.  バックアップが正常に実行されたことを確認します。 バックアップの整合性をテストするに、バックアップからランダムにファイルを選択して、それらを別の場所に復元および、復元されたファイルが元のファイルと同じであることを確認します。  
  
   |製品|リソース|
   |---|---|
   |Windows Small Business Server 2003|[バックアップと復元の Windows Small Business Server 2003](https://msdn.microsoft.com/library/cc875809.aspx) 
   |Windows Small Business Server 2008|[バックアップと復元の Windows Small Business Server 2008 上のデータ](https://technet.microsoft.com/library/cc527505\(WS.10\).aspx)
   |Windows Server 2008 Foundation|[バックアップと回復](https://technet.microsoft.com/library/cc754097\(WS.10\).aspx)  
   |Windows Small Business Server 2011 Essentials|[サーバー バックアップの設定について詳しく知る](https://technet.microsoft.com/library/server-backup-support-1.aspx)
   |Windows Small Business Server 2011 Standard|[サーバー バックアップの管理](https://technet.microsoft.com/library/cc527488.aspx)  
   |Windows Server Essentials|[バックアップを管理する windows Server Essentials と復元](https://technet.microsoft.com/library/jj713536.aspx)

###  <a name="BKMK_InstallTheMostRecentServicePacksToPrepareForMigration"></a>最新のサービス パックをインストールします。  
 移行する前に、移行元サーバーで、最新の更新プログラムとサービス パックをインストールする必要があります。  
  
###  <a name="BKMK_DeleteSvcAcctSetting"></a>サービス アカウント設定としてログを削除します。  
 、Windows Small Business Server 2003 または Windows Server 2003 から移行している場合は、削除、**サービスとしてログオン**アカウント グループ ポリシーを設定します。  
  
##### <a name="to-delete-the-log-on-as-a-service-account-setting"></a>サービス アカウント設定としてログを削除するには  
  
1.  開くには、**グループ ポリシーの管理**ツール] をクリックして**開始**、] をクリックして**コントロール パネルの [**、] をクリックして**管理ツール**、] をクリックし、**グループ ポリシーの管理**します。  
  
2.  右クリック**既定のドメイン コントローラー ポリシー**、] をクリックし、**編集**します。  
  
3.  移動**権利の割り当てをコンピューターの構成 \windows 設定 \ セキュリティの設定 \ ローカル ポリシー**します。  
  
4.  詳細ウィンドウでダブルクリック**サービスとしてログオン**します。  
  
5.  クリア、**これらのポリシー設定を定義する**チェック ボックスをオンします。  
  
6.  \\\Localhost\SYSVOL\\ < domainname\ > \scripts\SBS_LOGIN_SCRIPT.bat を削除します。  
  
###  <a name="BKMK_EvaluateHealth"></a>移行元サーバーの正常性を評価します。  
 移行を開始する前に、移行元サーバーの正常性の評価に重要です。 次の手順を使用して、更新プログラムが現在、システム正常性レポートを生成し、Windows Server Solutions ベスト プラクティス アナライザー (BPA) を実行することを確認します。  
  
#### <a name="download-and-install-critical-and-security-updates"></a>ダウンロードとインストールの重要なセキュリティ更新プログラム  
 重要なインストールとセキュリティ更新プログラムを移行元サーバーの移行が成功して、移行プロセス中に、ネットワークを保護するのに役立ちます。  
  
###### <a name="to-check-for-the-latest-updates"></a>最新の更新プログラムを確認するには  
  
1.  移行元サーバーから] をクリックして**開始**、] をクリックして**すべてのプログラム**、] をクリックし、**Windows Update**します。  
  
2.  をクリックして**更新プログラムのチェック**します。  
  
3.  更新プログラムが見つかった場合、] をクリックして**更新プログラムをインストール**します。  
  
#### <a name="run-the-best-practices-analyzer"></a>ベスト プラクティス アナライザーを実行します。  
 ないこと、サーバー、ネットワーク、またはドメイン上の問題の前に、移行プロセスを開始することを確認するベスト プラクティス アナライザー (BPA) を実行することができます。 BPA は、次のソースから構成情報を収集します。  
  
-   Active Directory Windows Management Instrumentation (WMI)  
  
-   レジストリ  
  
-   インターネット インフォメーション サービス (IIS)  
  
###### <a name="to-use-the-bpa-to-analyze-your-source-server"></a>BPA を使用して、移行元サーバーを分析するには  
  
1.  次の表は、Microsoft ダウンロード センターでダウンロードしてから、移行元サーバーのベスト プラクティス アナライザー (BPA) をインストールするリンクを示します。  
  
   |移行元サーバーが実行されている場合|BPA ツールを入手することができます。|
   |---|---|
   |Windows SBS 2003|[Microsoft Windows Small Business Server 2003 ベスト プラクティス アナライザー Web サイト](https://www.microsoft.com/download/details.aspx?id=5334)
   |Windows SBS 2008|[Microsoft Windows Small Business Server 2008 ベスト プラクティス アナライザー Web サイト](https://www.microsoft.com/download/details.aspx?id=6231)  
   |Windows SBS 2011 Essentials または Windows SBS 2011 Standard|[Windows Server Solutions ベスト プラクティス アナライザー Web サイト](https://www.microsoft.com/download/details.aspx?id=15556) 
   |Windows Server Essentials または Windows Server 2012|サーバー ダッシュ ボード  
  
2.  ダウンロードが完了したら、クリックして**開始**、] をポイント**すべてのプログラム**、] をクリックし、**SBS ベスト プラクティス アナライザー ツール**します。  
  
    > [!NOTE]
    >  サーバーをスキャンする前に、更新プログラムを確認します。  
  
3.  ナビゲーション ウィンドウで、をクリックして**スキャンを開始する**します。  
  
     移行元サーバーが Windows Server Essentials を実行している場合は、次の操作を行います。  
  
    1.  管理者は、移行先サーバーにログオンし、ダッシュ ボードを開きます。  
  
    2.  ダッシュ ボードで、をクリックして、**デバイス**] タブ。  
  
    3.  <**サーバー** >**タスク**] ウィンドウで、をクリックして**ベスト プラクティス アナライザー**します。  
  
4.  詳細ウィンドウで、スキャンのラベルを入力し、クリックして**スキャンを開始する**します。 スキャンのラベルはスキャン レポートの名前をなどは**SBS BPA Scan 1 年 2013年 7 月**します。  
  
5.  スキャンが完了したら、クリックして**このベスト プラクティス スキャンのレポートを表示**します。  
  
 BPA ツールは、サーバーの構成に関する情報を収集後の情報が正しいとし、重要度で並べ替えた情報と問題の一覧を管理者に対して表示ことを確認します。 一覧は、それぞれの問題について説明し、推奨事項または可能なソリューションを提供します。 3 種類のレポートを使用できます。  
  
|レポートの種類|説明
|-----------------|----------------- 
|レポートを一覧表示|1 次元のリストで、レポートを表示します。 
|ツリー レポート|階層リストで、レポートを表示します。

説明と問題の解決策を表示するには、レポートで問題をクリックします。 BPA ツールで報告された問題のないすべてが影響、移行は、多くの移行が成功したことを確認する限り問題と解決する必要があります。  
  
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
  
###  <a name="BKMK_MigrateLOB"></a>基幹業務アプリケーションを移行する計画を作成します。  
 基幹業務 (LOB) アプリケーションは、業務の遂行に欠かせない重要なコンピューター アプリケーションです。 LOB アプリケーション含める経理、サプライ チェーン管理、リソース計画アプリケーション。  
  
 LOB アプリケーションの移行を計画するときは、各アプリケーションを移行するための適切な方法を決定する LOB アプリケーションのプロバイダーに問い合わせてください。 移行先サーバーで LOB アプリケーションをインストールするために使用するメディアも検索する必要があります。  
  
> [!NOTE]
>  Windows Small Business Server 2011 Essentials SDK を使用して開発する場合は、カスタマイズしたシステム正常性またはアラート アドインをし、引き続き Windows Server Essentials のアドインを使用するも、アドインを更新して移行先サーバーに展開する必要があります。  
  
  
### <a name="create-a-plan-to-migrate-email-hosted-on-windows-sbs-2011-windows-sbs-2008-and-windows-sbs-2003"></a>Windows SBS 2011、Windows SBS 2008、および Windows SBS 2003 でホストされている電子メールの移行計画を作成します。  
 Windows SBS 2011、Windows SBS 2008、および Windows SBS 2003 の場合では、電子メールは Microsoft Exchange Server を通じて提供されます。 ただし、Windows Server Essentials では、受信トレイ電子メール サービスを提供しません。 S の会社の電子メールをホストする、現在 Windows SBS 2011、Windows SBS 2008、または Windows SBS 2003 を実行するサーバーを使用している、する、代替内部設置型に移行する必要がありますかソリューションをホストします。  
  
> [!NOTE]
>  更新して移行する移行元サーバーを準備した後、移行プロセスを続行する前に、更新したサーバーのバックアップを作成することをお勧めします。  
  
#### <a name="migrate-email-to-microsoft-office-365"></a>Microsoft Office 365 への電子メールを移行します。  
 ドメインの電子メール ソリューションとして Microsoft Office 365 を利用することを選択した場合のガイダンスに従って[Exchange のカット オーバー移行でクラウドへのすべてのメールボックスを移行](http://help.outlook.com/140/ms.exch.ecp.emailmigrationwizardexchangelearnmore.aspx)を Office 365 への電子メールの移行を開始します。 Windows Server Essentials をインストールする前に、電子メールの移行を完了することをお勧めします。  
  
> [!NOTE]
>  移行元サーバーで、内部設置型 Exchange サーバーを削除する手順は、Office 365 を Windows Server Essentials を統合する場合は必須です。 Office 365 に Exchange Server パブリック フォルダーを移行する方法については、ブログ記事を参照してください。[Microsoft Exchange 2013 パブリック フォルダー移行スクリプト Office 365 の](http://blogs.technet.com/b/fmustafa/archive/2013/04/11/microsoft-exchange-2013-public-folders-migration-scripts-for-office-365.aspx)します。  
>   
>  実行して Windows Server Essentials で Office 365 統合機能を有効にする必要があります、インストールを完了した後、**Microsoft Office 365 との統合**タスクです。  
  
> [!IMPORTANT]
>  移行元サーバーで実行されている Exchange サーバーに接続する Office 365 移行ツールを許可するには、移行元サーバーで HTTP 経由で、RPC を有効にする必要があります。 HTTP 経由で RPC を有効にする方法については、次を参照してください。[RPC over HTTP を初めて Small Business Server 2003 (標準またはプレミアム) で展開する方法](https://technet.microsoft.com/library/bb123622%28EXCHG.65%29.aspx)します。 HTTP 経由で RPC を有効にした後は、正常に Office 365 移行ツールを実行することはできません、表示、**ValidPorts**、レジストリの HKEY_LOCAL_MACHINE を設定し、移行元サーバーの完全修飾ドメイン名 (FQDN) が表示されていることを確認します。 FQDN が表示されない場合、次の例を使用して手動で追加します。  
>   
>  リモートします。 *contoso*.com:6001-6002; リモートします。 *contoso*.com:6004 (置換*contoso*、ドメインの名前)。  
  
#### <a name="migrate-email-to-another-on-premises-exchange-server"></a>電子メールを別のオンプレミス Exchange サーバーに移行します。  
 電子メールを別の移行する方法については、オンプレミス Exchange Server を参照してください[社内 Exchange Server を Windows Server Essentials と統合](https://technet.microsoft.com/library/jj200172.aspx)します。 Windows Server Essentials をインストールし、移行元サーバーを降格する前に、電子メールの移行を完了した後、新しいオンプレミス Exchange Server を設定することをお勧めします。  
  
> [!NOTE]
>  Windows Small Business Server POP3 コネクタは、Exchange Server に含まれていません。 電子メール データを別の Exchange サーバーに移行した後は、不要になった POP3 コネクタ機能を使用することができます。  
  
> [!NOTE]
>  更新して移行する移行元サーバーを準備した後、移行プロセスを続行する前に、更新したサーバーのバックアップを作成してください。  
  
## <a name="next-steps"></a>次の手順  
 Windows Server Essentials への移行、移行元サーバーを用意します。  移動できるようになりました[手順 2: Windows Server Essentials を新しいレプリカ ドメイン コントローラーとしてインストール](Step-2--Install-Windows-Server-Essentials-as-a-new-replica-domain-controller.md)します。  

すべての手順を参照してください[Windows Server Essentials への移行](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)します。

