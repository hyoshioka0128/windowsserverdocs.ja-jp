---
title: Windows Server Essentials の移行元サーバーを準備する migration1
description: Windows Server Essentials を使用する方法について説明します
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841153"
---
# <a name="prepare-your-source-server-for-windows-server-essentials-migration1"></a>Windows Server Essentials の移行元サーバーを準備する migration1

>適用先:Windows Server 2016 Essentials、Windows Server 2012 R2 Essentials、Windows Server 2012 Essentials

移行元サーバーの設定とデータが正常に移行先サーバーに移行されるようにするために、次の準備作業を完了してください。  
  
#### <a name="to-prepare-for-migration"></a>移行の準備をするには  
  

1.  [ソース サーバーをバックアップします。](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)  
  
2.  [最新のサービス パックをインストールします。](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)  
  
3.  [移行元サーバーの正常性を評価します。](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_UseWindowsBestPracticeAnalyzer)  
  
4.  [移行元サーバーで移行準備ツールを実行します。](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MPT)  
  
5.  [基幹業務アプリケーションを移行する計画を作成します。](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_PlanToMigrateLineOfBusinessApplications)  

1.  [ソース サーバーをバックアップします。](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)  
  
2.  [最新のサービス パックをインストールします。](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)  
  
3.  [移行元サーバーの正常性を評価します。](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_UseWindowsBestPracticeAnalyzer)  
  
4.  [移行元サーバーで移行準備ツールを実行します。](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MPT)  
  
5.  [基幹業務アプリケーションを移行する計画を作成します。](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_PlanToMigrateLineOfBusinessApplications)  

  
###  <a name="BKMK_BackUpYourSourceServerToPrepareForMigration"></a> ソース サーバーをバックアップします。  
 移行プロセスを開始する前に、移行元サーバーをバックアップします。 バックアップを作成すると、移行中に回復不可能なエラーが発生した場合に、データが不用意に失われることを防ぐことができます。  
  
##### <a name="to-back-up-the-source-server"></a>移行元サーバーをバックアップするには  
  
1.  移行元サーバーの完全バックアップを実行します。 Windows Small Business Server 2011 Essentials のバックアップの詳細については、次を参照してください。[サーバー バックアップの設定の詳細について](https://technet.microsoft.com/library/server-backup-support-1.aspx)します。  
  
2.  バックアップが正常に実行されたことを確認します。 バックアップの整合性をテストするには、バックアップからランダムにファイルを選択し、それらのファイルを別の場所に復元して、復元されたファイルが元のファイルと同じことを確認します。  
  
###  <a name="BKMK_InstallTheMostRecentServicePacksToPrepareForMigration"></a> 最新のサービス パックをインストールします。  
 移行前に、最新の更新プログラムとサービス パックを移行元サーバーにインストールする必要があります。  
  
###  <a name="BKMK_UseWindowsBestPracticeAnalyzer"></a> 移行元サーバーの正常性を評価します。  
 移行を開始する前に、移行元サーバーの正常性を評価することが重要です。 以下の手順を使用して、更新プログラムが最新であることを確認し、システム正常性レポートを生成し、Windows Server Solutions ベスト プラクティス アナライザー (BPA) を実行します。  
  
#### <a name="download-and-install-critical-and-security-updates"></a>重要な更新プログラムとセキュリティ更新プログラムをダウンロードしてインストールする  
 重要な更新プログラムとセキュリティ更新プログラムを移行元サーバーにインストールすると、移行を正常に行い、移行プロセスの間にネットワークを保護するのに役立ちます。  
  
###### <a name="to-check-for-the-latest-updates"></a>最新の更新プログラムを確認するには  
  
1.  移行元サーバーで、**[スタート]**、**[すべてのプログラム]**、**[Windows Update]** の順にクリックします。  
  
2.  **[更新プログラムのチェック]** をクリックします。  
  
3.  更新プログラムがある場合は、**[更新プログラムのインストール]** をクリックします。  
  
#### <a name="check-the-alert-viewer-for-critical-errors"></a>アラート ビューアーで重大なエラーを確認する  
 ダッシュボードのアラート ビューアーで重大なエラーを確認できます。  
  
#### <a name="run-the-windows-server-solutions-best-practices-analyzer"></a>Windows Server Solutions ベスト プラクティス アナライザーを実行する  
 移行プロセスを開始する前に、Windows Server Solutions ベスト プラクティス アナライザー (BPA) を実行して、サーバー、ネットワーク、ドメインに問題がないことを確認できます。 BPA は次のソースから構成情報を収集します。  
  
-   Active Directory® Windows Management Instrumentation (WMI)  
  
-   レジストリ  
  
-   インターネット インフォメーション サービス (IIS) メタベース  
  
###### <a name="to-use-the-windows-server-solutions-bpa-to-analyze-your-source-server"></a>Windows Server Solutions BPA を使用して移行元サーバーを分析するには  
  
1.  ダウンロードしてインストール、 [Windows Server Solutions ベスト プラクティス アナライザー](https://www.microsoft.com/en-us/download/details.aspx?id=15556) Microsoft ダウンロード センター。  
  
2.  ダウンロードが完了したら、**[スタート]** をクリックし、**[すべてのプログラム]** をポイントして、**[SBS ベスト プラクティス アナライザー ツール]** をクリックします。  
  
    > [!NOTE]
    >  サーバーをスキャンする前に、更新プログラムがないかどうかを確認してください。  
  
3.  ナビゲーション ウィンドウで、 **[スキャンの開始]** をクリックします。  
  
4.  詳細ウィンドウで、スキャン ラベルを入力し、**[スキャンを開始する]** をクリックします。 スキャンのラベルはスキャン レポートの名前です。たとえば、「**SBS BPA Scan 1Jul2012**」と入力します。  
  
5.  スキャンが完了したら、 **[このベスト プラクティス スキャンのレポートを表示する]** をクリックします。  
  
 サーバーの構成に関する情報を収集した後、Windows Server Solutions BPA は情報が正しいことを検証し、情報および重大度順に並べ替えられた問題の一覧を管理者に対して表示します。 一覧では各問題の説明と推奨事項または可能な解決策が提供されます。 レポートの種類には次の 3 種類があります。  
  
|レポートの種類|説明|  
|-----------------|-----------------|  
|リスト レポート|レポートを 1 次元のリストで表示します。|  
|ツリー レポート|レポートを階層リストで表示します。|  
|その他のレポート|実行時間ログなどのレポートを表示します。|  
  
 問題の説明と解決策を確認するには、レポート内の問題をクリックします。 移行にすべての Windows SBS 2011 Essentials BPA で報告された問題の影響が、移行が成功したことを確実にできるだけ多くの問題として解決する必要があります。  
  
####  <a name="BKMK_SynchronizeTheSourceServerTimeWithAnExternalTimeSource"></a> 移行元サーバーの時刻を外部タイム ソースと同期します。  
 移行元サーバーの時刻は、移行先サーバーの時刻の 5 分以内の誤差に設定し、日付とタイム ゾーンが両サーバー上で一致する必要があります。 移行元サーバーが仮想マシン上で実行されている場合、ホスト サーバーの日付、時刻、およびタイム ゾーンが、移行元サーバー、および移行先サーバーと一致する必要があります。 Windows Server Essentials が正常にインストールされていることを確認するには、インターネット上のネットワーク タイム プロトコル (NTP) サーバーに移行元サーバーの時刻を同期する必要があります。  
  
###### <a name="to-synchronize-the-source-server-time-with-the-ntp-server"></a>移行元サーバーの時刻を NTP サーバーと同期するには  
  
1.  ドメイン管理者のアカウントとパスワードを使用して移行元サーバーにサインオンします。  
  
2.  **[スタート]** をクリックし、**[ファイル名を指定して実行]** をクリックし、「 **cmd** 」と入力して、Enter キーを押します。  
  
3.  コマンド プロンプトで入力 w32tm/reliable:no/信頼性の高い: なし、/update と ENTER キーを押します。  
  
4.  コマンド プロンプトで net stop w32time を入力し、ENTER キーを押します。  
  
5.  コマンド プロンプトで net start w32time を入力し、ENTER キーを押します。  
  
> [!IMPORTANT]
>  Windows Server Essentials のインストール時に必要な場合、移行先サーバーの時刻を確認し、変更する機会があります。 この時刻と、移行元サーバーに設定されている時刻との差が、5 分以内であることを確認してください。 インストールが完了すると、移行先サーバーが NTP と同期されます。 ドメインに参加しているすべてのコンピューターは、移行元サーバーも含めて移行先サーバーと同期されます。これには、プライマリ ドメイン コントローラー (PDC) エミュレーター マスターの役割が必要です。  
  
###  <a name="BKMK_MPT"></a> 移行元サーバーで移行準備ツールを実行します。  
 最初に移行元サーバーで移行準備ツールを実行しないと、移行モードのインストールを実行できません。 Windows Server Essentials に移行するには、移行元サーバーとドメインを準備するのには、このツールは設計されています。  
  
> [!IMPORTANT]
>  移行準備ツールを実行する前に、移行元サーバーをバックアップします。 移行準備ツールがスキーマに対して行った変更はすべて元に戻すことはできません。 移行中に問題が発生した場合、移行元サーバーを移行準備ツールの実行前の状態に戻す唯一の方法は、システムのバックアップを復元することです。  
  
 移行準備ツールを実行するには、Enterprise Admins グループ、Schema Admins グループ、および Domain Admins グループのメンバーであることが必要です。  
  
##### <a name="to-verify-that-you-have-the-appropriate-permissions-to-run-the-tool-on-the-source-server"></a>移行元サーバーで移行準備ツールを実行するための適切なアクセス許可があることを確認するには  
  
1.  移行元サーバー上で **[スタート]** ボタン、**[管理ツール]** の順にクリックし、**[Active Directory ユーザーとコンピューター]** をクリックします。  
  
2.  コンソール ツリーで、ドメインをクリックして展開し、**[ユーザー]** をクリックします。  
  
3.  移行に使用している管理者アカウントを右クリックし、**[プロパティ]** をクリックします。  
  
4.  **[所属するグループ]** タブをクリックし、Enterprise Admins、Schema Admins、および Domain Admins が **[所属するグループ]** ボックスに一覧表示されていることを確認します。  
  
5.  これらのグループが一覧表示されていない場合は、**[追加]** をクリックし、一覧表示されていないグループを追加します。  
  
    > [!NOTE]
    >  -   Netlogon サービスが開始されない場合、アクセス許可のエラーを受け取る場合があります。  
    > -   変更を有効にするには、移行元サーバーからログオフし、再度ログオンする必要があります。  
  
     最新バージョンの Windows Update エージェントを使用して、サーバーの更新を適切に実行することができます。  
  
 最新バージョンの Windows Update エージェントを使用して、サーバーの更新を適切に実行することができます。  
  
 Windows Update エージェントをインストールするには、移行元サーバーで、前に、Windows PowerShell 2.0 と Microsoft Baseline Configuration Analyzer 2.0 をまずインストールする必要があります。  
  
-   ダウンロードして、Windows PowerShell 2.0 をインストールを参照してください。[記事 968929](https://go.microsoft.com/fwlink/p/?LinkId=241483)マイクロソフト サポート技術情報でします。  
  
-   ダウンロードして、Microsoft Baseline Configuration Analyzer 2.0 をインストールを参照してください、 [Microsoft Baseline Configuration Analyzer 2.0](https://go.microsoft.com/fwlink/p/?LinkId=241484) Microsoft ダウンロード センター。  
  
-   ダウンロードして、Windows Update エージェントの最新バージョンをインストールを参照してください。[記事 949104](https://go.microsoft.com/fwlink/p/?LinkId=237493)マイクロソフト サポート技術情報でします。  
  
##### <a name="to-install-and-run-the-migration-preparation-tool-on-the-source-server"></a>移行元サーバーに移行準備ツールをインストールおよび実行するには  
  
1.  移行元サーバーでの DVD ドライブに Windows Server Essentials の DVD1 を挿入します。  
  
2.  Windows エクスプローラーを開き、DVD の **\support\tools** フォルダーを参照して、**sourcetool.msi** ファイルをダブルクリックします。  
  
    > [!NOTE]
    >  -   移行準備ツールが既にサーバーにインストールされている場合は、**[スタート]** メニューからツールを実行します。  
    > -   できる限りスムーズに移行を行うための準備として、常に最新の更新プログラムをインストールすることをお勧めします。  
  
     ウィザードは、移行元サーバーに移行準備ツールをインストールします。 インストールが完了すると、移行準備ツールが自動的に起動し、最新の更新プログラムをインストールします。  
  
3.  移行準備ツール] で、**[バックアップが存在し、続行する準備が整っています]** を選択し、**[次へ]** をクリックします。  
  
    > [!WARNING]
    >  修正プログラムのインストールに関するエラー メッセージを受信する場合は、メソッドの 2 を参照してください。Catroot2 フォルダーの名前を変更[記事 822798](https://go.microsoft.com/FWLink/p/?LinkID=118672)マイクロソフト サポート技術情報でします。  
  
     移行準備ツールは、Active Directory スキーマを拡張することで、移行元ドメインの移行を準備します。 タスクが完了したら、**[次へ]** をクリックして処理を続行します。  
  
4.  移行元ドメインを準備した後、移行準備ツールは移行元サーバーをスキャンして、2 つのタイプの潜在的な問題点を特定します。  
  
    -   **エラー**移行をブロックしたり、移行が失敗する原因になる移行元サーバーで検出された問題。 エラー メッセージの指示に従って問題を解決し、**[再スキャン]** をクリックします。  
  
    -   **警告**移行中に機能の問題を引き起こす可能性のある移行元サーバーで検出された問題。 移行を続行する前に、エラー メッセージの指示に従って問題を解決することを強くお勧めします。  
  
     すべての問題を解決または確認した後で、**[次へ]** をクリックします。  
  
5.  移行準備ツールで、**[完了]** をクリックします。  
  
6.  移行準備ツールが完了したら、Windows Server Essentials への移行を開始する前に、移行元サーバーを再起動する必要があります。  
  
> [!NOTE]
>  成功した実行は、移行元サーバーで移行先サーバーで Windows Server Essentials のインストールの 2 週間以内の移行準備ツールを完了する必要があります。 それ以外の場合、移行先サーバーで Windows Server Essentials のインストールはブロックされます。 インストールがブロックされた場合は、移行元サーバーでもう一度移行準備ツールを実行する必要があります。  
  
###  <a name="BKMK_PlanToMigrateLineOfBusinessApplications"></a> 基幹業務アプリケーションを移行する計画を作成します。  
 基幹業務 (LOB) アプリケーションは、業務の遂行に欠かせない重要なコンピューター アプリケーションです。 LOB アプリケーションには、会計や、サプライチェーン管理、リソース計画アプリケーションなどがあります。  
  
 LOB アプリケーションの移行を計画する際は、LOB アプリケーションのプロバイダーに相談し、アプリケーションの適切な移行方法を決定してください。 また、移行先サーバーで LOB アプリケーションをインストールする際に使用するメディアも選択する必要があります。  
  
> [!NOTE]
>  開発に、Windows Small Business Server 2011 Essentials SDK を使用する場合は、カスタマイズしたシステム正常性またはアラート アドインとするが、引き続き Windows Server Essentials でアドインを使用したいもアドインを更新し、移行先サーバーに展開する必要があります。  
  
