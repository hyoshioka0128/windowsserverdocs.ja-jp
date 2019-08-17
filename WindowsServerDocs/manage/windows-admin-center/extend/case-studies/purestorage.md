---
title: Windows 管理センター SDK ケーススタディ-ピュアストレージ
description: Windows 管理センター SDK ケーススタディ-ピュアストレージ
ms.technology: extend
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 1/7/2019
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: cfd9d31d388b9acb1a4a4fa40b3975b235a8634b
ms.sourcegitcommit: 0467b8e69de66e3184a42440dd55cccca584ba95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69546614"
---
# <a name="pure-storage-extension"></a>純粋なストレージ拡張機能

## <a name="providing-end-to-end-array-management-for-windows-admin-center"></a>Windows 管理センターのエンドツーエンドの配列管理の提供 

[純粋なストレージ](https://www.purestorage.com/)は、データ中心のアーキテクチャを提供し、競争力を高めるためにビジネスを促進する、エンタープライズ、すべてのフラッシュデータストレージソリューションを提供します。  純粋は microsoft Gold パートナーであり、Microsoft Windows Server の認定を受けており、Azure、Hyper-v、SQL Server、System Center、Windows PowerShell、Windows SMB などの主要な Microsoft ソリューションの技術的な統合を開発します。 純粋に、純粋な FlashArray 製品に単一ペインのビューを提供する、Windows 管理センターの最新リリースをサポートする拡張機能の tech preview が発表されました。  この拡張機能から、ユーザーは1つのツールから、監視タスクの実行、リアルタイムのパフォーマンスメトリックの表示、およびストレージボリュームとイニシエーターの管理を行うことができます。

早い段階で、Windows 管理センターが "プロジェクトホノルル" と呼ばれていた場合、純粋には、Windows 管理センターで提供されている単一のウィンドウから複数の純粋なストレージ FlashArrays を管理する機能を顧客およびパートナーに提供できるという価値があります。

純粋に "プロジェクトホノルル" でユースケースを調査すると、Windows 管理センターと FlashArray の間で統合された管理エクスペリエンスを提供できる可能性がすぐに得られました。 純粋に Windows 管理センターエンジニアリングチームと密接に連携しています。これにより、機能の実装の詳細が定義されました。 純粋には、Windows 管理センターの初期段階でフィードバックを提供し、Microsoft チームに投稿することもできました。 

![純粋なストレージ拡張機能](../../media/extend-case-study-purestorage/purestorage-1.png)

> <cite>"Windows 管理センター内からのダイレクト管理を有効にするために、FlashArray web インターフェイスを模倣した機能セットを統合しました。Microsoft のお客様とパートナーは、1つのウィンドウガラスからメリットを得ることができ、2つの異なる管理ツールを使用する必要があります。単一の管理の利点に加えて、FlashArray に接続されている Windows サーバーをコンテキストで管理できます。 "</cite>
>
> --Barkz、テクニカルディレクターの Microsoft ソリューション & 統合、純粋なストレージ

純粋なストレージソリューション拡張機能に含まれる機能は次のとおりです。
- 複数の FlashArrays に接続しています。
- IOPs、帯域幅、待機時間、データの削減、領域管理など、FlashArray の詳細を表示します。 これらのすべての情報は、FlashArray 管理 GUI から取得したものと同じです。
- Windows Server ホストおよびクラスター化共有ボリューム (Csv) の共有ボリュームアクセスを有効にするために使用される構成済みのホストグループを表示します。
- ホストの表示—すべての接続情報は、ホスト名、iSCSI 修飾名 (Iqn)、ワールドワイド名 (Wwn) を含めて利用できます。
- ボリュームの管理: これには、ボリュームを作成および破棄する機能が含まれます。 ボリュームが破棄されると、破棄された項目のバケットに格納され、メインの FlashArray 管理 GUI から Xamarin.mac する必要があります。
- イニシエーターの管理: これは、Windows 管理センターの展開で管理されている個々のサーバーにコンテキストを提供する最も重要な機能の1つです。 接続されたディスク (ボリューム) を個々の Windows Server に表示し、マルチパス IO (MPIO) がインストールまたは構成されているかどうかを確認し、新しいボリュームを作成/マウントできます。

純粋なストレージソリューション拡張機能によって提供されるすべての機能を示す[デモビデオ](https://youtu.be/IFAeCAd6V2g)が作成されています。 

次のスクリーンショットは、特定の Windows Server ホストに接続されているディスク (ボリューム) を表示する方法を示しています。 接続の詳細を表示するだけでなく、マルチパス IO が構成されているかどうかを確認します。

![純粋なストレージ拡張機能](../../media/extend-case-study-purestorage/purestorage-2.png)

ディスクを表示するだけでなく、Windows ディスク管理ツールを使用せずに、新しいボリュームを作成し、すぐにホストにマウントすることができます。

![純粋なストレージ拡張機能](../../media/extend-case-study-purestorage/purestorage-3.png)

Technical Preview のリリース後、これまでに収集されたお客様のフィードバックは非常に肯定的で、今後のリリースで追加されるさまざまな機能についての洞察も提供しています。 

その他の情報:
- [純粋ストレージ拡張機能に関するお知らせのブログ投稿](https://blog.purestorage.com/tech-preview-of-the-pure-storage-extension-for-windows-admin-center/)
- [PureReport](https://itunes.apple.com/podcast/windows-admin-center-extension-from-pure-storage/id1392639991?i=1000424316130&mt=2)ポッドキャスト
