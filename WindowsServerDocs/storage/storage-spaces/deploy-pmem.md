---
title: 永続メモリの理解と配置
description: 永続メモリの概要と、Windows Server 2019 で記憶域スペースダイレクトを使用して設定する方法の詳細について説明します。
keywords: 記憶域スペースダイレクト、永続メモリ、pmem、ストレージ、S2D
ms.assetid: ''
ms.prod: ''
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 3/26/2019
ms.localizationpriority: ''
ms.openlocfilehash: 549cc6dbeec3d414e886f6ebf32315ae13627812
ms.sourcegitcommit: de71970be7d81b95610a0977c12d456c3917c331
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/04/2019
ms.locfileid: "71940806"
---
---
# <a name="understand-and-deploy-persistent-memory"></a>永続メモリの理解と配置

>適用対象:Windows Server 2019

永続メモリ (または PMem) は、手頃な価格の大きな容量と永続性を備えた一意の組み合わせを提供する新しい種類のメモリテクノロジです。 このトピックでは、PMem の背景と、記憶域スペースダイレクトで Windows Server 2019 を使用して展開する手順について説明します。

## <a name="background"></a>背景情報

PMem は、電力サイクルを通じてコンテンツを保持する非揮発性 RAM (NVDIMM) の一種です。 予期しない停電、ユーザーによるシャットダウン、システムクラッシュなどが発生した場合でも、システムの電源が切れた場合でも、メモリの内容は維持されます。この一意の特性は、PMem をストレージとして使用することもできることを意味します。これは、"ストレージクラスメモリ" として参照される可能性があるためです。

これらの利点の一部を確認するには、Microsoft Ignite 2018 からのこのデモを見てみましょう。

[![Microsoft Ignite 2018 Pmem デモ](http://img.youtube.com/vi/8WMXkMLJORc/0.jpg)](http://www.youtube.com/watch?v=8WMXkMLJORc)

フォールトトレランスを提供するすべてのストレージシステムは、ネットワークを経由してバックエンドの書き込み増幅を発生させる必要がある、書き込みの分散コピーを必ず作成します。 このため、最大の IOPS ベンチマーク番号は、通常、読み取り専用で実現されます。特に、ストレージシステムが、可能な限りローカルコピーからの読み取りを行うための共通の最適化がある場合は、特に記憶域スペースダイレクトます。

**100% の読み取りでは、クラスターは 13798674 IOPS を提供します。**

![13.7 m IOPS レコードスクリーンショット](media/deploy-pmem/iops-record.png)

ビデオをよく見ると、さらに多くの jaw を削除することが待機時間であることがわかります。 13.7 M を超える IOPS であっても、Windows のファイルシステムは、常に40μs 未満の待機時間を報告しています。 (これはマイクロ秒の記号で、1秒の万です)。これは、一般的なすべての flash ベンダ人格が現在提供しているものよりもはるかに高速な順序です。

Windows Server 2019 および Intel®™ Optane で記憶域スペースダイレクト、DC 永続メモリによってパフォーマンスが飛躍的に向上します。 この業界最先端の HCI ベンチマークは、予測可能で非常に短い待機時間で、13.7 M IOPS を超えています。これは、以前の業界トップレベルの6.7 ベンチマークである 6.7 M IOPS を超えています。 さらに、今回は12台のサーバーノードだけが必要でした。

![IOPS の向上](media/deploy-pmem/iops-gains.png)

使用されるハードウェアは、3方向のミラーリングと区切られた ReFS ボリュームを使用する12台のサーバークラスターで、 **12** x INTEL® S2600WFT、 **384 GiB** memory、2 x 28 コア "cascadelake"、 **1.5 TB** Intel® Optane™ DC 永続メモリ (キャッシュ)、 **32 TB** NVMe (4 x 8 TB Intel® DC P4510) 容量、 **2** x Mellanox/4 25 Gbps

次の表には、完全なパフォーマンスの数値が含まれています。 

| ベンチマーク                   | パフォーマンス         |
|-----------------------------|---------------------|
| 4K 100% のランダム読み取り         | 1380万 IOPS   |
| 4K 90/10% ランダム読み取り/書き込み | 945万 IOPS   |
| 2 MB 順次読み取り         | 549 GB/秒のスループット |

### <a name="supported-hardware"></a>サポートされているハードウェア

次の表は、Windows Server 2019 および Windows Server 2016 でサポートされている永続メモリハードウェアを示しています。 Intel Optane では、メモリ (揮発性) とアプリダイレクト (つまり、 永続的) モード。

| 永続メモリテクノロジ                                      | Windows Server 2016 | Windows Server 2019 |
|-------------------------------------------------------------------|--------------------------|--------------------------|
| 永続モードでの**NVDIMM**                                  | Supported                | Supported                |
| アプリダイレクトモードでの**Intel Optane™ DC 永続メモリ**             | サポート非対象            | Supported                |
| **Intel Optane™ DC 永続メモリ**(メモリモード) | Supported            | Supported                |

では、永続メモリの構成方法について説明します。

## <a name="interleave-sets"></a>インターリーブセット

### <a name="understanding-interleave-sets"></a>インターリーブセットについて

NVDIMM が standard DIMM (メモリ) スロットに存在し、プロセッサの近くにデータが配置されていることを思い出してください。これにより、待機時間が短縮され、パフォーマンスが向上します。 これを基にして、インターリーブセットは、2つ以上の NVDIMMs が N 方向インターリーブセットを作成し、スループットを向上させるためにストライプの読み取り/書き込み操作を行う場合に使用します。 最も一般的な設定は、2方向または4方向のインターリーブです。

インターリーブセットは、多くの場合、複数の永続メモリデバイスが1つの論理ディスクとして Windows Server に表示されるように、プラットフォームの BIOS で作成できます。 各永続メモリ論理ディスクには、次のものを実行して、物理デバイスのインターリーブセットが含まれています。

```PowerShell
Get-PmemDisk
```

出力例を次に示します。

```
DiskNumber Size   HealthStatus AtomicityType CanBeRemoved PhysicalDeviceIds UnsafeShutdownCount
---------- ----   ------------ ------------- ------------ ----------------- -------------------
2          252 GB Healthy      None          True         {20, 120}         0
3          252 GB Healthy      None          True         {1020, 1120}      0
```

論理 pmem ディスク #2 には、Id20 と Id120 の物理デバイスと論理 pmem ディスク #3 Id1020 と Id1120 の物理デバイスがあることがわかります。 また、次のように、特定の pmem ディスクを使用して、インターリーブセット内のすべての物理 NVDIMMs を取得することもできます。


```PowerShell
(Get-PmemDisk)[0] | Get-PmemPhysicalDevice
```

出力例を次に示します。

```
DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------------
20       Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_C1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
```

### <a name="configuring-interleave-sets"></a>インターリーブセットの構成

インターリーブセットを構成するには、次の PowerShell コマンドレットを実行します。

```PowerShell
Get-PmemUnusedRegion

RegionId TotalSizeInBytes DeviceId
-------- ---------------- --------
       1     270582939648 {20, 120}
       3     270582939648 {1020, 1120}
```

これは、システム上の論理永続メモリディスクに割り当てられていないすべての永続メモリ領域を示しています。

デバイスの種類、場所、状態、動作状態など、システム内のすべての永続的なメモリデバイス情報を表示するには、ローカルサーバーで次のコマンドレットを実行します。

```PowerShell
Get-PmemPhysicalDevice

DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile
                                                                                                                      memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------
1020     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_C1     102005310        126 GB                 0 GB
1120     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_F1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
20       Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_C1     102005310        126 GB                 0 GB
```

使用されていない pmem 領域があるため、新しい永続メモリディスクを作成できます。 未使用の領域を使用して複数の永続メモリディスクを作成するには、次の方法があります。

```PowerShell
Get-PmemUnusedRegion | New-PmemDisk
Creating new persistent memory disk. This may take a few moments.
```

この処理が完了すると、次のように実行して結果を確認できます。

```PowerShell
Get-PmemDisk

DiskNumber Size   HealthStatus AtomicityType CanBeRemoved PhysicalDeviceIds UnsafeShutdownCount
---------- ----   ------------ ------------- ------------ ----------------- -------------------
2          252 GB Healthy      None          True         {20, 120}         0
3          252 GB Healthy      None          True         {1020, 1120}      0
```

Get PhysicalDisk | を実行できることに注意してください。 **ここ**では、同じ結果を得るために、 **-PmemDisk**ではなく、MEDIATYPE-Eq SCM を指定します。 新しく作成された永続メモリディスクは、PowerShell と Windows 管理センターに表示されるドライブに1:1 対応します。

### <a name="using-persistent-memory-for-cache-or-capacity"></a>キャッシュまたは容量に永続的なメモリを使用する

Windows Server 2019 の記憶域スペースダイレクトでは、キャッシュまたは容量ドライブとして永続メモリの使用がサポートされています。 キャッシュと容量のドライブの設定の詳細については、こちらの[ドキュメント](understand-the-cache.md)を参照してください。

## <a name="creating-a-dax-volume"></a>DAX ボリュームの作成

### <a name="understanding-dax"></a>DAX について

永続メモリにアクセスするには、2つの方法があります。 これらは次のとおりです。

1. **直接アクセス (DAX)** 。これはメモリのように動作し、待機時間が最短になります。 アプリは、スタックをバイパスして、永続的なメモリを直接変更します。 これは NTFS でのみ使用できることに注意してください。
2. アプリの互換性のためにストレージのように動作する**アクセスをブロック**します。 データはこのセットアップのスタックを経由し、NTFS および ReFS と共に使用できます。

この例を次に示します。

![DAX スタック](media/deploy-pmem/dax.png)

### <a name="configuring-dax"></a>DAX の構成

永続メモリに DAX ボリュームを作成するには、PowerShell コマンドレットを使用する必要があります。 **-Isdax**スイッチを使用して、DAX が有効になるようにボリュームをフォーマットすることができます。

```PowerShell
Format-Volume -IsDax:$true
```

次のコードスニペットは、永続的なメモリディスクに DAX ボリュームを作成するのに役立ちます。

```PowerShell
# Here we use the first pmem disk to create the volume as an example
$disk = (Get-PmemDisk)[0] | Get-PhysicalDisk | Get-Disk
# Initialize the disk to GPT if it is not initialized
If ($disk.partitionstyle -eq "RAW") {$disk | Initialize-Disk -PartitionStyle GPT}
# Create a partition with drive letter 'S' (can use any available drive letter)
$disk | New-Partition -DriveLetter S -UseMaximumSize


   DiskPath: \\?\scmld#ven_8980&dev_097a&subsys_89804151&rev_0018#3&1b1819f6&0&03018089fb63494db728d8418b3cbbf549997891#{53f56307-b6
bf-11d0-94f2-00a0c91efb8b}

PartitionNumber  DriveLetter Offset                                               Size Type
---------------  ----------- ------                                               ---- ----
2                S           16777216                                        251.98 GB Basic

# Format the volume with drive letter 'S' to DAX Volume
Format-Volume -FileSystem NTFS -IsDax:$true -DriveLetter S

DriveLetter FriendlyName FileSystemType DriveType HealthStatus OperationalStatus SizeRemaining      Size
----------- ------------ -------------- --------- ------------ ----------------- -------------      ----
S                        NTFS           Fixed     Healthy      OK                    251.91 GB 251.98 GB

# Verify the volume is DAX enabled
Get-Partition -DriveLetter S | fl


UniqueId             : {00000000-0000-0000-0000-000100000000}SCMLD\VEN_8980&DEV_097A&SUBSYS_89804151&REV_0018\3&1B1819F6&0&03018089F
                       B63494DB728D8418B3CBBF549997891:WIN-8KGI228ULGA
AccessPaths          : {S:\, \\?\Volume{cf468ffa-ae17-4139-a575-717547d4df09}\}
DiskNumber           : 2
DiskPath             : \\?\scmld#ven_8980&dev_097a&subsys_89804151&rev_0018#3&1b1819f6&0&03018089fb63494db728d8418b3cbbf549997891#{5
                       3f56307-b6bf-11d0-94f2-00a0c91efb8b}
DriveLetter          : S
Guid                 : {cf468ffa-ae17-4139-a575-717547d4df09}
IsActive             : False
IsBoot               : False
IsHidden             : False
IsOffline            : False
IsReadOnly           : False
IsShadowCopy         : False
IsDAX                : True                   # <- True: DAX enabled
IsSystem             : False
NoDefaultDriveLetter : False
Offset               : 16777216
OperationalStatus    : Online
PartitionNumber      : 2
Size                 : 251.98 GB
Type                 : Basic
```

## <a name="monitoring-health"></a>正常性の監視

永続メモリを使用する場合、監視エクスペリエンスにはいくつかの違いがあります。

1. 永続メモリは物理ディスクのパフォーマンスカウンターを作成しないため、Windows 管理センターのグラフに表示されるかどうかはわかりません。
2. 永続メモリは Storport 505 データを作成しないため、プロアクティブな外れ値検出は行われません。

これとは別に、監視エクスペリエンスは他の物理ディスクと同じです。 次のように実行して、永続メモリディスクの正常性を照会できます。

```PowerShell
Get-PmemDisk

DiskNumber Size   HealthStatus AtomicityType CanBeRemoved PhysicalDeviceIds UnsafeShutdownCount
---------- ----   ------------ ------------- ------------ ----------------- -------------------
2          252 GB Unhealthy    None          True         {20, 120}         2
3          252 GB Healthy      None          True         {1020, 1120}      0

Get-PmemDisk | Get-PhysicalDisk | select SerialNumber, HealthStatus, OperationalStatus, OperationalDetails

SerialNumber               HealthStatus OperationalStatus  OperationalDetails
------------               ------------ ------------------ ------------------
802c-01-1602-117cb5fc      Healthy      OK
802c-01-1602-117cb64f      Warning      Predictive Failure {Threshold Exceeded,NVDIMM_N Error}
```

**HealthStatus**は、永続メモリディスクが正常であるかどうかを示します。 **Unsaf**は、この論理ディスクのデータ損失の原因となる可能性があるシャットダウンの数を追跡します。 これは、このディスクの基になるすべての永続メモリデバイスの unsafe シャットダウンカウントの合計です。 次のコマンドを使用して正常性の情報を照会することもできます。 **OperationalStatus**と**OperationalDetails**は、正常性状態に関する詳細情報を提供します。

永続メモリデバイスの正常性を照会するには:

```PowerShell
Get-PmemPhysicalDevice

DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------------
1020     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_C1     102005310        126 GB                 0 GB
1120     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_F1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
20       Intel INVDIMM device Unhealthy    {HardwareError}   CPU1_DIMM_C1     102005310        126 GB                 0 GB
```

これは、どの永続メモリデバイスが異常であるかを示します。 異常なデバイス (**DeviceId**) 20 は、上記の例のケースに一致します。 BIOS から**PhysicalLocation**を使用すると、障害が発生している永続メモリデバイスを特定するのに役立ちます。

## <a name="replacing-persistent-memory"></a>永続メモリの置換

ここでは、永続メモリの正常性状態を表示する方法について説明します。 障害が発生したモジュールを交換する必要がある場合は、永続メモリディスクを再プロビジョニングする必要があります (上記の手順を参照してください)。

トラブルシューティングを行うときに、特定の永続メモリディスクを削除する**削除 PmemDisk**を使用する必要がある場合があります。 現在のすべての永続ディスクを削除するには、次の方法があります。

```PowerShell
Get-PmemDisk | Remove-PmemDisk

cmdlet Remove-PmemDisk at command pipeline position 1
Supply values for the following parameters:
DiskNumber: 2

This will remove the persistent memory disk(s) from the system and will result in data loss.
Remove the persistent memory disk(s)?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): Y
Removing the persistent memory disk. This may take a few moments.
```

永続メモリディスクを削除すると、そのディスク上のデータが失われることに注意してください。

別のコマンドレットが必要になることもあります。 **PmemPhysicalDevice**は、物理永続メモリデバイスのラベルストレージ領域を初期化します。 これは、永続メモリデバイスの破損したラベルのストレージ情報を消去するために使用できます。

```PowerShell
Get-PmemPhysicalDevice | Initialize-PmemPhysicalDevice

This will initialize the label storage area on the physical persistent memory device(s) and will result in data loss.
Initializes the physical persistent memory device(s)?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "Y"): A
Initializing the physical persistent memory device. This may take a few moments.
Initializing the physical persistent memory device. This may take a few moments.
Initializing the physical persistent memory device. This may take a few moments.
Initializing the physical persistent memory device. This may take a few moments.
```

このコマンドは、永続的なメモリ関連の問題を修正するための最後の手段として使用する必要があることに注意してください。 これにより、永続メモリへのデータ損失が発生します。

## <a name="see-also"></a>関連項目

- [記憶域スペースダイレクトの概要](storage-spaces-direct-overview.md)
- [Windows での記憶域クラスメモリ (NVDIMM) の正常性管理](storage-class-memory-health.md)
- [キャッシュについて](understand-the-cache.md)
