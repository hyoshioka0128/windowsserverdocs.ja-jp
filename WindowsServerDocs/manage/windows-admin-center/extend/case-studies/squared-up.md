---
title: 管理センターの Windows SDK のケース スタディ - 2 乗
description: 管理センターの Windows SDK のケース スタディ - 2 乗
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 05/23/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ab0a7bdcf2388ffc867763c04e183b7388fd13e9
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2018
ms.locfileid: "2052546"
---
# <a name="squared-up-extension"></a>拡張子を 2 乗

## <a name="bringing-scom-based-monitoring-server-dependency-visibility-and-external-data-insights-into-windows-admin-center"></a>SCOM ベースの監視、サーバーの依存関係の表示設定 Windows 管理センターに外部データの分析結果を統合

乗を設立されましたビジョンのエンタープライズ IT の複雑さの問題を解決するために、データのビジュアル化を使用します。 Microsoft の強力なシステム センター Operations Manager プラットフォームと Microsoft の Azure ログ分析、アプリケーション分析システムからの他のデータ ソースとの統合の一番上に、一意軽量乗するは、UI 専用のソフトウェアの作成します。サード パーティ製品 ServiceNow、Splunk およびインフラストラクチャとアプリケーションの不動産、両方の内部設置型の大規模なエンタープライズ把握を提供する多くのハイブリッド クラウド環境全体に Service Manager 中央揃えにします。

> <cite>"おした頻度の高いを利用して Windows の管理センターでそのテクニカル プレビュー版で、構成演習に簡単にアクセスする、エンジニアなどの問題を解決する際に便利本当にヒット大きな既に経過しているし、プライマリ管理できるようにします。完全なリリースにヒット後にします。 お好き乗との統合と 1 つの場所のすべてのデータを表示する機能の潜在的なです。"</cite>
>
> --David Acevedo は/で NuStar エネルギー l. p. S スペシャ リスト

乗のクライアントが数百、多くの場合の桁を管理する、Windows サーバーおよびポートフォリオが、両方を 2 乗と Microsoft が提供がミッション IT チームを表示するには、さまざまなアプリケーションの迅速で、現在 web 分析結果を提供する UI の最適なする必要があります。 その結果、乗上にあるチームは、世代の Windows Server の管理には、これらの同じ値とプリンシパルいる Windows 管理センターですばらしい配置をすぐにしました。 チームを長期的なパフォーマンス データ、依存関係の分析結果をリアルタイム サーバー、およびアプリケーションのコンテキストを 2 乗で表示されるように完全に滑らかな、リアルタイムのデータと補完から提供されたサーバー管理機能と思わ具体的には、管理センターの Windows します。

![拡張子を 2 乗](../../media/extend-case-study-squared-up/squared-up-1.png)

> <cite>"管理を 2 乗の大規模なサーバー不動産、組織の場合は、ローカライズされた一元的なツールと中のような項目できるように、サーバーをメンテナンス モードに直接内からスロー完璧結婚は、Windows 管理センターの統合/Windows 管理センターは、お問い合わせの優れたの小さな wins"</cite>
>
> -– Kip Granson、パーデュ大学での仮想化システム管理者

Windows 管理センター内でシームレスにそのデータを表示したいの明確なビジョンを把握、乗を Windows 管理センター SDK の初期のプライベート preview 版を操作して簡単で、文書化された、柔軟なします。

Windows 管理センター SDK を使用して、乗を構築することが関連性の高い乗を Windows の管理センター内のビューのエクスペリエンスを埋め込む動的に拡張します。 たとえば、特定のサーバーまたはクラスターのコンテキスト内ビュー乗を自動的に埋め込まれているに可視を提供します。 ビューには、キーのパフォーマンスと容量の基準 (CPU、メモリを搭載しディスク) などの履歴傾向スタック (クラウド プラットフォームまたはデータ センターの仮想化)、SQL データベースやサービスなどのアプリケーションのコンポーネントをホストし、クラウド ベースのログの分析ITSM データです。

![拡張子を 2 乗](../../media/extend-case-study-squared-up/squared-up-2.png)

乗と管理センターの Windows を最新の web アーキテクチャおよびデザイン特徴、単純な技術的な統合とのシームレスなユーザー エクスペリエンスの両方が有効になっているを共有します。 基準になる web ベースの管理] でさまざまなシステムの間の統合には、この方法は、最新の統合管理の操作環境のロックを解除するキーと考えています。

> <cite>"わかります Windows 管理センター最先端の最新の Windows Server の管理] の名前を付けてように、チームとし、このような内に、このような速度、情熱、柔軟性を根本的に作業したしていることを密接に操作するための機能を十分に活用を経過しています。モダンな開発パラダイム行ったに最適な方法とリーン、アジャイル、ペースの速いソフトウェア開発会社、協力すれば、"。</cite>
>
> --2 乗リチャード Benwell] にある製品の設計者

この自然の配置] を 2 乗の開発チームが迅速に Windows 管理センターのユーザー エクスペリエンスのネイティブ乗を表示するプロトタイプの統合に発展する独自早期導入者、技術の手にアクセスすることが可能クライアントをプレビューします。 顧客の反応からストーリーが最大はすぐに明らかでした。

> <cite>"3,500 を超えるサーバーの環境にわたって優れたサービスは、さまざまな統合は維持するための主な課題のいずれかの横の管理およびツールなどを監視乗して、Windows 管理センター - の統合1 つに 1 つのコンソール – が多いのさまざまなソースからの大量のデータはへのご協力の大規模です。"</cite>
>
> --Martin Ehrnst、Intility A/S で Azure の技術的な潜在顧客

乗をクライアント既にから積極の種類とトンの優れた新機能も Windows 管理センターに乗をきわめて尽くしてこの統合と、クライアントのがすばらしいの選択肢が提供されると、条件を満たす 1 つのウィンドウ-の-ガラス、IT 運用管理のために旅します。

乗を/Windows 管理センターの統合が現在ベータ版です。アクセスする場合は、確認してくださいを[2 乗の専用] ページ](https://squaredup.com/product/honolulu/windows-admin-center-extension/?utm_source=microsoft-wac&utm_medium=public-relations&utm_campaign=honolulu)の詳細。 自分の組織で Microsoft システム センター Operations Manager 乗する (つまり、拡張子を操作するために必要な) がまだない場合は、[完全な機能を備えた、30 日間無料試用版の同じ場所から手も利用できます。 
