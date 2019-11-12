---
title: Windows Admin Center の概要
description: Windows Admin Center (Project Honolulu) を使って Windows Server を管理する方法の詳細
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 09/18/2019
ms.localizationpriority: high
ms.prod: windows-server
ms.openlocfilehash: c914a472869f9887c83733d6aab614b5676d17d7
ms.sourcegitcommit: 1da993bbb7d578a542e224dde07f93adfcd2f489
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/04/2019
ms.locfileid: "73567134"
---
# <a name="windows-admin-center"></a>Windows Admin Center

> 適用先:Windows Admin Center、Windows Admin Center Preview

**Windows Admin Center** (以前はコードネーム **Project Honolulu**) は Windows Server のインボックス管理ツールの進化形です。ローカルおよびリモート サーバー管理のすべての側面を統合する 1 つのウィンドウです。 ローカルに展開されたブラウザーベースの管理エクスペリエンスのため、インターネット接続や Azure は必要ありません。 Windows Admin Center では、インターネットに接続されていないプライベート ネットワークを含む、展開のあらゆる側面を完全に管理できます。

## <a name="introduction"></a>はじめに

>[!VIDEO https://www.youtube.com/embed/PcQj6ZklmK0]

![Windows Admin Center インフォグラフィック](media/WAC1910Poster_thumb.PNG)

[PDF をダウンロード](https://github.com/MicrosoftDocs/windowsserverdocs/raw/master/WindowsServerDocs/manage/windows-admin-center/media/WindowsAdminCenter1910Poster.pdf)

## <a name="quick-start"></a>クイック スタート

環境内で Windows Admin Center を数分で稼働できます。

1. [ダウンロード](https://aka.ms/windowsadmincenter)
2. [インストール](deploy/install.md)
3. [作業の開始](use/get-started.md)

## <a name="contents-at-a-glance"></a>内容の一覧

<table>
    <tr></tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>概要</h3>
            <ul>
            <li><a href="understand/what-is.md">Windows Admin Center とは?</a>
            <li><a href="understand/faq.md">FAQ</a>
            <li><a href="understand/case-studies.md">導入事例</a>
            <li><a href="understand/related-management.md">関連する管理製品</a>
            <li><a href="understand/videos.md">ビデオ</a>
            </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>計画</h3>
            <ul>
            <li><a href="plan/installation-options.md">お客様に適したインストールの種類はどれか?</a>
            <li><a href="plan/user-access-options.md">ユーザー アクセス オプション</a>
            <br>
            </ul>
        </td>
    </tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>展開</h3>
            <ul>
            <li><a href="deploy/prepare-environment.md">環境の準備</a>
            <li><a href="deploy/install.md">Windows Admin Center のインストール</a>
            <li><a href="deploy/high-availability.md">高可用性の有効化</a>
         </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>構成</h3>
            <ul>
            <li><a href="configure/settings.md">Windows Admin Center の設定</a>
            <li><a href="configure/user-access-control.md">ユーザー アクセスの制御とアクセス許可</a>
            <li><a href="configure/shared-connections.md">共有接続</a>
            <li><a href="configure/using-extensions.md">拡張機能</a>
            </ul>
        </td>
    </tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>vmmblue_2</h3>
            <ul>
            <li><a href="use/get-started.md">起動と接続の追加</a>
            <li><a href="use/manage-servers.md">サーバーの管理</a>
            <li><a href="use/deploy-hyperconverged-infrastructure.md">ハイパーコンバージド インフラストラクチャの展開</a>
            <li><a href="use/manage-hyper-converged.md">ハイパーコンバージド インフラストラクチャの管理</a>
            <li><a href="use/manage-failover-clusters.md">フェールオーバー クラスターの管理</a>
            <li><a href="use/manage-virtual-machines.md">仮想マシンの管理</a>
            <li><a href="use/logging.md">ログ記録</a>
            </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>Azure に接続する</h3>
            <ul>
            <li><a href="azure/index.md">Azure ハイブリッド サービス</a></li>
            <li><a href="azure/azure-integration.md">Windows Admin Center を Azure に接続する</a></li>
            <li><a href="azure/deploy-wac-in-azure.md">Windows Admin Center を Azure に展開する</a></li>
            <li><a href="azure/manage-azure-vms.md">Windows Admin Center の使用による Azure VM の管理</a></li>
            </ul>
        </td>
    </tr>
    <tr>
            <td style="vertical-align: top;">
            <h3>サポート</h3>
            <ul>
            <li><a href="support/index.md">サポート ポリシー</a>
            <li><a href="support/troubleshooting.md">一般的なトラブルシューティング手順</a>
            <li><a href="support/known-issues.md">既知の問題</a>
            </ul>
        </td>
            <td style="vertical-align: top;">
            <h3>拡張</h3>
            <ul>
            <li><a href="extend/extensibility-overview.md">拡張機能の概要</a>
            <li><a href="extend/understand-extensions.md">拡張機能について</a>
            <li><a href="extend/developing-extensions.md">拡張機能の開発</a>
            <li><a href="extend/publish-extensions.md">ガイド</a>
            <li><a href="extend/publish-extensions.md">拡張機能の公開</a>
            </ul>
        </td>
    </tr>

</table>

## <a name="release-history"></a>リリース履歴

次の最新の機能について確認してください。

- バージョン [1910](https://aka.ms/wac1910) は、いくつかの新しい Azure ハイブリッド サービスを導入し、プレビュー段階にあった機能を GA チャネルに取り込む最新の GA リリースです。
- バージョン [1909](https://aka.ms/wac1909) では、Azure VM 固有の接続の種類が導入され、従来のフェールオーバー クラスターと HCI クラスターの接続の種類が統合されています。
- バージョン [1908](https://aka.ms/wac1908) では、視覚的な更新、Packetmon、FlowLog Audit、クラスター用 Azure Monitor のオンボード、および HTTPS 経由の WinRM (ポート 5986) のサポートが追加されています。
- バージョン [1907](https://aka.ms/wac1907) では、Azure コスト見積もりのリンクを追加し、仮想マシンのインポート/エクスポートとタグ付けの機能を強化しました。
- バージョン [1906](https://aka.ms/wac1906) ではインポート/エクスポート VM を追加しました。Azure アカウントの切り替え。Azure からの接続の追加、接続設定の実験、パフォーマンスの向上、およびパフォーマンス プロファイリング ツール。
- バージョン 1904.1 は、ゲートウェイ プラグインの安定性を改善するためのメンテナンスに関する更新プログラムでした。
- バージョン [1904](https://aka.ms/wac1904) は、Azure ハイブリッド サービス ツールを導入し、プレビュー段階にあった機能を GA チャネルに取り込んだ GA リリースでした。
- バージョン [1903](https://aka.ms/wac1903) では、Azure Monitor からの電子メール通知と、Active Directory から Server または PC 接続を追加する機能と、Active Directory、DHCP、および DNS を管理するための新しいツールが追加されました。
- バージョン [1902](https://aka.ms/wac1902) では、共有接続リストと、ソフトウェア定義のネットワーク (SDN) 管理に対する改良点 (ACL、ゲートウェイ接続、および論理ネットワークを管理するための新しい SDN ツールを含む) が追加されました。
- バージョン [1812](https://aka.ms/wac1812) では、濃色テーマ (プレビュー版)、電源構成の設定、BMC 情報、PowerShell による[拡張機能](./configure/using-extensions.md#manage-extensions-with-powershell)と[接続](./use/get-started.md#use-powershell-to-import-or-export-your-connections-with-tags)の管理のサポートが追加されました。
- バージョン [1809.5](https://aka.ms/wac1809.5) は GA の累積的な更新プログラムでした。プラットフォーム全体にわたるさまざまな品質向上、機能強化、バグ修正と、ハイパーコンバージド インフラストラクチャの管理ソリューションに関するいくつかの新機能を含んでいます。
- バージョン [1809](https://cloudblogs.microsoft.com/windowsserver/2018/09/20/windows-admin-center-1809-and-sdk-now-generally-available/) は、以前にプレビュー版として提供されていた機能を GA チャネルに公開する GA リリースでした。
- バージョン [1808](https://aka.ms/WACPreview1808-InsiderBlog) では、"インストールされているアプリ" ツールが追加されたほか、多数の内部改良や、プレビュー SDK に対する大幅な更新が行われました。
- バージョン [1807](https://aka.ms/WACPreview1807-InsiderBlog) では、合理化された Azure 接続エクスペリエンスが追加されたほか、VM インベントリ ページ、ファイル共有機能、Azure 更新の管理の統合などが強化されました。 
- バージョン [1806](https://aka.ms/WACPreview1806-InsiderBlog) では、PowerShell スクリプトの表示、SDN 管理、2008 R2 接続、SDN、スケジュールされたタスクが追加され、その他の多くの機能強化が行われました。
- バージョン 1804.25 - ユーザーが Windows Admin Center を完全にオフラインの環境でインストールすることをサポートするためのメンテナンスに関する更新プログラムです。
- バージョン [1804](https://cloudblogs.microsoft.com/windowsserver/2018/04/12/announcing-windows-admin-center-our-reimagined-management-experience/) - Project Honolulu は Windows Admin Center になり、セキュリティ機能と役割ベースのアクセス制御が追加されました。 最初の GA リリースです。
- バージョン [1803](https://blogs.windows.com/windowsexperience/2018/03/13/announcing-project-honolulu-technical-preview-1803-and-rsat-insider-preview-for-windows-10) では、Azure AD アクセス制御、詳細なログ記録、サイズ変更できるコンテンツのサポートが追加され、多数のツールの機能が強化されました。
- バージョン [1802](https://blogs.windows.com/windowsexperience/2018/02/13/announcing-windows-server-insider-preview-build-17093-project-honolulu-technical-preview-1802) では、アクセシビリティ、ローカライズ、高可用性展開、タグ付け、Hyper-V ホストの設定、ゲートウェイ認証のサポートが追加されました。
- バージョン [1712](https://blogs.windows.com/windowsexperience/2017/12/19/announcing-project-honolulu-technical-preview-1712-build-05002) では、仮想マシンの機能がさらに追加され、ツール全体のパフォーマンスが向上しました。
- バージョン [1711](https://cloudblogs.microsoft.com/windowsserver/2017/12/01/1711-update-to-project-honolulu-technical-preview-is-now-available/) では、要望が多かったツール (リモート デスクトップと PowerShell) が追加され、その他の機能が強化されました。
- バージョン [1709](https://cloudblogs.microsoft.com/windowsserver/2017/09/22/project-honolulu-technical-preview-is-now-available-for-download/) は、最初のパブリック プレビュー リリースとして発売されました。

## <a name="stay-updated"></a>更新情報

![ ](//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOolR)[Twitter で Microsoft をフォローする](https://twitter.com/servermgmt)

![](//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOtyw)[こちらのブログを読む](https://blogs.technet.microsoft.com/servermanagement/)
