---
title: ヘルスサービスの設定
ms.prod: windows-server
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: ''
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: 1b10d7c5432b10262e8df85d427f17f402d4f64a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361040"
---
# <a name="health-service-settings"></a>ヘルスサービスの設定
> 適用対象:Windows Server 2019、Windows Server 2016

ヘルスサービスは、Windows Server 2016 の新機能であり、記憶域スペースダイレクトを実行しているクラスターの日常的な監視と操作エクスペリエンスを向上させます。

ヘルスサービスの動作を制御するパラメーターの多くは、設定として公開されます。 これらを変更して、障害やアクションの強度を調整したり、特定の動作をオン/オフにしたりすることができます。

設定を設定または変更するには、次の PowerShell コマンドレットを使用します。

### <a name="usage"></a>使用方法

```PowerShell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name <SettingName> -Value <Value>  
```

#### <a name="example"></a>例

```PowerShell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.Volume.CapacityThreshold.Warning" -Value 70
```

### <a name="common-settings"></a>共通設定

一般的に変更された設定の一部を既定値と共に以下に示します。

#### <a name="volume-capacity-threshold"></a>ボリューム容量のしきい値

```
"System.Storage.Volume.CapacityThreshold.Enabled"  = True
"System.Storage.Volume.CapacityThreshold.Warning"  = 80
"System.Storage.Volume.CapacityThreshold.Critical" = 90
```

#### <a name="pool-reserve-capacity-threshold"></a>プール予約容量のしきい値

```
"System.Storage.StoragePool.CheckPoolReserveCapacity.Enabled" = True
```

#### <a name="physical-disk-lifecycle"></a>物理ディスクのライフサイクル

```
"System.Storage.PhysicalDisk.AutoPool.Enabled"                             = True
"System.Storage.PhysicalDisk.AutoRetire.OnLostCommunication.Enabled"       = True
"System.Storage.PhysicalDisk.AutoRetire.OnUnresponsive.Enabled"            = True
"System.Storage.PhysicalDisk.AutoRetire.DelayMs"                           = 900000 (i.e. 15 minutes)
"System.Storage.PhysicalDisk.Unresponsive.Reset.CountResetIntervalSeconds" = 360 (i.e. 60 minutes)
"System.Storage.PhysicalDisk.Unresponsive.Reset.CountAllowed"              = 3
```

#### <a name="supported-components-document"></a>サポートされているコンポーネントドキュメント

前のセクションを参照してください。

#### <a name="firmware-rollout"></a>ファームウェアのロールアウト

```
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.SingleDrive.Enabled"       = True
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.Enabled"           = True
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.LongDelaySeconds"  = 604800 (i.e. 7 days)
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.ShortDelaySeconds" = 86400 (i.e. 1 day)
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.LongDelayCount"    = 1
"System.Storage.PhysicalDisk.AutoFirmwareUpdate.RollOut.FailureTolerance"  = 3
```

#### <a name="platform--quiescence"></a>Platform/休止

```
"Platform.Quiescence.MinDelaySeconds" = 120 (i.e. 2 minutes)
"Platform.Quiescence.MaxDelaySeconds" = 420 (i.e. 7 minutes)
```

#### <a name="metrics"></a>メトリック

```
"System.Reports.ReportingPeriodSeconds" = 1
```

#### <a name="debugging"></a>デバッグ

```
"System.LogLevel" = 4
```

## <a name="see-also"></a>関連項目

- [Windows Server 2016 のヘルスサービス](health-service-overview.md)
- [Windows Server 2016 の記憶域スペースダイレクト](../storage/storage-spaces/storage-spaces-direct-overview.md)
