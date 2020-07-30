---
title: Windows Server Essentials migration1 の移行元サーバーを準備する
description: Windows Server Essentials の使用方法について説明します。
ms.date: 10/03/2016
ms.topic: article
ms.assetid: f5861ae9-77cb-4d37-b4c5-8f0757213385
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 1097520110f876a8c29e05547d4407a13f1c5057
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/27/2020
ms.locfileid: "87180518"
---
# <a name="prepare-your-source-server-for-windows-server-essentials-migration1"></a>Windows Server Essentials migration1 の移行元サーバーを準備する

>適用対象: windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

移行元サーバーの設定とデータが正常に移行先サーバーに移行されるようにするために、次の準備作業を完了してください。

#### <a name="to-prepare-for-migration"></a>移行の準備をするには


1.  [移行元サーバーのバックアップ](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)

2.  [最新のサービス パックのインストール](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)

3.  [移行元サーバーの正常性の評価](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_UseWindowsBestPracticeAnalyzer)

4.  [移行元サーバーでの移行準備ツールの実行](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MPT)

5.  [基幹業務アプリケーションの移行計画の作成](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_PlanToMigrateLineOfBusinessApplications)

###  <a name="back-up-your-source-server"></a><a name="BKMK_BackUpYourSourceServerToPrepareForMigration"></a>移行元サーバーのバックアップ
 移行プロセスを開始する前に、移行元サーバーをバックアップします。 バックアップを作成すると、移行中に回復不可能なエラーが発生した場合に、データが不用意に失われることを防ぐことができます。


##### <a name="to-back-up-the-source-server"></a>移行元サーバーをバックアップするには

1.  移行元サーバーの完全バックアップを実行します。 Windows Small Business Server 2011 Essentials のバックアップの詳細については、[サーバー バックアップの詳細に関するページ](https://technet.microsoft.com/library/server-backup-support-1.aspx)を参照してください。

2.  バックアップが正常に実行されたことを確認します。 バックアップの整合性をテストするには、バックアップからランダムにファイルを選択し、それらのファイルを別の場所に復元して、復元されたファイルが元のファイルと同じことを確認します。

###  <a name="install-the-most-recent-service-packs"></a><a name="BKMK_InstallTheMostRecentServicePacksToPrepareForMigration"></a>最新のサービスパックをインストールする
 移行前に、最新の更新プログラムとサービス パックを移行元サーバーにインストールする必要があります。

###  <a name="evaluate-the-health-of-the-source-server"></a><a name="BKMK_UseWindowsBestPracticeAnalyzer"></a>移行元サーバーの正常性を評価する
 移行を開始する前に、移行元サーバーの正常性を評価することが重要です。 以下の手順を使用して、更新プログラムが最新であることを確認し、システム正常性レポートを生成し、Windows Server Solutions ベスト プラクティス アナライザー (BPA) を実行します。

#### <a name="download-and-install-critical-and-security-updates"></a>重要な更新プログラムとセキュリティ更新プログラムをダウンロードしてインストールする
 重要な更新プログラムとセキュリティ更新プログラムを移行元サーバーにインストールすると、移行を正常に行い、移行プロセスの間にネットワークを保護するのに役立ちます。

###### <a name="to-check-for-the-latest-updates"></a>最新の更新プログラムを確認するには

1.  移行元サーバーで、[**スタート**]、[**すべてのプログラム**]、[**Windows Update**] の順にクリックします。

2.  **[更新プログラムのチェック]** をクリックします。

3.  更新プログラムがある場合は、[**更新プログラムのインストール**] をクリックします。

#### <a name="check-the-alert-viewer-for-critical-errors"></a>アラート ビューアーで重大なエラーを確認する
 ダッシュボードのアラート ビューアーで重大なエラーを確認できます。

#### <a name="run-the-windows-server-solutions-best-practices-analyzer"></a>Windows Server Solutions ベスト プラクティス アナライザーを実行する
 移行プロセスを開始する前に、Windows Server Solutions ベスト プラクティス アナライザー (BPA) を実行して、サーバー、ネットワーク、ドメインに問題がないことを確認できます。 BPA は次のソースから構成情報を収集します。

-   Active Directory &reg; Windows Management Instrumentation (WMI)

-   レジストリ

-   インターネット インフォメーション サービス (IIS) メタベース

###### <a name="to-use-the-windows-server-solutions-bpa-to-analyze-your-source-server"></a>Windows Server Solutions BPA を使用して移行元サーバーを分析するには

1. Microsoft ダウンロード センターから [Windows Server Solutions ベスト プラクティス アナライザー](https://www.microsoft.com/download/details.aspx?id=15556)をダウンロードしてインストールします。

2. ダウンロードが完了したら、[**スタート**] をクリックし、[**すべてのプログラム**] をポイントして、[**SBS ベスト プラクティス アナライザー ツール**] をクリックします。

   > [!NOTE]
   >  サーバーをスキャンする前に、更新プログラムがないかどうかを確認してください。

3. ナビゲーション ウィンドウで、**[スキャンの開始]** をクリックします。

4. 詳細ウィンドウで、スキャン ラベルを入力し、[**スキャンを開始する**] をクリックします。 スキャンのラベルはスキャン レポートの名前です。たとえば、「**SBS BPA Scan 1Jul2012**」と入力します。

5. スキャンが完了したら、**[このベスト プラクティス スキャンのレポートを表示する]** をクリックします。

   サーバーの構成に関する情報を収集した後、Windows Server Solutions BPA は情報が正しいことを検証し、情報および重大度順に並べ替えられた問題の一覧を管理者に対して表示します。 一覧では各問題の説明と推奨事項または可能な解決策が提供されます。 レポートの種類には次の 3 種類があります。

|レポートの種類|説明|
|-----------------|-----------------|
|リスト レポート|レポートを 1 次元のリストで表示します。|
|ツリー レポート|レポートを階層リストで表示します。|
|その他のレポート|実行時間ログなどのレポートを表示します。|

 問題の説明と解決策を確認するには、レポート内の問題をクリックします。 Windows SBS 2011 Essentials BPA で報告された問題のすべてが移行に影響するとは限りませんが、移行が正常に行われるようにするには、できるだけ多くの問題を解決する必要があります。

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

###  <a name="run-the-migration-preparation-tool-on-the-source-server"></a><a name="BKMK_MPT"></a>移行元サーバーで移行準備ツールを実行する
 最初に移行元サーバーで移行準備ツールを実行しないと、移行モードのインストールを実行できません。 このツールは、Windows Server Essentials に移行する移行元サーバーとドメインを準備するために設計されています。

> [!IMPORTANT]
>  移行準備ツールを実行する前に、移行元サーバーをバックアップします。 移行準備ツールがスキーマに対して行った変更はすべて元に戻すことはできません。 移行中に問題が発生した場合、移行元サーバーを移行準備ツールの実行前の状態に戻す唯一の方法は、システムのバックアップを復元することです。

 移行準備ツールを実行するには、Enterprise Admins グループ、Schema Admins グループ、および Domain Admins グループのメンバーであることが必要です。

##### <a name="to-verify-that-you-have-the-appropriate-permissions-to-run-the-tool-on-the-source-server"></a>移行元サーバーで移行準備ツールを実行するための適切なアクセス許可があることを確認するには

1. 移行元サーバー上で [**スタート**] ボタン、[**管理ツール**] の順にクリックし、[**Active Directory ユーザーとコンピューター**] をクリックします。

2. コンソール ツリーで、ドメインをクリックして展開し、[**ユーザー**] をクリックします。

3. 移行に使用している管理者アカウントを右クリックし、[**プロパティ**] をクリックします。

4. [**所属するグループ**] タブをクリックし、Enterprise Admins、Schema Admins、および Domain Admins が [**所属するグループ**] ボックスに一覧表示されていることを確認します。

5. これらのグループが一覧表示されていない場合は、[**追加**] をクリックし、一覧表示されていないグループを追加します。

   > [!NOTE]
   > - Netlogon サービスが開始されない場合、アクセス許可のエラーを受け取る場合があります。
   >   -   変更を有効にするには、移行元サーバーからログオフし、再度ログオンする必要があります。

    最新バージョンの Windows Update エージェントを使用して、サーバーの更新を適切に実行することができます。

   最新バージョンの Windows Update エージェントを使用して、サーバーの更新を適切に実行することができます。

   移行元サーバーに Windows Update エージェントをインストールする前に、まず Windows PowerShell 2.0 と Microsoft Baseline Configuration Analyzer 2.0 をインストールする必要があります。

-   PowerShell 2.0 をダウンロードしてインストールするには、Microsoft サポート技術情報の[記事 968929](https://go.microsoft.com/fwlink/p/?LinkId=241483) を参照してください。

-   Microsoft Baseline Configuration Analyzer 2.0 のダウンロードとインストールについては、Microsoft ダウンロード センターの「[Microsoft Baseline Configuration Analyzer 2.0](https://go.microsoft.com/fwlink/p/?LinkId=241484)」を参照してください。

-   最新バージョンの Windows Update Agent のダウンロードとインストールについては、Microsoft サポート技術情報の[記事 949104](https://go.microsoft.com/fwlink/p/?LinkId=237493) を参照してください。

##### <a name="to-install-and-run-the-migration-preparation-tool-on-the-source-server"></a>移行元サーバーに移行準備ツールをインストールおよび実行するには

1. Windows Server Essentials DVD1 を移行元サーバーの DVD ドライブに挿入します。

2. Windows エクスプローラーを開き、DVD の **\support\tools** フォルダーを参照して、**sourcetool.msi** ファイルをダブルクリックします。

   > [!NOTE]
   > - 移行準備ツールが既にサーバーにインストールされている場合は、[**スタート**] メニューからツールを実行します。
   >   -   できる限りスムーズに移行を行うための準備として、常に最新の更新プログラムをインストールすることをお勧めします。

    ウィザードは、移行元サーバーに移行準備ツールをインストールします。 インストールが完了すると、移行準備ツールが自動的に起動し、最新の更新プログラムをインストールします。

3. [移行準備ツール] で、[**バックアップが存在し、続行する準備が整っています**] を選択し、[**次へ**] をクリックします。

   > [!WARNING]
   >  修正プログラムのインストールに関するエラーメッセージが表示された場合は、Microsoft サポート技術情報の[記事 822798](https://go.microsoft.com/FWLink/p/?LinkID=118672)の「方法 2: Catroot2 フォルダーの名前を変更する」を参照してください。

    移行準備ツールは、Active Directory スキーマを拡張することで、移行元ドメインの移行を準備します。 タスクが完了したら、[**次へ**] をクリックして処理を続行します。

4. 移行元ドメインを準備した後、移行準備ツールは移行元サーバーをスキャンして、2 つのタイプの潜在的な問題点を特定します。

   - **エラー**移行をブロックしたり、移行が失敗したりする可能性がある、移行元サーバーで検出された問題。 エラー メッセージの指示に従って問題を解決し、[**再スキャン**] をクリックします。

   - **警告**移行中に機能上の問題を引き起こす原因となる問題が移行元サーバーで検出されました。 移行を続行する前に、エラー メッセージの指示に従って問題を解決することを強くお勧めします。

     すべての問題を解決または確認した後で、[**次へ**] をクリックします。

5. 移行準備ツールで、[**完了**] をクリックします。

6. 移行準備ツールが完了すると、Windows Server Essentials への移行を開始する前に、移行元サーバーの再起動を求めるメッセージが表示される場合があります。

> [!NOTE]
>  移行元サーバーで移行準備ツールを正常に実行するには、移行先サーバーに Windows Server Essentials をインストールしてから2週間以内に完了する必要があります。 そうしないと、移行先サーバーへの Windows Server Essentials のインストールがブロックされます。 インストールがブロックされた場合は、移行元サーバーでもう一度移行準備ツールを実行する必要があります。

###  <a name="create-a-plan-to-migrate-line-of-business-applications"></a><a name="BKMK_PlanToMigrateLineOfBusinessApplications"></a>基幹業務アプリケーションを移行するための計画を作成する
 基幹業務 (LOB) アプリケーションは、業務の遂行に欠かせない重要なコンピューター アプリケーションです。 LOB アプリケーションには、会計や、サプライチェーン管理、リソース計画アプリケーションなどがあります。

 LOB アプリケーションの移行を計画する際は、LOB アプリケーションのプロバイダーに相談し、アプリケーションの適切な移行方法を決定してください。 また、移行先サーバーで LOB アプリケーションをインストールする際に使用するメディアも選択する必要があります。

> [!NOTE]
>  Windows Small Business Server 2011 Essentials SDK を使用して、カスタマイズされたシステム正常性アドインまたはアラートアドインを開発していて、引き続き Windows Server Essentials でアドインを使用する場合は、アドインを更新して移行先サーバーに展開する必要もあります。

