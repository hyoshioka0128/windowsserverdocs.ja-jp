---
title: 記憶域スペース ダイレクトのボリュームの割り当てを区切る
ms.author: cosmosdarwin
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 03/29/2018
ms.openlocfilehash: c93cbf4ba418f6702cf8747508605952d993508d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889053"
---
# <a name="delimit-the-allocation-of-volumes-in-storage-spaces-direct"></a>記憶域スペース ダイレクトのボリュームの割り当てを区切る
> 適用先:Windows Server Insider プレビュー、17093 およびそれ以降のビルド

Windows Server Insider プレビューには、手動で記憶域スペース ダイレクトのボリュームの割り当てを区切るためにオプションが導入されています。 そのため、特定の状況では、フォールト トレランスを大幅に増加することができますは、いくつかの追加の管理に関する考慮事項と複雑さです。 ここでは、方法は機能し、PowerShell で例を示して説明します。

   > [!IMPORTANT]
   > この機能は、Windows Server Insider プレビュー、17093 およびそれ以降のビルドの新機能です。 Windows Server 2016 でご利用いただけません。 IT プロフェッショナルの参加をご案内、 [Windows Server Insider Program](https://aka.ms/serverinsider) Windows サーバーを組織操作性を向上するために実行できることにフィードバックを提供します。

## <a name="prerequisites"></a>前提条件

### <a name="green-checkmark-iconmediadelimit-volume-allocationsupportedpng-consider-using-this-option-if"></a>![緑色のチェック マーク アイコン。](media/delimit-volume-allocation/supported.png) このオプションを使用する場合を考慮してください。

- クラスターが 6 つ以上のサーバーです。そして
- クラスターでのみ使用[3 方向ミラー](storage-spaces-fault-tolerance.md#mirroring)回復性

### <a name="red-x-iconmediadelimit-volume-allocationunsupportedpng-do-not-use-this-option-if"></a>![赤い X 印アイコン。](media/delimit-volume-allocation/unsupported.png) 場合は、このオプションを使用しないでください。

- クラスターが 6 個未満のサーバーです。または
- クラスターで使用[パリティ](storage-spaces-fault-tolerance.md#parity)または[ミラー アクセラレータを使用したパリティ](storage-spaces-fault-tolerance.md#mirror-accelerated-parity)回復性

## <a name="understand"></a>概要

### <a name="review-regular-allocation"></a>定期的な割り当ての確認:

通常 3 方向ミラーリングでは、ボリュームが多く小さな「されているスラブ」3 回のコピーおよびすべてのサーバーで、クラスター内の各ドライブに均等に分散されるに分けられます。 詳細については、「[この deep dive ブログ](https://blogs.technet.microsoft.com/filecab/2016/11/21/deep-dive-pool-in-spaces-direct/)します。

![ボリュームがされているスラブの 3 つのスタックに分割され、すべてのサーバーに均等に分散されているを示す図。](media/delimit-volume-allocation/regular-allocation.png)

この既定の割り当て、最大限の並列読み取りと書き込み、パフォーマンスの向上につながるし、その簡潔さで魅力的: すべてのサーバーがビジー状態に、すべてのドライブが均等に完全なおよびすべてのボリュームがオンラインまたはオフラインにまとめています。 すべてのボリュームとして同時に最大で 2 つの障害を存続することが保証されます[これらの例](storage-spaces-fault-tolerance.md#examples)を示しています。

ただし、この割り当ては、ボリュームは、3 つの同時障害を存続ことはできません。 3 台のサーバーが 1 回では、失敗した場合、または 3 台のサーバーのドライブが同時に失敗した場合は、少なくとも一部スラブが (非常に高い確率) で割り当てられるため、正確な 3 つのドライブまたは失敗したサーバーにボリュームにアクセスできません。

次の例では、1、3、および 5 サーバーは、同時に失敗します。 残りのコピーされているスラブの多くがありますが、いないいくつか実行します。

![赤、および全体的なボリュームで強調表示されている 6 つのサーバーの 3 つの図は赤です。](media/delimit-volume-allocation/regular-does-not-survive.png)

ボリュームがオフラインになり、サーバーを回復するまでにアクセスできなくなります。

### <a name="new-delimited-allocation"></a>割り当ての新機能: 区切り

区切り記号付きの割り当てでは、(3 方向ミラーの最低限の 3 つ) を使用するサーバーのサブセットを指定します。 ボリュームは 3 回は、以前のように、すべてのすべてのサーバーに割り当てるのではなくコピーされているスラブに分かれています **、スラブが指定したサーバーのサブセットにのみ割り当てられている**します。

![ボリュームがされているスラブの 3 つのスタックに分割され、3 つの 6 つのサーバーにのみ配布されているを示す図。](media/delimit-volume-allocation/delimited-allocation.png)

#### <a name="advantages"></a>長所

この割り当ては、ボリュームは 3 つの同時障害から復旧する可能性があります。 実際には、その確率のサバイバルから (通常の割り当て) を 0% に増加 (区切り記号付きの割り当て) の 95% ここで。 直感的に、それらの障害は影響されませんので、4、5、または 6 のサーバーには依存しないためにです。

上記の例では、1、3、および 5 サーバーは同時に失敗します。 区切られた割り当てがそのサーバー 2 には、すべてスラブのコピーが含まれています。 を保証するため、すべてスラブが残っているコピーと、ボリュームがオンラインでアクセス可能。

![全体的なボリュームは緑色、赤色で強調表示されている 6 つのサーバーの 3 つを示す図。](media/delimit-volume-allocation/delimited-does-survive.png)

サバイバル確率は、サーバーとその他の要因の数によって異なります。 – 表示[Analysis](#analysis)詳細についてはします。

#### <a name="disadvantages"></a>欠点

区切り記号付きの割り当てには、いくつかの追加の管理に関する考慮事項と複雑さがあります。

1. 管理者は、その」の説明に従って、サーバー間で記憶域使用率のバランスを取るしでの高確率を維持するには、各ボリュームの割り当てを区切り記号として、[ベスト プラクティス](#best-practices)セクション。

2. 区切り記号付きの割り当てと予約と同等の **(最大値なし) を持つサーバーごとに 1 つの容量ドライブ**します。 これよりも多く[推奨事項を発行](plan-volumes.md#choosing-the-size-of-volumes)の定期的な割り当て、4 つの容量をサポートできるはどのドライブの合計。

3. サーバーが失敗し、」の説明に従って、交換する必要があるかどうかは[サーバーとそのドライブを削除](remove-servers.md#remove-a-server-and-its-drives)管理者は、その新しいサーバーを追加して失敗の – 1 つの例の削除によって影響を受けるボリュームの区切りを更新するため以下に。

## <a name="usage-in-powershell"></a>PowerShell での使用法

使用することができます、`New-Volume`コマンドレットを記憶域スペース ダイレクトのボリュームを作成します。

たとえば、通常 3 方向ミラー ボリュームを作成するには、します。

```PowerShell
New-Volume -FriendlyName "MyRegularVolume" -Size 100GB
```

### <a name="create-a-volume-and-delimit-its-allocation"></a>ボリュームを作成し、その割り当てを区切る

3 方向ミラー ボリュームを作成すると、その割り当てを区切るため。

1. まず、クラスター内のサーバーを変数に割り当てる`$Servers`:

    ```PowerShell
    $Servers = Get-StorageFaultDomain -Type StorageScaleUnit | Sort FriendlyName
    ```

   > [!TIP]
   > 記憶域スペース ダイレクトでは、' のストレージ スケール ユニット ' という用語は、直接接続されたドライブと外部のエンクロージャをドライブに直接接続を含む 1 つのサーバーに接続されているすべての生のストレージを指します。 このコンテキストで 'server' と同じです。

2. 新しいを使用するサーバーの指定`-StorageFaultDomainsToUse`パラメーターにインデックスを作成して`$Servers`します。 例では、1、2 への割り当てを区切るために、および 3 番目のサーバー (インデックス 0、1、および 2)。

    ```PowerShell
    New-Volume -FriendlyName "MyVolume" -Size 100GB -StorageFaultDomainsToUse $Servers[0,1,2]
    ```

### <a name="see-a-delimited-allocation"></a>区切り記号付きの割り当てを参照してください。

表示する方法*MyVolume*は割り当てを使用して、`Get-VirtualDiskFootprintBySSU.ps1`でスクリプト[付録](#appendix):

```PowerShell
PS C:\> .\Get-VirtualDiskFootprintBySSU.ps1

VirtualDiskFriendlyName TotalFootprint Server1 Server2 Server3 Server4 Server5 Server6
----------------------- -------------- ------- ------- ------- ------- ------- -------
MyVolume                300 GB         100 GB  100 GB  100 GB  0       0       0      
```

Server1、Server2 というと Server3 のみが含まれていますされているスラブには*MyVolume*します。

### <a name="change-a-delimited-allocation"></a>区切られた割り当てを変更します。

使用して、新しい`Add-StorageFaultDomain`と`Remove-StorageFaultDomain`割り当ての区切り方法を変更するコマンドレットです。

たとえば、移動する*MyVolume*によって 1 つのサーバー。

1. 指定する 4 番目のサーバー**できます**格納されているスラブの*MyVolume*:

    ```PowerShell
    Get-VirtualDisk MyVolume | Add-StorageFaultDomain -StorageFaultDomains $Servers[3]
    ```

2. 指定する最初のサーバー**できません**格納されているスラブの*MyVolume*:

    ```PowerShell
    Get-VirtualDisk MyVolume | Remove-StorageFaultDomain -StorageFaultDomains $Servers[0]
    ```

3. 変更を反映するための記憶域プールを再調整します。

    ```PowerShell
    Get-StoragePool S2D* | Optimize-StoragePool
    ```

![2、3、および 4 のサーバーに 1、2、および 3 のサーバーからの一括を移行、スラブを示す図。](media/delimit-volume-allocation/move.gif)

再調整の進行状況を監視する`Get-StorageJob`します。

完了するとことを確認します。 *MyVolume*がを実行して移動`Get-VirtualDiskFootprintBySSU.ps1`もう一度です。

```PowerShell
PS C:\> .\Get-VirtualDiskFootprintBySSU.ps1

VirtualDiskFriendlyName TotalFootprint Server1 Server2 Server3 Server4 Server5 Server6
----------------------- -------------- ------- ------- ------- ------- ------- -------
MyVolume                300 GB         0       100 GB  100 GB  100 GB  0       0      
```

Server1 は含まれていないスラブの*MyVolume* Server04 は代わりに、– できなくなります。

## <a name="best-practices"></a>ベスト プラクティス

ボリュームの割り当てを使用して区切られたときに実行するベスト プラクティスを次に示します。

### <a name="choose-three-servers"></a>3 台のサーバーを選択します。

3 つのサーバーに各 3 方向ミラー ボリュームを区切ります。

### <a name="balance-storage"></a>分散ストレージ

ボリュームのサイズの各サーバーに記憶域の量が割り当てられているを分散します。

### <a name="every-delimited-allocation-unique"></a>一意の区切り記号付き割り当てごと

フォールト トレランスを最大化する各ボリュームの割り当てを一意に、つまりは共有しない*すべて*(が一部重複しては問題ありません)、別のボリュームとそのサーバー。 N のサーバーでは、一意の組み合わせを「N を選択して 3」– ここでは、そのため、いくつかの一般的なクラスター サイズ。

| サーバー (N) の数 | 一意の数 (N は、3 を選択) の割り当ての区切り |
|-----------------------|-----------------------------------------------------|
| 6                     | 20                                                  |
| 8                     | 56                                                  |
| 12                    | 220                                                 |
| 16                    | 560                                                 |

   > [!TIP]
   > この便利なレビューを検討してください。[組み合わせ表記法を選択して](https://betterexplained.com/articles/easy-permutations-and-combinations/)します。

フォールト トレランスを最大化する例を次に示します: すべてのボリュームが一意の区切り記号付きの割り当てを示します。

![一意の割り当て](media/delimit-volume-allocation/unique-allocation.png)

逆に、次の例では、最初の 3 つのボリューム (1、2、および 3 のサーバー) に同じ区切り記号付きの割り当てを使用して (4、5、および 6 のサーバー) に同じ区切り記号付きの割り当てを使用して、最後の 3 つのボリューム。 これはフォールト トレランスを最大化: 複数のボリュームがオフラインになりを同時にアクセスできなくなる 3 つのサーバーが失敗した場合。

![非一意の割り当て](media/delimit-volume-allocation/non-unique-allocation.png)

## <a name="analysis"></a>分析

このセクションでは派生ボリュームがオンラインでアクセス可能なままになることの数学的な確率 (または同等に、まだオンラインでアクセス可能なストレージの比率を予想される) の障害とクラスターのサイズの数の関数として。

   > [!NOTE]
   > このセクションは省略可能な読み取り。 熱心計算を表示する場合は、読み進めてください。 ない場合は、ご心配なきます。[PowerShell での使用状況](#usage-in-powershell)と[ベスト プラクティス](#best-practices)区切り記号付きの割り当てを正常に実装するために必要なだけです。

### <a name="up-to-two-failures-is-always-okay"></a>2 つの障害までは問題では常に

各 3 方向ミラー ボリュームとして、同時に最大 2 つの障害を存続することができます[これらの例](storage-spaces-fault-tolerance.md#examples)その割り当てに関係なく、説明します。 2 つのドライブが失敗するかどうか、または 2 台のサーバーが失敗するか、オンラインでアクセス可能で、通常の割り当てでも、すべて各 3 方向ミラー ボリュームのいずれかのままになります。

### <a name="more-than-half-the-cluster-failing-is-never-okay"></a>問題ありません。、半分以上のクラスターの失敗したことはありません。

逆に、1 回では、サーバーまたはクラスター内のドライブの半分以上失敗した極端なケースで[クォーラムが失われ](understand-quorum.md)すべて 3 方向ミラー ボリュームがオフラインになり、その割り当てに関係なくにアクセスできなくなったとします。

### <a name="what-about-in-between"></a>何との間のですか。

一度に 3 つ以上のエラーが発生する場合は、サーバーとドライブの半分以上がまだ起動で区切られた割り当てのボリュームはオンラインでアクセス可能で、どのサーバーがエラーによってを続ける場合があります。 正確なオッズを決定する数値を実行してみましょう。

わかりやすくするため、ボリュームは独立しているし、上のベスト プラクティスに従って同じ分散 (IID) とその十分な一意の組み合わせは一意であるすべてのボリュームの割り当てに使用できると仮定します。 特定のボリュームは存続する確率も期待の直線性によっては存続する全体的な記憶域の予想される分数。 

指定された**N**うちサーバー **F**に割り当てられているボリュームに、失敗した**3**うちがオフライン場合-と-専用の場合はすべて**3** 間では**F**しませんでした。 ある **(N は、F を選択)** 方法**F**うちが発生するエラー **(F は、3 を選択)** ボリュームをオフラインに移行し、アクセスできなくなると、します。 確率として表現できます。

![P_offline = Fc3 / NcF](media/delimit-volume-allocation/probability-volume-offline.png)

その他のすべてのケースでは、ボリュームはオンラインでアクセス可能をまだ。

![P_online = 1 – (Fc3/NcF)](media/delimit-volume-allocation/probability-volume-online.png)

次の表では、いくつかの一般的なクラスター サイズと最大 5 障害、区切り記号付きの割り当てに通常の割り当てと見なされるすべての場合と比較してフォールト トレランスが増えることを明らかに確率を評価します。

### <a name="with-6-servers"></a>6 つのサーバーで

| 割り当て                           | 1、失敗の確率 | 2 つの障害対応の確率 | 3 つの障害対応の確率 | 4 つの障害対応の確率 | 5 障害対応の確率 |
|--------------------------------------|------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| 通常、6 つすべてのサーバーに分散 | 100%                               | 100%                                | 0%                                  | 0%                                  | 0%                                  |
| 3 台のサーバーのみに区切られます          | 100%                               | 100%                                | 95.0%                               | 0%                                  | 0%                                  |

   > [!NOTE]
   > 3 つ以上のエラー合計 6 つのサーバーからでは後、は、クラスターはクォーラムを失います。

### <a name="with-8-servers"></a>8 台のサーバーで

| 割り当て                           | 1、失敗の確率 | 2 つの障害対応の確率 | 3 つの障害対応の確率 | 4 つの障害対応の確率 | 5 障害対応の確率 |
|--------------------------------------|------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| 通常、8 台すべてのサーバーに分散 | 100%                               | 100%                                | 0%                                  | 0%                                  | 0%                                  |
| 3 台のサーバーのみに区切られます          | 100%                               | 100%                                | 98.2%                               | 94.3%                               | 0%                                  |

   > [!NOTE]
   > 合計 8 台のサーバーからの 4 つ以上のエラーは後、は、クラスターはクォーラムを失います。

### <a name="with-12-servers"></a>12 サーバー

| 割り当て                            | 1、失敗の確率 | 2 つの障害対応の確率 | 3 つの障害対応の確率 | 4 つの障害対応の確率 | 5 障害対応の確率 |
|---------------------------------------|------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| 通常、12 のすべてのサーバーに分散 | 100%                               | 100%                                | 0%                                  | 0%                                  | 0%                                  |
| 3 台のサーバーのみに区切られます           | 100%                               | 100%                                | 99.5%                               | 99.2%                               | 98.7%                               |

### <a name="with-16-servers"></a>16 台のサーバーで

| 割り当て                            | 1、失敗の確率 | 2 つの障害対応の確率 | 3 つの障害対応の確率 | 4 つの障害対応の確率 | 5 障害対応の確率 |
|---------------------------------------|------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| 通常、すべて 16 台のサーバーに分散 | 100%                               | 100%                                | 0%                                  | 0%                                  | 0%                                  |
| 3 台のサーバーのみに区切られます           | 100%                               | 100%                                | 99.8%                               | 99.8%                               | 99.8%                               |

## <a name="frequently-asked-questions"></a>よく寄せられる質問

### <a name="can-i-delimit-some-volumes-but-not-others"></a>一部のボリュームを区切るはできますか。

[はい]。 ボリュームごとの割り当てを区切るかどうか選択できます。

### <a name="does-delimited-allocation-change-how-drive-replacement-works"></a>区切り記号付きの割り当ては、ドライブの交換のしくみを変更しますか。

いいえ、通常の割り当てと同じです。

## <a name="see-also"></a>関連項目

- [記憶域スペース ダイレクトの概要](storage-spaces-direct-overview.md)
- [記憶域スペース ダイレクトのフォールト トレランス](storage-spaces-fault-tolerance.md)

## <a name="appendix"></a>付録

このスクリプトでは、ボリュームの割り当て方法を確認できます。

前述のように使用、コピー/貼り付けと名前を付けて`Get-VirtualDiskFootprintBySSU.ps1`します。

```PowerShell
Function ConvertTo-PrettyCapacity {
    Param (
        [Parameter(
            Mandatory = $True,
            ValueFromPipeline = $True
            )
        ]
    [Int64]$Bytes,
    [Int64]$RoundTo = 0
    )
    If ($Bytes -Gt 0) {
        $Base = 1024
        $Labels = ("bytes", "KB", "MB", "GB", "TB", "PB", "EB", "ZB", "YB")
        $Order = [Math]::Floor( [Math]::Log($Bytes, $Base) )
        $Rounded = [Math]::Round($Bytes/( [Math]::Pow($Base, $Order) ), $RoundTo)
        [String]($Rounded) + " " + $Labels[$Order]
    }
    Else {
        "0"
    }
    Return
}

Function Get-VirtualDiskFootprintByStorageFaultDomain {

    ################################################
    ### Step 1: Gather Configuration Information ###
    ################################################

    Write-Progress -Activity "Get-VirtualDiskFootprintByStorageFaultDomain" -CurrentOperation "Gathering configuration information..." -Status "Step 1/4" -PercentComplete 00

    $ErrorCannotGetCluster = "Cannot proceed because 'Get-Cluster' failed."
    $ErrorNotS2DEnabled = "Cannot proceed because the cluster is not running Storage Spaces Direct."
    $ErrorCannotGetClusterNode = "Cannot proceed because 'Get-ClusterNode' failed."
    $ErrorClusterNodeDown = "Cannot proceed because one or more cluster nodes is not Up."
    $ErrorCannotGetStoragePool = "Cannot proceed because 'Get-StoragePool' failed."
    $ErrorPhysicalDiskFaultDomainAwareness = "Cannot proceed because the storage pool is set to 'PhysicalDisk' fault domain awareness. This cmdlet only supports 'StorageScaleUnit', 'StorageChassis', or 'StorageRack' fault domain awareness."

    Try  {
        $GetCluster = Get-Cluster -ErrorAction Stop
    }
    Catch {
        throw $ErrorCannotGetCluster
    }

    If ($GetCluster.S2DEnabled -Ne 1) {
        throw $ErrorNotS2DEnabled
    }

    Try  {
        $GetClusterNode = Get-ClusterNode -ErrorAction Stop
    }
    Catch {
        throw $ErrorCannotGetClusterNode
    }

    If ($GetClusterNode | Where State -Ne Up) {
        throw $ErrorClusterNodeDown
    }

    Try {
        $GetStoragePool = Get-StoragePool -IsPrimordial $False -ErrorAction Stop
    }
    Catch {
        throw $ErrorCannotGetStoragePool
    }

    If ($GetStoragePool.FaultDomainAwarenessDefault -Eq "PhysicalDisk") {
        throw $ErrorPhysicalDiskFaultDomainAwareness
    }

    ###########################################################
    ### Step 2: Create SfdList[] and PhysicalDiskToSfdMap{} ###
    ###########################################################

    Write-Progress -Activity "Get-VirtualDiskFootprintByStorageFaultDomain" -CurrentOperation "Analyzing physical disk information..." -Status "Step 2/4" -PercentComplete 25

    $SfdList = Get-StorageFaultDomain -Type ($GetStoragePool.FaultDomainAwarenessDefault) | Sort FriendlyName # StorageScaleUnit, StorageChassis, or StorageRack

    $PhysicalDiskToSfdMap = @{} # Map of PhysicalDisk.UniqueId -> StorageFaultDomain.FriendlyName
    $SfdList | ForEach {
        $StorageFaultDomain = $_
        $_ | Get-StorageFaultDomain -Type PhysicalDisk | ForEach {
            $PhysicalDiskToSfdMap[$_.UniqueId] = $StorageFaultDomain.FriendlyName
        }
    }

    ##################################################################################################
    ### Step 3: Create VirtualDisk.FriendlyName -> { StorageFaultDomain.FriendlyName -> Size } Map ###
    ##################################################################################################

    Write-Progress -Activity "Get-VirtualDiskFootprintByStorageFaultDomain" -CurrentOperation "Analyzing virtual disk information..." -Status "Step 3/4" -PercentComplete 50

    $GetVirtualDisk = Get-VirtualDisk | Sort FriendlyName

    $VirtualDiskMap = @{}

    $GetVirtualDisk | ForEach {
        # Map of PhysicalDisk.UniqueId -> Size for THIS virtual disk
        $PhysicalDiskToSizeMap = @{}
        $_ | Get-PhysicalExtent | ForEach {
            $PhysicalDiskToSizeMap[$_.PhysicalDiskUniqueId] += $_.Size
        }
        # Map of StorageFaultDomain.FriendlyName -> Size for THIS virtual disk
        $SfdToSizeMap = @{}
        $PhysicalDiskToSizeMap.keys | ForEach {
            $SfdToSizeMap[$PhysicalDiskToSfdMap[$_]] += $PhysicalDiskToSizeMap[$_]
        }
        # Store
        $VirtualDiskMap[$_.FriendlyName] = $SfdToSizeMap
    }

    #########################
    ### Step 4: Write-Out ###
    #########################

    Write-Progress -Activity "Get-VirtualDiskFootprintByStorageFaultDomain" -CurrentOperation "Formatting output..." -Status "Step 4/4" -PercentComplete 75

    $Output = $GetVirtualDisk | ForEach {
        $Row = [PsCustomObject]@{}

        $VirtualDiskFriendlyName = $_.FriendlyName
        $Row | Add-Member -MemberType NoteProperty "VirtualDiskFriendlyName" $VirtualDiskFriendlyName

        $TotalFootprint = $_.FootprintOnPool | ConvertTo-PrettyCapacity
        $Row | Add-Member -MemberType NoteProperty "TotalFootprint" $TotalFootprint

        $SfdList | ForEach {
            $Size = $VirtualDiskMap[$VirtualDiskFriendlyName][$_.FriendlyName] | ConvertTo-PrettyCapacity
            $Row | Add-Member -MemberType NoteProperty $_.FriendlyName $Size
        }

        $Row
    }

    # Calculate width, in characters, required to Format-Table
    $RequiredWindowWidth = ("TotalFootprint").length + 1 + ("VirtualDiskFriendlyName").length + 1
    $SfdList | ForEach {
        $RequiredWindowWidth += $_.FriendlyName.Length + 1
    }

    $ActualWindowWidth = (Get-Host).UI.RawUI.WindowSize.Width

    If (!($ActualWindowWidth)) {
        # Cannot get window width, probably ISE, Format-List
        Write-Warning "Could not determine window width. For the best experience, use a Powershell window instead of ISE"
        $Output | Format-Table
    }
    ElseIf ($ActualWindowWidth -Lt $RequiredWindowWidth) {
        # Narrower window, Format-List
        Write-Warning "For the best experience, try making your PowerShell window at least $RequiredWindowWidth characters wide. Current width is $ActualWindowWidth characters."
        $Output | Format-List
    }
    Else {
        # Wider window, Format-Table
        $Output | Format-Table
    }
}

Get-VirtualDiskFootprintByStorageFaultDomain
```
