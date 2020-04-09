---
title: 記憶域スペースダイレクトのボリュームの割り当てを区切ります。
ms.author: cosmosdarwin
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 03/29/2018
ms.openlocfilehash: 26454881279e1d33392a827f794788370def2cab
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858975"
---
# <a name="delimit-the-allocation-of-volumes-in-storage-spaces-direct"></a>記憶域スペースダイレクトのボリュームの割り当てを区切ります。
> 適用対象: Windows Server 2019

Windows Server 2019 では、記憶域スペースダイレクトでボリュームの割り当てを手動で区切るオプションが導入されています。 これにより、特定の条件下でフォールトトレランスを大幅に向上させることができますが、管理上の考慮事項と複雑さが増加します。 このトピックでは、そのしくみについて説明し、PowerShell の例を示します。

   > [!IMPORTANT]
   > この機能は、Windows Server 2019 で新しく追加された機能です。 Windows Server 2016 では使用できません。 

## <a name="prerequisites"></a>前提条件

### <a name="green-checkmark-icon-consider-using-this-option-if"></a>![緑のチェックマークアイコン。](media/delimit-volume-allocation/supported.png) 次の場合に、このオプションの使用を検討してください。

- クラスターには6台以上のサーバーがあります。そして
- クラスターが[3 方向ミラー](storage-spaces-fault-tolerance.md#mirroring)回復性のみを使用している

### <a name="red-x-icon-do-not-use-this-option-if"></a>![赤色の X アイコン。](media/delimit-volume-allocation/unsupported.png) 次の場合は、このオプションを使用しないでください。

- クラスターのサーバー数が6台未満です。もしくは
- クラスターが[パリティ](storage-spaces-fault-tolerance.md#parity)または[ミラーアクセラレータによるパリティ](storage-spaces-fault-tolerance.md#mirror-accelerated-parity)回復性を使用する

## <a name="understand"></a>概要

### <a name="review-regular-allocation"></a>レビュー: 通常の割り当て

通常の3方向ミラーリングでは、ボリュームは多数の小さな "スラブ" に分割され、3回コピーされ、クラスター内のすべてのサーバーのすべてのドライブに均等に分散されます。 詳細については、この詳細な[ブログ](https://blogs.technet.microsoft.com/filecab/2016/11/21/deep-dive-pool-in-spaces-direct/)を参照してください。

![ボリュームがスラブの3つのスタックに分割され、すべてのサーバーで均等に分散されていることを示す図。](media/delimit-volume-allocation/regular-allocation.png)

この既定の割り当てにより、並列読み取りと書き込みが最大化され、パフォーマンスが向上します。また、各サーバーが均等にビジー状態になり、すべてのドライブが均等にいっぱいになり、すべてのボリュームがオンラインになるか、同時にオフラインになります。 各ボリュームは、[次の例](storage-spaces-fault-tolerance.md#examples)に示すように、最大2つの同時エラーが発生することが保証されます。

ただし、この割り当てでは、ボリュームが同時に3つのエラーを発生させることはできません。 3台のサーバーで障害が発生した場合、または3台のサーバーのドライブが一度に失敗した場合、少なくとも一部のスラブ (確率が非常に高い) が、障害が発生した3台のドライブまたはサーバーに割り当てられているため、ボリュームにアクセスできなくなります。

次の例では、サーバー1、3、および5が同時に失敗します。 多くのスラブには残ったコピーがありますが、次のようなものはありません。

![3台のサーバーが赤で強調表示されていて、全体的なボリュームが赤である図。](media/delimit-volume-allocation/regular-does-not-survive.png)

ボリュームはオフラインになり、サーバーが回復するまでアクセスできなくなります。

### <a name="new-delimited-allocation"></a>新規: 区切られた割り当て

区切られた割り当てでは、使用するサーバーのサブセットを指定します (最小 4)。 ボリュームは、以前と同様に3回コピーされるスラブに分割されますが、すべてのサーバーに割り当てられるのではなく、**指定したサーバーのサブセットにのみスラブが割り当てら**れます。

たとえば、8ノードクラスター (ノード 1 ~ 8) を使用している場合は、ノード1、2、3、4のディスクにのみ配置するボリュームを指定できます。
#### <a name="advantages"></a>長所

この例の割り当てでは、ボリュームは同時に3つのエラーが発生する可能性があります。 ノード1、2、および6がダウンした場合、ボリュームの3つのデータコピーを保持しているノードのうち2つだけがダウンし、ボリュームはオンラインのままになります。

存続確率は、サーバーの数とその他の要因によって異なります。詳細については、「[分析](#analysis)」を参照してください。

#### <a name="disadvantages"></a>欠点

区切られた割り当てにより、管理上の考慮事項と複雑さが増加します。

1. 管理者は、各ボリュームの割り当てを区切ることによって、サーバー間での記憶域使用率のバランスを取るとともに、「[ベストプラクティス](#best-practices)」セクションで説明されているように、サバイバルの確率を高くします。

2. 区切られた割り当てでは、サーバーごとに1つの容量ドライブに相当するものを予約します **(最大値はありません)** 。 これは、通常の割り当てに関して公開されている[推奨事項](plan-volumes.md#choosing-the-size-of-volumes)を超えており、合計4つの容量ドライブを qpu します。

3. サーバー[とそのドライブの削除](remove-servers.md#remove-a-server-and-its-drives)に関するページで説明されているように、サーバーで障害が発生し、交換が必要になった場合、管理者は、新しいサーバーを追加して失敗したボリュームの delimitation を削除することで、影響を受けるボリュームの更新を行います。次の例を参照してください。

## <a name="usage-in-powershell"></a>PowerShell での使用法

`New-Volume` コマンドレットを使用して記憶域スペースダイレクトにボリュームを作成できます。

たとえば、通常の3方向ミラーボリュームを作成するには、次のようにします。

```PowerShell
New-Volume -FriendlyName "MyRegularVolume" -Size 100GB
```

### <a name="create-a-volume-and-delimit-its-allocation"></a>ボリュームを作成し、その割り当てを区切る

3方向ミラーボリュームを作成し、その割り当てを区切るには、次のようにします。

1. まず、クラスター内のサーバーを `$Servers`変数に割り当てます。

    ```PowerShell
    $Servers = Get-StorageFaultDomain -Type StorageScaleUnit | Sort FriendlyName
    ```

   > [!TIP]
   > 記憶域スペースダイレクトでは、"ストレージスケールユニット" という用語は、直接接続されたドライブとドライブを持つ直接接続された外部エンクロージャを含む、1台のサーバーに接続されているすべての未加工のストレージを指します。 このコンテキストでは、' server ' と同じです。

2. 新しい `-StorageFaultDomainsToUse` パラメーターで使用するサーバーと、`$Servers`にインデックスを付けることによって、どのサーバーを使用するかを指定します。 たとえば、1番目、2番目、3番目、および4番目のサーバー (インデックス0、1、2、および 3) への割り当てを区切るには、次のようにします。

    ```PowerShell
    New-Volume -FriendlyName "MyVolume" -Size 100GB -StorageFaultDomainsToUse $Servers[0,1,2,3]
    ```

### <a name="see-a-delimited-allocation"></a>区切られた割り当てを表示する

*Myvolume*がどのように割り当てられているかを確認するには、 [「付録](#appendix):」の `Get-VirtualDiskFootprintBySSU.ps1` スクリプトを使用します。

```PowerShell
PS C:\> .\Get-VirtualDiskFootprintBySSU.ps1

VirtualDiskFriendlyName TotalFootprint Server1 Server2 Server3 Server4 Server5 Server6
----------------------- -------------- ------- ------- ------- ------- ------- -------
MyVolume                300 GB         100 GB  100 GB  100 GB  100 GB  0       0      
```

Server1、Server2、Server3、およびサーバー4にのみ、 *Myvolume*のスラブが含まれていることに注意してください。

### <a name="change-a-delimited-allocation"></a>区切られた割り当てを変更する

新しい `Add-StorageFaultDomain` および `Remove-StorageFaultDomain` のコマンドレットを使用して、割り当ての区切り方法を変更します。

たとえば、1台のサーバーで*Myvolume*を移動するには、次のようにします。

1. 5番目のサーバーがスラブ*Myvolume*を格納**できる**ことを指定します。

    ```PowerShell
    Get-VirtualDisk MyVolume | Add-StorageFaultDomain -StorageFaultDomains $Servers[4]
    ```

2. 最初のサーバーがスラブの*Myvolume*を格納**できない**ことを指定します。

    ```PowerShell
    Get-VirtualDisk MyVolume | Remove-StorageFaultDomain -StorageFaultDomains $Servers[0]
    ```

3. 変更を有効にするために、記憶域プールを再調整します。

    ```PowerShell
    Get-StoragePool S2D* | Optimize-StoragePool
    ```

`Get-StorageJob`による再調整の進行状況を監視できます。

完了したら、`Get-VirtualDiskFootprintBySSU.ps1` を再実行して、 *Myvolume*が移動したことを確認します。

```PowerShell
PS C:\> .\Get-VirtualDiskFootprintBySSU.ps1

VirtualDiskFriendlyName TotalFootprint Server1 Server2 Server3 Server4 Server5 Server6
----------------------- -------------- ------- ------- ------- ------- ------- -------
MyVolume                300 GB         0       100 GB  100 GB  100 GB  100 GB  0      
```

Server1 には*Myvolume*のスラブがなく、代わりに Server5 が使用することに注意してください。

## <a name="best-practices"></a>ベスト プラクティス

区切られたボリューム割り当てを使用する場合のベストプラクティスを次に示します。

### <a name="choose-four-servers"></a>4台のサーバーを選択する

3方向ミラーボリュームをそれぞれ4台のサーバーに区切ります。

### <a name="balance-storage"></a>ストレージのバランスを取る

各サーバーに割り当てられる記憶域の量を調整します。ボリュームのサイズについては考慮します。

### <a name="stagger-delimited-allocation-volumes"></a>区切られた割り当てボリュームの時差

フォールトトレランスを最大化するには、各ボリュームの割り当てを一意にします。つまり、*すべて*のサーバーが別のボリュームと共有されることはありません (重複は問題ありません)。 

たとえば、8ノードシステムの場合: Volume 1: Servers 1、2、3、4 Volume 2: Servers 5、6、7、8 Volume 3: Servers 3、4、5、6 Volume 4: Servers 1、2、7、8

## <a name="analysis"></a>分析

このセクションでは、障害の数とクラスターサイズの機能として、ボリュームがオンラインでアクセス可能である (または、オンラインでアクセス可能なストレージ全体の予想される割合) ことを示す算術確率を導き出します。

   > [!NOTE]
   > このセクションは省略可能です。 数値演算の場合は、「」を参照してください。 そうでない場合は心配しないでください。 [PowerShell の使用方法](#usage-in-powershell)と[ベストプラクティス](#best-practices)は、区切られた割り当てを正常に実装するために必要な作業です。

### <a name="up-to-two-failures-is-always-okay"></a>常に最大2つのエラーが発生する

3方向ミラーボリュームはいずれも、割り当てに関係なく、同時に最大2つの障害に対応できます。 2つのドライブに障害が発生した場合、または2台のサーバーで障害が発生した場合、またはいずれかの場合は、通常の割り当てであっても、3方向ミラーボリュームはオンラインになり、アクセスできます。

### <a name="more-than-half-the-cluster-failing-is-never-okay"></a>クラスターの障害が半分を超えると、問題ありません。

逆に、クラスター内の半分以上のサーバーまたはドライブが一度に失敗した場合は、割り当てに関係なく、[クォーラムが失われ](understand-quorum.md)、3方向ミラーボリュームがすべてオフラインになり、アクセスできなくなります。

### <a name="what-about-in-between"></a>の間には何があるでしょうか。

3回以上の障害が発生しても、少なくとも半数のサーバーとドライブが稼働状態になっている場合、障害が発生しているサーバーによっては、区切られた割り当てを持つボリュームがオンラインでアクセス可能な状態になることがあります。

## <a name="frequently-asked-questions"></a>よく寄せられる質問

### <a name="can-i-delimit-some-volumes-but-not-others"></a>いくつかのボリュームを区切ることはできますか。

はい。 割り当てを区切るかどうかによって、ボリュームごとに選択できます。

### <a name="does-delimited-allocation-change-how-drive-replacement-works"></a>区切られた割り当てはドライブ置換の動作を変更しますか。

いいえ。通常の割り当てと同じです。

## <a name="see-also"></a>参照

- [記憶域スペースダイレクトの概要](storage-spaces-direct-overview.md)
- [記憶域スペースダイレクトのフォールトトレランス](storage-spaces-fault-tolerance.md)

## <a name="appendix"></a>付録

このスクリプトは、ボリュームがどのように割り当てられているかを確認するのに役立ちます。

前述のように使用するには、コピー/貼り付けを行って `Get-VirtualDiskFootprintBySSU.ps1`として保存します。

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
