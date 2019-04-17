---
title: Windows Admin Center についてよく寄せられる質問
description: Windows Admin Center (Project Honolulu) に関する回答を得る
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.date: 04/12/2019
ms.prod: windows-server-threshold
ms.openlocfilehash: 2f1591a32147e3c11ba635f1a11d36b7f38a3470
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296744"
---
# Windows Admin Center についてよく寄せられる質問

>適用対象: Windows Admin Center、Windows Admin Center Preview

ここでは、Windows Admin Center についてよく寄せられる質問に対する回答を示します。

## Windows Admin Center とは何ですか。

Windows Admin Center は、IT 管理者が Windows Server および Windows 10 を管理するための軽量のブラウザー ベースの GUI プラットフォームおよびツールセットです。 サーバー マネージャーおよび Microsoft 管理コンソール (MMC) などの使い慣れたインボックスの管理ツールが、最先端で簡素化および統合された安全なエクスペリエンスに進化したものです。

## 運用環境で Windows Admin Center を使用できますか。

はい、できます。 Windows Admin Center は一般公開されており、広範な使用法および運用環境の展開で利用可能です。 現在のプラットフォーム機能と主要なツールは、Microsoft の標準リリースの基準と使いやすさ、信頼性、パフォーマンス、アクセシビリティ、セキュリティ、および導入、品質基準を満たします。

[!INCLUDE [support-policy](../includes/support-policy.md)]

## Windows Admin Center を使用するにはいくらかかりますか。

Windows Admin Center には、Windows 以外の追加コストはありません。 Windows Admin Center (別のダウンロードとして利用可能) は、Windows Supplemental EULA に基づいて使用許諾されているため、Windows Server または Windows 10 の有効なライセンスと共に追加コストなしで使用することができます。

## Windows Admin Center で管理できるのはどのバージョンの Windows Server ですか。

Windows Admin Center は、Windows Server 2019 リリースで主なテーマを有効にする Windows Server 2019 用に最適化されています。 特に、ハイブリッド クラウドのシナリオとハイパーコンバージド インフラストラクチャの管理します。 お客様が既に使用しているバージョンのさまざまな管理をサポートしている Windows Admin Center は、Windows Server 2019 で最適に機能は、: Windows Server 2012 およびそれ以降は、完全にサポートされます。 Windows Server 2008 R2 を管理するための制限された機能もあります。

## Windows Admin Center は、すべての従来のインボックス ツールや RSAT ツールに完全に置き換わるものですか。

いいえ。 Windows Admin Center は多くの一般的なシナリオを管理できますが、従来のすべての Microsoft 管理コンソール (MMC) ツールに完全に置き換わるものではありません。 Windows Admin Center に含まれるどのようなツールについての詳細を参照詳しくは、ドキュメントで[サーバーを管理する](..\use\manage-servers.md)についてします。 Windows Admin Center は、サーバー マネージャー ソリューションに次の主要な機能を備えています。

* リソースとリソース使用率の表示
* 証明書の管理
* デバイスの管理
* イベント ビューアー
* エクスプローラー
* ファイアウォール管理
* アプリをインストールして管理します。
* ローカル ユーザーとグループの構成
* ネットワーク設定
* プロセスの表示/終了および Process Dump の作成
* レジストリの編集
* スケジュールされたタスクを管理します。
* Windows サービスの管理
* 役割と機能の有効化/無効化
* Hyper-V VM と仮想スイッチの管理
* 記憶域の管理
* 記憶域レプリカの管理
* Windows Updates の管理
* PowerShell コンソール
* リモート デスクトップ接続

Windows Admin Center では、次のソリューションも提供します。

* コンピューターの管理 – Windows 10 クライアント PC を管理するためのサーバー マネージャー機能のサブセットを提供します。
* フェールオーバー クラスター マネージャー – フェールオーバー クラスターおよびクラスター リソースの継続的な管理のためのサポートを提供します。
* ハイパーコンバージド クラスター マネージャー – 記憶域スペース ダイレクトおよび Hyper-V に合わせてカスタマイズされたまったく新しいエクスペリエンスを提供します。 ダッシュ ボードを備えており、監視のためのグラフとアラートが強調されます。

Active Directory、DHCP、DNS、IIS などの役割には、Windows Admin Center に表示される同等の管理機能がまだないため、Windows Admin Center はリモート サーバー管理ツール (RSAT) に代わるものではなく、補完するものです。

## 無料の Microsoft Hyper-V Server を管理するために Windows Admin Center を使用することはできますか。

はい、できます。 Windows Admin Center を使用して、Microsoft Hyper-V Server 2016 および Microsoft Hyper-V Server 2012 R2 を管理することができます。

## Windows 10 のコンピューターで Windows Admin Center を展開することができますか。

はい、Windows Admin Center はデスクトップ モードで実行される Windows 10 (バージョン 1709 以降) にインストールできます。  Windows Admin Center は、以上ゲートウェイ モードで Windows Server 2016 でのサーバーにインストールされていることもでき、Windows 10 コンピューターから web ブラウザーでアクセスします。 [インストール オプションの詳細については、こちらを参照してください](..\plan\installation-options.md)。

## Windows Admin Center は、内部的な PowerShell を使用して、使われる実際のスクリプトを参照できることを受けていますか。

うん！ [Showscript 機能](..\use\get-started.md#view-powershell-scripts-used-in-windows-admin-center)では、Windows Admin Center Preview 1806 に追加されており、GA チャネルに含まれているようになりました。

## Windows Admin Center が Windows Server 2008 R2 以前を管理できるようになる予定はありますか。

Windows Admin Center は、Windows Server 2008 R2 を管理するための**制限付き**機能をサポートしています。 Windows Admin Center は、Windows Server 2008 R2 以前には存在しない PowerShell 機能やプラットフォーム テクノロジを利用しているため、完全なサポートは実現不可能です。 Windows Server 2008/2008 R2 は終了が近づいて 2020 年 1 月でのサポートのため、お客様をお勧めします。 [Azure に移行するか、Windows Server の最新バージョンにアップグレード](https://www.microsoft.com/en-us/cloud-platform/windows-server-2008)します。

## Windows Admin Center が Linux 接続を管理できるようになる予定はありますか。

顧客の需要が原因を調査して、現在提供、ロックされた予定はありませんが SSH 経由のコンソール接続のみのサポートをで構成されます。

## Windows Admin Center でサポートされているのはどの Web ブラウザーですか。

最新バージョンの Microsoft Edge (Windows 10 バージョン 1709 以降) および Google Chrome のブラウザーが Windows 10 でテストおよびサポートされています。 [ビュー ブラウザー特定既知の問題](..\support\known-issues.md#browser-specific-issues)です。 その他の最新の web ブラウザーやその他のプラットフォーム現在、当社のテスト マトリックスの一部ではないを*公式に*サポートされています。

## Windows Admin Center ではセキュリティをどのように処理していますか。

ブラウザーから Windows Admin Center ゲートウェイへのトラフィックは、HTTPS を使用します。 ゲートウェイから管理対象サーバーへのトラフィックは標準の PowerShell および WMI over WinRM です。 Microsoft は、LAPS (Local Administrator Password Solution)、リソース ベースの制約付き委任、AD または Azure AD を使用したゲートウェイ アクセス制御、および対象サーバーを管理するための役割ベースのアクセス制御をサポートしています。

## Windows Admin Center は、CredSSP を使用しますか。

はい、場合によっては Windows Admin Center には、CredSSP が必要があります。 これがターゲットとしている特定のサーバーを超える管理のためのコンピューターに認証資格情報を渡す必要です。 たとえば、**サーバー B**、上の仮想マシンを管理している**サーバー C**でホストされているファイル共有にこれらの仮想マシンの vhdx ファイルを保存する場合は、Windows Admin Center する必要があります CredSSP の認証に使用**サーバー C**にアクセスすると、ファイルを共有します。

Windows Admin Center は、ユーザーから同意を求める後に自動的に CredSSP の構成を処理します。 CredSSP を構成するには、前に、Windows Admin Center は、システムに最新の CredSSP[の更新プログラム](https://support.microsoft.com/help/4093492/credssp-updates-for-cve-2018-0886-march-13-2018)があることを確認することを確認されます。 CredSSP が有効なときがあります、サーバーの概要と、それを無効にするためのオプションでバッジ

![CredSSP では、サーバーの概要](../media/CredSSP-overview.png)

Credssp では、次の領域で使用されています。

- 仮想マシン ツール (上記の例です。) での SMB の記憶域を使用して集約型
- 更新プログラムを使用するツール フェールオーバーまたはハイパーコンバージド クラスターのいずれかで、管理ソリューション[クラスター対応更新](https://docs.microsoft.com/windows-server/failover-clustering/cluster-aware-updating)を実行します。 

## クラウド依存関係はありますか。

Windows Admin Center では、インターネット アクセスと Microsoft Azure は必要ありません。 Windows Admin Center は、物理システム、任意のハイパーバイザー上、または任意のクラウドで実行される仮想マシンなど、任意の場所で Windows Server および Windows のインスタンスを管理します。 さまざまな Azure サービスとの統合が徐々に追加されていく予定ですが、これらはオプションの付加価値機能であり、Windows Admin Center を使用するための要件ではありません。

## その他の依存関係や前提条件はありますか。

Windows Admin Center は、Windows 10 Fall Anniversary Update (1709) 以降、または Windows Server 2016 以降にインストールできます。 Windows Server 2008 R2、2012、または 2012 R2 を管理するには、これらのサーバーに Windows Management Framework 5.1 をインストールすることが必要です。 その他の依存関係はありません。 IIS、エージェント、SQL Server は必要ありません。

## 機能拡張およびサード パーティのサポートはどうなりますか。

Windows Admin Center は、独自の拡張機能をだれでも作成できるように、利用可能な SDK はします。 プラットフォームとして、エコシステムを拡大し、パートナーの拡張性を有効にすることは、当初から最優先でした。 [Windows Admin Center SDK の詳細については、こちらを参照してください](..\extend\extensibility-overview.md)。

## Windows Admin Center でハイパーコンバージド インフラストラクチャを管理することができますか。

はい、できます。 Windows Admin Center は、Windows Server 2016 または Windows Server 2019 を実行しているハイパーコンバージド クラスターの管理をサポートしています。 Windows Admin Center でハイパーコンバージド クラスター マネージャー ソリューションがプレビューであった以前ができるようになりました**一般公開**プレビューでいくつかの新機能ができます。 詳細については、[ハイパーコンバージド インフラストラクチャの管理について確認してください](..\use\manage-hyper-converged.md)。

## Windows Admin Center に System Center は必要ですか。

いいえ。 Windows Admin Center は、System Center を補完するものですが、System Center は必要ありません。 [Windows Admin Center と System Center について確認してください](related-management.md#system-center)。

## Windows Admin Center で System Center Virtual Machine Manager (SCVMM) を置き換えることができますか。

Windows Admin Center と SCVMM は互いを補完する関係にあります。Windows Admin Center は従来の Microsoft 管理コンソール (MMC) スナップインとサーバー管理者のエクスペリエンスを置き換えることを目的としています。  Windows Admin Center は、SCVMM の監視の側面を置き換えることを目的としていません。 [Windows Admin Center と System Center について確認してください](related-management.md#system-center)。

## Windows Admin Center Preview とは何ですか。どちらのバージョンが適しているでしょうか。

次の 2 つのバージョンの Windows Admin Center をダウンロードできます。

### Windows Admin Center

* 頻繁に更新できないか、または実稼働環境で使用するリリースの検証時間がさらに必要な IT 管理者には、このバージョンが適しています。 現在の一般公開 (GA) リリースでは、Windows Admin Center 1904 です。
* [!INCLUDE [support-policy](../includes/support-policy.md)]
* 最新のリリースでは、[こちらでダウンロード](https://aka.ms/WACDownload)を取得します。

### Windows Admin Center Preview

>[!NOTE]
>現在の GA バージョン (Windows Admin Center 1904) には、以前のすべてのプレビュー機能が含まれています。
>数か月後に、Insider Preview が返されます。

* 一定間隔で最新かつ最大の機能を必要とする IT 管理者には、このバージョンが最適です。 当社の目的は、毎月のリリース後の更新を提供するか。 コア プラットフォームは引き続き実稼働レベルであり、ライセンスにより製品の使用権が提供されます。 ただし、明確に PREVIEW としてマークされた新しいツールや機能が導入されており、評価やテストに適しています。
* Insider Preview の最新リリースを取得するのに登録されている insider の皆様は、 [Windows Server の Insider Preview のダウンロード ページ](https://www.microsoft.com/en-us/software-download/windowsinsiderpreviewserver)、[その他のダウンロード ドロップダウンから直接 Windows Admin Center Preview をダウンロードできます。 まだ Insider として登録していない場合は、Windows Insiders for Business ポータルの [Windows Server の概要](https://insider.windows.com/en-us/for-business-getting-started-server/)に関するページを参照してください。

## "Project Honolulu" の最終的な名前として "Windows Admin Center" が選択されたのはなぜですか。

Windows Admin Center は、"Project Honolulu" の正式な製品名で、当社のビジョンである、幅広い主要な管理シナリオでの IT 管理者の統合エクスペリエンスを強化しています。 また、主に当社でどのように投資し、何を提供するかについて、IT 管理ユーザーのニーズに対する顧客の焦点が強調されています。

## Windows Admin Center の詳細、または上のトピックの詳細をどこで確認できますか。

Microsoft の[起動画面](https://aka.ms/WindowsAdminCenter)は出発点として最適であり、新たに分類されたドキュメント コンテンツ、ダウンロード場所、フィードバックの提供方法、リファレンス情報、その他のリソースへのリンクがあります。

## Windows Admin Center のバージョン履歴とは何ですか。

[次に、バージョン履歴を表示します。](..\overview.md#release-history)

## Windows Admin Center で問題が発生していますが、どこでサポート情報を入手できますか。

[トラブルシューティング ガイド](..\use\troubleshooting.md)および[既知の問題](..\use\known-issues.md)の一覧を参照してください。
