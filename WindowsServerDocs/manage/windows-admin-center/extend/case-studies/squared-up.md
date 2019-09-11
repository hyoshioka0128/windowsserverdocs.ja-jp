---
title: Windows 管理センター SDK ケーススタディ-二乗アップ
description: Windows 管理センター SDK ケーススタディ-二乗アップ
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 05/23/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 0d4469684ad9cbdadec5c40cb3b5178345b64a6d
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70865334"
---
# <a name="squared-up-extension"></a>2乗されるアップ拡張

## <a name="bringing-scom-based-monitoring-server-dependency-visibility-and-external-data-insights-into-windows-admin-center"></a>SCOM ベースの監視、サーバー依存関係の可視性、外部データ分析を Windows 管理センターに

二乗型アップは、企業の IT の複雑さの課題を解決するために、データの視覚化を使用するビジョンによって設立されました。 2乗された、軽量の UI 専用のソフトウェアは、Microsoft の強力な System Center Operations Manager プラットフォームの上に構築されます。また、Microsoft 独自の Azure Log Analytics、Application Insights、システムからの追加のデータソースとの統合にも対応しています。オンプレミスとハイブリッドクラウド環境の両方で、大規模なエンタープライズインフラストラクチャとアプリケーション資産の可視性を実現するために、ServiceNow、などのサードパーティ製品にセンターを Service Manager します。

> <cite>「Technical Preview 全体にわたって Windows 管理センターを利用してきましたが、これは既に大きなヒットでした。私たちのエンジニアが私たちの構成ラボに簡単にアクセスできるようにするという課題を解決するために、microsoft は主な管理を行います。完全リリースに達した後のコンソール。2乗との統合の可能性と、すべてのデータを1か所に格納する機能があります。」</cite>
>
> --David Acevedo, I/S スペシャリスト (NuStar エネルギー L.P.)

2乗されたクライアントは、数百、数千もの Windows サーバーを管理しており、それらによって提供されるさまざまなアプリケーションポートフォリオを1平方アップし、Microsoft は、IT チームが必要な洞察を提供するための高速で最新の web UI に最適になるようにしています。 結果として、2乗アップのチームは、Windows 管理センターとの優れた配置をすぐに見ました。これにより、同じ値とプリンシパルが次世代の Windows Server 管理に導入されます。 特に、このチームでは、2乗されたパフォーマンスデータ、リアルタイムのサーバー依存関係の洞察、およびアプリケーションコンテキストが、によって提供される流線型のリアルタイムのデータおよびサーバー管理機能を完全に補完すると考えました。Windows 管理センター。

![2乗されるアップ拡張](../../media/extend-case-study-squared-up/squared-up-1.png)

> <cite>「大規模なサーバー資産を管理する組織では、2乗されたアップ/Windows 管理センターの統合は、ローカライズおよび一元化されたツールに最適な結婚であり、内部からメンテナンスモードにサーバーを簡単に組み込むことができます。Windows 管理センターは、お客様にとって非常に簡単です。</cite>
>
> -–キープ Granson、仮想化システム管理者 (Purdue 大学)

Windows 管理センター内でデータをシームレスに表示したいという明確なビジョンにより、二乗アップは Windows 管理センター SDK の早期プライベートプレビュー版を使用して機能し、わかりやすく、ドキュメント化された柔軟性があります。

Windows 管理センター SDK を使用すると、二乗 Up は、Windows 管理センターのエクスペリエンス内で、関連する2乗されたビューを動的に埋め込む拡張機能を構築できました。 たとえば、特定のサーバーまたはクラスターのコンテキスト内では、四角形のアップビューは拡張された可視性に自動的に埋め込まれます。 ビューには、主要なパフォーマンスと容量のメトリック (CPU、メモリ、ディスクなど)、ホストスタック (クラウドプラットフォームまたはデータセンターの仮想化)、SQL データベースやサービスなどのアプリケーションコンポーネント、クラウドベースのログ分析などの履歴傾向が含まれます。データを ITSM します。

![2乗されるアップ拡張](../../media/extend-case-study-squared-up/squared-up-2.png)

二乗アップと Windows 管理センターは、最新の web アーキテクチャと設計ためしを共有しています。これにより、シンプルな技術的統合とシームレスなユーザーエクスペリエンスの両方が実現しました。 Web ベースの管理が従来よりも一般的になっているため、さまざまなシステム間でこのような統合を行うことは、統合された最新の管理エクスペリエンスをロック解除するための鍵となります。

> <cite>"Windows 管理センターは、windows Server の最新の管理の最先端として機能しています。そのため、チームと密接に連携していて、このような速度、小学校、柔軟性などを使用して作業しています。現代的な開発のパラダイムにより、アジャイルで迅速に発展する、迅速なソフトウェア開発会社であるという形で、非常に優れた機能を実現しました。」</cite>
>
> --Richard Benwell、製品アーキテクト (二乗)

この自然な配置では、2乗された開発チームが、Windows 管理センターのエクスペリエンス内でネイティブに正方形を表示し、それを早期導入者の手に入れるために、プロトタイプの統合に迅速に進めることができました。クライアントをプレビューします。 顧客の反応から、ストーリーが勝者になったことがすぐに明らかになりました。

> <cite>"3500 サーバーを超える環境で未処理のサービスを維持するための主な課題の1つは、管理ツールと監視ツールのさまざまなランドスケープを統合することです。これにより、2乗された Up と Windows 管理センター間の統合が実現します。多くの異なるソースから1つのコンソールに至るまで、膨大な量のデータをまとめています。」</cite>
>
> --Martin Ehrnst、Intility A/S での Azure の技術リーダー

この種の小学校は、既に Windows 管理センターに提供されている多数の優れた新機能を備えています。また、この統合の未来と、クライアント向けに開いているすばらしい可能性については、作っ興奮になります。IT 運用管理の真の単一のウィンドウを表示します。

二乗された Up/Windows 管理センターの統合は、現在ベータ版です。アクセスする場合、詳細については、2乗された[専用ページ](https://squaredup.com/product/honolulu/windows-admin-center-extension/?utm_source=microsoft-wac&utm_medium=public-relations&utm_campaign=honolulu)をご確認ください。 組織で Microsoft System Center Operations Manager を使用していて、まだ2乗していない場合 (拡張機能を機能させるために不可欠)、同じ場所から、完全な機能を備えた30日間の無料試用版を入手することもできます。 
