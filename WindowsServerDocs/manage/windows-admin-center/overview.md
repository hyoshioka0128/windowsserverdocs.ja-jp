---
title: Windows Admin Center の概要
description: Windows Admin Center (Project Honolulu) を使って Windows Server を管理する方法の詳細
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 04/12/2019
ms.localizationpriority: high
ms.prod: windows-server-threshold
ms.openlocfilehash: 3208c20e8bf9f4cfab4340aa33b24175bbc72dda
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66188330"
---
# <a name="windows-admin-center"></a>Windows Admin Center

>適用先:Windows Admin Center、Windows Admin Center プレビュー

**Windows Admin Center** (コードネーム**プロジェクト ホノルル**) Windows Server 付属の管理ツールの進化版ですが 1 つのローカルとリモート サーバー管理のすべての側面に統合するガラスのウィンドウ。 ローカルに展開されたブラウザー ベースの管理エクスペリエンスのため、インターネット接続や Azure は必要ありません。 Windows Admin Center では、インターネットに接続されていないプライベート ネットワークを含む、展開のあらゆる側面を完全に管理できます。

## <a name="introduction"></a>概要

>[!VIDEO https://www.youtube.com/embed/PcQj6ZklmK0]

![Windows Admin Center インフォグラフィック](media/WAC1809Poster_thumb.PNG)

[PDF をダウンロードします。](https://github.com/MicrosoftDocs/windowsserverdocs/raw/master/WindowsServerDocs/manage/windows-admin-center/media/WindowsAdminCenter1809Poster.pdf)

## <a name="quick-start"></a>クイック スタート

環境内で Windows Admin Center を数分で稼働できます。

1. [ダウンロード](https://aka.ms/windowsadmincenter)
2. [インストール](deploy/install.md)
3. [開始するには](use/get-started.md)

## <a name="contents-at-a-glance"></a>内容の概要

<table>
    <tr></tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>概要</h3>
            <ul>
            <li><a href="understand/what-is.md">Windows Admin Center とは何ですか。</a>
            <li><a href="understand/faq.md">FAQ</a>
            <li><a href="understand/case-studies.md">ケース スタディ</a>
            <li><a href="understand/related-management.md">関連する管理製品</a>
            <li><a href="understand/videos.md">ビデオ</a>
            </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>プラン</h3>
            <ul>
            <li><a href="plan/installation-options.md">インストールの種類は、適切なでしょうか。</a>
            <li><a href="plan/user-access-options.md">ユーザー アクセス オプション</a>
            <br>
            </ul>
        </td>
    </tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>配置</h3>
            <ul>
            <li><a href="deploy/prepare-environment.md">環境を準備します。</a>
            <li><a href="deploy/install.md">Windows Admin Center のインストール</a>
            <li><a href="deploy/high-availability.md">高可用性を有効にします。</a>
         </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>[構成]</h3>
            <ul>
            <li><a href="configure/settings.md">Windows Admin Center の設定</a>
            <li><a href="configure/user-access-control.md">ユーザー アクセス制御とアクセス許可</a>
            <li><a href="configure/using-extensions.md">拡張機能</a>
            </ul>
        </td>
    </tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>使用</h3>
            <ul>
            <li><a href="use/get-started.md">起動し、接続の追加</a>
            <li><a href="use/manage-servers.md">サーバーを管理します。</a>
            <li><a href="use/manage-hyper-converged.md">ハイパー コンバージド インフラストラクチャを管理します。</a>
            <li><a href="use/manage-failover-clusters.md">フェールオーバー クラスターを管理します。</a>
            <li><a href="use/manage-virtual-machines.md">仮想マシンを管理します。</a>
            <li><a href="use/logging.md">ログ記録</a>
            </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>Azure への接続します。</h3>
            <ul>
            <li><a href="azure/index.md">Azure のハイブリッド サービス</a></li>
            <li><a href="azure/azure-integration.md">Windows Admin Center を Azure に接続します。</a></li>
            <li><a href="azure/deploy-wac-in-azure.md">Azure で Windows Admin Center を展開します。</a></li>
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
            <li><a href="extend/understand-extensions.md">拡張機能の理解</a>
            <li><a href="extend/developing-extensions.md">拡張機能を開発します。</a>
            <li><a href="extend/publish-extensions.md">ガイド</a>
            <li><a href="extend/publish-extensions.md">公開の拡張機能</a>
            </ul>
        </td>
    </tr>

</table>

## <a name="release-history"></a>リリース履歴

次の最新の機能について確認してください。

- バージョン[1904](https://aka.ms/wac1904)は、Azure Hybrid Services ツールを紹介しは、GA チャネルのプレビューに含まれていた機能を提供する最新の GA リリース。
- バージョン[1903](https://aka.ms/wac1903) Azure Monitor では、Active Directory、DHCP、DNS を管理するには、Active Directory、および新しいツールからサーバーや PC の接続を追加する機能から電子メール通知が表示されます。
- バージョン[1902](https://aka.ms/wac1902) Acl、ゲートウェイの接続、および論理ネットワークを管理する新しい SDN ツールなど、ソフトウェア定義ネットワーク (SDN) の管理に機能強化 (&)、共有接続の一覧を追加します。
- バージョン [1812](https://aka.ms/wac1812) では、濃色テーマ (プレビュー版)、電源構成の設定、BMC 情報、PowerShell による[拡張機能](./configure/using-extensions.md#manage-extensions-with-powershell)と[接続](./use/get-started.md#use-powershell-to-import-or-export-your-connections-with-tags)の管理のサポートが追加されました。
- バージョン [1809.5](https://aka.ms/wac1809.5) は GA の累積的な更新プログラムで、プラットフォーム全体にわたるさまざまな品質向上、機能強化、バグ修正と、ハイパーコンバージド インフラストラクチャの管理ソリューションに関するいくつかの新機能を含んでいます。
- バージョン [1809](https://cloudblogs.microsoft.com/windowsserver/2018/09/20/windows-admin-center-1809-and-sdk-now-generally-available/) は、以前にプレビュー版として提供されていた機能を GA チャネルに公開する GA リリースでした。
- バージョン [1808](https://aka.ms/WACPreview1808-InsiderBlog) では、"インストールされているアプリ" ツールが追加されたほか、多数の内部改良や、プレビュー SDK に対する大幅な更新が行われました。
- バージョン [1807](https://aka.ms/WACPreview1807-InsiderBlog) では、合理化された Azure 接続エクスペリエンスが追加されたほか、VM インベントリ ページ、ファイル共有機能、Azure 更新の管理の統合などが強化されました。 
- バージョン [1806](https://aka.ms/WACPreview1806-InsiderBlog) では、PowerShell スクリプトの表示、SDN 管理、2008 R2 接続、SDN、スケジュールされたタスクが追加され、その他の多くの機能強化が行われました。
- バージョン 1804.25 - ユーザーが Windows Admin Center を完全にオフラインの環境でインストールすることをサポートするためのメンテナンス更新。
- バージョン [1804](https://cloudblogs.microsoft.com/windowsserver/2018/04/12/announcing-windows-admin-center-our-reimagined-management-experience/) - Project Honolulu は Windows Admin Center になり、セキュリティ機能と役割ベースのアクセス制御が追加されました。 最初の GA リリースです。
- バージョン [1803](https://blogs.windows.com/windowsexperience/2018/03/13/announcing-project-honolulu-technical-preview-1803-and-rsat-insider-preview-for-windows-10) では、Azure AD アクセス制御、詳細なログ記録、サイズ変更できるコンテンツのサポートが追加され、多数のツールの機能が強化されました。
- バージョン [1802](https://blogs.windows.com/windowsexperience/2018/02/13/announcing-windows-server-insider-preview-build-17093-project-honolulu-technical-preview-1802) では、アクセシビリティ、ローカライズ、高可用性展開、タグ付け、Hyper-V ホストの設定、ゲートウェイ認証のサポートが追加されました。
- バージョン [1712](https://blogs.windows.com/windowsexperience/2017/12/19/announcing-project-honolulu-technical-preview-1712-build-05002) では、仮想マシンの機能がさらに追加され、ツール全体のパフォーマンスが向上しました。
- バージョン [1711](https://cloudblogs.microsoft.com/windowsserver/2017/12/01/1711-update-to-project-honolulu-technical-preview-is-now-available/) では、要望が多かったツール (リモート デスクトップと PowerShell) が追加され、その他の機能が強化されました。
- バージョン [1709](https://cloudblogs.microsoft.com/windowsserver/2017/09/22/project-honolulu-technical-preview-is-now-available-for-download/) は、最初のパブリック プレビュー リリースとして発売されました。

## <a name="stay-updated"></a>最新情報に更新

![ ](//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOolR)[Twitter でフォローします。](https://twitter.com/servermgmt)

![ ](//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOtyw)[このブログを読む](https://blogs.technet.microsoft.com/servermanagement/)
