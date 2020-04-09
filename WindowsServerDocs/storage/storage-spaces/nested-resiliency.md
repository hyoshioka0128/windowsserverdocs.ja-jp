---
title: 記憶域スペースダイレクトのための入れ子になった回復性
ms.prod: windows-server
ms.author: jgerend
manager: dansimp
ms.technology: storagespaces
ms.topic: article
author: cosmosdarwin
ms.date: 03/15/2019
ms.openlocfilehash: ac4edccf0c1f8882dd2544b2544c3d8555bbc716
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857345"
---
# <a name="nested-resiliency-for-storage-spaces-direct"></a>記憶域スペースダイレクトのための入れ子になった回復性

> 適用対象: Windows Server 2019

入れ子になった回復性は、Windows Server 2019 の[記憶域スペースダイレクト](storage-spaces-direct-overview.md)の新機能であり、2台のサーバーからなるクラスターが記憶域の可用性を失うことなく同時に複数のハードウェア障害に耐えられるようにします。そのため、ユーザー、アプリ、および仮想マシンは中断することなく実行されます。 このトピックでは、そのしくみについて説明します。また、作業を開始するための詳細な手順について説明し、よく寄せられる質問に回答します。

## <a name="prerequisites"></a>前提条件

### <a name="green-checkmark-icon-consider-nested-resiliency-if"></a>![緑のチェックマークアイコン。](media/nested-resiliency/supported.png) 次の場合は、入れ子になった回復性を考慮します

- クラスターで Windows Server 2019 が実行されているそして
- クラスターには、2つのサーバーノードがあります。

### <a name="red-x-icon-you-cant-use-nested-resiliency-if"></a>![赤色の X アイコン。](media/nested-resiliency/unsupported.png) 次の場合、入れ子になった回復性は使用できません。

- クラスターで Windows Server 2016 が実行されているもしくは
- クラスターに3つ以上のサーバーノードがある

## <a name="why-nested-resiliency"></a>入れ子になった回復性の理由

入れ子になった回復性を使用するボリュームは、従来の[双方向のミラーリング](storage-spaces-fault-tolerance.md)の回復性とは異なり、同時**に複数のハードウェア障害が発生した場合でもオンラインでアクセス**できます。 たとえば、2つのドライブで障害が発生した場合、またはサーバーが停止してドライブに障害が発生した場合、入れ子になった回復性を使用するボリュームはオンライン状態を維持し、アクセスすることができます。 ハイパー集約型インフラストラクチャでは、アプリと仮想マシンの稼働時間が増加します。ファイルサーバーのワークロードの場合、ユーザーのファイルへのアクセスが中断されないことを意味します。

![ストレージの可用性](media/nested-resiliency/storage-availability.png)

トレードオフとは、入れ子になった回復性が**従来の双方向ミラーリングよりも容量効率が低い**ことを意味します。つまり、使用可能な領域がわずかに少なくなります。 詳細については、以下の「[容量の効率性](#capacity-efficiency)」セクションを参照してください。

## <a name="how-it-works"></a>方法

### <a name="inspiration-raid-51"></a>インスピレーション: RAID 5 + 1

RAID 5 + 1 は、入れ子になった回復性を理解するのに役立つ背景を提供する、確立された分散記憶域の回復性の形式です。 RAID 5 + 1 では、各サーバー内で、1つのドライブの損失から保護するために、RAID 5 (または*シングルパリティ*) によってローカルの回復性が提供されます。 次に、2台のサーバー間で、いずれかのサーバーの損失から保護するために、RAID 1 または*双方向のミラーリング*によってさらに回復性が提供されます。

![RAID 5 + 1](media/nested-resiliency/raid-51.png)

### <a name="two-new-resiliency-options"></a>2つの新しい回復性オプション

Windows Server 2019 の記憶域スペースダイレクトには、ソフトウェアに2つの新しい回復性オプションが用意されており、特別な RAID ハードウェアは必要ありません。

- **入れ子になった双方向ミラー。** 各サーバー内では、双方向のミラーリングによってローカルの回復性が提供され、その後、2つのサーバー間で双方向のミラーリングによって回復性が提供されます。 基本的には4方向ミラーで、各サーバーに2つのコピーがあります。 入れ子になった双方向ミラーリングは、妥協のないパフォーマンスを実現します。書き込みはすべてのコピーに送信され、読み取りは任意のコピーから取得されます。

  ![入れ子になった双方向ミラー](media/nested-resiliency/nested-two-way-mirror.png)

- **入れ子になったミラーアクセラレータパリティ。** 入れ子になった双方向ミラーリングを、上記の入れ子になったパリティと結合します。 各サーバー内では、ほとんどのデータのローカル回復性は、2方向ミラーリングを使用する新しい最近の書き込みを除き、単一の[ビットごとのパリティ演算](storage-spaces-fault-tolerance.md#parity)によって提供されます。 その後、すべてのデータの回復性をさらに向上させるには、サーバー間の双方向のミラーリングを使用します。 ミラーアクセラレータパリティの動作の詳細については、「[ミラーアクセラレータパリティ](https://docs.microsoft.com/windows-server/storage/refs/mirror-accelerated-parity)」を参照してください。

  ![入れ子になったミラーアクセラレータパリティ](media/nested-resiliency/nested-mirror-accelerated-parity.png)

### <a name="capacity-efficiency"></a>容量の効率

容量の効率は、[ボリュームフットプリント](plan-volumes.md#choosing-the-size-of-volumes)に使用できる領域の比率です。 回復性に起因する容量のオーバーヘッドについて説明し、選択した回復性オプションによって異なります。 単純な例として、回復性のないデータの格納は100% の容量効率に優れています (1 TB のデータは 1 tb の物理ストレージ容量を必要とします)。一方、双方向のミラーリングは50% の効率が高くなります (1 TB のデータでは物理ストレージ容量が 2 TB になります)。

- **入れ子になった双方向ミラー**は、4つのコピーを書き込みます。つまり、1 tb のデータを格納するには、4 tb の物理ストレージ容量が必要です。 シンプルさは魅力的ですが、入れ子になった双方向ミラーの容量効率が25% になっているのは、記憶域スペースダイレクトの回復性オプションの中で最も低いものです。

- **入れ子になったミラーアクセラレータのパリティ**は、最大で 35%-40% の容量効率を実現します。これは、各サーバーの容量ドライブの数と、ボリュームに対して指定したミラーとパリティの組み合わせによって異なります。 次の表は、一般的な構成の参照を示しています。

  | サーバーあたりの容量ドライブ | 10% ミラー | 20% ミラー | 30% ミラー |
  |----------------------------|------------|------------|------------|
  | 4                          | 35.7%      | 34.1%      | 32.6%      |
  | 5                          | 37.7%      | 35.7%      | 33.9%      |
  | 6                          | 39.1%      | 36.8%      | 34.7%      |
  | 7 +                         | 40.0%      | 37.5%      | 35.3%      |

  > [!NOTE]
  > **興味をお持ちの場合は、完全な数学の例を次に示します。** 2台のサーバーそれぞれに6つの容量ドライブがあり、10 gb のミラーと 90 GB のパリティで構成される 1 100 GB のボリュームを作成するとします。 サーバーローカル双方向ミラーは50.0% の効率を実現します。つまり、10 GB のミラーデータは、各サーバーに格納するのに 20 GB かかります。 両方のサーバーにミラー化され、合計フットプリントは 40 GB です。 サーバーローカルの単一パリティ (この場合は 5/6 = 83.3% 効率)。つまり、90 GB のパリティデータは、各サーバーに格納するために 108 GB を必要とします。 両方のサーバーにミラー化され、合計フットプリントは 216 GB です。 総フットプリントは [(10 GB/50.0%) + (90 GB/83.3%)] × 2 = 256 GB であり、全体的な容量の効率39.1 を最大にしたものになります。

従来の双方向ミラーリングの容量効率 (約50%)および入れ子になったミラーアクセラレータパリティ (最大40%)の違いはあまりありません。 要件によっては、容量の効率が若干低くなると、記憶域の可用性が大幅に向上する可能性があります。 ボリュームごとの回復性を選択すると、同じクラスター内で、入れ子になった回復性ボリュームと従来の双方向ミラーボリュームを混在させることができます。

![トレードオフ](media/nested-resiliency/tradeoff.png)

## <a name="usage-in-powershell"></a>PowerShell での使用法

PowerShell で使い慣れた記憶域コマンドレットを使用して、入れ子になった回復性を備えたボリュームを作成できます。

### <a name="step-1-create-storage-tier-templates"></a>手順 1: 記憶域階層テンプレートを作成する

まず、`New-StorageTier` コマンドレットを使用して新しい記憶域階層テンプレートを作成します。 この操作は一度だけ行う必要があります。作成したすべての新しいボリュームでこれらのテンプレートを参照できます。 容量ドライブの `-MediaType` と、必要に応じて任意の `-FriendlyName` を指定します。 他のパラメーターは変更しないでください。

容量ドライブがハードディスクドライブ (HDD) の場合は、管理者として PowerShell を起動し、次のように実行します。

```PowerShell 
# For mirror
New-StorageTier -StoragePoolFriendlyName S2D* -FriendlyName NestedMirror -ResiliencySettingName Mirror -MediaType HDD -NumberOfDataCopies 4

# For parity
New-StorageTier -StoragePoolFriendlyName S2D* -FriendlyName NestedParity -ResiliencySettingName Parity -MediaType HDD -NumberOfDataCopies 2 -PhysicalDiskRedundancy 1 -NumberOfGroups 1 -FaultDomainAwareness StorageScaleUnit -ColumnIsolation PhysicalDisk 
``` 

容量ドライブがソリッドステートドライブ (SSD) の場合は、代わりに `-MediaType` を `SSD` に設定します。 他のパラメーターは変更しないでください。

> [!TIP]
> `Get-StorageTier`を使用して、階層が正常に作成されたことを確認します。

### <a name="step-2-create-volumes"></a>手順 2: ボリュームを作成する

次に、`New-Volume` コマンドレットを使用して新しいボリュームを作成します。

#### <a name="nested-two-way-mirror"></a>入れ子になった双方向ミラー

入れ子になった双方向ミラーを使用するには、`NestedMirror` 層テンプレートを参照し、サイズを指定します。 例 :

```PowerShell
New-Volume -StoragePoolFriendlyName S2D* -FriendlyName Volume01 -StorageTierFriendlyNames NestedMirror -StorageTierSizes 500GB
```

#### <a name="nested-mirror-accelerated-parity"></a>入れ子になったミラーアクセラレータパリティ

入れ子になったミラーアクセラレータのパリティを使用するには、`NestedMirror` 層と `NestedParity` 層の両方のテンプレートを参照し、ボリュームの各部分に1つずつ、2つのサイズを指定します (ミラーの最初、パリティ 2)。 たとえば、20% の入れ子になった双方向ミラーと80% の入れ子になったパリティである 1 500 GB ボリュームを作成するには、次のように実行します。

```PowerShell
New-Volume -StoragePoolFriendlyName S2D* -FriendlyName Volume02 -StorageTierFriendlyNames NestedMirror, NestedParity -StorageTierSizes 100GB, 400GB
```

### <a name="step-3-continue-in-windows-admin-center"></a>手順 3: Windows 管理センターで続行する

入れ子になった回復性を使用するボリュームは、次のスクリーンショットのように、明確なラベル付きで[Windows 管理センター](https://docs.microsoft.com/windows-server/manage/windows-admin-center/understand/windows-admin-center)に表示されます。 作成されると、記憶域スペースダイレクトの他のボリュームと同じように、Windows 管理センターを使用してそれらを管理および監視できます。

![](media/nested-resiliency/windows-admin-center.png)

### <a name="optional-extend-to-cache-drives"></a>省略可能: キャッシュドライブに拡張する

入れ子になった回復性は、既定の設定を使用して、複数の容量ドライブが同時に失われたり、1台のサーバーと1つの容量のドライブが同時に失われたりするのを防ぎます。 この保護を[キャッシュドライブ](understand-the-cache.md)に拡張するには、追加の考慮事項があります。多くの場合、キャッシュドライブは*複数*の容量ドライブに対して読み取り*と書き込み*のキャッシュを提供するため、他のサーバーがダウンしているときにキャッシュドライブの損失を許容できるようにする唯一の方法は、書き込みをキャッシュするのではなく、パフォーマンスに影響

このシナリオに対処するために、記憶域スペースダイレクトには、2台のサーバークラスター内の1台のサーバーがダウンしたときに書き込みキャッシュを自動的に無効にするオプションが用意されています。サーバーがバックアップされたら、書き込みキャッシュを再び有効にすることができます。 パフォーマンスに影響を与えずにルーチンの再起動を許可するために、サーバーが30分間停止するまで、書き込みキャッシュは無効になります。 書き込みキャッシュを無効にすると、書き込みキャッシュの内容が容量デバイスに書き込まれます。 その後、サーバーはオンラインサーバーで障害が発生しているキャッシュデバイスを許容できます。ただし、キャッシュデバイスで障害が発生した場合、キャッシュからの読み取りが遅れるか、失敗する可能性があります。

この動作を設定する (省略可能) には、管理者として PowerShell を起動し、次のように実行します。

```PowerShell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.NestedResiliency.DisableWriteCacheOnNodeDown.Enabled" -Value "True"
```

**True**に設定すると、キャッシュの動作は次のようになります。

| 状況                       | キャッシュの動作                           | キャッシュドライブの損失を許容できるか。 |
|---------------------------------|------------------------------------------|--------------------------------|
| 両方のサーバーが稼働しています                 | キャッシュの読み取りと書き込み、完全なパフォーマンス | はい                            |
| サーバーダウン、最初は30分   | キャッシュの読み取りと書き込み、完全なパフォーマンス | いいえ (一時的)               |
| 最初の30分後          | キャッシュ読み取りのみ、パフォーマンスに影響する   | はい (キャッシュが容量ドライブに書き込まれた後)                           |

## <a name="frequently-asked-questions"></a>よく寄せられる質問

### <a name="can-i-convert-an-existing-volume-between-two-way-mirror-and-nested-resiliency"></a>双方向ミラーと入れ子になった回復性の間で既存のボリュームを変換することはできますか。

いいえ、回復性の種類の間でボリュームを変換することはできません。 Windows Server 2019 の新しい展開では、ニーズに最も適した回復性の種類を事前に決定します。 Windows Server 2016 からアップグレードする場合は、入れ子になった回復性を持つ新しいボリュームを作成し、データを移行してから、古いボリュームを削除することができます。

### <a name="can-i-use-nested-resiliency-with-multiple-types-of-capacity-drives"></a>複数の種類の容量ドライブで入れ子になった回復性を使用できますか。

はい、上記の[手順 1](#step-1-create-storage-tier-templates)で、それぞれのレベルの `-MediaType` を指定するだけです。 たとえば、同じクラスター内の NVMe、SSD、HDD では、NVMe はキャッシュを提供し、後者の2つは容量を提供します。 `NestedMirror` レベルを `-MediaType SSD` に、`NestedParity` レベルを `-MediaType HDD`に設定します。 この場合、パリティ容量の効率は HDD のドライブの数によってのみ異なります。また、サーバーごとに少なくとも4つのディスクが必要です。

### <a name="can-i-use-nested-resiliency-with-3-or-more-servers"></a>入れ子になった回復性を3台以上のサーバーで使用できますか。

いいえ。クラスターにサーバーが2つだけある場合は、入れ子になった回復性のみを使用します。

### <a name="how-many-drives-do-i-need-to-use-nested-resiliency"></a>入れ子になった回復性を使用するには、何個のドライブが必要ですか。

記憶域スペースダイレクトに必要なドライブの最小数は、サーバーノードあたり4台の容量ドライブと、サーバーノードあたり2つのキャッシュドライブ (存在する場合) です。 これは、Windows Server 2016 から変更されていません。 入れ子になった回復性に関する追加の要件はありません。また、予約容量の推奨事項も変更されません。

### <a name="does-nested-resiliency-change-how-drive-replacement-works"></a>[回復性の入れ子になっている場合、ドライブの交換方法を変更しますか?]

No:

### <a name="does-nested-resiliency-change-how-server-node-replacement-works"></a>回復性を入れ子にすると、サーバーノードの交換のしくみが変わりますか。

No: サーバーノードとそのドライブを置き換えるには、次の順序に従います。

1. 発信サーバーのドライブをインベントリから削除する
2. 新しいサーバーとそのドライブをクラスターに追加します。
3. 記憶域プールが再調整される
4. 発信サーバーとそのドライブを削除する

詳細については、[サーバーの削除](remove-servers.md)に関するトピックを参照してください。

## <a name="see-also"></a>参照

- [記憶域スペースダイレクトの概要](storage-spaces-direct-overview.md)
- [記憶域スペースダイレクトのフォールトトレランスについて](storage-spaces-fault-tolerance.md)
- [記憶域スペースダイレクトのボリュームを計画する](plan-volumes.md)
- [記憶域スペースダイレクトでボリュームを作成する](create-volumes.md)
