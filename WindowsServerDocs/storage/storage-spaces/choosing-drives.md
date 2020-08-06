---
ms.assetid: 1368bc83-9121-477a-af09-4ae73ac16789
title: 記憶域スペース ダイレクト用のドライブの選択
ms.prod: windows-server
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 07/01/2020
ms.localizationpriority: medium
ms.openlocfilehash: aae554c87b8a4ac6005ad359bc474026f5f1ed9e
ms.sourcegitcommit: acfdb7b2ad283d74f526972b47c371de903d2a3d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/05/2020
ms.locfileid: "87769410"
---
# <a name="choosing-drives-for-storage-spaces-direct"></a>記憶域スペース ダイレクト用のドライブの選択

>適用先:Windows Server 2019、Windows Server 2016

このトピックでは、パフォーマンスや容量の要件を満たすように[記憶域スペース ダイレクト](storage-spaces-direct-overview.md)でドライブを選ぶ方法のガイダンスについて説明します。

## <a name="drive-types"></a>ドライブの種類

記憶域スペース ダイレクトは現在、次の 4 種類のドライブで動作します。

<table>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/pmem-100px.png" alt="Image of PMem (persistent memory)">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>PMem</b> とは永続メモリを意味します。これは、低待機時間かつ高パフォーマンスの新しい種類の記憶域です。
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/NVMe-100px.png" alt="Image of NVMe (Non-Volatile Memory Express)">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>NVMe</b> (Non-Volatile Memory Express) とは、PCIe バスに直接接続されたソリッドステート ドライブを指します。 一般的なフォーム ファクターは、2.5 インチU.2、PCIe Add-In-Card (AIC)、および M.2 です。 NVMe は、永続メモリを除き、現在サポートされている他の種類のドライブよりも高い IOPS と IO スループットを提供します。
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px" >
            <img src="media/understand-the-cache/SSD-100px.png" alt="Image of SSD drive">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>SSD</b>は、従来の SATA または SAS 経由で接続するソリッドステートドライブを指します。
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/HDD-100px.png" alt="Image of HDD">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>Hdd</b>は、大量の記憶域容量を提供する、磁気ハードディスクドライブの回転を指します。
        </td>
    </tr>
</table>

## <a name="built-in-cache"></a>ビルトイン キャッシュ

記憶域スペース ダイレクトは、組み込みのサーバー側キャッシュを特徴とします。 これは、大容量で永続的な、リアルタイムの読み取りおよび書き込みキャッシュです。 複数の種類のドライブを使用するデプロイでは、"最速" の種類のすべてのドライブを使用するように自動的に構成されます。 残りのドライブは、キャパシティとして使用されます。

詳細については、「[記憶域スペース ダイレクトのキャッシュについて](understand-the-cache.md)」を参照してください。

## <a name="option-1--maximizing-performance"></a>オプション 1 – パフォーマンスの最大化

任意のデータに対するランダムな読み取りと書き込みの間で予測可能で統一されたサブミリ秒の待機時間を実現したり、非常に高い IOPS ( [600万](https://www.youtube.com/watch?v=0LviCzsudGY&t=28m)! 以上) または IO スループット ( [1 Tb/秒](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=16m50s)を超えて完了) を実現したりするには、"すべてのフラッシュ" を行う必要があります。

これを行うには、現在次の 3 つの方法があります。

![All-Flash-Deployment-Possibilities](media/choosing-drives-and-resiliency-types/All-Flash-Deployment-Possibilities.png)

1. **NVMe のみ。** NVMe のみを使用すると、最も予測可能な低待機時間を含む、比類のないパフォーマンスが得られます。 すべてのドライブが同じモデルの場合、キャッシュはありません。 耐久性の高い NVMe モデルと耐久性の低い NVMe モデルを混在させ、後者に対する書き込みをキャッシュするように前者を構成することもできます ([セットアップが必要です](understand-the-cache.md#manual-configuration))。

2. **NVMe + SSD。** NVMe を SSD とともに使用すると、NVMe によって SSD への書き込みが自動的にキャッシュされます。 これにより、書き込みがキャッシュ内で結合され、必要に応じてのみデステージングされるため、SSD の消耗が軽減されます。 これにより、 NVMe に似た書き込み特性が得られる一方で、読み取りは同じく高速な SSD から直接提供されます。

3. **SSD のみ。** NVMe のみの場合と同様に、すべてのドライブが同じモデルの場合、キャッシュはありません。 耐久性の高いモデルと耐久性の低いモデルを混在させる場合は、後者に対する書き込みをキャッシュするように前者を構成することができます ([セットアップが必要です](understand-the-cache.md#manual-configuration))。

   >[!NOTE]
   > キャッシュなしで NVMe のみまたは SSD のみを使用する利点は、すべてのドライブから使用可能なストレージ容量を取得できることです。 キャッシュに "費やされる" 容量がないため、小規模のスケールで有用である場合があります。

## <a name="option-2--balancing-performance-and-capacity"></a>オプション 2 – パフォーマンスと容量のバランスを取る

さまざまなアプリケーションやワークロードがあり、パフォーマンス要件が厳しい環境や、非常に多くのストレージ容量を必要とする環境では、大容量の HDD に対して NVMe または SSD キャッシュを使用して "ハイブリッド" にする必要があります。

![Hybrid-Deployment-Possibilities](media/choosing-drives-and-resiliency-types/Hybrid-Deployment-Possibilities.png)

1. **NVMe + HDD**。 NVMe ドライブは、読み取りと書き込みをキャッシュすることによって、その両方を高速化します。 読み取りのキャッシュにより、HDD は書き込みに集中することができます。 書き込みのキャッシュは、バーストを吸収し、必要な場合にのみ書き込みの結合とデステージングを可能にします。これは、HDD IOPS と IO スループットを最大化する、人為的にシリアル化された方法で行われます。 これにより、NVMe に似た書き込み特性が得られ、頻繁にまたは最近読み取られたデータに対して、NVMe に似た読み取り特性も得られます。

2. **SSD + HDD**。 上記と同様に、SSD は、読み取りと書き込みをキャッシュすることによって、その両方を高速化します。 これにより、SSD に似た書き込み特性と、頻繁にまたは最近読み取られたデータに対して、SSD に似た読み取り特性が得られます。

    "*3 つすべて*" の種類のドライブ使用するという、もう 1 つ別の特殊なオプションがあります。

3. **NVMe + SSD + HDD。** 3 つすべての種類のドライブを使用する場合は、NVMe ドライブで SSD とHDD の両方に対してキャッシュが提供されます。 ここでの魅力的な点は、SSD 上にボリュームを作成し、HDD 上にボリュームを作成し、それらを同じクラスター内に並置して、すべて NVMe によって高速化できることです。 前者は "オール フラッシュ" デプロイとまったく同じであり、後者は上記の "ハイブリッド" デプロイとまったく同じです。 これは概念的には、大部分が独立した容量管理、障害および修復サイクルなどを備えた 2 つのプールを持つようなものです。

   >[!IMPORTANT]
   > SSD 階層を使用して、最もパフォーマンス要件の厳しいワークロードをオール フラッシュに配置することをお勧めします。

## <a name="option-3--maximizing-capacity"></a>オプション 3 – 容量の最大化

アーカイブ、バックアップ対象、データ ウェアハウス、"コールド" ストレージなど、膨大な容量が必要で書き込み頻度が高くないワークロードでは、キャッシュ用のいくつかの SSD とデータ格納用の大容量 HDD を組み合わせてください。

![容量を最大化するためのデプロイ オプション](media/choosing-drives-and-resiliency-types/maximizing-capacity.png)

1. **SSD + HDD**。 SSD は、読み取りと書き込みをキャッシュしてバーストを吸収し、SSD に似た書き込みパフォーマンスを提供し、後で HDD に対する最適化されたデステージングを行います。

>[!IMPORTANT]
>HDD のみを使用した構成はサポートされていません。 耐久性の低い SSD に対する耐久性の高い SSD のキャッシュはお勧めしません。

## <a name="sizing-considerations"></a>サイズに関する考慮事項

### <a name="cache"></a>キャッシュ

各サーバーには、少なくとも 2 つのキャッシュ ドライブ (冗長性のために必要な最小値) が必要です。 容量ドライブの数は、キャッシュ ドライブの数の倍数にすることをお勧めします。 たとえば、4 台のキャッシュ ドライブがある場合、7 台や 9 台よりも 8 台の容量ドライブ (1:2 の比率) を使用した方がより一貫性のあるパフォーマンスを得ることができます。

キャッシュは、アプリケーションとワークロードのワーキングセット (つまり、特定の時点でアクティブに読み取りおよび書き込みを行っているすべてのデータ) に合わせてサイズ設定する必要があります。 それを超えるキャッシュ サイズの要件はありません。 Hdd を使用した展開では、1台のサーバーの容量が10% になります。たとえば、各サーバーに4× 4 TB HDD = 16 TB の容量がある場合は、サーバーあたり 2 x 800 GB SSD = 1.6 TB のキャッシュが必要です。 すべてのフラッシュデプロイ (特に非常に[耐久性の高い](https://techcommunity.microsoft.com/t5/storage-at-microsoft/understanding-ssd-endurance-drive-writes-per-day-dwpd-terabytes/ba-p/426024)ssd) では、容量の5% に近い状態にすることができます。たとえば、各サーバーに 24 x 1.2 tb SSD = 28.8 TB の容量がある場合は、サーバーあたり 2 x 750 GB NVMe = 1.5 tb のキャッシュを使用します。 キャッシュ ドライブは、後でいつでも追加または削除して調整できます。

### <a name="general"></a>全般

サーバーあたりの合計ストレージ容量は、約 400 テラバイト (TB) に制限することをお勧めします。 サーバーあたりのストレージ容量が大きいほど、ソフトウェア更新プログラムを適用する場合など、ダウンタイムや再起動後のデータの再同期に必要な時間が長くなります。 記憶域プールあたりの現在の最大サイズは、Windows Server 2019 の場合は4ペタバイト (PB) (4000 TB)、Windows Server 2016 の場合は1ペタバイトです。

## <a name="additional-references"></a>その他の参照情報

- [記憶域スペース ダイレクトの概要](storage-spaces-direct-overview.md)
- [記憶域スペース ダイレクトのキャッシュについて](understand-the-cache.md)
- [記憶域スペース ダイレクトのハードウェア要件](storage-spaces-direct-hardware-requirements.md)
- [記憶域スペース ダイレクトのボリュームの計画](plan-volumes.md)
- [フォールト トレランスとストレージの効率性](storage-spaces-fault-tolerance.md)
