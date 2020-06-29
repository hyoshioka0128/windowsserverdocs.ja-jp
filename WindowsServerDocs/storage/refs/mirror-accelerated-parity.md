---
title: ミラーリングによって高速化されたパリティ
ms.prod: windows-server
ms.author: gawatu
manager: masriniv
ms.technology: storage-file-systems
ms.topic: article
author: gawatu
ms.date: 10/17/2018
ms.assetid: ''
ms.openlocfilehash: 3efbc6ae29ddaa4f3a4a4f2a2409bbeb87fec2ed
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475169"
---
# <a name="mirror-accelerated-parity"></a>ミラーリングによって高速化されたパリティ

>適用先:Windows Server 2019、Windows Server 2016

記憶域スペースは、2 つの基本的な手法 (ミラーおよびパリティ) を使ってデータのフォールト トレランスを提供できます。 [記憶域スペース ダイレクト](../storage-spaces/storage-spaces-direct-overview.md)では、ミラーリングによって高速化されたパリティが ReFS により導入されています。これにより、ミラーとパリティの両方の回復性を備えたボリュームを作成できます。 ミラーリングによって高速化されたパリティにより、パフォーマンスを犠牲にせずに安価で容量効率の高いストレージが実現します。

![ミラーリングによって高速化されたパリティ ボリューム](media/mirror-accelerated-parity/Mirror-Accelerated-Parity-Volume.png)

## <a name="background"></a>背景

ミラーとパリティの回復性スキームは、ストレージおよびパフォーマンス特性が根本的に異なっています。
- ミラーの回復性を使用すると、ユーザーは高速な書き込みパフォーマンスを得ることができますが、各コピーのデータをレプリケートするのは領域の効率が悪くなります。
- 一方、パリティは書き込みごとにパリティを再計算する必要があるため、ランダム書き込みのパフォーマンスという弱点があります。 一方、パリティではユーザーがスペース効率よくデータを格納できます。 詳細については、「[記憶域スペースのフォールトトレランス](../storage-spaces/Storage-Spaces-Fault-Tolerance.md)」を参照してください。

したがって、ミラーはパフォーマンス重視のストレージが実現する傾向がありますが、パリティはストレージ容量の使用率を上げることができます。 ミラーリングによって高速化されたパリティでは、1 つのボリューム内で両方の回復性スキームを組み合わせることにより、ReFS がそれぞれの回復性の種類のメリットを生かして容量効率が高くパフォーマンスも重視したストレージが実現します。

## <a name="data-rotation-on-mirror-accelerated-parity"></a>ミラーリングによって高速化されたパリティにおけるデータのローテーション

ReFS は、ミラーとパリティの間でデータをリアルタイムでアクティブにローテーションします。 これにより、入力書き込みをミラーにすばやく書き込んだ後、パリティーにローテーションして効率的に格納することができます。 こうすることで、入力 IO がミラーですばやく処理される一方、コールド データはパリティに効率的に格納されるため、同じボリューム内で最適なパフォーマンスと低コストのストレージの両方が実現します。

ミラーおよびパリティ間でデータをローテーションするため、ReFS はボリュームを 64 MiB の領域 (ローテーションの単位) に論理的に分割します。 以下の図は、領域に分割された、ミラーリングによって高速化されたパリティ ボリュームを示しています。

![ミラーリングによって拘束されたパリティ ボリュームとストレージ コンテナー](media/mirror-accelerated-parity/Mirror-Accelerated-Parity-Volume-with-Storage-Containers.png)

ReFS は、ミラー層が指定された容量レベルに達すると、領域全体のミラーからパリティへのローテーションを開始します。 データをミラーからパリティにすぐに移動する代わりに、ReFS はできる限り長く待機してデータをミラーに保持し、データの最適なパフォーマンスを維持できるようにします (以下の「IO パフォーマンス」をご覧ください)。

データがミラーからパリティに移動するとき、データが読み取られ、パリティ エンコーディングが計算された後、そのデータがパリティに書き込まれます。 次の図は、ローテーション中にイレイジャー コーディングに変換される、3 方向にミラーリングされた領域を使ってこれを示しています。

![ミラーリングによって高速化されたパリティのローテーション](media/mirror-accelerated-parity/Container-Rotation.gif)

## <a name="io-on-mirror-accelerated-parity"></a>ミラーリングによって高速化されたパリティでの IO
### <a name="io-behavior"></a>IO の動作
**書き込み:** ReFS は入力書き込みを 3 つの異なる方法で処理します。

1.  **ミラーに書き込み:**

    - **1a.** 入力書き込みによってミラーの既存のデータが変更される場合、ReFS は所定の位置のデータを変更します。
    - **1b.** 入力書き込みが新しい書き込みのであり、この書き込みをサービスするのに十分な領域を ReFS がミラーで見つけることができた場合、ReFS はミラーに書き込みます。
    ![ミラーに書き込み](media/mirror-accelerated-parity/Write-to-Mirror.png)

2. **ミラーに書き込み、パリティから再割り当て:**

    受信書き込みによってパリティ内のデータが変更され、ReFS が受信書き込みを処理するのに十分な空き領域をミラーに正しく検出できた場合、ReFS はまずパリティ内の以前のデータを無効にしてから、ミラーに書き込みます。 この無効化は、高速でコストのかからないメタデータ操作であるため、パリティへの書き込みパフォーマンスが大幅に向上します。
    ![再割り当てされた書き込み](media/mirror-accelerated-parity/Reallocated-Write.png)

3. **パリティに書き込み:**

    ReFS がミラーで十分な空き領域を見つけることができない場合、ReFS はパリティに新しいデータを書き込むか、パリティの既存のデータを直接変更します。 以下の「パフォーマンスの最適化」セクションでは、パリティへの書き込みを最小限に抑えるためのガイダンスを示します。
    ![パリティに書き込み](media/mirror-accelerated-parity/Write-to-Parity.png)

**読み取り:** ReFS は関連するデータを含む階層から直接読み取ります。 パリティが HDD で構築されている場合、今後の読み取りを高速化するため、記憶域スペース内のキャッシュにこのデータがキャッシュされます。

> [!NOTE]
> 読み取りの結果、ReFS がデータをミラー層に再度ローテーションすることはありません。

### <a name="io-performance"></a>IO パフォーマンス

**書き込み:** 前述の書き込みの種類ごとにパフォーマンス特性が異なります。 大まかに言うと、ミラー層への書き込みは再割り当てられた書き込みよりある程度高速であり、再割り当てられた書き込みはパリティ層への直接書き込みよりかなり高速です。 この関係を以下の不等式で示します。


- **ミラー層 > 再割り当てした書き込み >> パリティ層**


**読み取り:** パリティから読み取っても、パフォーマンスに大きな悪影響はありません。
- ミラーおよびパリティが同じメディアの種類で構築されている場合、読み取りのパフォーマンスは同じになります。
- ミラーおよびパリティが異なるメディアの種類で構築されている場合 (ミラーリング SSD とパリティ HDD など)、[記憶域スペース ダイレクトのキャッシュ](../storage-spaces/understand-the-cache.md)にホット データをキャッシュしてパリティからの読み取りを高速化できます。

## <a name="refs-compaction"></a>ReFS の圧縮

この秋の半年単位のリリースでは、ReFS によって圧縮が導入されています。これにより、90以上のミラーアクセラレータパリティボリュームのパフォーマンスが大幅に向上します。

**バック グラウンド:** 以前は、ミラーリングによって高速化されたパリティ ボリュームがいっぱいになると、これらのボリュームのパフォーマンスが低下することがありました。 時間が経過するとボリューム全体でホット データとコールド データが混在するため、パフォーマンスが低下します。 つまり、ホット データが使用できるミラー内の領域をコールド データが占有するため、ミラーに格納できるホット データが少なくなります。 ミラーへの直接書き込みは再割り当てされた書き込みよりある程度高速で、パリティへの直接書き込みより数桁高速なため、高いパフォーマンスを維持するには、ホット データをミラーに格納することが重要です。 したがって、コールド データをミラーに格納すると、ReFS がミラーに直接書き込むことができる可能性が下がるため、パフォーマンス上よくありません。

ReFS の圧縮は、ホット データ用にミラー内の領域を解放することでこのようなパフォーマンスの問題に対処します。 圧縮ではまずすべてのデータが (ミラーとパリティの両方から) パリティに統合されます。 これによって、ボリューム内の断片化が軽減され、ミラーのアドレス指定可能な領域の量が増加します。 最も重要な点として、この処理により ReFS がホット データをミラーにもう一度統合することができます。
-   新しい書き込みが発生すると、ミラーで処理されます。 したがって、新しく書き込まれたホット データはミラーに格納されます。
-   パリティ内のデータに変更書き込みが行われると、ReFS は再割り当てされた書き込みを行うため、この書き込みはミラーでも処理されます。 その結果、圧縮時にパリティに移動されたホット データはミラーにもう一度再割り当てされます。

## <a name="performance-optimizations"></a>パフォーマンスの最適化

>[!IMPORTANT]
> 書き込みが多い Vhd を異なるサブディレクトリに配置することをお勧めします。 これは、ReFS が、ディレクトリとそのファイルのレベルでメタデータの変更を書き込むためです。 そのため、ディレクトリ間で書き込み負荷の高いファイルを配布すると、メタデータ操作のサイズが小さくなり、並列に実行されるため、アプリの待機時間が短縮されます。

### <a name="performance-counters"></a>パフォーマンス カウンター

ReFS には、ミラーリングによって高速化されたパリティのパフォーマンスを評価できるようにパフォーマンス カウンターが保持されています。
- 前述の「パリティへの書き込み」セクションで説明したように、ミラーリングの空き領域が見つからない場合、ReFS はパリティに直接書き込まれます。 一般に、これはミラーリングされた階層が早くいっぱいになって ReFS がデータをパリティにローテーションできないときに発生します。 つまり、ReFS のローテーションが取り込み速度に追いつかない場合です。 以下のパフォーマンス カウンターは、ReFS がいつパリティに直接書き込むかを識別します。

  ```
  # Windows Server 2016
  ReFS\Data allocations slow tier/sec
  ReFS\Metadata allocations slow tier/sec

  # Windows Server 2019
  ReFS\Allocation of Data Clusters on Slow Tier/sec
  ReFS\Allocation of Metadata Clusters on Slow Tier/sec
  ```

- これらのカウンターが 0 以外の場合、ReFS がデータをミラーからローテーションする速度が十分でないことを示します。 これを軽減するには、ローテーションの積極性を変更するか、ミラーリングされた階層のサイズを大きくすることができます。

### <a name="rotation-aggressiveness"></a>ローテーション強度

ReFS は、ミラーが指定された容量しきい値に達するとデータのローテーションを開始します。
-   このローテーションしきい値が大きいほど、ReFS はミラー層に長くデータを保持できます。 ホット データをミラー層に残しておくとパフォーマンス上は最適ですが、ReFS は大量の入力 IO を効率的に処理できません。
-   値を小さくすると、ReFS がデータを積極的にデステージでき、取り込み入力 IO が向上します。 これは、アーカイブ ストレージなど、取り込み量が多いワークロードに当てはまります。 ただし、一般的な用途のワークロードの場合、値を小さくするとパフォーマンスが低下する可能性があります。 ミラー層からデータを不必要にローテーションすると、パフォーマンスが低下します。

ReFS には、このしきい値を調整するための調整可能なパラメーターが導入されており、レジストリ キーを使って構成できます。 このレジストリ キーは、**記憶域スペース ダイレクト展開内の各ノード**で構成する必要があり、変更を有効にするには再起動が必要です。
-   **キー:** HKEY_LOCAL_MACHINE\System\CurrentControlSet\Policies
-   **ValueName (DWORD):** DataDestageSsdFillRatioThreshold
-   **ValueType:** 割合

このレジストリ キーが設定されていない場合、ReFS は 85% の既定値を使います。  この既定値はほとんどの展開に推奨され、50% 未満の値は推奨されません。 次の PowerShell コマンドは、値を 75% にしてこのレジストリ キーを設定する方法を示しています。
```PowerShell
Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Policies -Name DataDestageSsdFillRatioThreshold -Value 75
 ```
 記憶域スペース ダイレクトの展開で、各ノード間でこのレジストリ キーを構成するには、次の PowerShell コマンドを使用できます。
 ```PowerShell
 $Nodes = 'S2D-01', 'S2D-02', 'S2D-03', 'S2D-04'
 Invoke-Command $Nodes {Set-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Policies -Name DataDestageSsdFillRatioThreshold -Value 75}
 ```

### <a name="increasing-the-size-of-the-mirrored-tier"></a>ミラー化された層のサイズを増やす

ミラーリングされた階層のサイズを増やすと、ReFS が大きいワーキング セットをミラーに保持できるようになります。 これにより、ReFS がミラーに直接書き込むことができる可能性が高まるため、パフォーマンスの向上に貢献します。 次の PowerShell コマンドレットは、ミラーリングされた階層のサイズを増やす方法を示しています。
```PowerShell
Resize-StorageTier -FriendlyName “Performance” -Size 20GB
Resize-StorageTier -InputObject (Get-StorageTier -FriendlyName “Performance”) -Size 20GB
```
>[!TIP]
>**StorageTier** のサイズを変更したら、**Partition** と **Volume** のサイズを変更していることを確認します。 詳細と例については、「[Resize-Volumes](../storage-spaces/resize-volumes.md)」を参照してください。

## <a name="creating-a-mirror-accelerated-parity-volume"></a>ミラーリングによって高速化されたパリティ ボリュームを作成する

次の PowerShell コマンドレットは、ミラー:パリティ比が 20:80 (ほとんどのワークロードに推奨) のミラーリングによって高速化されたパリティ ボリュームを作成します。 詳細と例については、「[記憶域スペース ダイレクトのボリュームの作成](../storage-spaces/Create-volumes.md)」をご覧ください。

```PowerShell
New-Volume – FriendlyName “TestVolume” -FileSystem CSVFS_ReFS -StoragePoolFriendlyName “StoragePoolName” -StorageTierFriendlyNames Performance, Capacity -StorageTierSizes 200GB, 800GB
```

## <a name="additional-references"></a>その他のリファレンス

-   [ReFS の概要](refs-overview.md)
-   [ReFS のブロックの複製](block-cloning.md)
-   [ReFS 整合性ストリーム](integrity-streams.md)
-   [記憶域スペースダイレクトの概要](../storage-spaces/storage-spaces-direct-overview.md)
