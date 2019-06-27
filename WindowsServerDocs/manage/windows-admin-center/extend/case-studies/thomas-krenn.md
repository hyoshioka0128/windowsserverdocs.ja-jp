---
title: Windows Admin Center SDK のケース スタディ - Thomas Krenn
description: Windows Admin Center SDK のケース スタディ - Thomas Krenn
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 06/24/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 93b8a450aa86a454ec6febd349fcaa35df590266
ms.sourcegitcommit: 3be280c8638214857dc355b201eb56a04499a5e5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2019
ms.locfileid: "67396762"
---
# <a name="thomas-krennag-extension"></a>Thomas-Krenn.AG Extension

## <a name="intuitive-server-and-storage-health-management"></a>サーバーとストレージの直感的な正常性管理

Thomas Krenn.AG Windows Admin Center の拡張機能は、高可用性の 2 つのノードの向けに設計されて[s 2d-クラスター マイクロ](https://www.thomas-krenn.com/en/products/application/software-defined-storage/s2d-micro-cluster.html)アプライアンスです。 視覚的にわかりやすい web インターフェイスでは、単純なダッシュ ボードを通じてマイクロ-クラスターの正常性状態を視覚化して、ストレージ デバイス、ネットワーク インターフェイスまたはクラスター全体の詳細を表示するにドリル ダウンすることができます。

拡張機能は、通常のシリアル番号、ソフトウェアのバージョン、記憶域使用率など、最初のレベルのサービスとサポートの呼び出しに必要な情報を直感的なアクセスを提供します。 Windows Server のハイパー コンバージド インフラストラクチャを使用した経験を持たない管理者に役立つように設計されています。

使用可能な洞察のいくつか次のとおりです。
- Micro ノードと Micro クラスターに関する一般情報
- OS ブート デバイスの状態/
- 容量の HDD と SSD の状態のキャッシュ
- クラスター イベント
- ネットワークの状態と情報

ダッシュ ボードを使用すると、クラスターの正常性状態とシリアル番号、モデル、OS のバージョンの使用率などの重要なシステム情報を確認します。 さらに、ファン、NIC、ノードのハードウェアの全体的な正常性は、同様のダッシュ ボードに表示されます。

![Thomas-Krenn Extension](../../media/extend-case-study-thomas-krenn/thomas-krenn-1.png)

シリアル番号、スマート状態、および容量使用率を表示する記憶域デバイスにドリルダウンすることができます。 ブート デバイスには、インジケーターをセクターと能力を再割り当て時、SSD の正常性の最善の指標の摩耗も表示されます。

![Thomas-Krenn Extension](../../media/extend-case-study-thomas-krenn/thomas-krenn-2.png)

クラスターの状態アイコンは、クラスターの操作詳細が表示の概要を表示するのに展開されます。

![Thomas-Krenn Extension](../../media/extend-case-study-thomas-krenn/thomas-krenn-3.png)

このマイクロ-クラスターの Azure クラウドのミラーリング監視サーバーが利用できない全体の夜の後に、問題を特定するのに十分なは 1 つの概要です。 すぐに [通知] をクリックすると、すばやく修復に関連するイベントが一覧表示します。 クラスターのイベントはローカライズし、基本の OS 言語によって決まります。 拡張機能自体は、英語とドイツ語をサポートします。

![Thomas-Krenn Extension](../../media/extend-case-study-thomas-krenn/thomas-krenn-4.png)

ネットワークの情報はもすぐに使用できます。

![Thomas-Krenn Extension](../../media/extend-case-study-thomas-krenn/thomas-krenn-5.png)

お客様からのフィードバックに基づき、Windows Admin Center v1904 で使用できる「ダーク モード」も実装しました。 ダーク データ センターとライトが不十分なキャビネットとクローゼットを使用するようになります。 また、Windows Admin Center よりアクセス可能な特定の視覚障碍を持つ管理者まぶしくを減らすことで。

![Thomas-Krenn Extension](../../media/extend-case-study-thomas-krenn/thomas-krenn-6.png)

Thomas Krenn では、使いやすさとトレーニングを受けていない管理者のユーザー補助機能がある小規模および中規模ビジネスの市場でのハイパー コンバージド インフラストラクチャの優れたカスタマー エクスペリエンスにキーをすぐに実現します。 Thomas-Krenn のマイクロ クラスターの拡張機能がダッシュ ボードの専用ハードウェア情報を含む、新しいクラスターの重要な正常性の情報を再グループ化して HCI 管理機能のネイティブ Windows Admin Center を完全に補完します。わかりやすいインターフェイスです。

開発プロセス中にノードが失敗した後も管理の容易性を確保自体には、クラスターで高可用性構成で Windows Admin Center 1904 を展開することができます。 拡張機能は、OS 全体と同様、プレインストールされています。

拡張機能は、Microsoft で開発されている Windows Admin Center 1904 と並列で構築されています。 協力関係と製品の年 2019年 4 月で正常に起動する前に解決された共同で両方の側での継続的なフィードバックが公開されている問題を閉じます。 Thomas Krenn は完全にサポートされ、Windows Admin Center 1904 の新機能を実装する最初の 1 つである非常に誇りに思っています。
