---
title: ドライブの記憶域スペース ダイレクトの対称性に関する考慮事項
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 10/08/2018
Keywords: 記憶域スペース ダイレクト
ms.localizationpriority: medium
ms.openlocfilehash: 629e49a0c1919286d8e4f418b3e99d69e720f4fd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866883"
---
# <a name="drive-symmetry-considerations-for-storage-spaces-direct"></a>ドライブの記憶域スペース ダイレクトの対称性に関する考慮事項 

> 適用対象:Windows Server 2019、Windows Server 2016

[記憶域スペース ダイレクト](storage-spaces-direct-overview.md)はすべてのサーバーが正確に同じドライブを持つ場合に最適です。

実際には、この実用的ではないと認識しています。記憶域スペース ダイレクトは、組織のニーズの拡大に伴い、年とスケールを実行しています。 今日では、する可能性があります購入 spacious 3 TB ハード ドライブです。次の年を大きいもの見つけ出せなくなったりしまいます。 そのため、混在一致の程度がサポートされています。

このトピックでは、制約について説明し、サポートされているとサポートされていない構成の例を示します。

## <a name="constraints"></a>制約

### <a name="type"></a>種類

すべてのサーバーは同じである必要があります[の種類のドライブ](choosing-drives.md#drive-types)します。

たとえば、1 つのサーバーに NVMe がある場合は、べき*すべて*NVMe があります。

### <a name="number"></a>数値

すべてのサーバーには、同じ数の各種類のドライブの必要があります。

たとえば、1 つのサーバーに 6 つの SSD がある場合は、べき*すべて*6 つの SSD があります。

   > [!NOTE]
   > ドライブの障害時に一時的にまたはを追加またはドライブを削除する際に異なる数のことができます。

### <a name="model"></a>モデル

可能であれば、ファームウェアのバージョン、同じモデルのドライブを使用することをお勧めします。 できない場合は、可能な限り類似したドライブを慎重に選択します。 お勧めしませんはっきりとさまざまなパフォーマンスや耐久性の特性を持つ同じ種類の混在とマッチング ドライブ (1 つは、キャッシュ、他の容量) しない限り、記憶域スペース ダイレクト IO を均等に分散し、モデルに基づいて識別しないため、.

   > [!NOTE]
   > 混在のような SATA、SAS ドライブをことができます。

### <a name="size"></a>サイズ

可能であれば、同じサイズのドライブを使用することをお勧めします。 さまざまなサイズの容量のドライブを使用して可能性があるいくつか使用不可の容量では、さまざまなサイズのキャッシュ ドライブを使用してキャッシュのパフォーマンスは向上しません。 詳細については、次のセクションを参照してください。

   > [!WARNING]
   > 異なるサーバー間での容量ドライブのサイズは、孤立した容量があります。

## <a name="understand-capacity-imbalance"></a>容量の不均衡を理解するには:

記憶域スペース ダイレクトは堅牢な容量の不均衡をドライブにわたって、複数のサーバーです。 不均衡が重大な場合でもすべてのものは引き続き機能します。 ただし、いくつかの要因に応じて容量をすべてのサーバーで使用できない可能性があります役に立ちません。

このような理由を表示するには、次の簡略化された図を検討してください。 各カラー ボックスでは、ミラー化されたデータのコピーを 1 つを表します。 たとえば、A、A のマークのボックス '、および ' は、同じデータのコピーを 3 つ。 サーバーのフォールト トレランスをこれらのコピーを優先する*する必要があります*別のサーバーに格納します。

### <a name="stranded-capacity"></a>孤立した容量

描画、Server 1 (10 TB) とサーバー 2 (10 TB) がいっぱいです。 サーバー 3 より大きなドライブを持つため、その合計容量が大きい (15 TB)。 ただし、3 のサーバーで 3 方向ミラーのより多くのデータを格納するが必要になります Server 1 と 2 のサーバー上のコピーも完全に属する。 サーバー 3 で残りの 5 TB の容量を使用することはできません: *「取り残された」* 容量。

![取り残された容量を 3 方向ミラー、3 台のサーバー](media/drive-symmetry-considerations/Size-Asymmetry-3N-Stranded.png)

### <a name="optimal-placement"></a>最適な配置

逆に、10 TB、10 TB、10 TB は、15 TB の容量と 3 方向ミラー回復性の 4 つのサーバーでその*は*をお持ちのお客様として描画されたすべての利用可能な容量を使用する方法でコピーを配置できます。 この方法が使用されるたびに、記憶域スペース ダイレクトのアロケーターは検索し、最適の配置を使用して、孤立した容量いない状態になります。

![3 方向ミラー、4 台のサーバーなしの孤立した容量](media/drive-symmetry-considerations/Size-Asymmetry-4N-No-Stranded.png)

サーバー、回復性、容量の不均衡、およびその他の要因の重要度の数は、孤立した容量があるかどうかに影響します。 **賢明な最も一般的な規則では、使用するのにはすべてのサーバーで使用可能な唯一の容量が保証されることを前提としています。**

## <a name="understand-cache-imbalance"></a>キャッシュの不均衡を理解するには:

記憶域スペース ダイレクトは堅牢なキャッシュの不均衡をドライブにわたって、複数のサーバーです。 不均衡が重大な場合でもすべてのものは引き続き機能します。 さらに、記憶域スペース ダイレクトは常に使用を最大限利用可能なすべてのキャッシュ。

ただし、さまざまなサイズのキャッシュ ドライブを使用していないパフォーマンスが向上キャッシュ一様に分布または予測どおり: IO を[バインドをドライブ](understand-the-cache.md#server-side-architecture)キャッシュ サイズのドライブにはパフォーマンスの向上も参照してください可能性があります。 記憶域スペース ダイレクト IO をバインディングに均等に分散し、キャッシュの容量の比率に基づいて区別しません。

![キャッシュの不均衡](media/drive-symmetry-considerations/Cache-Asymmetry.png)

   > [!TIP]
   > 参照してください[キャッシュについて](understand-the-cache.md)キャッシュ バインドの詳細を表示します。

## <a name="example-configurations"></a>構成の例

一部のサポートされているとサポートされていない構成を次に示します。

### <a name="supportedmediadrive-symmetry-considerationssupportedpng-supported-different-models-between-servers"></a>![サポート](media/drive-symmetry-considerations/supported.png) サーバー間で異なるモデルをサポートされています。

NVMe モデル"X"を使用して、最初の 2 つのサーバーが、3 番目のサーバーとよく似ている NVMe モデル"Z"を使用します。

| サーバー 1                    | サーバー 2                    | サーバー 3                    |
|-----------------------------|-----------------------------|-----------------------------|
| 2 倍の NVMe モデル X (キャッシュ)    | 2 倍の NVMe モデル X (キャッシュ)    | NVMe モデル Z x 2 (キャッシュ)    |
| 10 倍の SSD モデル Y (容量) | 10 倍の SSD モデル Y (容量) | 10 倍の SSD モデル Y (容量) |

サポートされています。

### <a name="supportedmediadrive-symmetry-considerationssupportedpng-supported-different-models-within-server"></a>![サポート](media/drive-symmetry-considerations/supported.png) サーバー内の別のモデルをサポートされています。

すべてのサーバーでは、"Y"および"Z"は非常に似ていますが、HDD モデルのいくつかの異なる組み合わせを使用します。 すべてのサーバーでは、合計 10 個の HDD があります。

| サーバー 1                   | サーバー 2                   | サーバー 3                   |
|----------------------------|----------------------------|----------------------------|
| 2 倍の SSD モデル X (キャッシュ)    | 2 倍の SSD モデル X (キャッシュ)    | 2 倍の SSD モデル X (キャッシュ)    |
| HDD モデル Y x 7 (容量) | 5 倍の HDD モデル Y (容量) | 1 x HDD モデル Y (容量) |
| 3 倍の HDD モデル Z (容量) | 5 倍の HDD モデル Z (容量) | HDD モデル Z x 9 (容量) |

サポートされています。

### <a name="supportedmediadrive-symmetry-considerationssupportedpng-supported-different-sizes-across-servers"></a>![サポート](media/drive-symmetry-considerations/supported.png) サーバー間でのさまざまなサイズのサポートされています。

4 TB HDD を使用して、最初の 2 つのサーバーが、3 番目のサーバーがほぼ 6 TB HDD を使用します。

| サーバー 1                | サーバー 2                | サーバー 3                |
|-------------------------|-------------------------|-------------------------|
| 800 GB NVMe (キャッシュ) x 2 | 800 GB NVMe (キャッシュ) x 2 | 800 GB NVMe (キャッシュ) x 2 |
| 4 × 4 TB HDD (容量) | 4 × 4 TB HDD (容量) | 4 x 6 TB の HDD (容量) |

これがサポートされますが、孤立した容量になります。

### <a name="supportedmediadrive-symmetry-considerationssupportedpng-supported-different-sizes-within-server"></a>![サポート](media/drive-symmetry-considerations/supported.png) サーバー内のさまざまなサイズのサポートされています。

すべてのサーバーでは、1.2 TB とよく似ています 1.6 TB SSD のいくつかの異なる組み合わせを使用します。 すべてのサーバーでは、合計 4 つの SSD を持っています。

| サーバー 1                 | サーバー 2                 | サーバー 3                 |
|--------------------------|--------------------------|--------------------------|
| 3 x 1.2 TB SSD (キャッシュ)   | 2 x 1.2 TB SSD (キャッシュ)   | 4 x 1.2 TB SSD (キャッシュ)   |
| 1 x 1.6 TB SSD (キャッシュ)   | 2 x 1.6 TB SSD (キャッシュ)   | -                        |
| 20 × 4 TB HDD (容量) | 20 × 4 TB HDD (容量) | 20 × 4 TB HDD (容量) |

サポートされています。

### <a name="unsupportedmediadrive-symmetry-considerationsunsupportedpng-not-supported-different-types-of-drives-across-servers"></a>![サポートされていない](media/drive-symmetry-considerations/unsupported.png) サポートされていません別の種類のサーバー間でのドライブ。

サーバー 1 が NVMe が、他のユーザーはありません。

| サーバー 1            | サーバー 2            | サーバー 3            |
|---------------------|---------------------|---------------------|
| 6 x NVMe (キャッシュ)    | -                   | -                   |
| -                   | 6 x SSD (キャッシュ)     | 6 x SSD (キャッシュ)     |
| 18 x HDD (容量) | 18 x HDD (容量) | 18 x HDD (容量) |

これはサポートされていません。 ドライブの種類が同じすべてのサーバーである必要があります。

### <a name="unsupportedmediadrive-symmetry-considerationsunsupportedpng-not-supported-different-number-of-each-type-across-servers"></a>![サポートされていない](media/drive-symmetry-considerations/unsupported.png) サポートされていません: サーバー間では、各型の別の数

サーバー 3 では、他よりも多くのドライブがあります。

| サーバー 1            | サーバー 2            | サーバー 3            |
|---------------------|---------------------|---------------------|
| 2 x NVMe (キャッシュ)    | 2 x NVMe (キャッシュ)    | 4 x NVMe (キャッシュ)    |
| 10 x HDD (容量) | 10 x HDD (容量) | 20 x HDD (容量) |

これはサポートされていません。 各種類のドライブの数は、すべてのサーバーで同じになります。

### <a name="unsupportedmediadrive-symmetry-considerationsunsupportedpng-not-supported-only-hdd-drives"></a>![サポートされていない](media/drive-symmetry-considerations/unsupported.png) サポートされていません: HDD ドライブのみ

すべてのサーバーでは、接続されている HDD ドライブのみがあります。

|サーバー 1|サーバー 2|サーバー 3|
|-|-|-| 
|18 x HDD (容量) |18 x HDD (容量)|18 x HDD (容量)|

これはサポートされていません。 2 つキャッシュ (NvME または SSD) に接続されたドライブの各サーバーの最小値を追加する必要があります。

## <a name="summary"></a>概要

要約すると、クラスター内のすべてのサーバーは、同じ種類のドライブと同じ数の各型が必要です。 混在 - ドライブのモデルとドライブのサイズを必要に応じて、上の考慮事項はサポートされています。

| 制約                               |               |
|------------------------------------------|---------------|
| 同じ種類のすべてのサーバーのドライブ     | **必須**  |
| すべてのサーバーの各型の同じ番号 | **必須**  |
| すべてのサーバーで同じドライブのモデル        | 推奨   |
| すべてのサーバーで同じドライブのサイズ         | 推奨   |

## <a name="see-also"></a>関連項目

- [記憶域スペース ダイレクトのハードウェア要件](storage-spaces-direct-hardware-requirements.md)
- [記憶域スペース ダイレクトの概要](storage-spaces-direct-overview.md)
