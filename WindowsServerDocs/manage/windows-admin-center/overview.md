---
title: Windows Admin Center の概要
description: Windows Admin Center (Project Honolulu) を使って Windows Server を管理する方法の詳細
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 01/07/2020
ms.localizationpriority: high
ms.prod: windows-server
ms.openlocfilehash: 7b3a75258086a73fbd618c2e8221454d7e616556
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/14/2020
ms.locfileid: "75949979"
---
# <a name="windows-admin-center"></a>Windows Admin Center

> 適用先:Windows Admin Center、Windows Admin Center Preview

Windows Admin Center は、Windows サーバー、クラスター、ハイパーコンバージド インフラストラクチャ、Windows 10 PC を管理するための、ローカルに展開されるブラウザー ベースのアプリです。 Windows 以外の追加費用は必要なく、運用環境で使用できます。

新機能については、[リリース履歴](support/release-history.md)を参照してください。

## <a name="download-now"></a>今すぐダウンロード

**Microsoft Evaluation Center から、[Windows Admin Center](https://www.microsoft.com/evalcenter/evaluate-windows-admin-center)** をダウンロードできます。 "評価を開始する" と記載されていますが、これは、Windows または Windows Server のライセンスの一部として含まれる、運用環境での使用のために一般公開されているバージョンです。

インストールの詳細については、[インストール](deploy/install.md)に関する記事を参照してください。 Windows Admin Center の概要に関するヒントは、[概要](use/get-started.md)に関する記事を参照してください。

Windows Admin Center の非プレビュー バージョンの更新は、Microsoft Update を使用して行うことも、手動で Windows Admin Center をダウンロード、インストールして行うこともできます。 Windows Admin Center の各非プレビュー バージョンは、次への非プレビュー バージョンがリリースされてから 30 日が経過するまでサポートされます。 詳細については、Microsoft の[サポート ポリシー](support/index.md)に関するページをご覧ください。

## <a name="windows-admin-center-scenarios"></a>Windows Admin Center のシナリオ

Windows 管理センターを使用して、次のことを行うことができます。

|     |     |
| --- | --- |
| ![](media/simple-icon.png)| **サーバー管理の簡素化** <br/> サーバー マネージャーなどの使い慣れたツールの最新バージョンを使用して、サーバーとクラスターを管理できます。 5 分以内にインストールして、環境内ですぐにサーバーを管理できます。ターゲット構成は必要ありません。 詳細については、「[Windows Admin Center とは](understand/what-is.md)」を参照してください。 |
| ![](media/future-icon.png)| **ハイブリッド ソリューションとの連携** <br/> Azure との統合により、必要に応じてオンプレミスのサーバーを関連するクラウド サービスに接続することができます。 詳細については、[Azure ハイブリッドサービス](azure/index.md)に関する記事を参照してください |
| ![](media/secure-icon.png)| **ハイパーコンバージド管理の効率化** <br/> Azure Stack HCI または Windows Server のハイパーコンバージド クラスターの管理が効率化します。 簡略化されたワークロードを使用して、VM、記憶域スペース ダイレクトのボリューム、ソフトウェア定義のネットワークなどを作成して管理することができます。 詳細については、「[Manage Hyper-Converged Infrastructure with Windows Admin Center](use/manage-hyper-converged.md)」(Windows Admin Center を使用したハイパーコンバージド インフラストラクチャの管理) を参照してください|

次に、概要を説明するビデオと、詳細を説明するポスターを示します。
>[!VIDEO https://www.youtube.com/embed/WCWxAp27ERk]

[![Windows Admin Center のポスター](media/WAC1910Poster_thumb_small.PNG)](media/WAC1910Poster_thumb.png)

[PDF をダウンロード](https://github.com/MicrosoftDocs/windowsserverdocs/raw/master/WindowsServerDocs/manage/windows-admin-center/media/WindowsAdminCenter1910Poster.pdf)


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
            <li><a href="configure/use-powershell.md">PowerShell を使用した自動化</a>
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
            <li><a href="support/release-history.md">リリース履歴</a>
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

## <a name="video-based-learning"></a>ビデオを使った学習

Microsoft Ignite 2019 セッションのビデオを次に示します。

- [Windows Admin Center: Azure ハイブリッドの価値を最大限に活用する](https://aka.ms/WAC-BRK3165)
- [Windows Admin Center: 新機能と今後の予定](https://aka.ms/WAC-BRK2048)
- [Windows Admin Center を使用して Azure からオンプレミスのサーバーを自動的に監視、セキュリティ保護、更新する](https://aka.ms/WAC-THR2146)
- [Windows Admin Center のサードパーティの拡張機能を使用して効率化する](https://aka.ms/WAC-THR2140)
- [Windows Admin Center のエキスパートになろう: 展開、構成、セキュリティのベスト プラクティス](https://aka.ms/WAC-THR2135)
- [Windows Admin Center: System Center と Microsoft Azure をさらに連携させる](https://aka.ms/WAC-THR2176)
- [Microsoft Azure ハイブリッド サービスを Windows Admin Center や Windows Server と連携させる方法](https://aka.ms/WAC-THR2073)
- [ライブ Q & A: Windows Admin Center を使用してハイブリッド サーバー環境を管理する](https://aka.ms/WAC-MLS1055)
- [ラーニング パス: ハイブリッド管理テクノロジ](https://aka.ms/WAC-HybridMgmtTech)
- [ハンズオン ラボ: Windows Admin Center とハイブリッド](https://aka.ms/WAC-HOL2019)

Windows Server サミット 2019 セッションのビデオを次に示します。

- [Windows Admin Center でのハイブリッド](https://aka.ms/WAC-WSS2019-GoHybridWAC)
- [Windows Admin Center v1904 の新機能](https://aka.ms/WAC-WSS2019-WhatsNewv1904)

さらに、いくつかのリソースを次に示します。

- [新たに想像された Windows Admin Center サーバー管理](https://aka.ms/WAC-ServerMgmtReimagined)
- [Windows Admin Center を使用してサーバーと仮想マシンをどこからでも管理する](https://aka.ms/WAC-Webinar2019)
- [Windows Admin Center の使用を開始する方法](https://www.youtube.com/embed/PcQj6ZklmK0)

## <a name="see-how-customers-are-benefitting-from-windows-admin-center"></a>Windows Admin Center の活用事例

|     |
| --- |
| "[Windows Admin Center] によって、管理システムの管理における弊社の時間と作業が 75% 以上削減されました。"<br> *- Convergent Computing 社、社長、Rand Morimoto 氏* |
| "[Windows Admin Center] のおかげで、Azure Active Directory との完全な統合により問題なく HTML5 ポータルからリモートでお客様を管理することができます。また、多要素認証を利用することで、セキュリティを向上することができます。"<br/> *- Inside Technologies 社、創設者兼シニア コンサルタント、Silvio Di Benedetto 氏* |
| “弊社では、より効果的な方法で [Server Core] SKU を展開し、リソースの効率、セキュリティ、および自動化を向上しながら、ある程度の生産性を実現し、スクリプトのみに依存する場合に発生する可能性のあるエラーを削減しています。” <br/> *- VaiSulWeb 社、創設者兼 CEO、Guglielmo Mengora 氏* |
| “[Windows Admin Center] により、特に SMB 市場のお客様は社内のインフラストラクチャを管理するための使いやすいツールを手にしました。 これにより、管理作業が最小限に抑えられ、多くの時間が節減されます。 そして、一番いいのは、[Windows Admin Center] には追加ライセンス料がないことです。” <br/> *- SecureGUARD 社、常務取締役、Helmut Otto 氏* |

[運用環境で Windows Admin Center を使用している会社の詳細を確認してください。](understand/case-studies.md)

## <a name="related-products"></a>関連製品

Windows Admin Center は、1 つのサーバーまたはクラスターの管理用に設計されています。 これにより、リモート サーバー管理ツール (RSAT)、System Center、Intune、または Azure Stack のような、既存の Microsoft の監視および管理ソリューションが補完されますが、置き換わるものではありません。

[Windows Admin Center で他の Microsoft 管理ソリューションを補完する方法について確認してください。](understand/related-management.md)

## <a name="stay-updated"></a>更新情報

![](//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOolR)[Twitter で Microsoft をフォローする](https://twitter.com/servermgmt)

![](//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOtyw)[こちらのブログを読む](https://blogs.technet.microsoft.com/servermanagement/)
