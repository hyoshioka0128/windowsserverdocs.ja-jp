---
title: 理解し、永続的なメモリの展開
description: どの永続的なメモリとを設定する方法、記憶域スペース ダイレクトでは、Windows Server 2019 の詳細についてはします。
keywords: 記憶域スペース ダイレクト、永続的なメモリ、pmem、ストレージ、S2D
ms.assetid: ''
ms.prod: ''
ms.author: adagashe
ms.technology: storage-spaces
ms.topic: article
author: adagashe
ms.date: 3/26/2019
ms.localizationpriority: ''
ms.openlocfilehash: ed4b2669ad35a2ce0f818c65f7024ce905d9e4d6
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280044"
---
---
# <a name="understand-and-deploy-persistent-memory"></a>理解し、永続的なメモリの展開

>適用対象:Windows Server 2019

永続的なメモリ (PMem) は、新しい種類のメモリ テクノロジの大規模な容量を手頃な価格と永続化の組み合わせを提供します。 このトピックでは、PMem と手順では、Windows Server の 2019 記憶域スペース ダイレクトで展開することで、バック グラウンドを提供します。

## <a name="background"></a>背景

PMem は型の非揮発性 DRAM (NVDIMM) DRAM の速度が (メモリの内容のままシステムの電源がダウンした場合でも、予期しない電源切れ、ユーザーが開始したシャット ダウン、システムのクラッシュが発生した場合、電源サイクルによってメモリ コンテンツを保持など)。 このため、した箇所から再開ははるかに高速、RAM の内容を再読み込みする必要があるためです。 別の一意の特性が PMem バイト アドレス指定可能なつまり、このため、記憶域クラス メモリとして参照される PMem 耳にすることがあります) のストレージとして使用することもできます。


これらの特典の一部を表示する見て、これから Microsoft Ignite 2018 のデモ。

[![Microsoft Ignite 2018 Pmem デモ](http://img.youtube.com/vi/8WMXkMLJORc/0.jpg)](http://www.youtube.com/watch?v=8WMXkMLJORc)

フォールト トレランスを必ずしも提供する任意のストレージ システムでは、書き込みでは、ネットワークを通過する必要があり、バックエンド書き込み増幅を負担の分散のコピーを作成します。 このため、絶対的な最大 IOPS ベンチマーク数字は通常によって実現読み取りのみ、記憶域システムがある常識的な最適化を読み取り可能であれば、ローカル コピーからどの記憶域スペース ダイレクトは場合に特にです。

**100% の読み取りでは、クラスターは、13,798,674 IOPS を提供します。**

![13.7 m IOPS レコードのスクリーン ショット](media/deploy-pmem/iops-record.png)

密接に、ビデオを視聴することがわかります thatwhat のさらに多くのドロップその一部始終は、待機時間: 超える 13.7 の M IOPS であっても、ファイル システムでは、Windows が一貫してより小さい 40 マイクロ秒の待機時間を報告します。 (は、シンボルのマイクロ秒、1 つ分の 1 秒) です。どのような一般的なオール フラッシュ ベンダー答えるアドバタイズ今日よりも高速桁違いになります。

同時に、Storage Spaces Direct in Windows Server 2019 と Intel® Optane™ DC の永続的なメモリの配信、常識を覆すパフォーマンス。 IOPS、13.7 M 以上の予測可能で非常に短い待ち時間では、この業界をリードする HCI ベンチマークは、6.7 M IOPS の前、業界をリードするベンチマーク 2 倍以上です。 詳細については、この時間が必要でしただけ 12 個のサーバー ノード、25% が 2 年前よりも少なくなります。

![IOPS の向上](media/deploy-pmem/iops-gains.png)

使用されるハードウェア 3 方向ミラーリングを使用して 12 サーバー クラスター、ReFS ボリュームでは、区切られた**12** x Intel® S2600WFT、 **384 GiB**メモリ、コア 2 x 28"CascadeLake" **1.5 TB**キャッシュとして永続的なメモリを Intel® Optane™ DC **32 TB** NVMe (4 x 8 TB Intel® DC P4510)、容量として**2** Mellanox ConnectX 4 25 Gbps x

次の表では、完全なパフォーマンスの数値があります。 

| ベンチマーク                   | パフォーマンス         |
|-----------------------------|---------------------|
| 4 K の 100% のランダムな読み取り         | 13.8 件の IOPS   |
| 4 K 90/10% ランダム読み取り/書き込み | 9.45 件の IOPS   |
| 2 MB のシーケンシャルな読み取り         | 549 GB/秒のスループット |

### <a name="supported-hardware"></a>サポートされているハードウェア

次の表は、Windows Server 2019 および Windows Server 2016 用の永続的なメモリがサポートされているハードウェアを示します。 メモリ モードとアプリ ダイレクト モードの両方に、Intel Optane を具体的にはサポートすることに注意してください。 Windows Server 2019 では、混合モードの操作をサポートします。

| 永続的なメモリのテクノロジ                                      | Windows Server 2016 | Windows Server 2019 |
|-------------------------------------------------------------------|--------------------------|--------------------------|
| **NVDIMM-N**アプリ ダイレクト モード                                       | サポート対象                | サポート対象                |
| **Intel Optane™ DC の永続的なメモリ**アプリ ダイレクト モード             | サポートされない            | サポート対象                |
| **Intel Optane™ DC の永続的なメモリ**メモリ レベルの 2 つのモード (2LM) | サポートされない            | サポート対象                |

ここで、永続的なメモリを構成する方法について詳しく見ていきます。

## <a name="interleave-sets"></a>インターリーブ セット

### <a name="understanding-interleave-sets"></a>Understanding インターリーブ セット

NVDIMM-N が置かれている標準の DIMM (メモリ) スロットで (つまり、待機時間を短縮とパフォーマンスの向上をフェッチしています) のプロセッサに近い位置でデータを配置することを思い出してください。 これをビルドするには、インターリーブ セットは、2 つ以上の NVDIMMs N-way インターリーブのスループットを向上させるストライプ読み取り/書き込み操作を提供する設定を作成するときにです。 最も一般的な設定は、双方向または 4 ウェイのインターリーブです。

インターリーブ セットは、Windows Server への 1 つの論理ディスクとして表示される複数の永続的なメモリ デバイス プラットフォームの BIOS で多くの場合、作成できます。 各永続的なメモリの論理ディスクにはを実行して、物理デバイスのインターリーブ セットが含まれています。

```PowerShell
Get-PmemDisk
```

出力の例は、以下に示します。

```
DiskNumber Size   HealthStatus AtomicityType CanBeRemoved PhysicalDeviceIds UnsafeShutdownCount
---------- ----   ------------ ------------- ------------ ----------------- -------------------
2          252 GB Healthy      None          True         {20, 120}         0
3          252 GB Healthy      None          True         {1020, 1120}      0
```

論理 pmem ディスク 2 に Id20 と Id120 の物理デバイスがあり、論理 pmem ディスク 3 が Id1020 と Id1120 の物理デバイスことがわかります。 特定 pmem ディスクを次に示すように設定するインターリーブでのすべての物理 NVDIMMs を取得するには、Get-PmemPhysicalDevice もフィードことができます。


```PowerShell
(Get-PmemDisk)[0] | Get-PmemPhysicalDevice
```

出力の例は、以下に示します。

```
DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------------
20       Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_C1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
```

### <a name="configuring-interleave-sets"></a>インターリーブ セットの構成

で、インターリーブ セットを構成するには、次の PowerShell コマンドレットを実行します。

```PowerShell
Get-PmemUnusedRegion

RegionId TotalSizeInBytes DeviceId
-------- ---------------- --------
       1     270582939648 {20, 120}
       3     270582939648 {1020, 1120}
```

これには、システム上の永続的なメモリの論理ディスクに割り当てられていないすべての永続的なメモリのリージョンが表示されます。

デバイスの種類、場所を含む、システムですべての永続的なメモリのデバイス情報を表示するには、正常性と運用の状態などは、ローカル サーバー、次のコマンドレットを実行することができます。

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

使用可能な未使用 pmem 領域があるために、永続的なメモリの新しいディスクを作成できます。 によって使用されていないリージョンを使用して複数の永続的なメモリのディスクを作成できます。

```PowerShell
Get-PmemUnusedRegion | New-PmemDisk
Creating new persistent memory disk. This may take a few moments.
```

これが完了した後を実行して結果が表示ことができます。

```PowerShell
Get-PmemDisk

DiskNumber Size   HealthStatus AtomicityType CanBeRemoved PhysicalDeviceIds UnsafeShutdownCount
---------- ----   ------------ ------------- ------------ ----------------- -------------------
2          252 GB Healthy      None          True         {20, 120}         0
3          252 GB Healthy      None          True         {1020, 1120}      0
```

実行した可能性が注目に値します**Get-physicaldisk |場所 MediaType-eq SCM**の代わりに**Get PmemDisk**同じ結果を取得します。 新しく作成された永続的なメモリ、ディスクでは、PowerShell と Windows Admin Center に表示されるドライブに 1 対 1 対応しています。

### <a name="using-persistent-memory-for-cache-or-capacity"></a>キャッシュまたは容量を永続的なメモリの使用

記憶域スペース ダイレクトでは、Windows Server 2019 は永続的なメモリを使用して、キャッシュまたは容量ドライブとしてサポートしています。 これを参照してください[ドキュメント](understand-the-cache.md)キャッシュ、容量のドライブ設定の詳細についてはします。

## <a name="creating-a-dax-volume"></a>DAX ボリュームを作成します。

### <a name="understanding-dax"></a>DAX について

永続的なメモリにアクセスするための 2 つの方法はあります。 それらは以下のとおりです。

1. **直接アクセス (DAX)** 、最小の待機時間を取得するためのメモリのように動作します。 アプリには、スタックはバイパスされます、永続的なメモリが直接変更します。 この使用できることのみを NTFS に注意してください。
2. **アクセスをブロック**アプリの互換性のための記憶域のように動作します。 このセットアップでは、スタックのデータ フローし、これは、NTFS や refs などので使用できます。

この例は、次に示すことができます。

![DAX のスタック](media/deploy-pmem/dax.png)

### <a name="configuring-dax"></a>DAX の構成

PowerShell コマンドレットを使用して、永続的なメモリの DAX ボリュームを作成する必要があります。 使用して、 **- IsDax**スイッチを有効になっている DAX を使用するボリュームをフォーマットことができます。

```PowerShell
Format-Volume -IsDax:$true
```

次のコード スニペットを使用すると、永続的なメモリ、ディスク上の DAX ボリュームを作成できます。

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

永続的なメモリを使用する場合は、監視のエクスペリエンスのいくつかの違いがあります。

1. 永続的なメモリは、Windows Admin Center でのグラフに表示される場合は表示されませんので、パフォーマンス カウンターの物理ディスクを作成しません。
2. 永続的なメモリは、事前対応型の外れ値を検出しないため、Storport 505 データを作成しません。

別に、監視のエクスペリエンスとは、他の物理ディスクと同じです。 永続的なメモリ、ディスクの正常性クエリを実行してを使用できます。

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

**HealthStatus**永続的なメモリ、ディスクが正常であるかどうかを示しています。 **UnsafeshutdownCount**論理ディスクにデータの損失を引き起こす可能性のあるシャット ダウンの数を追跡します。 このディスクの基になるすべての永続的なメモリ デバイスのシャット ダウンが安全でない数の合計になります。 使うこともできます、次のクエリの状態情報をコマンド。 **OperationalStatus**と**OperationalDetails**正常性状態の詳細について説明します。

永続的なメモリ デバイスの正常性を照会するには。

```PowerShell
Get-PmemPhysicalDevice

DeviceId DeviceType           HealthStatus OperationalStatus PhysicalLocation FirmwareRevision Persistent memory size Volatile memory size
-------- ----------           ------------ ----------------- ---------------- ---------------- ---------------------- --------------------
1020     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_C1     102005310        126 GB                 0 GB
1120     Intel INVDIMM device Healthy      {Ok}              CPU2_DIMM_F1     102005310        126 GB                 0 GB
120      Intel INVDIMM device Healthy      {Ok}              CPU1_DIMM_F1     102005310        126 GB                 0 GB
20       Intel INVDIMM device Unhealthy    {HardwareError}   CPU1_DIMM_C1     102005310        126 GB                 0 GB
```

これは、永続的なメモリ デバイスが正常では示しています。 異常なデバイス (**DeviceId**) 20 が上記の例のケースに一致します。 **PhysicalLocation** BIOS から特定するのに役立ちますどの永続的なメモリ デバイスが障害のある状態。

## <a name="replacing-persistent-memory"></a>永続的なメモリを交換

上記の永続的なメモリのヘルス状態を表示する方法を説明します。 障害が発生したモジュールを交換する必要がある場合は、永続的なメモリ、ディスクをプロビジョニングし直す必要があります (上記で説明した手順を参照してください)。

トラブルシューティングを行うには、使用する必要があります**削除 PmemDisk**、特定の永続的なメモリのディスクを削除します。 によって現在すべての永続ディスクは削除できます。

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

永続的なメモリ、ディスクを削除するがそのディスク上のデータが失われる発生ことに注意してください。

必要に応じて別のコマンドレットは**Initialize PmemPhysicalDevice**、永続的なメモリの物理デバイスで、ラベルの記憶域を初期化するものです。 永続的なメモリ デバイスでストレージ情報を破損したラベルをオフにするために使用できます。

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

重要なは関連する問題を永続的なメモリを修正する最後の手段としてこのコマンドを使用する必要があることに注意してください。 これが永続的なメモリにデータが失われる発生します。

## <a name="see-also"></a>関連項目

- [記憶域スペース ダイレクトの概要](storage-spaces-direct-overview.md)
- [Windows での記憶域クラス メモリ (NVDIMM-N) 状態の管理](storage-class-memory-health.md)
- [キャッシュについて](understand-the-cache.md)