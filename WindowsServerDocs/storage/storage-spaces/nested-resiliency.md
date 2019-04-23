---
title: 記憶域スペース ダイレクトの入れ子になったの回復性
ms.prod: windows-server-threshold
ms.author: jgerend
ms.manager: dansimp
ms.technology: storagespaces
ms.topic: article
author: cosmosdarwin
ms.date: 11/06/2018
ms.openlocfilehash: 206d5d19ec55774f9055e7265d4c87d276c60590
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879573"
---
# <a name="nested-resiliency-for-storage-spaces-direct"></a>記憶域スペース ダイレクトの入れ子になったの回復性

> 適用対象:Windows Server 2019

入れ子になったの回復性の新しい機能は、[記憶域スペース ダイレクト](storage-spaces-direct-overview.md)で 2 台のサーバー クラスターに記憶域の可用性、ため、ユーザー、アプリ、損失することがなく同時に複数のハードウェア障害に耐えられるようにする Windows Server 2019仮想マシンは引き続き中断せずに実行します。 このトピックでは、そのしくみについて説明します、最初に、詳細な手順と回答が最もよく寄せられる質問を提供します。

## <a name="prerequisites"></a>前提条件

### <a name="green-checkmark-iconmedianested-resiliencysupportedpng-consider-nested-resiliency-if"></a>![緑色のチェック マーク アイコン。](media/nested-resiliency/supported.png) 場合は、入れ子になったの回復性を考慮してください。

- クラスターで実行される Windows Server 2019;そして
- クラスターが正確に 2 つのサーバー ノード

### <a name="red-x-iconmedianested-resiliencyunsupportedpng-you-cant-use-nested-resiliency-if"></a>![赤い X 印アイコン。](media/nested-resiliency/unsupported.png) 場合は、入れ子になったの回復性を使用することはできません。

- クラスターで実行される Windows Server 2016。または
- クラスターが 3 つ以上のサーバー ノード

## <a name="why-nested-resiliency"></a>なぜ入れ子になったの回復性

入れ子になったの回復性を使用しているボリュームは**と同時に複数のハードウェア障害が発生する場合でも、オンラインでアクセス可能のまま**、クラシックとは異なり[双方向ミラーリング](storage-spaces-fault-tolerance.md)回復性。 たとえばと同時に、2 つのドライブが失敗した場合、または、サーバーが停止し、ドライブが失敗した場合は、入れ子になったの回復性を使用しているボリュームはオンラインでアクセス可能なままです。 ハイパー コンバージド インフラストラクチャ、アプリと仮想マシンの稼働時間が向上します。ファイル サーバー ワークロードにユーザーが中断される、ファイルにアクセスを楽しむことを意味します。

![記憶域の可用性](media/nested-resiliency/storage-availability.png)

トレードオフは、その入れ子になったの回復性が**双方向ミラーリングを従来よりも容量効率を下げる**、つまり若干小さいサイズの使用可能な領域を取得します。 詳細については、次を参照してください。、[容量効率](#capacity-efficiency)以下のセクション。

## <a name="how-it-works"></a>方法

### <a name="inspiration-raid-51"></a>インスピレーションを得ません。RAID 5 + 1

RAID 5 + 1 は、入れ子になった回復性を理解するための便利な背景を提供する分散型の記憶域の回復性の確立されたフォームです。 Raid 5 + 1、各サーバーでは、ローカルの回復性では、RAID 5、によって提供または*シングル パリティ*、1 台のドライブの損失を防ぐためにします。 次に、RAID 1 で回復性がさらに提供されるまたは*双方向ミラーリング*、いずれかのサーバーの損失を防ぐために 2 台のサーバー。

![RAID 5 + 1](media/nested-resiliency/raid-51.png)

### <a name="two-new-resiliency-options"></a>2 つの回復性オプション

記憶域スペース ダイレクトでは、Windows Server 2019 には、RAID の特殊なハードウェアを必要としないソフトウェアで実装されている 2 つの新しい回復性オプションが用意されています。

- **双方向ミラーの入れ子になった。** サーバーごとでは、双方向ミラーでは、ローカルの回復性が提供され、2 つのサーバー間の双方向ミラーリングによってさらに回復性を提供し。 各サーバーで 2 つのコピーに、4 方向ミラーの本質的にすることをお勧めします。 妥協のないパフォーマンスを提供して双方向ミラーリングを入れ子になった: すべてのコピーにへの書き込みと読み取りはすべてのコピーから取得します。

  ![入れ子になったの双方向ミラー](media/nested-resiliency/nested-two-way-mirror.png)

- **入れ子になったミラー アクセラレータを使用したパリティ。** 結合から、上の双方向ミラーリングを入れ子になったパリティの入れ子になった。 各サーバー内で、ほとんどのデータのローカルの回復性が 1 つによって提供される[算術演算のパリティ](storage-spaces-fault-tolerance.md#parity)、双方向ミラーリングを使用する新しいの最近の書き込みを除きます。 次に、さらにすべてのデータの回復性は、サーバー間で双方向ミラーリングによって提供されます。 パリティの動作をミラー アクセラレータを使用する方法についての詳細については、次を参照してください。[ミラー アクセラレータを使用したパリティ](https://docs.microsoft.com/windows-server/storage/refs/mirror-accelerated-parity)します。

  ![入れ子になったミラー アクセラレータを使用したパリティ](media/nested-resiliency/nested-mirror-accelerated-parity.png)

### <a name="capacity-efficiency"></a>容量の効率性

容量の効率性を使用可能な領域の比率は、[ボリュームのフット プリント](plan-volumes.md#choosing-the-size-of-volumes)します。 回復性に起因する容量のオーバーヘッドについて説明し、選択した回復性のオプションによって異なります。 単純な例としては 50% 効率 (2 TB の物理記憶域容量を占有するデータの 1 TB) には双方向ミラーリング中にデータを含まない回復性は 100% の容量の効率 (1 TB の物理記憶域容量を占有するデータの 1 TB) 格納します。

- **入れ子になったの双方向ミラー** 4 個のコピーを書き込み、すべての意味を 1 TB のデータを格納する必要があります 4 TB の物理記憶域容量。 その簡潔さは魅力的ですが、25% の入れ子になったの双方向ミラーの容量の効率性、記憶域スペース ダイレクトでは、任意の回復性オプションの最小値です。

- **ミラー アクセラレータを使用したパリティを入れ子になった**容量効率の高い、約 35% ~ 40%、2 つの要因に依存しているは実現: サーバーごとに、および複数のミラーおよびパリティ ボリュームに指定したドライブの容量の数。 この表では、一般的な構成の参照を示します。

  | サーバーあたりの容量のドライブ | ミラーの 10% | ミラーの 20% | 30% ミラー |
  |----------------------------|------------|------------|------------|
  | 4                          | 35.7%      | 34.1%      | 32.6%      |
  | 5                          | 37.7%      | 35.7%      | 33.9%      |
  | 6                          | 39.1%      | 36.8%      | 34.7%      |
  | 7+                         | 40.0%      | 37.5%      | 35.3%      |

  > [!NOTE]
  > **興味がある場合は、完全な数値演算の例を示します。** 2 台のサーバーのそれぞれに 6 つの容量ドライブがあるし、10 GB のミラーおよびパリティの 90 GB から成る 1 つの 100 GB のボリュームを作成したいとします。 サーバーのローカルの双方向ミラーは 50.0% 効率、各サーバーに格納する 20 GB を受け取り、10 GB のミラーのデータを意味します。 両方のサーバーにミラー化された、その合計のフット プリントは、40 GB です。 サーバーのローカルのシングル パリティは、この場合は、5/6 は 83.3 = % 効率性、つまり 90 GB パリティ データは、各サーバーに格納する 108 GB。 両方のサーバーにミラー化された、その合計のフット プリントは、216 GB です。 合計のフット プリントはそのため、[(10 GB/50.0%) + (90 GB/83.3%)] × 2 = 256 GB、39.1% の全体的な容量の効率。

注意して従来の双方向ミラーリング (約 50%) の容量の効率ミラー アクセラレータを使用したパリティを入れ子になったと (最大 40%)非常に違いはありません。 要件に応じて、記憶域の可用性が著しく増加だけの価値が若干低く容量効率性があります。 回復性をボリュームを選択するため、回復性の入れ子になったボリュームと同じクラスター内のクラシックの双方向ミラー ボリュームを混在させることができます。

![トレードオフ](media/nested-resiliency/tradeoff.png)

## <a name="usage-in-powershell"></a>PowerShell での使用法

PowerShell で使い慣れたストレージ コマンドレットを使用して、入れ子になったの回復性を備えたボリュームを作成することができます。

### <a name="step-1-create-storage-tier-templates"></a>手順 1:ストレージ層のテンプレートを作成します。

最初を使用して、新しいストレージ層のテンプレートを作成、`New-StorageTier`コマンドレット。 のみ、1 回、これを行う必要があり、作成したすべての新しいボリュームがこれらのテンプレートを参照します。 指定、`-MediaType`容量ドライブと、オプションで、`-FriendlyName`好みの。 その他のパラメーターを変更しないでください。

大容量のドライブがハード ディスク ドライブ (HDD) の場合は、管理者として PowerShell を起動し、実行します。

```PowerShell 
# For mirror
New-StorageTier -StoragePoolFriendlyName S2D* -FriendlyName NestedMirror -ResiliencySettingName Mirror -MediaType HDD -NumberOfDataCopies 4

# For parity
New-StorageTier -StoragePoolFriendlyName S2D* -FriendlyName NestedParity -ResiliencySettingName Parity -MediaType HDD -NumberOfDataCopies 2 -PhysicalDiskRedundancy 1 -NumberOfGroups 1 -FaultDomainAwareness StorageScaleUnit -ColumnIsolation PhysicalDisk 
``` 

大容量のドライブがソリッド ステート ドライブ (SSD) の場合は、設定、`-MediaType`に`SSD`代わりにします。 その他のパラメーターを変更しないでください。

> [!TIP]
> 正常に作成するレベルを確認します。`Get-StorageTier`します。

### <a name="step-2-create-volumes"></a>手順 2:ボリュームの作成

使用して新しいボリュームを作成し、`New-Volume`コマンドレット。

#### <a name="nested-two-way-mirror"></a>入れ子になったの双方向ミラー

入れ子になったの双方向ミラーを使用する参照、`NestedMirror`層のテンプレートとサイズを指定します。 次に、例を示します。

```PowerShell
New-Volume -StoragePoolFriendlyName S2D* -FriendlyName Volume01 -StorageTierFriendlyNames NestedMirror -StorageTierSizes 500GB
```

#### <a name="nested-mirror-accelerated-parity"></a>入れ子になったミラー アクセラレータを使用したパリティ

入れ子になったミラー アクセラレータを使用したパリティを使用するには、両方を参照、`NestedMirror`と`NestedParity`層のテンプレートと、ボリュームの各部分に 1 つずつ、2 つのサイズを指定 (ミラー、パリティ 2 つ目)。 たとえば、入れ子になった双方向ミラーの 20% から 80% である 1 つの 500 GB のボリュームを作成するには、パリティ、実行が入れ子に。

```PowerShell
New-Volume -StoragePoolFriendlyName S2D* -FriendlyName Volume02 -StorageTierFriendlyNames NestedMirror, NestedParity -StorageTierSizes 100GB, 400GB
```

### <a name="step-3-continue-in-windows-admin-center"></a>手順 3:Windows Admin Center で続行します。

入れ子になったの回復性を使用しているボリュームが表示される[Windows Admin Center](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center)クリア ラベル付け、次のスクリーン ショットのように使用します。 作成されるとは、管理し、他の記憶域スペース ダイレクトのボリュームと同じように Windows Admin Center を使用してそれらを監視します。

![](media/nested-resiliency/windows-admin-center.png)

### <a name="optional-extend-to-cache-drives"></a>省略可能: キャッシュ ドライブを拡張します。

既定の設定では、入れ子になったの回復性は、同時に複数の容量ドライブの損失または 1 つのサーバーと同時に 1 つの容量ドライブから保護します。 この保護を拡張する[キャッシュ ドライブ](understand-the-cache.md)が別の考慮事項: キャッシュ ドライブは、多くの場合読み取りを提供するため*読み書き*のキャッシュを*複数*容量ドライブ、キャッシュへの書き込み、単に、その他のサーバーがダウンしている場合は、キャッシュ ドライブの損失を許容できるようにする唯一の方法ですが、パフォーマンスに影響する場合。

このシナリオに対処するには、記憶域スペース ダイレクトは、2 台のサーバー クラスター内の 1 つのサーバーがダウン、ときに書き込みキャッシュを自動的に無効にし、再度有効にする、サーバーがバックアップされて後、書き込みキャッシュするためのオプションを提供します。 パフォーマンスの影響を与えずに日常的な再起動を許可するのには、30 分間サーバー ダウンされるまでにキャッシュが無効にされていないを記述します。

(省略可能) この動作を設定するには、管理者として PowerShell を起動し、実行します。

```PowerShell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.NestedResiliency.DisableWriteCacheOnNodeDown.Enabled" -Value "True"
```

1 回設定`True`キャッシュの動作は。

| 状況                       | キャッシュの動作                           | キャッシュ ドライブの損失を許容できるでしょうか。 |
|---------------------------------|------------------------------------------|--------------------------------|
| 両方のサーバー                 | キャッシュの読み取りし、書き込み、フル パフォーマンス | 〇                            |
| 最初の 30 分間ダウン サーバー   | キャッシュの読み取りし、書き込み、フル パフォーマンス | いいえ (一時的に)               |
| 最初の 30 分後          | キャッシュの読み取りのみ、パフォーマンスが影響を受ける   | 〇                            |

## <a name="frequently-asked-questions"></a>よく寄せられる質問

### <a name="can-i-convert-an-existing-volume-between-two-way-mirror-and-nested-resiliency"></a>双方向ミラーと入れ子になったの回復性の間の既存のボリュームを変換できますか。

いいえ、ボリュームは、回復性の種類の間で変換できません。 Windows Server 2019 の新しい配置を前もってお客様ニーズに合った最適などの回復性の種類を決定します。 Windows Server 2016 からアップグレードする場合は、入れ子になったの回復性を備えた新しいボリュームを作成に、データを移行および以前のボリュームを削除します。

### <a name="can-i-use-nested-resiliency-with-multiple-types-of-capacity-drives"></a>複数の種類のドライブの容量で入れ子になったの回復性を使用できますか。

[はい] を指定するだけです、`-MediaType`それに応じてそれぞれの層で[手順 1](#step-1-create-storage-tier-templates)上。 たとえば、NVMe、SSD、HDD、同じクラスター内と、NVMe は後の 2 つの容量を提供するときにキャッシュを提供: 設定、`NestedMirror`レベルを`-MediaType SSD`と`NestedParity`レベルを`-MediaType HDD`します。 この場合は、パリティ容量効率の向上がのみ、HDD のドライブの数に依存し、サーバーごとに 4 以上にする必要があることに注意してください。

### <a name="can-i-use-nested-resiliency-with-3-or-more-servers"></a>3 つ以上のサーバーで入れ子になったの回復性を使用できますか。

いいえ場合に、のみ使用入れ子になったの回復性がある正確に 2 台のサーバーのクラスター。

### <a name="how-many-drives-do-i-need-to-use-nested-resiliency"></a>入れ子になったの回復性を使用する必要があるドライブの数をでしょうか。

記憶域スペース ダイレクトに必要なドライブの最小数は、1 つのサーバー ノード、4 の容量ドライブと 1 つのサーバー ノード (存在する場合) の 2 つのキャッシュ ドライブです。 これは、Windows Server 2016 から変更されていません。 入れ子になったの回復性の追加要件がないと、予約容量の推奨事項は変更されませんが。

### <a name="does-nested-resiliency-change-how-drive-replacement-works"></a>入れ子になったの回復性は、ドライブの交換のしくみを変更しますか。

いいえ。

### <a name="does-nested-resiliency-change-how-server-node-replacement-works"></a>入れ子になったの回復性は、サーバー ノードの置換の動作を変更しますか。

いいえ。 サーバー ノードとそのドライブを置換するには、この順序に従います。

1. 送信サーバーのドライブをインベントリから削除します。
2. そのドライブを持つ、新しいサーバーをクラスターに追加します。
3. 記憶域プールを再調整します。
4. 送信サーバーとそのドライブを削除します。

詳細を参照してください、[サーバーを削除する](remove-servers.md)トピック。

## <a name="see-also"></a>関連項目

- [記憶域スペース ダイレクトの概要](storage-spaces-direct-overview.md)
- [記憶域スペース ダイレクトのフォールト トレランスを理解します。](storage-spaces-fault-tolerance.md)
- [記憶域スペース ダイレクトのボリュームを計画します。](plan-volumes.md)
- [記憶域スペース ダイレクトのボリュームを作成します。](create-volumes.md)
