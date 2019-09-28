---
title: Windows Server の管理
description: Windows Server の管理に関するツール、推奨事項、ガイダンスについて説明します
ms.prod: windows-server
ms.technology: manage
ms.topic: article
author: lizap
ms.author: elizapo
ms.date: 03/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 880f8da5bfb872fba6fe4886198d932c91f4bf86
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71370468"
---
# <a name="manage-windows-server"></a>Windows Server の管理

>適用対象:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

>[!TIP]
> 以前のバージョンの Windows Server に関する情報をお探しの場合は、 docs.microsoft.com の他の [Windows Server ライブラリ](/previous-versions/windows/)を参照してください。 また、[このサイトで検索して](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions)、具体的な情報を確認することもできます。

 <ul class="cardse panelContent cols cols3">
    <li>
        <a href="https://docs.microsoft.com/windows-insider/at-work-pro/wip-4-biz-feedback-hub">
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                        <h2>管理</h2>
                <p>必要な機能を使用するためのロールを含め、Windows Server を環境に展開した後は、次のステップとしてそれらのサーバを管理します。 Windows Server には、Windows Server 環境の理解、特定のサーバーの管理、パフォーマンスの微調整、そして最終的には数多くの管理タスクの自動化に役立ついくつかのツールが用意されています。 </p>
                    </div>
                </div>
            </div>
        </div>
        </a>
    </li> 
</ul> 

## <a name="manage-windows-server-systems-and-environments"></a>Windows Server システムと環境の管理
Windows Server インスタンスの管理に使用するツールは、展開したシステムの種類 (デスクトップ エクスペリエンス搭載 Windows Server または Server Core)、物理マシンか仮想マシンか、またサーバの場所によって異なります。 以下では、Windows Server での基本的な管理タスクの実行について説明します。

次の表を参照して、使用するツールを決定します。

| 操作環境   | Windows Admin Center のインストールおよび管理 | Windows Server でのサーバー マネージャーの実行 | Windows 10 での RSAT を使用したサーバー マネージャーの実行 |
|--------|----------------------|--------------------------------------|------------------------------------------|
| Windows 10 PC で作業 | x  |                                      | x                                        |
| デスクトップ エクスペリエンスを実行する Windows Server システムで作業 | x | X | x |
| Server Core を実行する Windows Server システムで作業 |X (Windows 10 上にインストールし、Server Core の管理に使用) | | x |
| Windows Server システムから離れた場所で作業 |x | | x |
| Windows Server システムから離れた場所で作業するが、デスクトップ エクスペリエンスは実行 |x | RDS を使用してサーバーにリモート接続し、サーバー マネージャーを使用 | x |

以下で説明するツールに加え、[リモート デスクトップ サービス](../remote/remote-desktop-services/welcome-to-rds.md)を使用して、オンプレミス サーバー、リモート サーバー、仮想サーバーにアクセスすることもできます。 その後、サーバー マネージャーを使用して管理タスクを実行できます。

### <a name="manage-on-premises-systems-remote-systems-and-systems-without-ui-with-windows-admin-center"></a>Windows Admin Center による UI を使用しないオンプレミス システム、リモート システム、およびシステムの管理
[Windows Admin Center](../manage/windows-admin-center/overview.md) は、Azure やクラウドに依存せずに、Windows サーバーのオンプレミス管理を実現する、ブラウザー ベースの管理アプリです。 Windows Admin Center では、サーバー インフラストラクチャのあらゆる側面を完全に管理できます。特に、インターネットに接続されていないプライベート ネットワークでの管理に便利です。 Windows Admin Center は、Windows 10、ゲートウェイ サーバー、または管理対象の Windows Server システム上に直接インストールできます。

>[!NOTE]
>Windows Admin Center は、旧称 "Project Honolulu" の正式名です。

### <a name="manage-on-premises-systems-with-server-manager"></a>サーバー マネージャーを使用したオンプレミス システムの管理
[サーバー マネージャー](server-manager/server-manager.md)は、Windows Server のフル インストールに含まれる管理コンソールです (UI を持たないインストールでは使用できません。Server Core には、サーバー マネージャーが含まれていません)。サーバー マネージャーを使用して、サーバー ロールのインストールと削除、リモート サーバーの追加と削除、サービスの開始と停止、環境に関して収集したデータの表示を行うことができます。

### <a name="manage-remote-systems-and-systems-without-ui-with-remote-server-administration-tools-rsat"></a>リモート システムと UI のないシステムの管理には、リモート サーバー管理ツール (RSAT) を使用します。
環境に Server Core または リモート サーバー (オンプレミスまたは仮想マシン) のインストールが含まれている場合は、[リモート サーバー管理ツール (RSAT)](../remote/remote-server-administration-tools.md) を使用して、それらのシステムを管理することができます。 RSAT にはサーバー マネージャーが含まれているため、すべてのサーバーの管理に使用できます。

> [!IMPORTANT]
> RSAT は、Windows 10 で動作します。 Windows Server Core に RSAT をインストールすることはできません。

また、コマンド ラインから Server Core のインストールを管理することもできます。 くわしくは、「[Server Core での基本的な管理タスク](server-core/server-core-administer.md)」を参照してください。

### <a name="manage-updates-to-windows-server-systems"></a>Windows Server システムの更新プログラムの管理
Windows Server 環境内のシステムへの更新プログラムの管理および展開には、[Windows Server Update Services (WSUS)](windows-server-update-services/get-started/windows-server-update-services-wsus.md) を使用できます。

## <a name="gather-information-about-your-environment"></a>環境に関する情報の収集
管理者として行う決定の多くは、環境内のシステムとユーザーに関するデータに依存します。 以下では、このデータの収集に使用する情報やツールを示します。

まず、Windows 10 や Windows Server から収集できる診断データの情報について、[組織内の Windows 診断データを構成](/windows/configuration/configure-windows-diagnostic-data-in-your-organization)します。

### <a name="setup-and-boot-event-collectionget-started-with-setup-and-boot-event-collectionmd"></a>[セットアップおよびブート イベント収集](get-started-with-setup-and-boot-event-collection.md)
セットアップおよびブート イベント収集では、"コレクター" コンピューターを指定して、起動時またはセットアップ プロセスの実行時に、他のコンピューターで発生するさまざまな重要イベントを収集できます。 その後、収集されたイベントは、イベント ビューアー、メッセージ アナライザー、Wevtutil、または Windows PowerShell コマンドレットを使用して分析できます。 

### <a name="software-inventory-logging-silsoftware-inventory-loggingget-started-with-software-inventory-loggingmd"></a>[ソフトウェア インベントリ ログ (SIL)](software-inventory-logging/get-started-with-software-inventory-logging.md)

Windows Server のソフトウェア インベントリ ログは、サーバー管理者が簡単な PowerShell コマンドレットのセットを使用して、サーバーにインストールされた Microsoft ソフトウェアの一覧を取得できる機能です。 また、HTTPS プロトコルを使用して、このデータをネットワーク経由で定期的に収集し、集計のためにターゲット Web サーバーへと転送することもできます。 この機能の管理には、PowerShell コマンドも使用できます (主に毎時の収集と転送のため)。

### <a name="user-access-logging-ualuser-access-loggingget-started-with-user-access-loggingmd"></a>[ユーザー アクセス ログ (UAL)](user-access-logging/get-started-with-user-access-logging.md)

ユーザー アクセス ログは、Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 でログ記録された固有のクライアント デバイスとユーザー要求イベントをローカル データベースに集約します。 サーバー管理者は、クエリによってこれらの記録を使用し、サーバー ロール別、ユーザー別、デバイス別、ローカル サーバー別、日付別に数量とインスタンスを取得できます。 さらにマイクロソフト以外のソフトウェア開発者も、UAL を使用して、UAL イベントを集計することができます。 

## <a name="tune-your-windows-server-environment-for-performance"></a>Windows Server 環境のパフォーマンスの調整
以下では、環境のパフォーマンスの調整に役立つ情報を示します。

### <a name="performance-tuning-guidelinesperformance-tuningindexmd"></a>[パフォーマンスの調整ガイドライン](performance-tuning/index.md)
Windows Server 2016 のサーバ設定を調整し、特に、時間が経過してもワークロードの性質がほとんど変化しない場合に、パフォーマンスを改善して、エネルギー効率を向上させるためのガイドラインを参照してください。

### <a name="microsoft-server-performance-advisorserver-performance-advisormicrosoft-server-performance-advisormd"></a>[Microsoft Server Performance Advisor](server-performance-advisor/microsoft-server-performance-advisor.md)

Microsoft サーバー パフォーマンス アドバイザー (SPA) を使用すると、ソフトウェア エージェントの追加や運用サーバの再構成を行わずに、他に影響を与えずに Windows サーバーのパフォーマンスの問題を診断するためのメトリックを収集できます。 SPA では、推奨事項を記載した包括的なパフォーマンス レポートと履歴チャートが作成されます。


## <a name="automate-windows-server-management"></a>Windows Server の管理の自動化

Windows Server には、管理タスクを自動化するために使用できる一連のコマンドと Windows PowerShell モジュールが含まれています。

### <a name="windows-powershellpowershellscriptingpowershell-scriptingviewpowershell-51"></a>[Windows PowerShell](/powershell/scripting/powershell-scripting?view=powershell-5.1)
Windows PowerShell は、管理タスクの迅速な自動化に重点を置いて設計されたコマンド ライン シェル兼スクリプト言語です。 

### <a name="windows-commandswindows-commandswindows-commandsmd"></a>[Windows コマンド](windows-commands/windows-commands.md)

Windows のコマンド ライン ツールを使用して、Windows の管理タスクを実行できます。 コマンド リファレンスを使用して、コマンドライン ツールを理解し、コマンド シェルについて知識を深めるとともに、バッチ ファイルやスクリプト ツールを使用してコマンド ライン タスクを自動化することができます。

## <a name="windows-server-insider-preview"></a>Windows Server Insider Preview
### <a name="system-insightsmanagesystem-insightsoverviewmd"></a>[システム インサイト](../manage/system-insights/overview.md)
システム インサイトは、Windows Server でネイティブの予測分析を行う新しい機能です。 これらの予測機能は、パフォーマンス カウンターや ETW イベントなどの Windows Server システム データをローカルで分析し、展開されたシステム内で問題のある動作を事前に検出して対処できるよう、IT 管理者を支援します。 
