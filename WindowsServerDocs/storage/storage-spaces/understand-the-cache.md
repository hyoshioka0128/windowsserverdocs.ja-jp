---
title: 記憶域スペース ダイレクトのキャッシュについて
ms.assetid: 69b1adc0-ee64-4eed-9732-0fb216777992
ms.prod: windows-server-threshold
ms.author: cosdar
ms.manager: dongill
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 07/18/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62fa33d08af25c424c786c10191fe6ae2b3d02bc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855513"
---
# <a name="understanding-the-cache-in-storage-spaces-direct"></a>記憶域スペース ダイレクトのキャッシュについて

>適用対象:Windows Server 2019、Windows Server 2016

[記憶域スペース ダイレクト](storage-spaces-direct-overview.md)には、記憶域のパフォーマンスを最大化するために組み込みのサーバー側キャッシュ機能が用意されています。 これは、大規模で永続的なリアルタイムの読み取り*および*書き込みキャッシュです。 記憶域スペース ダイレクトを有効にすると、このキャッシュが自動的に構成されます。 ほとんどの場合、何らかの手動管理が必要になることはありません。
キャッシュの動作は、存在するドライブの種類によって決まります。

次のビデオでは、記憶域スペース ダイレクトに対するキャッシュの動作に加え、その他の設計に関する考慮事項について説明します。

<strong>記憶域スペース ダイレクトの設計に関する考慮事項</strong><br>(20 分)<br>
<iframe src="https://channel9.msdn.com/Blogs/windowsserver/Design-Considerations-for-Storage-Spaces-Direct/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

## <a name="drive-types-and-deployment-options"></a>ドライブの種類と展開オプション

現在、記憶域スペース ダイレクトは、次の 3 種類の記憶装置で動作します。

<table>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/NVMe-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            NVMe (Non-Volatile Memory Express)
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/SSD-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            SATA/SAS SSD (ソリッドステート ドライブ)
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/HDD-100px.png">
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            HDD (ハード ディスク ドライブ)
        </td>
    </tr>
</table>

これらの組み合わせには 6 通りあり、"オールフラッシュ" と "ハイブリッド" の 2 つのカテゴリに分けられます。

### <a name="all-flash-deployment-possibilities"></a>オールフラッシュ展開の組み合わせ

オールフラッシュ展開では、記憶域のパフォーマンスを最大化することを目標とし、回転式のハード ディスク ドライブ (HDD) は含まれません。

![利用可能なオールフラッシュ展開](media/understand-the-cache/All-Flash-Deployment-Possibilities.png)

### <a name="hybrid-deployment-possibilities"></a>ハイブリッド展開の組み合わせ

ハイブリッド展開では、パフォーマンスと容量のバランスを保つこと、または容量を最大化することを目標とし、回転式ハード ディスク ドライブ (HDD) が含まれます。

![Hybrid-Deployment-Possibilities](media/understand-the-cache/Hybrid-Deployment-Possibilities.png)

## <a name="cache-drives-are-selected-automatically"></a>キャッシュ ドライブの自動選択

複数の種類のドライブが展開に存在する場合、記憶域スペース ダイレクトは、自動的に "最速" の種類のドライブをキャッシュとして使用します。 残りのドライブはデータ格納用に使われます。

どの種類が "最速" であるかは、次の順序に従って決定されます。

![Drive-Type-Hierarchy](media/understand-the-cache/Drive-Type-Hierarchy.png)

たとえば、NVMe と SSD がある場合は、NVMe が SSD のキャッシュになります。

SSD と HDD がある場合は、SSD が HDD のキャッシュになります。

   >[!NOTE]
   > キャッシュ ドライブは、使用可能な記憶域容量には含められません。 キャッシュに格納されているすべてのデータは、他の場所にも格納されているか、そうでない場合はステージング解除されるときに他の場所に格納されます。 つまり、展開内の生の記憶域容量の合計は、容量ドライブのみの合計値になります。

すべてのドライブの種類が同じ場合、キャッシュの自動構成は行われません。 手動で構成を行うと、耐久性の高いドライブを、同じ種類の耐久性の低いドライブのキャッシュとして使うことができます。構成方法については、「[手動構成](#manual)」セクションをご覧ください。

   >[!TIP]
   > すべて NVMe またはすべて SSD の展開では、特に規模が非常に小さい場合、キャッシュとして "消費" するドライブをなくした方が、記憶域の効率が大きく向上する可能性があります。

## <a name="cache-behavior-is-set-automatically"></a>キャッシュ動作の自動設定

キャッシュ動作は、キャッシュ対象のドライブの種類に基づいて自動的に決定されます。 ソリッドステート ドライブを対象とするキャッシュ (SSD 用の NVMe キャッシュなど) では、書き込みだけがキャッシュされます。 ハード ディスク ドライブを対象とするキャッシュ (HDD 用の SSD キャッシュなど) では、読み取りと書き込みの両方がキャッシュされます。

![Cache-Read-Write-Behavior](media/understand-the-cache/Cache-Read-Write-Behavior.png)

### <a name="write-only-caching-for-all-flash-deployments"></a>オールフラッシュ展開での書き込み専用キャッシュ

ソリッドステート ドライブ (NVMe または SSD) をキャッシュする場合は、書き込みだけがキャッシュされます。 これによって容量ドライブの劣化が軽減されます。つまり、多数の書き込みと再書き込みがキャッシュ内でまとめられ、必要時にのみステージング解除されるため、容量ドライブへの累積トラフィックが減り、容量ドライブの寿命を伸ばすことができます。 このような動作を考慮して、キャッシュには、[耐久性が高く、書き込み用に最適化された](http://whatis.techtarget.com/definition/DWPD-device-drive-writes-per-day)ドライブを選択することをお勧めします。 容量ドライブは、書き込みに対する耐久性が比較的低くてもかまいません。

読み取りはフラッシュの寿命に大きく影響しないことに加えて、ソリッドステート ドライブは一般に読み取り待機時間が短いため、読み取りはキャッシュされず、容量ドライブから直接行われます (データが最近書き込まれたためにまだステージング解除されていない場合は除きます)。 これにより、キャッシュ全体を書き込みのためだけに使用でき、キャッシュの効果が最大限に発揮されます。

この展開では、書き込み待機時間などの書き込み特性はキャッシュ ドライブによって決まり、読み取り特性は容量ドライブによって決まることになります。 どちらも一貫性があり、予測可能で定常的です。

### <a name="readwrite-caching-for-hybrid-deployments"></a>ハイブリッド展開での読み取り/書き込みキャッシュ

ハード ディスク ドライブ (HDD) をキャッシュする場合は、読み取り *と* 書き込みの両方がキャッシュされ、どちらについてもフラッシュと同様の待機時間 (多くの場合は最大 10 倍向上) が達成されます。 読み取りキャッシュには、最近読み取られたデータと頻繁に読み取られるデータが格納されます。これによって高速アクセスが実現され、HDD へのランダム トラフィックも最小限に抑えられます  (ためシークおよび回転の遅延、待機時間と HDD へのランダム アクセスによって発生した時間のロスは重要です。)書き込みは急増を吸収するキャッシュであり、以前と同様、coalesce を書き込みます再書き込みし、容量ドライブへの累積的なトラフィックを最小限に抑えます。

記憶域スペース ダイレクトには、書き込みをステージング解除する前にランダム化を解除するアルゴリズムが実装されています。これにより、ワークロード (仮想マシンなど) から生じた実際の IO がランダムであっても、ディスクに対する IO パターンはシーケンシャルになるようにエミュレートされます。 これで HDD の IOPS とスループットが最大限に引き出されます。

### <a name="caching-in-deployments-with-drives-of-all-three-types"></a>3 種類すべてのドライブを含む展開でのキャッシュ

3 種類すべてのドライブが存在する場合は、NVMe ドライブが SSD と HDD の両方のキャッシュを提供します。 動作は既に説明したとおりで、SSD に対しては書き込みだけがキャッシュされ、HDD に対しては読み取りと書き込みの両方がキャッシュされます。 HDD をキャッシュするための負荷は、キャッシュ ドライブ間で均等に分散されます。 

## <a name="summary"></a>概要

次の表は、それぞれの組み合わせの展開について、キャッシュとして使われるドライブ、容量として使われるドライブ、キャッシュ動作をまとめたものです。

| 展開       | キャッシュ ドライブ                        | 容量ドライブ | キャッシュ動作 (既定)                  |
|------------------|-------------------------------------|-----------------|-------------------------------------------|
| すべて NVMe         | なし (オプション: 手動構成) | NVMe            | 書き込みのみ (構成した場合)                |
| すべて SSD          | なし (オプション: 手動構成) | SSD             | 書き込みのみ (構成した場合)                |
| NVMe + SSD       | NVMe                                | SSD             | 書き込みのみ                                |
| NVMe + HDD       | NVMe                                | HDD             | 読み取りと書き込み                              |
| SSD + HDD        | SSD                                 | HDD             | 読み取りと書き込み                              |
| NVMe + SSD + HDD | NVMe                                | SSD + HDD       | HDD に対しては読み取りと書き込み、SSD に対しては書き込みのみ  |

## <a name="server-side-architecture"></a>サーバー側アーキテクチャ

キャッシュはドライブ レベルで実装されます。1 台のサーバー内の個々のキャッシュ ドライブは、同じサーバー内の 1 台以上の容量ドライブにバインドされます。

キャッシュは Windows ソフトウェア定義記憶域スタックの他の部分よりも下層に位置するため、記憶域スペースやフォールト トレランスといった概念を意識する必要はありません。 これは、"ハイブリッド" (一部はフラッシュ、一部はディスク) のドライブを作成して Windows に渡すようなものと考えることができます。 実際のハイブリッド ドライブと同様に、物理メディアの高速部分と低速部分をまたぐホット データとコールド データのリアルタイムの移動が外部から認識されることはほとんどありません。

記憶域スペース ダイレクトの回復性は少なくともサーバー レベルである (データ コピーは常に複数のサーバーに書き込まれ、サーバーごとに最大 1 つのコピーが保持される) ことから、キャッシュ内のデータにも、キャッシュに含まれていないデータと同等の回復性が与えられます。

![Cache-Server-Side-Architecture](media/understand-the-cache/Cache-Server-Side-Architecture.png)

たとえば、3 方向ミラーリングを使用する場合、データの 3 つのコピーが別々のサーバーに書き込まれます。これらは各サーバーのキャッシュに追加されます。 後でステージング解除されるかどうかに関係なく、コピーは常に 3 つ存在することになります。

## <a name="drive-bindings-are-dynamic"></a>動的なドライブ バインディング

キャッシュと容量ドライブのバインディングは、1:1 から 1:12 以上まで、どのような比率にもすることができます。 これは、スケール アップの実行時や障害の発生後など、ドライブが追加または取り外されたときに動的に調整されます。 このため、キャッシュ ドライブや容量ドライブは、いつでも必要に応じて個別に追加することが可能です。

![Dynamic-Binding](media/understand-the-cache/Dynamic-Binding.gif)

対象性を保つために、容量ドライブの数はキャッシュ ドライブの数の倍数にすることをお勧めします。 たとえば、4 台のキャッシュ ドライブがある場合は、容量ドライブが 7 台や 9 台ではなく 8 台 (1:2 の比率) の場合に、より均等なパフォーマンスが得られます。

## <a name="handling-cache-drive-failures"></a>キャッシュ ドライブの障害の処理

キャッシュ ドライブで障害が発生すると、まだステージング解除されていない書き込みはすべて*ローカル サーバーから*失われ、(他のサーバー上の) 他のコピーだけが存在する状態になります。 他のドライブで障害が発生した場合と同じように、記憶域スペースは、残っているコピーを参照して自動的に回復します。

失われたキャッシュ ドライブにバインドされている容量ドライブは、短時間だけ異常状態として表示されます。 キャッシュの再バインドが行われ (自動)、データの修復が完了すると (自動)、再び正常として表示されます。

このシナリオは、パフォーマンスを維持するためにはサーバーごとに少なくとも 2 台のキャッシュ ドライブが必要であることを示しています。

![Handling-Failure](media/understand-the-cache/Handling-Failure.gif)

その後、他のドライブを交換する場合と同じようにキャッシュ ドライブを交換できます。

   >[!NOTE]
   > 拡張カード (AIC) または M.2 フォーム ファクターの NVMe を安全に交換するには、電源を切る必要があることがあります。

## <a name="relationship-to-other-caches"></a>他のキャッシュとの関係

Windows ソフトウェア定義記憶域スタックには、関連のない他のキャッシュがいくつかあります。 例として、記憶域スペースのライト バック キャッシュや、クラスターの共有ボリューム (CSV) のメモリ内読み取りキャッシュがあります。

記憶域スペース ダイレクトでは、記憶域スペースのライト バック キャッシュは既定の動作から変更しないでください。 たとえば、**New-Volume** コマンドレットの **-WriteCacheSize** などのパラメーターは使わないでください。

CSV のキャッシュを使うかどうかは任意に選択できます。 記憶域スペース ダイレクトでは既定でオフになっていますが、このトピックで説明している新しいキャッシュと競合することはありません。 特定のシナリオでは、効果的なパフォーマンスの向上を見込める可能性があります。 詳しくは、[CSV キャッシュを有効にする方法に関する記事](https://blogs.msdn.microsoft.com/clustering/2013/07/19/how-to-enable-csv-cache/)をご覧ください。

## <a name="manual"></a> 手動による構成

ほとんどの展開では、手動構成は必要ありません。 必要になった場合は読み進めてください。

### <a name="specify-cache-drive-model"></a>キャッシュ ドライブ モデルの指定

すべて NVMe やすべて SSD の展開のようにすべてのドライブが同じ種類の展開では、書き込みに対する耐久性などの特性について、同じ種類のドライブ間の違いを Windows で自動的に識別することができないため、キャッシュは構成されません。

耐久性の高いドライブを使って同じ種類の耐久性の低いドライブをキャッシュするには、**Enable-ClusterS2D** コマンドレットの **-CacheDeviceModel** パラメーターに、キャッシュとして使用するドライブ モデルを指定します。 記憶域スペース ダイレクトを有効にすると、そのモデルのすべてのドライブがキャッシュとして使用されます。

   >[!TIP]
   > モデルの文字列は、**Get-PhysicalDisk** の出力に表示された文字列と一致させる必要があります。

####  <a name="example"></a>例

```
PS C:\> Get-PhysicalDisk | Group Model -NoElement

Count Name
----- ----
    8 FABRIKAM NVME-1710
   16 CONTOSO NVME-1520

PS C:\> Enable-ClusterS2D -CacheDeviceModel "FABRIKAM NVME-1710"
```

意図したドライブがキャッシュとして使用されていることを確かめるには、PowerShell で **Get-PhysicalDisk** を実行し、**Usage** プロパティが **"Journal"** になっていることを確認します。

### <a name="manual-deployment-possibilities"></a>手動展開で使用できる組み合わせ

手動構成では、次のような組み合わせの展開が可能になります。

![Exotic-Deployment-Possibilities](media/understand-the-cache/Exotic-Deployment-Possibilities.png)

### <a name="set-cache-behavior"></a>キャッシュ動作の設定

キャッシュの既定の動作はオーバーライドできます。 たとえば、オールフラッシュ展開でも読み取りをキャッシュするように設定することができます。 ただし、既定の動作がワークロードに適していないことが確かでない限り、動作を変更することはお勧めしません。

動作をオーバーライドするには、**Set-ClusterS2D** コマンドレットの **-CacheModeSSD** パラメーターと **-CacheModeHDD** パラメーターを使用します。 **CacheModeSSD** パラメーターは、ソリッドステート ドライブをキャッシュする場合のキャッシュ動作を設定します。 **CacheModeHDD** パラメーターは、ハード ディスク ドライブをキャッシュする場合のキャッシュ動作を設定します。 これは、記憶域スペース ダイレクトを有効にした後であればいつでも実行できます。

動作が設定されたかどうかを確認するには、**Get-ClusterS2D** を使用します。

#### <a name="example"></a>例

```
PS C:\> Get-ClusterS2D

CacheModeHDD : ReadWrite
CacheModeSSD : WriteOnly
...

PS C:\> Set-ClusterS2D -CacheModeSSD ReadWrite

PS C:\> Get-ClusterS2D

CacheModeHDD : ReadWrite
CacheModeSSD : ReadWrite
...
```

## <a name="sizing-the-cache"></a>キャッシュのサイズの設定

キャッシュは、アプリケーションやワークロードのワーキング セット (任意の時点でアクティブに読み取られているデータまたは書き込まれているデータ) を格納できるサイズに設定する必要があります。

これは、ハード ディスク ドライブを含むハイブリッド展開で特に重要になります。 アクティブなワーキング セットがキャッシュのサイズを超過した場合、またはアクティブなワーキング セットの変動が激しい場合、読み取りではキャッシュ ミスが増加し、書き込みではより積極的なステージング解除が必要となり、全体のパフォーマンスが低下します。

Windows の組み込みのパフォーマンス モニター (PerfMon.exe) ユーティリティを使うと、キャッシュ ミスの割合を調べることができます。 具体的には、**Cluster Storage Hybrid Disk** カウンター セットの **Cache Miss Reads/sec** を、展開の全体の読み取り IOPS と比較します。 各 "Hybrid Disk" は 1 台の容量ドライブに対応します。

たとえば、2 台のキャッシュ ドライブが 4 台の容量ドライブにバインドされている場合、サーバーごとに 4 つの "Hybrid Disk" オブジェクト インスタンスが存在することになります。

![Performance-Monitor](media/understand-the-cache/PerfMon.png)

普遍的な規則ではありませんが、読み取りのキャッシュ ミスが多すぎる場合は、キャッシュのサイズが不足している可能性があるため、キャッシュ ドライブを追加してキャッシュを拡張することを検討してください。 キャッシュ ドライブや容量ドライブは、いつでも個別に追加できます。

## <a name="see-also"></a>関連項目

- [ドライブと回復性の種類を選択します。](choosing-drives.md)
- [フォールト トレランスと記憶域の効率性](storage-spaces-fault-tolerance.md)
- [記憶域スペース ダイレクトのハードウェア要件](storage-spaces-direct-hardware-requirements.md)
