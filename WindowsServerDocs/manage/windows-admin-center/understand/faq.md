---
title: Windows Admin Center についてよく寄せられる質問
description: Windows Admin Center (Project Honolulu) に関する回答を得る
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.date: 06/07/2019
ms.prod: windows-server-threshold
ms.openlocfilehash: 5c306dd181d4db400e6ab5bab919399fdebca9f3
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811668"
---
# <a name="windows-admin-center-frequently-asked-questions"></a>Windows Admin Center についてよく寄せられる質問

> 適用対象:Windows Admin Center、Windows Admin Center プレビュー

ここでは、Windows Admin Center についてよく寄せられる質問に対する回答を示します。

## <a name="what-is-windows-admin-center"></a>Windows Admin Center とは

Windows Admin Center は、IT 管理者が Windows Server および Windows 10 を管理するための軽量のブラウザー ベースの GUI プラットフォームおよびツールセットです。 サーバー マネージャーおよび Microsoft 管理コンソール (MMC) などの使い慣れたインボックスの管理ツールが、最先端で簡素化および統合された安全なエクスペリエンスに進化したものです。

## <a name="can-i-use-windows-admin-center-in-production-environments"></a>運用環境で Windows Admin Center を使用できますか。

[はい]。 Windows Admin Center は一般公開されており、広範な使用法および運用環境の展開で利用可能です。 現在のプラットフォーム機能と core ツールは、Microsoft の標準的なリリース条件と使いやすさ、信頼性、パフォーマンス、アクセシビリティ、セキュリティ、および導入の品質基準を満たしています。

[!INCLUDE [support-policy](../includes/support-policy.md)]

## <a name="how-much-does-it-cost-to-use-windows-admin-center"></a>Windows Admin Center を使用するにはいくらかかりますか。

Windows Admin Center には、Windows 以外の追加コストはありません。 Windows Admin Center (別のダウンロードとして利用可能) は、Windows Supplemental EULA に基づいて使用許諾されているため、Windows Server または Windows 10 の有効なライセンスと共に追加コストなしで使用することができます。

## <a name="what-versions-of-windows-server-can-i-manage-with-windows-admin-center"></a>Windows Admin Center で管理できるのはどのバージョンの Windows Server ですか。

Windows Server 2019 のリリースでの主要なテーマを有効にする Windows Server 2019 Windows Admin Center は最適化されています: ハイブリッド クラウド シナリオとハイパー コンバージド インフラストラクチャの管理に特にです。 Windows Admin Center には Windows Server 2019 最適使用、さまざまな顧客が既に使用しているバージョンの管理をサポートします。Windows Server 2012 以降は完全にサポートします。 Windows Server 2008 R2 を管理するための限られた機能もあります。

## <a name="is-windows-admin-center-a-complete-replacement-for-all-traditional-in-box-and-rsat-tools"></a>Windows Admin Center は、すべての従来のインボックス ツールや RSAT ツールに完全に置き換わるものですか。

No. Windows Admin Center は多くの一般的なシナリオを管理できますが、従来のすべての Microsoft 管理コンソール (MMC) ツールに完全に置き換わるものではありません。 どのようなツールは Windows Admin Center では、付属について詳しく説明では、詳細をご覧くださいの[サーバーを管理する](../use/manage-servers.md)ドキュメント。 Windows Admin Center は、サーバー マネージャー ソリューションに次の主要な機能を備えています。

* リソースとリソース使用率の表示
* 証明書の管理
* デバイスの管理
* イベント ビューアー
* エクスプローラー
* ファイアウォール管理
* インストールされているアプリを管理します。
* ローカル ユーザーとグループの構成
* ネットワーク設定
* プロセスの表示/終了および Process Dump の作成
* レジストリの編集
* スケジュールされたタスクを管理します。
* Windows サービスの管理
* 役割と機能の有効化/無効化
* Hyper-V VM と仮想スイッチの管理
* 記憶域の管理
* 記憶域レプリカを管理します。
* Windows Updates の管理
* PowerShell コンソール
* リモート デスクトップ接続

Windows Admin Center では、次のソリューションも提供します。

* コンピューターの管理 – Windows 10 クライアント PC を管理するためのサーバー マネージャー機能のサブセットを提供します。
* フェールオーバー クラスター マネージャー – フェールオーバー クラスターおよびクラスター リソースの継続的な管理のためのサポートを提供します。
* ハイパーコンバージド クラスター マネージャー – 記憶域スペース ダイレクトおよび Hyper-V に合わせてカスタマイズされたまったく新しいエクスペリエンスを提供します。 ダッシュ ボードを備えており、監視のためのグラフとアラートが強調されます。

Active Directory、DHCP、DNS、IIS などの役割には、Windows Admin Center に表示される同等の管理機能がまだないため、Windows Admin Center はリモート サーバー管理ツール (RSAT) に代わるものではなく、補完するものです。

## <a name="can-windows-admin-center-be-used-to-manage-the-free-microsoft-hyper-v-server"></a>無料の Microsoft Hyper-V Server を管理するために Windows Admin Center を使用することはできますか。

[はい]。 Windows Admin Center を使用して、Microsoft Hyper-V Server 2016 および Microsoft Hyper-V Server 2012 R2 を管理することができます。

## <a name="can-i-deploy-windows-admin-center-on-a-windows-10-computer"></a>Windows 10 のコンピューターで Windows Admin Center を展開することができますか。

はい、Windows Admin Center はデスクトップ モードで実行される Windows 10 (バージョン 1709 以降) にインストールできます。  Windows Admin Center では、ゲートウェイ モードで Windows Server 2016 でサーバーにインストールされている以上にすることもでき、Windows 10 コンピューターからの web ブラウザー経由でアクセスします。 [インストール オプションの詳細については、こちらを参照してください](../plan/installation-options.md)。

## <a name="ive-heard-that-windows-admin-center-uses-powershell-under-the-hood-can-i-see-the-actual-scripts-that-it-uses"></a>耳にして、Windows Admin Center は PowerShell を使用して内部的を使用して実際のスクリプトを表示できますか。

うん！ [Showscript 機能](../use/get-started.md#view-powershell-scripts-used-in-windows-admin-center)Windows Admin Center プレビュー 1806 で追加されており、GA のチャネルに追加されました。

## <a name="are-there-any-plans-for-windows-admin-center-to-manage-windows-server-2008-r2-or-earlier"></a>Windows Admin Center が Windows Server 2008 R2 以前を管理できるようになる予定はありますか。

Windows Admin Center のようになりました**限定**Windows Server 2008 R2 を管理する機能。 Windows Admin Center は、Windows Server 2008 R2 以前には存在しない PowerShell 機能やプラットフォーム テクノロジを利用しているため、完全なサポートは実現不可能です。 Windows Server 2008/2008 R2 は、お客様が Microsoft にお勧めしますので、年 2020年 1 月にサポートが終了が近づいて[Azure または Windows Server の最新バージョンにアップグレードする移動](https://www.microsoft.com/en-us/cloud-platform/windows-server-2008)します。

## <a name="are-there-any-plans-for-windows-admin-center-to-manage-linux-connections"></a>Windows Admin Center が Linux 接続を管理できるようになる予定はありますか。

顧客の需要、原因を調査して現在ロックされているプランを配信するはありませんが、SSH 経由でのみ、コンソール接続のサポートをで構成されます。

## <a name="which-web-browsers-are-supported-by-windows-admin-center"></a>Windows Admin Center でサポートされているのはどの Web ブラウザーですか。

最新バージョンの Microsoft Edge (Windows 10 バージョン 1709 以降) および Google Chrome のブラウザーが Windows 10 でテストおよびサポートされています。 [ビュー ブラウザー固有の既知の問題](../support/known-issues.md#browser-specific-issues)します。 その他の最新の web ブラウザーやその他のプラットフォームは、現在、テストのマトリックスの一部ではないとできないためです*正式に*サポートされています。

## <a name="how-does-windows-admin-center-handle-security"></a>Windows Admin Center ではセキュリティをどのように処理していますか。

ブラウザーから Windows Admin Center ゲートウェイへのトラフィックは、HTTPS を使用します。 ゲートウェイから管理対象サーバーへのトラフィックは標準の PowerShell および WMI over WinRM です。 Microsoft は、LAPS (Local Administrator Password Solution)、リソース ベースの制約付き委任、AD または Azure AD を使用したゲートウェイ アクセス制御、および対象サーバーを管理するための役割ベースのアクセス制御をサポートしています。

## <a name="does-windows-admin-center-use-credssp"></a>Windows Admin Center は、CredSSP を使用しますか。

はい、Windows Admin Center いくつかのケースで CredSSP が必要です。 これは、管理のための特定の対象としているサーバー以外のマシンに認証用の資格情報を渡す必要です。 たとえば、上の仮想マシンを管理している場合**サーバー B**、によってホストされているファイル共有にこれらの仮想マシンの vhdx ファイルを保存したい**サーバー C**、Windows Admin Center に CredSSP を使用する必要があります認証**サーバー C**ファイル共有にアクセスします。

Windows Admin Center では、同意を確認した後に自動的に CredSSP の構成を処理します。 CredSSP を構成する前に Windows Admin Center は、システムが最近の CredSSP を持っているかどうかを確認する確認[更新](https://support.microsoft.com/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018)します。 サーバーの概要と、それを無効にするオプションでバッジがあります、CredSSP が有効になっています。

![CredSSP をサーバーの概要](../media/CredSSP-overview.png)

CredSSP は、次の領域で使用されています。

- 仮想マシンのツール (上記の例です。) での SMB 記憶域を使用して細分類
- 更新プログラムを使用してツール フェールオーバーまたはハイパーコンバージド クラスター管理ソリューションを実行する[クラスター対応更新](https://docs.microsoft.com/windows-server/failover-clustering/cluster-aware-updating) 

## <a name="are-there-any-cloud-dependencies"></a>クラウド依存関係はありますか。

Windows Admin Center では、インターネット アクセスと Microsoft Azure は必要ありません。 Windows Admin Center は、物理システム、任意のハイパーバイザー上、または任意のクラウドで実行される仮想マシンなど、任意の場所で Windows Server および Windows のインスタンスを管理します。 さまざまな Azure サービスとの統合が徐々に追加されていく予定ですが、これらはオプションの付加価値機能であり、Windows Admin Center を使用するための要件ではありません。

## <a name="are-there-any-other-dependencies-or-prerequisites"></a>その他の依存関係や前提条件はありますか。

Windows Admin Center は、Windows 10 Fall Anniversary Update (1709) 以降、または Windows Server 2016 以降にインストールできます。 Windows Server 2008 R2、2012、または 2012 R2 を管理するには、これらのサーバーに Windows Management Framework 5.1 をインストールすることが必要です。 その他の依存関係はありません。 IIS、エージェント、SQL Server は必要ありません。

## <a name="what-about-extensibility-and-3rd-party-support"></a>機能拡張およびサード パーティのサポートはどうなりますか。

Windows Admin Center では、使用可能な SDK を持っているすべてのユーザーが独自の拡張機能を書き込めるようにします。 プラットフォームとして、エコシステムを拡大し、パートナーの拡張性を有効にすることは、当初から最優先でした。 [Windows Admin Center SDK の詳細については、こちらを参照してください](../extend/extensibility-overview.md)。

## <a name="can-i-manage-hyper-converged-infrastructure-with-windows-admin-center"></a>Windows Admin Center でハイパーコンバージド インフラストラクチャを管理することができますか。

[はい]。 Windows Admin Center では、Windows Server 2016 または Windows Server 2019 を実行するハイパー コンバージド クラスターの管理をサポートします。 Windows Admin Center でのハイパー コンバージド クラスター マネージャー ソリューションは以前のプレビューでしたが、ここでは、**一般**、いくつかの新しいプレビュー機能とします。 詳細については、[ハイパーコンバージド インフラストラクチャの管理について確認してください](../use/manage-hyper-converged.md)。

## <a name="does-windows-admin-center-require-system-center"></a>Windows Admin Center に System Center は必要ですか。

No. Windows Admin Center は、System Center を補完するものですが、System Center は必要ありません。 [Windows Admin Center および System Center について読む](related-management.md#system-center)します。

## <a name="can-windows-admin-center-replace-system-center-virtual-machine-manager-scvmm"></a>Windows Admin Center で System Center Virtual Machine Manager (SCVMM) を置き換えることができますか。

Windows Admin Center と SCVMM は互いを補完する関係にあります。Windows Admin Center は従来の Microsoft 管理コンソール (MMC) スナップインとサーバー管理者のエクスペリエンスを置き換えることを目的としています。  Windows Admin Center は、SCVMM の監視の側面を置き換えることを目的としていません。 [Windows Admin Center および System Center について読む](related-management.md#system-center)します。

## <a name="what-is-windows-admin-center-preview-which-version-is-right-for-me"></a>Windows Admin Center Preview とは何ですか。どちらのバージョンが適しているでしょうか。

次の 2 つのバージョンの Windows Admin Center をダウンロードできます。

### <a name="windows-admin-center"></a>Windows Admin Center

* 頻繁に更新できないか、または実稼働環境で使用するリリースの検証時間がさらに必要な IT 管理者には、このバージョンが適しています。 現在、一般 (公開 GA) リリースでは、Windows Admin Center 1904 です。
* [!INCLUDE [support-policy](../includes/support-policy.md)]
* 最新のリリースを取得する[ここからダウンロード](https://aka.ms/WACDownload)します。

### <a name="windows-admin-center-preview"></a>Windows Admin Center Preview

> [!NOTE]
> 現在の GA バージョン (Windows Admin Center 1904) には、すべての以前のプレビュー機能が含まれています。
> Insider Preview は、今後数か月で返します。

* 一定間隔で最新かつ最大の機能を必要とする IT 管理者には、このバージョンが最適です。 自分の意図は、毎月のリリース以降の更新を提供することです。 そのため、または。 コア プラットフォームは引き続き実稼働レベルであり、ライセンスにより製品の使用権が提供されます。 ただし、明確に PREVIEW としてマークされた新しいツールや機能が導入されており、評価やテストに適しています。
* 最新の Insider Preview リリースを取得するには、登録されている内部関係者から直接 Windows Admin Center プレビューをダウンロードして可能性があります、 [Windows Server Insider プレビューのダウンロード ページ](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver)、その他のダウンロードのドロップダウン リスト。 まだ Insider として登録していない場合は、Windows Insiders for Business ポータルの [Windows Server の概要](https://insider.windows.com/en-us/for-business-getting-started-server/)に関するページを参照してください。

## <a name="why-was-windows-admin-center-chosen-as-the-final-name-for-project-honolulu"></a>"Project Honolulu" の最終的な名前として "Windows Admin Center" が選択されたのはなぜですか。

Windows Admin Center は、"Project Honolulu" の正式な製品名で、当社のビジョンである、幅広い主要な管理シナリオでの IT 管理者の統合エクスペリエンスを強化しています。 また、主に当社でどのように投資し、何を提供するかについて、IT 管理ユーザーのニーズに対する顧客の焦点が強調されています。

## <a name="where-can-i-learn-more-about-windows-admin-center-or-get-more-details-on-the-topics-above"></a>Windows Admin Center の詳細、または上のトピックの詳細をどこで確認できますか。

Microsoft の[起動画面](https://aka.ms/WindowsAdminCenter)は出発点として最適であり、新たに分類されたドキュメント コンテンツ、ダウンロード場所、フィードバックの提供方法、リファレンス情報、その他のリソースへのリンクがあります。

## <a name="what-is-the-version-history-of-windows-admin-center"></a>Windows Admin Center のバージョン履歴とは何ですか。

[ここで、バージョン履歴を表示します。](../overview.md#release-history)

## <a name="im-having-an-issue-with-windows-admin-center-where-can-i-get-help"></a>Windows Admin Center で問題が発生していますが、どこでサポート情報を入手できますか。

[トラブルシューティング ガイド](../use/troubleshooting.md)および[既知の問題](../use/known-issues.md)の一覧を参照してください。
