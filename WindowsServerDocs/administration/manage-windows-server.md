---
title: 管理
description: Windows Server の管理に関するツール、推奨事項、ガイダンスについて説明します
ms.prod: windows-server
layout: LandingPage
ms.technology: manage
ms.topic: landing-page
author: lizap
ms.author: elizapo
ms.localizationpriority: high
ms.openlocfilehash: 4166d4e8d2819946cdc859ef643cf53315e7290a
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "71370422"
---
# <a name="management"></a>管理


>[!TIP]
> 以前のバージョンの Windows Server に関する情報をお探しの場合は、 docs.microsoft.com の他の [Windows Server ライブラリ](/previous-versions/windows/)を参照してください。 また、[このサイトで検索して](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions)、具体的な情報を確認することもできます。

<hr />

必要な機能を使用するためのロールを含め、Windows Server を環境に展開した後は、次のステップとしてそれらのサーバを管理します。 Windows Server には、Windows Server 環境の理解、特定のサーバーの管理、パフォーマンスの微調整、そして最終的には数多くの管理タスクの自動化に役立ついくつかのツールが用意されています。 

Windows Server インスタンスの管理に使用するツールは、展開したシステムの種類 (デスクトップ エクスペリエンス搭載 Windows Server または Server Core)、物理マシンか仮想マシンか、またサーバの場所によって異なります。 以下では、Windows Server での基本的な管理タスクの実行について説明します。

次の表を参照して、使用するツールを決定します。

| 操作環境   | Windows Admin Center のインストールおよび管理 | Windows Server でのサーバー マネージャーの実行 | Windows 10 での RSAT を使用したサーバー マネージャーの実行 |
|--------|----------------------|--------------------------------------|------------------------------------------|
| Windows 10 PC で作業 | X  |                                      | X                                        |
| デスクトップ エクスペリエンスを実行する Windows Server システムで作業 | X | X | X |
| Server Core を実行する Windows Server システムで作業 |X (Windows 10 上にインストールし、Server Core の管理に使用) | | X |
| Windows Server システムから離れた場所で作業 |X | | X |
| Windows Server システムから離れた場所で作業するが、デスクトップ エクスペリエンスは実行 |X | RDS を使用してサーバーにリモート接続し、サーバー マネージャーを使用 | X |

以下で説明するツールに加え、[リモート デスクトップ サービス](../remote/remote-desktop-services/welcome-to-rds.md)を使用して、オンプレミス サーバー、リモート サーバー、仮想サーバーにアクセスすることもできます。 その後、サーバー マネージャーを使用して管理タスクを実行できます。

<HR />

<ul class="cardsI panelContent">
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                    <h3>Windows Server システムと環境の管理</h3>
<HR />
                        <p><h3><a href="../manage/windows-admin-center/overview.md">Windows Admin Center による UI を使用しないオンプレミス システム、リモート システム、およびシステムの管理</a></h3>Azure やクラウドに依存せずに、Windows サーバーのオンプレミス管理を実現する、ブラウザー ベースの管理アプリです。 Windows Admin Center (以前は "Project Honolulu" と呼ばれていました) では、サーバー インフラストラクチャのあらゆる側面を完全に管理できます。特に、インターネットに接続されていないプライベート ネットワークでの管理に便利です。 Windows Admin Center は、Windows 10、ゲートウェイ サーバー、または管理対象の Windows Server システム上に直接インストールできます。</p>
<HR />
                        <p><h3><a href="server-manager/server-manager.md">サーバー マネージャーを使用したオンプレミス システムの管理</a></h3>Windows Server のフル インストールに含まれる管理コンソールです (UI を持たないインストールでは使用できません。Server Core には、サーバー マネージャーが含まれていません)。サーバー マネージャーを使用して、サーバー ロールのインストールと削除、リモート サーバーの追加と削除、サービスの開始と停止、環境に関して収集したデータの表示を行うことができます。</p>
<HR />
                        <p><h3><a href="../remote/remote-server-administration-tools.md">リモート システムと UI のないシステムの管理には、リモート サーバー管理ツール (RSAT) を使用します。</a></h3>環境に Server Core または リモート サーバー (オンプレミスまたは仮想マシン) のインストールが含まれている場合は、RSAT を使用して、それらのシステムを管理することができます。 RSAT にはサーバー マネージャーが含まれているため、すべてのサーバーの管理に使用できます。 RSAT が Windows 10 で実行されることに注意してください。 Windows Server Core に RSAT をインストールすることはできません。 また、コマンド ラインから Server Core のインストールを管理することもできます。 「<a href="server-core/server-core-administer.md">Server Core での基本的な管理タスク</a>」を参照してください
<HR />
                        <p><h3><a href="windows-server-update-services/get-started/windows-server-update-services-wsus.md">Windows Server システムの更新プログラムの管理</a></h3>Windows Server 環境内のシステムでの更新プログラムの管理および展開には、Windows Server Update Services (WSUS) を使用します。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                    <h3>環境に関する情報の収集</h3>
<HR />
                        <p><h3><a href="get-started-with-setup-and-boot-event-collection.md">セットアップおよびブート イベント収集</a></h3>セットアップおよびブート イベント収集では、"コレクター" コンピューターを指定して、起動時またはセットアップ プロセスの実行時に、他のコンピューターで発生するさまざまな重要イベントを収集できます。 その後、収集されたイベントは、イベント ビューアー、メッセージ アナライザー、Wevtutil、または Windows PowerShell コマンドレットを使用して分析できます。 </p>
<HR />
                        <p><h3><a href="software-inventory-logging/get-started-with-software-inventory-logging.md">ソフトウェア インベントリ ログ (SIL)</a></h3>Windows Server のソフトウェア インベントリ ログは、簡単な PowerShell コマンドレットのセットを使用して、サーバー管理者がサーバーにインストールされた Microsoft ソフトウェアの一覧を取得できる機能です。 また、HTTPS プロトコルを使用して、このデータをネットワーク経由で定期的に収集し、集計のためにターゲット Web サーバーへと転送することもできます。 この機能の管理には、PowerShell コマンドも使用できます (主に毎時の収集と転送のため)。</p>
<HR />
                        <p><h3><a href="user-access-logging/get-started-with-user-access-logging.md">ユーザー アクセス ログ (UAL)</a></h3>ユーザー アクセス ログは、Windows Server 2016、Windows Server 2012 R2、または Windows Server 2012 でログ記録された固有のクライアント デバイスとユーザー要求イベントをローカル データベースに集約します。 サーバー管理者は、クエリによってこれらの記録を使用し、サーバーの役割別、ユーザー別、デバイス別、ローカル サーバー別、日付別に数量とインスタンスを取得できます。 さらにマイクロソフト以外のソフトウェア開発者も、UAL を使用して、UAL イベントを集計することができます。 </a>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                    <h3>Windows Server 環境のパフォーマンスの調整</h3>
<HR />
                        <p><h3><a href="performance-tuning/index.md">パフォーマンスの調整ガイドライン</a></h3>Windows Server のサーバー設定を調整し、特に、時間が経過してもワークロードの性質がほとんど変化しない場合に、パフォーマンスを改善して、エネルギー効率を向上させるためのガイドラインを参照してください。</p>
<HR />
                        <p><h3><a href="server-performance-advisor/microsoft-server-performance-advisor.md">Microsoft Server Performance Advisor</a></h3>Microsoft サーバー パフォーマンス アドバイザー (SPA) を使用すると、ソフトウェア エージェントの追加や運用サーバの再構成を行わずに、他に影響を与えずに Windows サーバーのパフォーマンスの問題を診断するためのメトリックを収集できます。 SPA では、推奨事項を記載した包括的なパフォーマンス レポートと履歴チャートが作成されます。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                    <h3>Windows Server の管理の自動化</h3>
<HR />
                        <p><h3><a href="https://docs.microsoft.com/powershell/scripting/powershell-scripting?view=powershell-5.1">Windows PowerShell</a></h3>Windows PowerShell は、管理タスクの迅速な自動化に重点を置いて設計されたコマンド ライン シェル兼スクリプト言語です。 </p>
<HR />
                        <p><h3><a href="windows-commands/windows-commands.md">Windows コマンド</a></h3>Windows のコマンド ライン ツールを使用して、Windows の管理タスクを実行できます。 コマンド リファレンスを使用して、コマンドライン ツールを理解し、コマンド シェルについて知識を深めるとともに、バッチ ファイルやスクリプト ツールを使用してコマンド ライン タスクを自動化することができます。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
<li>
        <div class="cardSize">
            <div class="cardPadding">
                <div class="card">
                    <div class="cardImageOuter">
                        <div class="cardImage">
                            <img src="../media/i-manage.svg" alt="" />
                        </div>
                    </div>
                    <div class="cardText">
                    <h3>Windows Server の管理の自動化</h3>
<HR />
                        <p><h3><a href="..\manage\system-insights\overview.md">システム インサイト</h3></a>ネイティブの予測分析機能では、パフォーマンス カウンターや ETW イベントなどの Windows Server システム データがローカルで分析されます。これにより、IT 管理者は、展開されたシステム内で問題のある動作を事前に検出して対処することが楽になります。</p>
                    </div>
                </div>
            </div>
        </div>
    </li>
</ul>