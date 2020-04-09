---
ms.assetid: 1368bc83-9121-477a-af09-4ae73ac16789
title: 記憶域スペース ダイレクト用のドライブの選択
ms.prod: windows-server
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 09/19/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8c623049c33e02dd99974723d4cd257ca9304219
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80859005"
---
# <a name="choosing-drives-for-storage-spaces-direct"></a>記憶域スペース ダイレクト用のドライブの選択

>適用対象: Windows 2019、Windows Server 2016

このトピックでは、パフォーマンスや容量の要件を満たすように[記憶域スペース ダイレクト](storage-spaces-direct-overview.md)でドライブを選ぶ方法のガイダンスについて説明します。

## <a name="drive-types"></a>ドライブの種類

現在、記憶域スペース ダイレクトは、次の 3 種類のドライブで動作します。

<table>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/NVMe-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>NVMe</b> (Non-Volatile Memory Express) は、PCIe バスに直接取り付けられるソリッドステート ドライブです。 一般的なフォーム ファクターは、2.5" U.2、PCIe アドイン カード (AIC)、および M.2 です。 NVMe は、現在サポートされている他の種類のドライブと比較すると、より短い待機時間で、より高い IOPS と IO スループットを実現します。
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px" >
            <img src="media/understand-the-cache/SSD-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>SSD</b> は、従来の SATA または SAS 経由で接続されるソリッドステート ドライブです。
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/HDD-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            <b>HDD</b> は、膨大な記憶域容量を提供する、回転式の磁気ハード ディスク ドライブです。
        </td>
    </tr>
</table>

## <a name="built-in-cache"></a>組み込みのキャッシュ

記憶域スペース ダイレクトには、組み込みのサーバー側キャッシュが装備されています。 これは、大規模で永続的なリアルタイムの読み取りおよび書き込みキャッシュです。 複数の種類のドライブが存在する展開では、"最速" の種類のすべてのドライブを自動的に使うように構成されます。 残りのドライブはデータ格納用に使われます。

詳しくは、「[記憶域スペース ダイレクトのキャッシュについて](understand-the-cache.md)」をご覧ください。

## <a name="option-1--maximizing-performance"></a>オプション 1 – パフォーマンスを最大化する

データに対するランダムな読み取りや書き込みで一定した予測可能なサブミリ秒の待機時間を実現する場合、または非常に高い IOPS (弊社では [600 万を超える](https://www.youtube.com/watch?v=0LviCzsudGY&t=28m) IOPS を記録) や IO スループット (弊社では [1 秒あたり 1 TB を超える](https://www.youtube.com/watch?v=-LK2ViRGbWs&t=16m50s) IO スループットを記録) を実現する場合に、"オールフラッシュ" を採用してください。

この展開を行うには、現在 3 つの方法があります。

![利用可能なオールフラッシュ展開](media/choosing-drives-and-resiliency-types/All-Flash-Deployment-Possibilities.png)

1. **すべての NVMe。** すべて NVMe の展開を使用すると、優れたパフォーマンスが実現され、予測可能な待機時間が最も短くなります。 すべてのドライブが同じモデルである場合、キャッシュはありません。 耐久性が高い NVMe モデルと耐久性が低い NVMe モデルを組み合わせ、耐久性が高い NVMe モデルを、耐久性が低い NVMe モデルに対する書き込みをキャッシュするように構成することもできます ([セットアップが必要です](understand-the-cache.md#manual-configuration))。

2. **NVMe + SSD。** NVMe を SSD と共に使用すると、NVMe は SSD への書き込みを自動的にキャッシュします。 これにより、書き込みをキャッシュにまとめ、必要な場合にのみステージングを解除して、SSD の摩耗を減らすことができます。 この展開には NVMe と同様な書き込み特性があり、読み取りは高速な SSD で直接処理されます。

3. **すべての SSD。** すべて NVMe の展開と同様に、すべてのドライブが同じモデルである場合は、キャッシュはありません。 耐久性が高いモデルと耐久性が低いモデルを組み合わせた場合、耐久性が高い NVMe モデルを、耐久性が低い NVMe モデルに対する書き込みをキャッシュするように構成することができます ([セットアップが必要です](understand-the-cache.md#manual-configuration))。

   >[!NOTE]
   > すべて NVMe の展開やすべて SSD の展開にはキャッシュがありませんが、その利点は、使用可能な記憶域容量をすべてのドライブから取得できることです。 キャッシュで "消費される" 容量がないため、場合によっては、小規模な環境に適しています。

## <a name="option-2--balancing-performance-and-capacity"></a>オプション 2 – パフォーマンスと容量のバランスを取る

さまざまなアプリケーションやワークロードを利用している環境では、厳密なパフォーマンス要件がある場合と、膨大な記憶域容量が必要になる場合があるため、大容量の HDD のキャッシュに NVMe または SSD を使う "ハイブリッド" を採用してください。

![Hybrid-Deployment-Possibilities](media/choosing-drives-and-resiliency-types/Hybrid-Deployment-Possibilities.png)

1. **NVMe + HDD**。 NVMe ドライブによって、読み取りと書き込みの両方がキャッシュされ、読み取りと書き込みの速度が上がります。 読み取りをキャッシュすることで、HDD では書き込みが重視されます。 書き込みをキャッシュすると、バーストが吸収されます。また、HDD の IOPS や IO スループットを最大化するために人為的にシリアル化された方法で書き込みをキャッシュにまとめ、必要な場合にのみステージングを解除することができます。 この展開には NVMe と同様な書き込み特性があります。また、頻繁に読み取られるデータや最近読み取られたデータに対しては、NVMe と同様な読み取り特性による効果が発揮されます。

2. **SSD + HDD**。 上記と同様に、SSD によって、読み取りと書き込みの両方がキャッシュされ、読み取りと書き込みの速度が上がります。 この展開には SSD と同様な書き込み特性があります。また、頻繁に読み取られるデータや最近読み取られたデータに対しては、SSD と同様な読み取り特性による効果が発揮されます。

    上記の展開のほかに、*3 種類すべて*のドライブを使用するという、特殊な方法があります。

3. **NVMe + SSD + HDD。** 3 種類すべてのドライブを使用します。NVMe ドライブは SSD と HDD の両方のキャッシュを行います。 この展開の特徴は、SSD 上のボリュームと HDD 上のボリュームを同じクラスター内で並列に作成できることです。また、これらすべてのボリュームは NVMe によって高速化されます。 この場合、SSD 上のボリュームは "オールフラッシュ" 展開と完全に同じであり、HDD 上のボリュームは上で説明した "ハイブリッド" 展開と完全に同じです。 これは概念的には、ほとんどが独立して機能する容量管理や、障害と修復のサイクルなどを備えた 2 つプールの使うようなものです。

   >[!IMPORTANT]
   > SSD 階層を使って、パフォーマンスを最も重視するワークロードをオールフラッシュに配置することをお勧めします。

## <a name="option-3--maximizing-capacity"></a>オプション 3 – 容量を最大化する

アーカイブ、バックアップ対象、データ ウェアハウス、"コールド" ストレージなど、膨大な容量が必要で書き込み頻度が高くないワークロードでは、キャッシュ用のいくつかの SSD とデータ格納用の大容量 HDD を組み合わせてください。

![容量を最大化するための展開オプション](media/choosing-drives-and-resiliency-types/maximizing-capacity.png)

1. **SSD + HDD**。 SSD が読み取りと書き込みをキャッシュし、バーストが吸収され、SSD と同様の書き込みパフォーマンスが実現されます。また、HDD に対するステージング解除が後で最適化されます。

>[!IMPORTANT]
>Hdd のみを使用した構成はサポートされていません。 高耐久性な Ssd キャッシュを低耐久性の Ssd にキャッシュすることはお勧めしません。

## <a name="sizing-considerations"></a>サイズ設定に関する考慮事項

### <a name="cache"></a>キャッシュ

すべてのサーバーには、少なくとも 2 台のキャッシュ ドライブ (冗長性を確保するために必要な最小台数) が必要です。 データ格納用ドライブの数は、キャッシュ ドライブの数の倍数にすることをお勧めします。 たとえば、4 台のキャッシュ ドライブがある場合は、容量ドライブが 7 台や 9 台ではなく 8 台 (1:2 の比率) の場合に、より一貫したパフォーマンスが得られます。

キャッシュは、アプリケーションとワークロードのワーキングセット (つまり、特定の時点でアクティブに読み取りおよび書き込みを行っているすべてのデータ) に合わせてサイズ設定する必要があります。 キャッシュのサイズについては、それ以外の要件はありません。 Hdd を使用した展開では、1台のサーバーの容量が10% になります。たとえば、各サーバーに4× 4 TB HDD = 16 TB の容量がある場合は、サーバーあたり 2 x 800 GB SSD = 1.6 TB のキャッシュが必要です。 すべてのフラッシュデプロイ (特に非常に[耐久性の高い](https://blogs.technet.microsoft.com/filecab/2017/08/11/understanding-dwpd-tbw/)ssd) では、容量の5% に近い状態にすることができます。たとえば、各サーバーに 24 x 1.2 tb SSD = 28.8 TB の容量がある場合は、サーバーあたり 2 x 750 GB NVMe = 1.5 tb のキャッシュを使用します。 キャッシュ ドライブは、いつでも追加または取り外して、後で調整することができます。

### <a name="general"></a>全般

サーバーごとのストレージ容量の合計を約400テラバイト (TB) に制限することをお勧めします。 サーバーごとの記憶域容量がこれよりも多くなると、ソフトウェア更新プログラムを適用する場合など、ダウンタイムや再起動の後でデータを再同期する際に必要となる時間が長くなります。 記憶域プールあたりの現在の最大サイズは、Windows Server 2019 の場合は4ペタバイト (PB) (4000 TB)、Windows Server 2016 の場合は1ペタバイトです。

## <a name="see-also"></a>参照

- [記憶域スペースダイレクトの概要](storage-spaces-direct-overview.md)
- [記憶域スペースダイレクトのキャッシュについて](understand-the-cache.md)
- [ハードウェア要件の記憶域スペースダイレクト](storage-spaces-direct-hardware-requirements.md)
- [記憶域スペースダイレクトのボリュームの計画](plan-volumes.md)
- [フォールト トレランスと記憶域の効率](storage-spaces-fault-tolerance.md)
