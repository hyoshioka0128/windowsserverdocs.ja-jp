---
title: Windows Admin Center SDK のケース スタディ - 2 乗
description: Windows Admin Center SDK のケース スタディ - 2 乗
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 05/23/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: ab0a7bdcf2388ffc867763c04e183b7388fd13e9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863943"
---
# <a name="squared-up-extension"></a>拡張機能を 2 乗

## <a name="bringing-scom-based-monitoring-server-dependency-visibility-and-external-data-insights-into-windows-admin-center"></a>SCOM ベースの監視、サーバー依存関係の可視性、および Windows Admin Center に外部データの洞察

2 乗がデータの視覚化を使用して、エンタープライズ IT の複雑さの課題を解決するためのビジョンを創設しました。 一意、ライトウェイト乗上の Microsoft の強力な System Center Operations Manager のプラットフォームだけでなく Microsoft の Azure Log Analytics、Application Insights とシステムからの追加のデータ ソースとの統合の上には、UI のみのソフトウェアサード パーティの製品、オンプレミス インフラストラクチャとアプリケーションの資産を大規模なエンタープライズの可視性を提供するには、ServiceNow、Splunk、さらに多くのように、ハイブリッド クラウド環境で Service Manager が中央にします。

> <cite>"私たちした大きくを利用して、Technical Preview で Windows Admin Center と本当に、構成 labs に簡単にアクセスを取得するエンジニアなどの課題を解決を支援ヒット大きな既にとなっていますしようとすることをプライマリ管理コンソールは完全リリース版にヒットしたとします。We love を 2 乗との統合を 1 か所ですべてのデータを表示すること、および潜在的な。"</cite>
>
> -- David Acevedo, I/S Specialist at NuStar Energy L.P.

2 乗をクライアント管理の数百、何千も多くの場合、Windows サーバーと、両方の 2 乗と Microsoft によって提供されるポートフォリオは、IT チームにミッション クリティカルでは、さまざまなアプリケーションの最良の高速で最新の web UI 分析情報を提供する必要があります。 その結果、チームの 2 乗をそれら同じの値とプリンシパルを次世代の Windows サーバーの管理に提供する Windows Admin Center で魅力的な配置をすぐに説明しました。 具体的には、チームでは、長期的なパフォーマンス データやリアルタイムのサーバー依存関係の洞察を 2 乗して表示されるアプリケーションのコンテキストが完全に補完、光沢のある、リアルタイムのデータとサーバーの管理機能によって提供されると考えられるWindows Admin Center。

![拡張機能を 2 乗](../../media/extend-case-study-squared-up/squared-up-1.png)

> <cite>"を 2 乗の大規模なサーバー資産を管理する組織として Windows Admin Center の統合は、ローカライズされた一元的なツールや中など、サーバーをメンテナンス モードに直接格納内からスローすることの完璧な結婚/Windows Admin Center は、私たちにとって優れたの小さな wins"</cite>
>
> --Kip Granson、Purdue 大学での仮想化システム管理者

Windows Admin Center 内でそのデータをシームレスに提示する必要があるの明確なビジョンは、有効活用 2 乗を初期のプライベート プレビュー バージョンの Windows Admin Center SDK と協力して、簡単で適切に文書化された柔軟な。

Windows Admin Center SDK を使用して、2 乗を構築することが拡張機能を動的に関連する 2 乗を Windows Admin Center 内のビューのエクスペリエンスを埋め込みます。 など、特定のサーバーまたはクラスターのコンテキスト内でビューの 2 乗を自動的に埋め込まれているに拡張表示が実現します。 ビューには、主要なパフォーマンスと容量のメトリック (CPU、メモリ、ディスク) などの傾向の履歴スタック (クラウド データ センターのプラットフォームや仮想化)、SQL データベースやサービスなどのアプリケーション コンポーネントをホストとクラウド ベースのログ分析ITSM データです。

![拡張機能を 2 乗](../../media/extend-case-study-squared-up/squared-up-2.png)

2 乗を Windows Admin Center は、最新の web アーキテクチャと設計功を奏した、単純な技術的な統合とシームレスなユーザー エクスペリエンスの両方が有効になっているを共有します。 ますます、norm web ベースの管理のさまざまなシステム間の統合には、このメソッドは、最新の統一された管理エクスペリエンスのロックを解除するキーと考えています。

> <cite>"がわかります Windows Admin Center として最先端の最新の Windows Server 管理のため、チームやこのような速度、情熱、柔軟性と内などの根本的に操作がいるという事実と密接に作業するための優れたエクスペリエンスとなっています最新の開発パラダイムが行ったに最適な方法で、リーンのテンポの速いアジャイル ソフトウェア開発会社で私たちは自分たちです"。</cite>
>
> --2 乗 Richard Benwell、製品のアーキテクトで

この自然な配置では、2 乗の開発チームがネイティブは、Windows Admin Center エクスペリエンス内で、2 乗を表示するプロトタイプの統合を迅速に進行状況を独自早期導入者、技術の手に取得することが可能クライアントをプレビューします。 顧客の反応からには、ストーリーに優勝したことがすぐにクリアしました。

> <cite>"3,500 を超えるサーバー、環境全体で優れたサービスは、多様な統合が維持するための主要な課題の 1 つ landscape 管理と監視ツールなどの 2 乗とが表示されます - Windows Admin Center の統合まとめて 1 つのコンソール – 多くのさまざまなソースからの大量のデータは私たちにとって大きなです。"</cite>
>
> --Martin Ehrnst、Intility A/S で Azure のテクニカル リード

その種の 2 乗のクライアントから既に情熱ともの優れた新機能の核と Windows Admin Center に付属する 2 乗はきわめて興奮この統合と、クライアントを起動してすばらしい可能性の将来についてと、true 単一-ウィンドウ-の-の入ったグラスの IT 運用管理のためには工程をします。

2 乗を]、[Windows Admin Center の統合は現在ベータ版です。アクセスする場合は、くださいチェック アウト[専用ページ 2 乗の](https://squaredup.com/product/honolulu/windows-admin-center-extension/?utm_source=microsoft-wac&utm_medium=public-relations&utm_campaign=honolulu)の詳細。 組織で Microsoft System Center Operations Manager を使用して、2 乗を (これは、拡張機能を操作するために不可欠な) がまだない場合は、フル機能 30 日間無料試用版と同じ場所から自分の手も取得できます。 
