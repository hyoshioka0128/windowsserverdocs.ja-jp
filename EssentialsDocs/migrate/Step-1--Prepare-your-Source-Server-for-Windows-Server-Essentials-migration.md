---
title: '手順 1: Windows Server Essentials への移行に向けて移行元サーバーを準備する'
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.topic: article
ms.assetid: 244c8a06-04c6-4863-8b52-974786455373
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 6666a0f68863913c0c0a5a1b1e903eaebf5470a4
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87180488"
---
# <a name="step-1-prepare-your-source-server-for-windows-server-essentials-migration"></a>手順 1: Windows Server Essentials への移行に向けて移行元サーバーを準備する

> 適用対象: Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials

このトピックでは、移行元サーバーのバックアップ、移行元サーバーのシステム正常性の評価、最新のサービス パックと修正プログラムのインストール、およびネットワーク構成の検証の方法について説明します。

## <a name="to-prepare-for-migration"></a>移行の準備をするには
 移行元サーバーの設定とデータが正常に移行先サーバーに移行されるようにするために、次の準備作業を完了してください。

1.  [移行元サーバーのバックアップ](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)

2.  [最新のサービス パックのインストール](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)

3.  [[サービスとしてログオン] アカウント設定を削除します。](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_DeleteSvcAcctSetting)

4.  [移行元サーバーの正常性の評価](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_EvaluateHealth)

5.  [基幹業務アプリケーションの移行計画の作成](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MigrateLOB)

###  <a name="back-up-your-source-server"></a><a name="BKMK_BackUpYourSourceServerToPrepareForMigration"></a>移行元サーバーのバックアップ
 移行プロセスを開始する前に、移行元サーバーをバックアップします。 バックアップを作成すると、移行中に回復不可能なエラーが発生した場合に、データが不用意に失われることを防ぐことができます。

##### <a name="to-back-up-the-source-server"></a>移行元サーバーをバックアップするには

1. 次の表のいずれかのリソースを使用して、移行元サーバーの完全バックアップを実行します。

2. バックアップが正常に実行されたことを確認します。 バックアップの整合性をテストするには、バックアップからランダムにファイルを選択し、それらのファイルを別の場所に復元して、復元されたファイルが元のファイルと同じことを確認します。

   |製品|リソース|
   |---|---|
   |Windows Small Business Server 2003|[Windows Small Business Server 2003 のバックアップと復元](https://msdn.microsoft.com/library/cc875809.aspx)
   |Windows Small Business Server 2008|[Windows Small Business Server 2008 のデータのバックアップと復元](https://technet.microsoft.com/library/cc527505\(WS.10\).aspx)
   |Windows Server 2008 Foundation|[バックアップと回復](https://technet.microsoft.com/library/cc754097\(WS.10\).aspx)
   |Windows Small Business Server 2011 Essentials|[サーバー バックアップのセットアップに関する詳細情報](https://technet.microsoft.com/library/server-backup-support-1.aspx)
   |Windows Small Business Server 2011 Standard|[サーバー バックアップの管理](https://technet.microsoft.com/library/cc527488.aspx)
   |Windows Server Essentials|[Windows Server Essentials でのバックアップと復元の管理](https://technet.microsoft.com/library/jj713536.aspx)

###  <a name="install-the-most-recent-service-packs"></a><a name="BKMK_InstallTheMostRecentServicePacksToPrepareForMigration"></a>最新のサービスパックをインストールする
 移行前に、最新の更新プログラムとサービス パックを移行元サーバーにインストールする必要があります。

###  <a name="delete-the-log-on-as-a-service-account-setting"></a><a name="BKMK_DeleteSvcAcctSetting"></a>[サービスとしてログオン] アカウント設定を削除します。
 Windows Small Business Server 2003 または Windows Server 2003 から移行する場合、グループ ポリシーから [**サービスとしてログオン**] アカウント設定を削除します。

##### <a name="to-delete-the-log-on-as-a-service-account-setting"></a>[サービスとしてログオン] アカウント設定を削除するには

1.  [**グループ ポリシーの管理**] ツールを開くには、[**スタート**] をクリックし、[**コントロール パネル**] をクリックして、[**管理ツール**] をクリックし、[**グループ ポリシーの管理**] をクリックします。

2.  [**既定のドメイン コントローラー ポリシー**] を右クリックし、[**編集**] をクリックします。

3.  **[コンピューターの構成] &gt; [Windows の設定] &gt; [セキュリティの設定] &gt; [ローカル ポリシー] &gt; [ユーザー権利の割り当て]** の順に移動します。

4.  詳細ウィンドウで、[**サービスとしてログオン**] をダブルクリックします。

5.  [**これらのポリシー設定を定義する**] チェック ボックスをオフにします。

6.  \\\Localhost\SYSVOL \\<domainname \>\scripts\SBS_LOGIN_SCRIPT.bat を削除します。

###  <a name="evaluate-the-health-of-the-source-server"></a><a name="BKMK_EvaluateHealth"></a>移行元サーバーの正常性を評価する
 移行を開始する前に、移行元サーバーの正常性を評価することが重要です。 以下の手順を使用して、更新プログラムが最新であることを確認し、システム正常性レポートを生成し、Windows Server Solutions ベスト プラクティス アナライザー (BPA) を実行します。

#### <a name="download-and-install-critical-and-security-updates"></a>重要な更新プログラムとセキュリティ更新プログラムをダウンロードしてインストールする
 重要な更新プログラムとセキュリティ更新プログラムを移行元サーバーにインストールすると、移行を正常に行い、移行プロセスの間にネットワークを保護するのに役立ちます。

###### <a name="to-check-for-the-latest-updates"></a>最新の更新プログラムを確認するには

1.  移行元サーバーで、[**スタート**]、[**すべてのプログラム**]、[**Windows Update**] の順にクリックします。

2.  **[更新プログラムのチェック]** をクリックします。

3.  更新プログラムがある場合は、[**更新プログラムのインストール**] をクリックします。

#### <a name="run-the-best-practices-analyzer"></a>ベスト プラクティス アナライザーを実行します。
 移行プロセスを開始する前に、ベスト プラクティス アナライザー (BPA) を実行して、サーバー、ネットワーク、またはドメインに問題がないことを確認できます。 BPA は次のソースから構成情報を収集します。

-   Active Directory Windows Management Instrumentation (WMI)

-   レジストリ

-   インターネット インフォメーション サービス (IIS)

###### <a name="to-use-the-bpa-to-analyze-your-source-server"></a>BPA を使用して、移行元サーバーを分析するには

1. 次の表に、移行元サーバー用のベスト プラクティス アナライザー (BPA) をダウンロードしてインストールできる Microsoft ダウンロード センターへのリンクを示しています。


   |             移行元サーバーでが実行されている場合             |                                                     BPA ツールは、                                                      |
   |----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
   |                     Windows SBS 2003                     | [Microsoft Windows Small Business Server 2003 ベスト プラクティス アナライザー Web サイト](https://www.microsoft.com/download/details.aspx?id=5334) |
   |                     Windows SBS 2008                     | [Microsoft Windows Small Business Server 2008 ベスト プラクティス アナライザー Web サイト](https://www.microsoft.com/download/details.aspx?id=6231) |
   | Windows SBS 2011 Essentials または Windows SBS 2011 Standard |          [Windows Server Solutions ベスト プラクティス アナライザー Web サイト](https://www.microsoft.com/download/details.aspx?id=15556)           |
   |     Windows Server Essentials または Windows Server 2012     |                                                          サーバー ダッシュボード                                                           |


2. ダウンロードが完了したら、[**スタート**] をクリックし、[**すべてのプログラム**] をポイントして、[**SBS ベスト プラクティス アナライザー ツール**] をクリックします。

   > [!NOTE]
   >  サーバーをスキャンする前に、更新プログラムがないかどうかを確認してください。

3. ナビゲーション ウィンドウで、**[スキャンの開始]** をクリックします。

    移行元サーバーで Windows Server Essentials が実行されている場合は、次の手順を実行します。

   1.  移行先サーバーに管理者としてログオンし、ダッシュボードを開きます。

   2.  ダッシュボードで [**デバイス**] タブをクリックします。

   3.  [<**Server**の  > **タスク**] ウィンドウで、[**ベストプラクティスアナライザー**] をクリックします。

4. 詳細ウィンドウで、スキャン ラベルを入力し、[**スキャンを開始する**] をクリックします。 スキャンのラベルはスキャン レポートの名前です。たとえば、「**SBS BPA Scan 1Jul2013**」などと入力します。

5. スキャンが完了したら、**[このベスト プラクティス スキャンのレポートを表示する]** をクリックします。

   BPA ツールはサーバーの構成に関する情報を収集した後に、情報が正しいことを検証し、重大度で並べ替えた情報と問題の一覧を管理者に提示します。 一覧では各問題の説明と推奨事項または可能な解決策が提供されます。 レポートの種類には次の 3 種類があります。

|レポートの種類|説明
|-----------------|-----------------
|リスト レポート|レポートを 1 次元のリストで表示します。
|ツリー レポート|レポートを階層リストで表示します。

問題の説明と解決策を確認するには、レポート内の問題をクリックします。 BPA ツールで報告された問題のすべてが移行に影響するとは限りませんが、移行が正常に行われるようにするには、できるだけ多くの問題を解決する必要があります。

####  <a name="synchronize-the-source-server-time-with-an-external-time-source"></a><a name="BKMK_SynchronizeTheSourceServerTimeWithAnExternalTimeSource"></a>移行元サーバーの時刻を外部タイムソースと同期する
 移行元サーバーの時刻は、移行先サーバーの時刻の 5 分以内の誤差に設定し、日付とタイム ゾーンが両サーバー上で一致する必要があります。 移行元サーバーが仮想マシン上で実行されている場合、ホスト サーバーの日付、時刻、およびタイム ゾーンが、移行元サーバー、および移行先サーバーと一致する必要があります。 Windows Server Essentials が正常にインストールされていることを確認するには、移行元サーバーの時刻をインターネット上のネットワークタイムプロトコル (NTP) サーバーと同期する必要があります。

###### <a name="to-synchronize-the-source-server-time-with-the-ntp-server"></a>移行元サーバーの時刻を NTP サーバーと同期するには

1.  ドメイン管理者のアカウントとパスワードを使用して移行元サーバーにサインオンします。

2.  [**スタート**] をクリックし、[**ファイル名を指定して実行**] をクリックし、「**cmd**」と入力して、Enter キーを押します。

3.  コマンド プロンプトで、「w32tm /config /syncfromflags:domhier /reliable:no /update」と入力して Enter キーを押します。

4.  コマンド プロンプトで、「net stop w32time」と入力して Enter キーを押します。

5.  コマンド プロンプトで、「net start w32time」と入力して Enter キーを押します。

> [!IMPORTANT]
>  Windows Server Essentials のインストール中に、移行先サーバーの時刻を確認し、必要に応じて変更することができます。 この時刻と、移行元サーバーに設定されている時刻との差が、5 分以内であることを確認してください。 インストールが完了すると、移行先サーバーが NTP と同期されます。 ドメインに参加しているすべてのコンピューターは、移行元サーバーも含めて移行先サーバーと同期されます。これには、プライマリ ドメイン コントローラー (PDC) エミュレーター マスターの役割が必要です。

###  <a name="create-a-plan-to-migrate-line-of-business-applications"></a><a name="BKMK_MigrateLOB"></a>基幹業務アプリケーションを移行するための計画を作成する
 基幹業務 (LOB) アプリケーションは、業務の遂行に欠かせない重要なコンピューター アプリケーションです。 LOB アプリケーションには、会計や、サプライチェーン管理、リソース計画アプリケーションなどがあります。

 LOB アプリケーションの移行を計画する際は、LOB アプリケーションのプロバイダーに相談し、アプリケーションの適切な移行方法を決定してください。 また、移行先サーバーで LOB アプリケーションをインストールする際に使用するメディアも選択する必要があります。

> [!NOTE]
>  Windows Small Business Server 2011 Essentials SDK を使用して、カスタマイズされたシステム正常性アドインまたはアラートアドインを開発していて、引き続き Windows Server Essentials でアドインを使用する場合は、アドインを更新して移行先サーバーに展開する必要もあります。


### <a name="create-a-plan-to-migrate-email-hosted-on-windows-sbs-2011-windows-sbs-2008-and-windows-sbs-2003"></a>Windows SBS 2011、Windows SBS 2008、および Windows SBS 2003 でホストされている電子メールの移行計画を作成します。
 Windows SBS 2011、Windows SBS 2008、および Windows SBS 2003 では、電子メールは Microsoft Exchange Server によって提供されます。 ただし、Windows Server Essentials では、受信トレイ電子メールサービスは提供されません。 会社の電子メールをホストするために、Windows SBS 2011、Windows SBS 2008、または Windows SBS 2003 を実行するサーバーを現在使用している場合は、別のオンプレミスまたはホスト型ソリューションに移行する必要があります。

> [!NOTE]
>  移行元サーバーを更新し、移行の準備が完了したら、移行プロセスを続行する前に、更新したサーバーのバックアップを作成することをお勧めします。

#### <a name="migrate-email-to-microsoft-office-365"></a>電子メールを Microsoft Office 365 に移行する
 ドメインの電子メール ソリューションとして Microsoft Office 365 を利用することにした場合は、「 [Exchange のカットオーバー移行によるすべてのメールボックスのクラウドへの移行](https://help.outlook.com/140/ms.exch.ecp.emailmigrationwizardexchangelearnmore.aspx) 」に記載されているガイダンスに従って、Office 365 への電子メールの移行を開始します。 Windows Server Essentials をインストールする前に、電子メールの移行を完了することをお勧めします。

> [!NOTE]
>  Windows Server Essentials と Office 365 を統合する場合は、移行元サーバーでオンプレミスの Exchange Server を削除する手順は必須です。 Office 365 に Exchange Server パブリック フォルダーを移行する方法については、ブログの投稿「 [Office 365 用 Microsoft Exchange 2013 パブリック フォルダー移行スクリプト](https://blogs.technet.com/b/fmustafa/archive/2013/04/11/microsoft-exchange-2013-public-folders-migration-scripts-for-office-365.aspx)」を参照してください。
>
>  インストールが完了したら、 **Microsoft Office 365 との統合**タスクを実行して、Windows Server Essentials の Office 365 統合機能を有効にする必要があります。

> [!IMPORTANT]
>  Office 365 移行ツールが移行元サーバーで実行している Exchange Server に接続できるようにするには、移行元サーバーで RPC over HTTP を有効にする必要があります。 RPC over HTTP を有効にする方法の詳細については、「 [Small Business Server 2003 に RPC over HTTP を初めて展開する方法 (標準またはプレミアム)](https://technet.microsoft.com/library/bb123622%28EXCHG.65%29.aspx)」を参照してください。 RPC over HTTP を有効にした後で Office 365 移行ツールを正常に実行できない場合は、レジストリの HKEY_LOCAL_MACHINE\Software\Microsoft\Rpc\RpcProxy にある [ **ValidPorts** ] の設定を表示し、移行元サーバーの完全修飾ドメイン名 (FQDN) が含まれていることを確認してください。 FQDN が表示されていない場合は、次の例に従って手動で追加します。
>
>  remote. *contoso*.com:6001-6002;remote. *contoso*.com:6004 (*contoso* は実際のドメイン名で置き換えてください)。

#### <a name="migrate-email-to-another-on-premises-exchange-server"></a>電子メールをオンプレミスの別の Exchange Server に移行する
 電子メールを別のオンプレミスの Exchange Server に移行する方法については、「[オンプレミスの Exchange server と Windows Server Essentials の統合](https://technet.microsoft.com/library/jj200172.aspx)」を参照してください。 Windows Server Essentials をインストールした後で、新しいオンプレミスの Exchange Server をセットアップし、移行元サーバーを降格する前に電子メールの移行を完了することをお勧めします。

> [!NOTE]
>  Windows Small Business Server POP3 コネクタは、Exchange Server には含まれていません。 電子メール データを別の Exchange Server に移行すると、POP3 コネクタの機能は使用できなくなります。

> [!NOTE]
>  移行元サーバーを更新し、移行の準備が完了したら、移行プロセスを続行する前に、更新したサーバーのバックアップを作成してください。

## <a name="next-steps"></a>次の手順
 Windows Server Essentials への移行のために移行元サーバーを準備しました。  [次に、「手順 2: Windows Server Essentials を新しいレプリカドメインコントローラーとしてインストール](Step-2--Install-Windows-Server-Essentials-as-a-new-replica-domain-controller.md)する」に進みます。

すべての手順を表示するには、「 [Windows Server Essentials への移行](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md)」を参照してください。

