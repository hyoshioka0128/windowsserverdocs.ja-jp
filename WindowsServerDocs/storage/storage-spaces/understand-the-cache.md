---
title: 記憶域スペース ダイレクトのキャッシュについて
ms.assetid: 69b1adc0-ee64-4eed-9732-0fb216777992
ms.author: cosdar
manager: dongill
ms.topic: article
author: cosmosdarwin
ms.date: 07/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: 315b645cf3c2adc60bd8eeed0406e1226b2d2128
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87968849"
---
# <a name="understanding-the-cache-in-storage-spaces-direct"></a>記憶域スペース ダイレクトのキャッシュについて

>適用先:Windows Server 2019、Windows Server 2016

[記憶域スペース ダイレクト](storage-spaces-direct-overview.md)は、記憶域のパフォーマンスを最大化する組み込みのサーバー側キャッシュを特徴とします。 これは、大容量で永続的な、リアルタイムの読み取り "*および*" 書き込みキャッシュです。 キャッシュは、記憶域スペース ダイレクトが有効になっている場合は自動的に構成されます。 ほとんどの場合、手動管理は一切必要ありません。
キャッシュの動作方法は、存在するドライブの種類によって異なります。

次のビデオでは、記憶域スペース ダイレクトにおけるキャッシュのしくみと、その他の設計上の考慮事項について詳しく説明しています。

<strong>記憶域スペース ダイレクトの設計に関する考慮事項</strong><br>(20 分)<br>
<iframe src="https://channel9.msdn.com/Blogs/windowsserver/Design-Considerations-for-Storage-Spaces-Direct/player" width="960" height="540" allowFullScreen frameBorder="0"></iframe>

## <a name="drive-types-and-deployment-options"></a>ドライブの種類とデプロイ オプション

現在、記憶域スペース ダイレクトは、次の 3 種類の記憶装置で動作します。

<table>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/NVMe-100px.png" alt="Image of NVMe (Non-Volatile Memory Express)" >
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            NVMe (Non-Volatile Memory Express)
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/SSD-100px.png" alt="Image of SSD" >
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            SATA/SAS SSD (ソリッドステート ドライブ)
        </td>
    </tr>
    <tr style="border: 0;">
        <td style="padding: 10px; border: 0; width:70px">
            <img src="media/understand-the-cache/HDD-100px.png"alt="Image of HDD" >
        </td>
        <td style="padding: 10px; border: 0;" valign="middle">
            HDD (ハード ディスク ドライブ)
        </td>
    </tr>
</table>

これらの組み合わせには 6 通りあり、"オールフラッシュ" と "ハイブリッド" の 2 つのカテゴリに分けられます。

### <a name="all-flash-deployment-possibilities"></a>オールフラッシュ デプロイの可能性

オールフラッシュ型のデプロイは、ストレージのパフォーマンスを最大化することを目標としたものであり、回転式のハード ディスク ドライブ (HDD) が含まれません。

![オールフラッシュ デプロイの可能性](media/understand-the-cache/All-Flash-Deployment-Possibilities.png)

### <a name="hybrid-deployment-possibilities"></a>ハイブリッド デプロイの可能性

ハイブリッド型のデプロイは、パフォーマンスとキャパシティのバランスの調和またはキャパシティの最大化を目標としたもので、回転式のハード ディスク ドライブ (HDD) が含まれます。

![ハイブリッド デプロイの可能性](media/understand-the-cache/Hybrid-Deployment-Possibilities.png)

## <a name="cache-drives-are-selected-automatically"></a>キャッシュ ドライブが自動的に選択される

複数の種類のドライブがあるデプロイでは、記憶域スペース ダイレクトにより "最も高速" な種類のドライブが自動的にキャッシュとして使用されます。 残りのドライブは、キャパシティとして使用されます。

どの種類が "最も高速" であるかは、次の階層に従って決定されます。

![ドライブの種類の階層](media/understand-the-cache/Drive-Type-Hierarchy.png)

たとえば、NVMe と SSD がある場合、NVMe は SSD のキャッシュとして使用されます。

SSD と HDD がある場合、SSD が HDD のキャッシュとして使用されます。

   >[!NOTE]
   > キャッシュ ドライブは、使用可能な記憶域容量には含まれません。 キャッシュに格納されているすべてのデータは、他の場所にも格納されているか、またはデステージされると格納されます。 つまり、デプロイの未加工の合計記憶域容量は、お使いの容量ドライブの合計のみです。

すべてのドライブが同じ種類である場合、キャッシュは自動的に構成されません。 手動で構成を行うと、耐久性の高いドライブを、同じ種類の耐久性の低いドライブのキャッシュとして使うことができます。構成方法については、「[手動構成](#manual-configuration)」セクションをご覧ください。

   >[!TIP]
   > NVMe のみまたは SSD のみのデプロイでは、非常に小規模な場合は特に、キャッシュに "費やす" ドライブをなくすことで、記憶域の効率を有意に向上できます。

## <a name="cache-behavior-is-set-automatically"></a>キャッシュ動作が自動的に設定される

キャッシュの動作は、キャッシュの対象となるドライブの種類に応じて自動的に決まります。 キャッシュの対象がソリッドステート ドライブの場合 (SSD のキャッシュを NVMe に保存する場合など) には、書き込みのみがキャッシュに保存されます。 キャッシュの対象がハード ディスク ドライブの場合 (HDD のキャッシュを SSD に保存する場合など) には、読み取りと書き込みの両方がキャッシュに保存されます。

![キャッシュの読み取りと書き込みの動作](media/understand-the-cache/Cache-Read-Write-Behavior.png)

### <a name="write-only-caching-for-all-flash-deployments"></a>オールフラッシュ デプロイ用の書き込み専用キャッシュ

キャッシュの対象がソリッドステート ドライブの場合 (NVMe または SSD) には、書き込みのみがキャッシュに保存されます。 これによって容量ドライブの劣化が軽減されます。つまり、多数の書き込みと再書き込みがキャッシュ内でまとめられ、必要時にのみステージング解除されるため、容量ドライブへの累積トラフィックが減り、容量ドライブの寿命を伸ばすことができます。 このため、[耐久性に優れ、書き込みが最適化された](http://whatis.techtarget.com/definition/DWPD-device-drive-writes-per-day)ドライブをキャッシュとして選択することをお勧めします。 容量ドライブでは、書き込みの耐久性が低い可能性があります。

読み取りはフラッシュの寿命に大きく影響しないことに加えて、ソリッドステート ドライブは一般に読み取り待機時間が短いため、読み取りはキャッシュされず、容量ドライブから直接行われます (データが最近書き込まれたためにまだステージング解除されていない場合は除きます)。 これにより、キャッシュを完全に書き込み専用にし、その有効性を最大限に高めることができます。

この展開では、書き込み待機時間などの書き込み特性はキャッシュ ドライブによって決まり、読み取り特性は容量ドライブによって決まることになります。 どちらも一貫性を持ち、予測可能性であり、一様です。

### <a name="readwrite-caching-for-hybrid-deployments"></a>ハイブリッド デプロイの読み取り/書き込みキャッシュ

キャッシュの対象がハード ディスク ドライブ (HDD) の場合には、読み取りと書き込みのどちらにもフラッシュと同等の待ち時間 (多くの場合、約 10 倍のスピード) を実現できるよう、読み取り "*と*" 書き込みの両方がキャッシュに保存されます。 読み取りキャッシュでは、高速アクセスのために、最近の頻繁に読み取られるデータを格納し、HDD へのランダムなトラフィックを最小限に抑えることができます。 (HDD へのランダム アクセスでは、シーク遅延と回転遅延のためにかなりの待機時間や損失時間が生じます)。書き込みキャッシュは、バーストを吸収すると共に、既に説明したように書き込みと再書き込みをまとめ、容量ドライブへの累積トラフィックを最小限に抑えます。

記憶域スペース ダイレクトには、書き込みをステージング解除する前にランダム化を解除するアルゴリズムが実装されています。これにより、ワークロード (仮想マシンなど) から生じた実際の IO がランダムであっても、ディスクに対する IO パターンはシーケンシャルになるようにエミュレートされます。 これにより、HDD の IOPS とスループットが最大限に高められます。

### <a name="caching-in-deployments-with-drives-of-all-three-types"></a>3 種類すべてのドライブを使用したデプロイでのキャッシュ

3 種類すべてのドライブが存在する場合、NVMe ドライブは、SSD と HDD の両方にキャッシュを提供します。 この動作は、前に説明したように、SSD の場合は書き込みのみがキャッシュされ、HDD の場合は読み取りと書き込みの両方がキャッシュされます。 HDD を対象とするキャッシュの負荷は、キャッシュ ドライブ間で均等に分散されます。

## <a name="summary"></a>まとめ

次の表は、それぞれの組み合わせの展開について、キャッシュとして使われるドライブ、容量として使われるドライブ、キャッシュ動作をまとめたものです。

| デプロイ     | キャッシュ ドライブ                        | 容量ドライブ | キャッシュの動作 (既定)  |
| -------------- | ----------------------------------- | --------------- | ------------------------- |
| NVMe のみ         | なし (オプション: 手動で構成) | NVMe            | 書き込み専用 (構成されている場合)  |
| SSD のみ          | なし (オプション: 手動で構成) | SSD             | 書き込み専用 (構成されている場合)  |
| NVMe + SSD       | NVMe                                | SSD             | 書き込み専用                  |
| NVMe + HDD       | NVMe                                | HDD             | 読み取り + 書き込み                |
| SSD + HDD        | SSD                                 | HDD             | 読み取り + 書き込み                |
| NVMe + SSD + HDD | NVMe                                | SSD + HDD       | HDD の場合は読み取りと書き込み、SSD の場合は書き込み専用  |

## <a name="server-side-architecture"></a>サーバー側のアーキテクチャ

キャッシュはドライブ レベルで実装されます。1 台のサーバー内の個々のキャッシュ ドライブは、同じサーバー内の 1 台以上の容量ドライブにバインドされます。

キャッシュは Windows ソフトウェア定義記憶域スタックの他の部分よりも下層に位置するため、記憶域スペースやフォールト トレランスといった概念を意識する必要はありません。 これは、Windows に提示される "ハイブリッド" (部分フラッシュ、部分ディスク) ドライブを作成していると考えることができます。 実際のハイブリッド ドライブと同様に、物理メディアの高速部分と低速部分をまたぐホット データとコールド データのリアルタイムの移動が外部から認識されることはほとんどありません。

記憶域スペース ダイレクトの回復性は少なくともサーバー レベルである (データ コピーは常に複数のサーバーに書き込まれ、サーバーごとに最大 1 つのコピーが保持される) ことから、キャッシュ内のデータにも、キャッシュに含まれていないデータと同等の回復性が与えられます。

![キャッシュのサーバー側のアーキテクチャ](media/understand-the-cache/Cache-Server-Side-Architecture.png)

たとえば、3 方向のミラーリングを使用する場合、データの 3 つのコピーが異なるサーバーに書き込まれ、そこでキャッシュに保存されます。 これらが後でデステージされるかどうかにかかわらず、3 つのコピーが常に存在します。

## <a name="drive-bindings-are-dynamic"></a>ドライブのバインドが動的である

キャッシュと容量ドライブ間のバインドには、1:1 から最大 1:12 までの任意の比率が設定されます。 これは、ドライブが追加または削除されるたびに動的に調整されます (スケールアップ時や障害の発生後など)。 つまり、必要な場合はいつでも、キャッシュ ドライブまたは容量ドライブを個別に追加できます。

![動的バインド](media/understand-the-cache/Dynamic-Binding.gif)

容量ドライブの数は、対称とするために、キャッシュ ドライブの倍数にすることをお勧めします。 たとえば、4 台のキャッシュ ドライブがある場合は、容量ドライブが 7 台や 9 台ではなく 8 台 (1:2 の比率) の場合に、より均等なパフォーマンスが得られます。

## <a name="handling-cache-drive-failures"></a>キャッシュ ドライブの障害の処理

キャッシュ ドライブで障害が発生すると、まだステージング解除されていない書き込みはすべて*ローカル サーバーから*失われ、(他のサーバー上の) 他のコピーだけが存在する状態になります。 他のドライブ障害が発生した場合と同様に、記憶域スペースは、残っているコピーを調べて自動的に回復できます。

一時的に、失われたキャッシュ ドライブにバインドされていた容量ドライブが異常と表示されます。 キャッシュの再バインドが (自動) 実行され、データの (自動) 修復が完了すると、再び正常として表示されます。

パフォーマンスを維持するために、サーバーあたり少なくとも 2 つのキャッシュ ドライブが必要であるのは、このようなシナリオのためです。

![障害の処理](media/understand-the-cache/Handling-Failure.gif)

その後、他のドライブの交換と同様に、キャッシュ ドライブを交換できます。

   >[!NOTE]
   > アドイン カード (AIC) または M.2 フォーム ファクターである NVMe を安全に交換するために、電源の切断が必要な場合があります。

## <a name="relationship-to-other-caches"></a>他のキャッシュとの関係

Windows ソフトウェアで定義された記憶域スタックには、関連付けられていない他のキャッシュがいくつかあります。 例としては、記憶域スペースのライトバック キャッシュやクラスターの共有ボリューム (CSV) のメモリ内読み取りキャッシュなどがあります。

記憶域スペース ダイレクトでは、記憶域スペースのライトバック キャッシュを既定の動作から変更することはできません。 たとえば、**New-Volume** コマンドレットの **-WriteCacheSize** などのパラメーターは使用できません。

CSV キャッシュを使用するかどうかはユーザーが自由に選択できます。 記憶域スペース ダイレクトでは既定でオフになっていますが、このトピックで説明している新しいキャッシュと競合することはありません。 特定のシナリオでは、パフォーマンスを向上させることができます。 詳細については、[CSV キャッシュを有効にする方法](../../failover-clustering/failover-cluster-csvs.md#enable-the-csv-cache-for-read-intensive-workloads-optional)に関する記事を参照してください。

## <a name="manual-configuration"></a>手動構成

ほとんどのデプロイで、手動の構成は必要ありません。 必要な場合は、以降のセクションを参照してください。

セットアップ後にキャッシュ デバイス モデルを変更する必要がある場合は、[ヘルス サービスの概要](../../failover-clustering/health-service-overview.md#supported-components-document)に関する記事で説明されているように、ヘルス サービスのサポート コンポーネント ドキュメントを編集してください。

### <a name="specify-cache-drive-model"></a>キャッシュ ドライブ モデルを指定する

すべて NVMe やすべて SSD の展開のようにすべてのドライブが同じ種類の展開では、書き込みに対する耐久性などの特性について、同じ種類のドライブ間の違いを Windows で自動的に識別することができないため、キャッシュは構成されません。

耐久性の高いドライブを使って同じ種類の耐久性の低いドライブをキャッシュするには、**Enable-ClusterS2D** コマンドレットの **-CacheDeviceModel** パラメーターに、キャッシュとして使用するドライブ モデルを指定します。 記憶域スペース ダイレクトが有効になると、そのモデルのすべてのドライブがキャッシュに使用されます。

   >[!TIP]
   > モデルの文字列は、**Get-PhysicalDisk**の出力に示されるものと完全に一致させる必要があります。

####  <a name="example"></a>例

まず、物理ディスクの一覧を取得します。

```PowerShell
Get-PhysicalDisk | Group Model -NoElement
```

出力例を次に示します。

```
Count Name
----- ----
    8 FABRIKAM NVME-1710
   16 CONTOSO NVME-1520
```

次に、以下のコマンドを入力して、キャッシュ デバイス モデルを指定します。

```PowerShell
Enable-ClusterS2D -CacheDeviceModel "FABRIKAM NVME-1710"
```

意図したドライブがキャッシュとして使用されていることを確かめるには、PowerShell で **Get-PhysicalDisk** を実行し、**Usage** プロパティが **"Journal"** になっていることを確認します。

### <a name="manual-deployment-possibilities"></a>手動デプロイの可能性

手動構成によって、次のデプロイが可能になります。

![特殊なデプロイの可能性](media/understand-the-cache/Exotic-Deployment-Possibilities.png)

### <a name="set-cache-behavior"></a>キャッシュの動作を設定する

キャッシュの既定の動作をオーバーライドできます。 たとえば、オールフラッシュ デプロイでも、読み取りをキャッシュするように設定できます。 既定値がワークロードに合わないことが明らかな場合を除き、動作を変更することはお勧めしません。

動作をオーバーライドするには、パラメーター **-CacheModeSSD** と **-CacheModeHDD** を指定して **Set-ClusterStorageSpacesDirect**コマンドレットを使用します。 **CacheModeSSD** パラメーターは、ソリッド ステート ドライブのキャッシュ時のキャッシュ動作を設定します。 **CacheModeHDD** パラメーターは、ハード ディスク ドライブのキャッシュ時のキャッシュ動作を設定します。 これは記憶域スペース ダイレクトを有効にした後、いつでも実行できます。

**Get-ClusterStorageSpacesDirect** を使用して、動作が設定されていることを確認できます。

#### <a name="example"></a>例

まず、記憶域スペース ダイレクトの設定を取得します。

```PowerShell
Get-ClusterStorageSpacesDirect
```

出力例を次に示します。

```
CacheModeHDD : ReadWrite
CacheModeSSD : WriteOnly
```

次に、以下を実行します。

```PowerShell
Set-ClusterStorageSpacesDirect -CacheModeSSD ReadWrite

Get-ClusterS2D
```

出力例を次に示します。

```
CacheModeHDD : ReadWrite
CacheModeSSD : ReadWrite
```

## <a name="sizing-the-cache"></a>キャッシュのサイズ変更

キャッシュは、アプリケーションやワークロードのワーキング セット (任意の時点でアクティブに読み取られているデータまたは書き込まれているデータ) を格納できるサイズに設定する必要があります。

これは、ハード ディスク ドライブがあるハイブリッド デプロイで特に重要です。 アクティブなワーキング セットがキャッシュのサイズを超過した場合、またはアクティブなワーキング セットの変動が激しい場合、読み取りではキャッシュ ミスが増加し、書き込みではより積極的なステージング解除が必要となり、全体のパフォーマンスが低下します。

Windows の組み込みのパフォーマンス モニター (PerfMon.exe) ユーティリティを使用して、キャッシュ ミス率を調べることができます。 具体的には、**Cluster Storage Hybrid Disk** カウンター セットの **Cache Miss Reads/sec** を、展開の全体の読み取り IOPS と比較します。 各 "ハイブリッド ディスク" は 1 つの容量ドライブに対応します。

たとえば、4 つの容量ドライブにバインドされている 2 つのキャッシュ ドライブは、サーバーあたり 4 つの "ハイブリッド ディスク" オブジェクト インスタンスになります。

![パフォーマンス モニター](media/understand-the-cache/PerfMon.png)

普遍的な規則ではありませんが、読み取りのキャッシュ ミスが多すぎる場合は、キャッシュのサイズが不足している可能性があるため、キャッシュ ドライブを追加してキャッシュを拡張することを検討してください。 キャッシュ ドライブまたは容量ドライブは、必要時にいつでも個別に追加できます。

## <a name="additional-references"></a>その他の参照情報

- [ドライブと回復性の種類の選択](choosing-drives.md)
- [フォールト トレランスとストレージの効率性](storage-spaces-fault-tolerance.md)
- [記憶域スペース ダイレクトのハードウェア要件](storage-spaces-direct-hardware-requirements.md)
