---
title: 永続メモリの理解と配置
description: 永続メモリの概要と、Windows Server 2019 で記憶域スペースダイレクトを使用して設定する方法の詳細について説明します。
keywords: 記憶域スペースダイレクト、永続メモリ、pmem、ストレージ、S2D
ms.prod: windows-server
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 1/27/2020
ms.localizationpriority: medium
ms.openlocfilehash: a9070d2e2ab73c7882f4b2ef585ccb01986695bb
ms.sourcegitcommit: 07c9d4ea72528401314e2789e3bc2e688fc96001
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822315"
---
# <a name="understand-and-deploy-persistent-memory"></a>永続メモリの理解と配置

> 適用対象: Windows Server 2019

永続メモリ (または PMem) は、手頃な価格の大きな容量と永続性を備えた一意の組み合わせを提供する新しい種類のメモリテクノロジです。 この記事では、記憶域スペースダイレクトを使用して、PMem の背景と、Windows Server 2019 に展開する手順について説明します。

## <a name="background"></a>背景

PMem は、電力サイクルを通じてコンテンツを保持する非揮発性 RAM (NVDIMM) の一種です。 システムの電源が切れた場合でも、予期しない停電、ユーザーによるシャットダウン、システムクラッシュなどが発生した場合でも、メモリの内容は維持されます。 この一意の特性は、ストレージとして PMem を使用することもできることを意味します。 これは、"ストレージクラスメモリ" として、PMem を参照しているユーザーを聞いてくる可能性があります。

これらの利点の一部を確認するには、Microsoft Ignite 2018 の次のデモを参照してください。

[![Microsoft Ignite 2018 Pmem demo](http://img.youtube.com/vi/8WMXkMLJORc/0.jpg)](http://www.youtube.com/watch?v=8WMXkMLJORc)

フォールトトレランスを提供するストレージシステムでは、必ず書き込みの分散コピーが作成されます。 このような操作では、ネットワークを経由し、バックエンドの書き込みトラフィックを増幅する必要があります。 このため、最大の IOPS ベンチマーク番号は、通常、読み取りのみを測定することで達成されます。特に、可能な限りローカルコピーから読み取るためにストレージシステムに共通の意味の最適化がある場合は特にそうです。 記憶域スペースダイレクトは、そのために最適化されています。

**読み取り操作のみを使用して測定された場合、クラスターは 13798674 IOPS を提供します。**

![13.7 m IOPS レコードスクリーンショット](media/deploy-pmem/iops-record.png)

ビデオをよく見ると、さらに多くの jaw が削除されていることがわかります。 Windows のファイルシステムは、13.7 M を超える IOPS でも、常に40μs 未満の待機時間を報告しています。 (これはマイクロ秒の記号で、1秒の万です)。この速度は、一般的なすべての flash ベンダ人格が現在提供しているものよりもはるかに高速です。

Windows Server 2019 および Intel®™ Optane で記憶域スペースダイレクト、DC 永続メモリによってパフォーマンスが飛躍的に向上します。 この業界トップレベルの HCI ベンチマークは、予測可能で非常に短い待機時間で、13.7 M IOPS を超えています。これは、以前の業界トップレベルの6.7 ベンチマークである 6.7 M IOPS を超えています。 さらに、この時点では、12% 未満のサーバーノードを2年前に&mdash;必要があります。

![IOPS の向上](media/deploy-pmem/iops-gains.png)

テストハードウェアは、3方向のミラーリングと区切られた ReFS ボリュームを使用するように構成された12サーバークラスターでした。 **12** x INTEL® S2600WFT、 **384 GiB** memory、2 x 28 コア "cascadelake" **1.5 TB** Intel® Optane™ DC 永続メモリ (キャッシュとして)、32 **TB NVMe** (4 x 8 TB intel® DC P4510) (容量× 2 **x** Mellanox Gbps)。 4 25

次の表は、完全なパフォーマンスの値を示しています。  

| ベンチマーク                   | [パフォーマンス]         |
|-----------------------------|---------------------|
| 4K 100% のランダム読み取り         | 1380万 IOPS   |
| 4K 90/10% ランダム読み取り/書き込み | 945万 IOPS   |
| 2 MB 順次読み取り         | 549 GB/秒のスループット |

### <a name="supported-hardware"></a>サポートされているハードウェア

次の表は、Windows Server 2019 および Windows Server 2016 でサポートされる永続メモリハードウェアを示しています。  

| 永続メモリテクノロジ                                      | Windows Server 2016 | Windows Server 2019 |
|-------------------------------------------------------------------|--------------------------|--------------------------|
| 永続モードでの**NVDIMM**                                  | サポートされる                | サポートされる                |
| アプリダイレクトモードでの**Intel Optane™ DC 永続メモリ**             | サポートしていません。            | サポートされる                |
| **Intel Optane™ DC 永続メモリ**(メモリモード) | サポートされる            | サポートされる                |

> [!NOTE]  
> Intel Optane は、*メモリ*(揮発性) モードと*アプリダイレクト*(永続的) モードの両方をサポートしています。
   
> [!NOTE]  
> 複数の Intel® Optane™ PMem モジュールがあるシステムを、複数の名前空間に分割されたアプリダイレクトモードで再起動すると、関連する論理記憶域ディスクの一部またはすべてにアクセスできなくなる可能性があります。 この問題は、バージョン1903よりも前のバージョンの Windows Server 2019 で発生します。
>   
> このようなアクセスが失われるのは、システムの起動時に、PMem モジュールが未トレーニングまたは失敗したためです。 このような場合は、システム上のすべての PMem モジュールのすべてのストレージ名前空間が失敗します。これには、障害が発生したモジュールに物理的にマップされていない名前空間も含まれます。
>   
> すべての名前空間へのアクセスを復元するには、失敗したモジュールを置き換えます。
>   
> Windows Server 2019 バージョン1903またはそれ以降のバージョンでモジュールが失敗した場合、影響を受けたモジュールに物理的にマップされている名前空間にのみアクセスできなくなります。 その他の名前空間は影響を受けません。

では、永続メモリの構成方法について説明します。

## <a name="interleaved-sets"></a>インターリーブセット

### <a name="understanding-interleaved-sets"></a>インターリーブセットについて

NVDIMM が standard DIMM (メモリ) スロットに存在することを思い出してください。これにより、データがプロセッサの近くに配置されます。 この構成により、待機時間が短縮され、フェッチのパフォーマンスが向上します。 スループットをさらに向上させるために、2つ以上の NVDIMMs が n 方向インターリーブセットを作成して、読み取り/書き込み操作をストライピングします。 最も一般的な構成は、双方向または4方向のインターリーブです。 インターリーブセットを使用すると、複数の永続メモリデバイスが1つの論理ディスクとして Windows Server に表示されるようになります。 次のように、Windows PowerShell の**Get PmemDisk**コマンドレットを使用して、このような論理ディスクの構成を確認できます。

```PowerShell
Get-PmemDisk

DiskNumber Size   HealthStatus AtomicityType CanBeRemoved PhysicalDeviceIds UnsafeShutdownCount
---------- ----   ------------ ------------- ------------ ----------------- -------------------
2          252 GB Healthy      None          True         {20, 120}         0
3          252 GB Healthy      None          True         {1020, 1120}      0
```

論理 PMem ディスク #2 が物理デバイス Id20 と Id120 を使用し、論理 PMem ディスク #3 物理デバイス Id1020 と Id1120 を使用していることがわかります。  

論理ドライブが使用するインターリーブセットに関する詳細情報を取得するには、次のように**取得**します。

```PowerShell
(Get-PmemDisk)[0] | Get-PmemPhysicalDevice

DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------------
20       Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_C1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
```

### <a name="configuring-interleaved-sets"></a>インターリーブセットの構成

インターリーブされたセットを構成するには、まず、システム上の論理 PMem ディスクに割り当てられていないすべての永続メモリ領域を確認します。 これを行うには、次の PowerShell コマンドレットを実行します。

```PowerShell
Get-PmemUnusedRegion

RegionId TotalSizeInBytes DeviceId
-------- ---------------- --------
       1     270582939648 {20, 120}
       3     270582939648 {1020, 1120}
```

デバイスの種類、場所、状態、動作状態など、システム内のすべての PMem デバイス情報を表示するには、ローカルサーバーで次のコマンドレットを実行します。

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

使用可能な使用されていない PMem 領域があるため、新しい永続メモリディスクを作成できます。 未使用の領域を使用して、次のコマンドレットを実行することで、複数の永続メモリディスクを作成できます。

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

Get-PhysicalDisk | を実行できることに注意してください。 **ここ**では、同じ結果を得るために、 **-PmemDisk**ではなく、MEDIATYPE-Eq SCM を指定します。 新しく作成された PMem ディスクは、PowerShell と Windows 管理センターに表示されるドライブと1対1で対応します。

### <a name="using-persistent-memory-for-cache-or-capacity"></a>キャッシュまたは容量に永続的なメモリを使用する

Windows Server 2019 の記憶域スペースダイレクトでは、キャッシュまたは容量ドライブのいずれかとして永続メモリを使用することがサポートされています。 キャッシュと容量のドライブを設定する方法の詳細については、「[記憶域スペースダイレクトのキャッシュについ](understand-the-cache.md)て」を参照してください。

## <a name="creating-a-dax-volume"></a>DAX ボリュームの作成

### <a name="understanding-dax"></a>DAX について

永続メモリにアクセスするには、2つの方法があります。 以下の説明を参照してください。

1. **直接アクセス (DAX)** 。これはメモリのように動作し、待機時間が最短になります。 アプリは、スタックをバイパスして、永続的なメモリを直接変更します。 DAX は NTFS と組み合わせてのみ使用できることに注意してください。
1. アプリの互換性のためにストレージのように動作する**アクセスをブロック**します。 このような場合、データはスタックを介して流れます。 この構成は、NTFS および ReFS と組み合わせて使用できます。

次の図は、DAX 構成の例を示しています。

![DAX スタック](media/deploy-pmem/dax.png)

### <a name="configuring-dax"></a>DAX の構成

永続メモリディスクに DAX ボリュームを作成するには、PowerShell コマンドレットを使用する必要があります。 **-Isdax**スイッチを使用して、DAX が有効になるようにボリュームをフォーマットすることができます。

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

- 永続メモリは物理ディスクのパフォーマンスカウンターを作成しないので、Windows 管理センターのグラフには表示されません。
- 永続メモリは Storport 505 データを作成しないため、プロアクティブな外れ値検出は行われません。

これとは別に、監視エクスペリエンスは他の物理ディスクの場合と同じです。 次のコマンドレットを実行して、永続的なメモリディスクの正常性を照会できます。

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

**HealthStatus**は、PMem ディスクが正常であるかどうかを示します。  

**Unsaf のカウント**値は、この論理ディスクのデータ損失の原因となる可能性があるシャットダウンの数を追跡します。 これは、このディスクの基になるすべての PMem デバイスの安全でないシャットダウン数の合計です。 正常性状態の詳細に**ついては**、get-help などの情報を検索するために、 **Get PmemPhysicalDevice**コマンドレットを使用します。

```PowerShell
Get-PmemPhysicalDevice

DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------------
1020     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_C1     102005310        126 GB                 0 GB
1120     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_F1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
20       Intel INVDIMM device Unhealthy    {HardwareError}   CPU1_DIMM_C1     102005310        126 GB                 0 GB
```

このコマンドレットは、どの永続メモリデバイスが異常であるかを示します。 異常なデバイス (**DeviceId** 20) は、前の例のケースと一致します。 BIOS の**PhysicalLocation**を使用すると、どの永続メモリデバイスが障害状態であるかを特定するのに役立ちます。

## <a name="replacing-persistent-memory"></a>永続メモリの置換

この記事では、永続メモリの正常性状態を表示する方法について説明します。 障害が発生したモジュールを交換する必要がある場合は、PMem ディスクを再プロビジョニングする必要があります (前に説明した手順を参照してください)。

トラブルシューティングを行うときに、**削除 PmemDisk**を使用する必要がある場合があります。 このコマンドレットは、特定の永続メモリディスクを削除します。 次のコマンドレットを実行して、現在のすべての PMem ディスクを削除できます。

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

> [!IMPORTANT]  
> 永続メモリディスクを削除すると、そのディスク上のデータが失われます。

もう1つのコマンドレットには**Initialize-PmemPhysicalDevice**を使用する必要があります。 このコマンドレットは、物理永続メモリデバイスのラベル記憶域領域を初期化し、PMem デバイス上の破損したラベルストレージ情報を消去できます。

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

> [!IMPORTANT]  
> **Initialize-PmemPhysicalDevice は、** 永続メモリ内のデータ損失を発生させます。 これは、永続メモリ関連の問題を修正するための最後の手段として使用します。

## <a name="see-also"></a>「

- [記憶域スペースダイレクトの概要](storage-spaces-direct-overview.md)
- [Windows での記憶域クラスメモリ (NVDIMM) の正常性管理](storage-class-memory-health.md)
- [キャッシュについて](understand-the-cache.md)
