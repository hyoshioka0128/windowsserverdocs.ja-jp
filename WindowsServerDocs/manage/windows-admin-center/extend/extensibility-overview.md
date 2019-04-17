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
ms.openlocfilehash: fa3d7e75b32f0195346e58db54b7932c8d2fd3b9
ms.sourcegitcommit: 659544db1e19d6eecc52c7de07116ae735280544
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/11/2019
ms.locfileid: "9001844"
---
# Windows Admin Center の拡張機能

>適用対象: Windows Admin Center、Windows Admin Center Preview

Windows Admin Center は拡張可能なプラットフォームとして構築され、パートナーと開発者が Windows Admin Center 内で既存の機能を利用できるようにすることで、他の IT 管理製品およびソリューションとシームレスに統合し、お客様に付加価値を提供しています。 Windows Admin Center の各ソリューションおよびツールは、パートナーと開発者が利用できるのと同じ拡張機能を使用して拡張機能として構築されています。そのため、現在 Windows Admin Center で利用可能なものと同様の強力なツールを作成することができます。

Windows Admin Center 拡張機能は、HTML5、CSS、Angular、TypeScript、jQuery など最新の Web テクノロジを使用して構築されており、PowerShell や WMI を介して対象サーバーを管理することができます。 また、Windows Admin Center のゲートウェイ プラグインを構築することで、REST などの異なるプロトコルで対象のサーバー、サービス、またはデバイスを管理することもできます。

## Windows Admin Center の拡張機能の開発を考慮する必要がある理由

Windows Admin Center の拡張機能を開発することで、製品やお客様にもたらすことができる価値を次に示します。

- **Windows Admin Center ツールとの統合:** Windows Admin Center でサーバーおよびクラスター管理ツールを使用して製品とサービスを統合し、監視、管理、トラブルシューティングの統一されたシームレスなエンド ツー エンドのエクスペリエンスをお客様に提供できます。
- **プラットフォーム セキュリティ、ID、管理機能の利用:** Windows Admin Center プラットフォームの機能を利用することで、製品とサービスに対して、Azure Active Directory (AAD) サポート、多要素認証、役割ベースのアクセス制御 (RBAC)、ログ、監査を有効にし、現在の IT 組織の複雑な要件に対応できます。
- **最新の Web テクノロジを使用した開発:** HTML5、CSS、Angular、TypeScript および jQuery、また Windows Admin Center SDK に含まれる充実した強力な UI コントロールを含む最新の Web テクノロジを使用して、魅力的なユーザー エクスペリエンスを簡単に作成できます。
- **製品のアウトリーチの拡大:** 急速に拡大する顧客基盤へのアウトリーチを持つ新しい Windows Admin Center エコシステムに参加し、今年後半発売の Windows Server 2019 の推進力を利用できます。

## Windows Admin Center SDK で開発を始める

Windows Admin Center の開発を開始するは簡単です。  サンプル コードは、SDK ドキュメントの[ツール](develop-tool.md)、[ソリューション](develop-solution.md)、および[ゲートウェイ プラグイン](develop-gateway-plugin.md)の拡張機能の種類の確認できます。 新しい拡張機能プロジェクトをビルドし、ニーズに合わせて、プロジェクトをカスタマイズする個々 の手順に従って Windows Admin Center CLI を活用します。

Windows Admin Center スタイル、コントロール、およびページ テンプレートを使用して拡張機能を PowerPoint でモック作成[SDK 設計ツールキット](https://github.com/Microsoft/windows-admin-center-sdk/blob/master/WindowsAdminCenterDesignToolkit.zip)急速にするために使用できる Windows Admin Center を行っています。 拡張機能がどのように Windows Admin Center でコーディングを開始する前に参照してください。

GitHub でホストされているサンプル コードもある:[開発者ツール](https://aka.ms/wacsdk)は、ソリューション拡張機能のサンプルを参照して、独自の拡張機能で使用できるコントロールの豊富なコレクションを格納します。 開発者ツールは、開発者モードで Windows Admin Center にサイド ローディングすることができる完全に機能する拡張機能です。

SDK の詳細を確認し、作業を開始するには、次のトピックを参照してください。

- [拡張機能のしくみについて](understand-extensions.md)
- [拡張機能の開発](developing-extensions.md)
- [ガイド](guides.md)
- [拡張機能の公開](publish-extensions.md)

## パートナー スポットライト

パートナーが Windows Admin Center エコシステムにもたらし始めたすばらしい価値を確認し、今すぐそれらの拡張機能を試してください。 Windows Admin Center から[拡張機能をインストールする方法](../configure/using-extensions.md)の詳細については、こちらを参照してください。

### DataON

DataON の MUST 拡張機能は、監視、DataON のハイパーコンバージド インフラストラクチャとストレージ システムに Windows Server に基づく管理とエンド ツー エンドの洞察が表示されます。 MUST 拡張機能の履歴データの報告、ディスクのマッピング、システムのアラート、Windows Admin Center のサーバーとシームレスなを通じて、ハイパーコンバージド インフラストラクチャの管理機能を補完する、SAN のような呼び出しホーム サービスなどの一意の値を追加します。統合されたエクスペリエンスです。 [DataON の MUST 拡張機能と開発エクスペリエンスの詳細については、こちらを参照してください](case-studies/dataon.md)。

![DataON MUST 拡張機能](../media/extensibility-overview/dataon-must-extension.png)

### Fujitsu

Windows Admin Center 用の Fujitsu の ServerView Health および RAID Health 拡張機能は、Fujitsu PRIMERGY サーバー用のプロセッサ、メモリ、電源および記憶域のサブシステムなど、重要なハードウェア コンポーネントの詳細な監視および管理を提供します。 Windows Admin Center UX の設計パターンと UI コントロールを利用することで、Fujitsu は Windows Admin Center プラットフォームを通じて、サーバー ロールとサービス、オペレーティング システム、ハードウェア管理に至るまで、エンド ツー エンドの洞察のビジョンに対して大きな前進をもたらしました。 [Fujitsu の拡張機能と開発エクスペリエンスの詳細については、こちらを参照してください](case-studies/fujitsu.md)。

![Fujitsu ServerView 拡張機能](../media/extensibility-overview/fujitsu-serverview-extension.png)

### Lenovo

Lenovo の XClarity インテグレーターの拡張機能では、次のレベルにハードウェア管理は Windows Admin Center 内でのさまざまなエクスペリエンスにシームレスに統合します。 XClarity インテグレーター ソリューションは、Lenovo サーバーの高度なビューを提供し、1 台のサーバー、フェールオーバー クラスターまたはハイパーコンバージド クラスターに接続しているかどうか、別のツールの拡張機能がハードウェアの詳細を提供します。 [Lenovo XClarity インテグレーター拡張機能について詳しく説明します](case-studies/lenovo.md)。

![Lenovo の拡張機能](../media/extensibility-overview/lenovo-extension.png)

### 純粋な記憶域

純粋な記憶域は、enterprise、競争力のビジネスを加速するデータを中心としたアーキテクチャを提供するオール フラッシュ データ記憶域ソリューションを提供します。 Windows Admin Center の純粋な記憶域の拡張機能は純粋な FlashArray 製品に 1 つのウィンドウのビューを提供し、監視のタスクの実施、リアルタイムのパフォーマンスのメトリックを表示および記憶域ボリュームと 1 つの UI を通じてイニシエーターを管理するユーザーを支援エクスペリエンスです。 [純粋なの拡張機能と開発エクスペリエンスについて詳しく説明します](case-studies/purestorage.md)。

![純粋な記憶域の拡張機能](../media/extensibility-overview/purestorage-extension.png)

### Squared Up

Squared Up により、System Center Operations Manager に基づくクラス最高の監視エクスペリエンスと、Azure Log Analytics、Application Insights、およびその他の監視ソリューションとの統合機能が提供されます。 [Squared Up の拡張機能](https://squaredup.com/product/honolulu/windows-admin-center-extension/?utm_source=microsoft-docs&utm_medium=public-relations&utm_campaign=honolulu)により、過去のパフォーマンス データやライブ アプリケーションのトポロジと依存関係を Windows Admin Center が提供するサーバーおよびクラスター管理のコンテキストにもたらしています。また、初期のお客様は、多数の異なるソースからの膨大なデータを単一のエクスペリエンスに統合することの価値を高く評価しています。 [Squared Up の拡張機能と開発エクスペリエンスの詳細については、こちらを参照してください](case-studies/squared-up.md)。

![Squared Up の拡張機能](../media/extensibility-overview/squaredup-extension.png)