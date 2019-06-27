---
title: Windows Admin Center の拡張機能
description: Windows Admin Center SDK の拡張機能 (Project Honolulu)
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 09/17/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: beb2b3d1eefc5d70e39baa461708938ac9c17be5
ms.sourcegitcommit: 3be280c8638214857dc355b201eb56a04499a5e5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2019
ms.locfileid: "67396680"
---
# <a name="extensions-for-windows-admin-center"></a>Windows Admin Center の拡張機能

>適用先:Windows Admin Center、Windows Admin Center プレビュー

Windows Admin Center は拡張可能なプラットフォームとして構築され、パートナーと開発者が Windows Admin Center 内で既存の機能を利用できるようにすることで、他の IT 管理製品およびソリューションとシームレスに統合し、お客様に付加価値を提供しています。 Windows Admin Center の各ソリューションおよびツールは、パートナーと開発者が利用できるのと同じ拡張機能を使用して拡張機能として構築されています。そのため、現在 Windows Admin Center で利用可能なものと同様の強力なツールを作成することができます。

Windows Admin Center 拡張機能は、HTML5、CSS、Angular、TypeScript、jQuery など最新の Web テクノロジを使用して構築されており、PowerShell や WMI を介して対象サーバーを管理することができます。 また、Windows Admin Center のゲートウェイ プラグインを構築することで、REST などの異なるプロトコルで対象のサーバー、サービス、またはデバイスを管理することもできます。

## <a name="why-you-should-consider-developing-an-extension-for-windows-admin-center"></a>Windows Admin Center の拡張機能の開発を考慮する必要がある理由

Windows Admin Center の拡張機能を開発することで、製品やお客様にもたらすことができる価値を次に示します。

- **Windows Admin Center ツールを統合します。** Windows Admin Center でのサーバーとクラスターの管理ツールを使用して、製品やサービスを統合し、統一されたでシームレスなエンド ツー エンド監視、管理、トラブルシューティング エクスペリエンスを顧客に提供します。
- **プラットフォームのセキュリティ、id、および管理機能を活用するには。** Azure Active Directory (AAD) のサポートを有効にする、多要素認証、ロールベースのアクセス制御 (RBAC)、ログ記録、今日の複雑な要件を満たす Windows Admin Center プラットフォームの機能を利用して、製品とサービスの監査IT 組織。
- **最新の web テクノロジを使用して開発します。** などの HTML5、CSS、Angular、TypeScript、jQuery では、最新の web テクノロジを使用して、優れたユーザー エクスペリエンスとリッチで強力な UI コントロールが、Windows Admin Center SDK に含まれるすばやく作成できます。
- **製品への支援を拡張します。** 今年の後半を迅速に拡大する顧客基盤や起動勢いを活用して、Windows Server 2019 アウトリーチと新しい Windows Admin Center エコシステムの一部となります。

## <a name="start-developing-with-the-windows-admin-center-sdk"></a>Windows Admin Center SDK を使用した開発を開始します。

Windows Admin Center 開発を開始するは簡単です。  サンプル コードが見つかる[ツール](develop-tool.md)、[ソリューション](develop-solution.md)、および[ゲートウェイ プラグイン](develop-gateway-plugin.md)SDK ドキュメントの拡張機能の種類。 ありますは新しい拡張機能プロジェクトをビルドし、ニーズに合わせてプロジェクトをカスタマイズする個々 の手順に従って、Windows Admin Center CLI を活用します。

Windows Admin Center を行いました[SDK デザイン ツールキット](https://github.com/Microsoft/windows-admin-center-sdk/blob/master/WindowsAdminCenterDesignToolkit.zip)Windows Admin Center スタイル、コントロール、およびページ テンプレートを使用して PowerPoint の拡張機能を迅速に模擬テストを実行するために使用できます。 拡張機能はどのように Windows Admin Center でコーディングを開始する前に参照してください。

GitHub でホストされているサンプル コードもあります。[開発者ツール](https://aka.ms/wacsdk)ソリューション拡張機能のサンプルを参照して、独自の拡張機能で使用するコントロールの豊富なコレクションを格納しています。 開発者ツールは、開発者モードで Windows Admin Center にサイド ローディングすることができる完全に機能する拡張機能です。

SDK の詳細を確認し、作業を開始するには、次のトピックを参照してください。

- [拡張機能のしくみを理解します。](understand-extensions.md)
- [拡張機能の開発](developing-extensions.md)
- [ガイド](guides.md)
- [拡張機能を公開します。](publish-extensions.md)

## <a name="partner-spotlight"></a>パートナー スポットライト

パートナーが Windows Admin Center エコシステムにもたらし始めたすばらしい価値を確認し、今すぐそれらの拡張機能を試してください。 Windows Admin Center から[拡張機能をインストールする方法](../configure/using-extensions.md)の詳細については、こちらを参照してください。

### <a name="biitops"></a>BiitOps
BiitOps 変更拡張機能は、変更の追跡、Windows Server の物理/仮想マシンのハードウェア、ソフトウェアや構成設定を提供します。 拡張機能が表示されます、BiitOps 変更正確に新機能については、変更内容と、単一ウィンドウ-の-ガラスの問題を追跡するで削除されましたは、コンプライアンス、信頼性、セキュリティに関連します。 [BiitOps 変更拡張機能の詳細について](case-studies/biitops.md)します。

![BiitOps 拡張機能](../media/extensibility-overview/biitops-1.png)

### <a name="dataon"></a>DataON

データにする必要があります拡張機能は、監視、管理、データのハイパー コンバージド インフラストラクチャと Windows Server ベースの記憶域システムをエンド ツー エンドの分析情報が表示されます。 履歴データの報告、ディスク マッピング、システム アラートおよび、Windows Admin Center サーバーと、シームレスなを介して、ハイパー コンバージド インフラストラクチャの管理機能を補完するものとして、SAN のような呼び出しホーム サービスなどの一意の値を追加する必要がありますの拡張機能統合された操作。 [DataON の MUST 拡張機能と開発エクスペリエンスの詳細については、こちらを参照してください](case-studies/dataon.md)。

![DataON MUST 拡張機能](../media/extensibility-overview/dataon-must-extension.png)

### <a name="fujitsu"></a>Fujitsu

Fujitsu の ServerView 正常性と Windows Admin Center の RAID の正常性の拡張機能は、Fujitsu PRIMERGY サーバーの詳細な監視とプロセッサ、メモリ、能力と記憶域サブシステムなどの重要なハードウェア コンポーネントの管理を提供します。 Windows Admin Center UX の設計パターンと UI コントロールを利用することで、Fujitsu は Windows Admin Center プラットフォームを通じて、サーバー ロールとサービス、オペレーティング システム、ハードウェア管理に至るまで、エンド ツー エンドの洞察のビジョンに対して大きな前進をもたらしました。 [Fujitsu の拡張機能と開発エクスペリエンスの詳細については、こちらを参照してください](case-studies/fujitsu.md)。

![Fujitsu ServerView 拡張機能](../media/extensibility-overview/fujitsu-serverview-extension.png)

### <a name="lenovo"></a>Lenovo

Lenovo XClarity インテグレーターの拡張機能は、Windows Admin Center 内のさまざまなエクスペリエンスにシームレスに統合することで、次のレベルにハードウェアの管理を移動します。 XClarity インテグレーター ソリューションは、すべての Lenovo サーバーの概要を確認し、1 台のサーバー、フェールオーバー クラスターまたはハイパーコンバージド クラスターに接続しているかどうか、別のツールの拡張機能がハードウェアの詳細を指定します。 [Lenovo XClarity インテグレーターの拡張機能の詳細について](case-studies/lenovo.md)します。

![Lenovo の拡張機能](../media/extensibility-overview/lenovo-extension.png)

### <a name="pure-storage"></a>Pure Storage

純粋なストレージでは、enterprise、競争優位性のビジネスを促進するデータ中心のアーキテクチャを提供するオール フラッシュ データ ストレージ ソリューションを提供します。 Windows Admin Center の純粋なストレージ拡張機能は、純粋な FlashArray 製品単一枠ビューを提供し、監視タスクを実行、リアルタイムのパフォーマンスのメトリックを表示および記憶域ボリュームと 1 つの UI でイニシエーターの管理ユーザーには、発生します。 [詳細については、純粋の拡張機能と、開発エクスペリエンスは](case-studies/purestorage.md)します。

![純粋なストレージの拡張機能](../media/extensibility-overview/purestorage-extension.png)

### <a name="qct"></a>QCT

QCT Management Suite の拡張機能は、物理サーバーの監視とシステムの認定 QCT Azure Stack HCI の管理を提供することで、Windows Admin Center を補完します。 QCT Management Suite 拡張機能は、サーバーのハードウェア情報を表示し、ハードウェア イベント ログのツール、および S.M.A.R.T.、直感的なウィザード UI を置き換える物理ディスク、効率的に提供します 予測的なディスクの管理に基づいています。 [QCT Management Suite の拡張機能の詳細について](case-studies/qct.md)します。

![QCT 拡張機能](../media/extensibility-overview/qct-extension.png)

### <a name="squared-up"></a>Squared Up

Squared Up により、System Center Operations Manager に基づくクラス最高の監視エクスペリエンスと、Azure Log Analytics、Application Insights、およびその他の監視ソリューションとの統合機能が提供されます。 [Squared Up の拡張機能](https://squaredup.com/product/honolulu/windows-admin-center-extension/?utm_source=microsoft-docs&utm_medium=public-relations&utm_campaign=honolulu)により、過去のパフォーマンス データやライブ アプリケーションのトポロジと依存関係を Windows Admin Center が提供するサーバーおよびクラスター管理のコンテキストにもたらしています。また、初期のお客様は、多数の異なるソースからの膨大なデータを単一のエクスペリエンスに統合することの価値を高く評価しています。 [Squared Up の拡張機能と開発エクスペリエンスの詳細については、こちらを参照してください](case-studies/squared-up.md)。

![Squared Up の拡張機能](../media/extensibility-overview/squaredup-extension.png)