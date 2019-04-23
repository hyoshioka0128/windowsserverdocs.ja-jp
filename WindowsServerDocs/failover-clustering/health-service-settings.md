---
title: ヘルス サービスの設定
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: ''
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: 569cf7ba30fd3f993394efd3735a56d116c067e0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858333"
---
# <a name="health-service-settings"></a>ヘルス サービスの設定
> 適用対象: Windows Server 2016

ヘルス サービスは、日常的な監視を強化する Windows Server 2016 で記憶域スペース ダイレクトを実行するクラスターの運用エクスペリエンスの新しい機能です。

ヘルス サービスの動作を制御するパラメーターの多くは、設定として公開されます。 これらの障害またはアクションの強度を調整は、オン/オフ、特定の動作を有効にして詳細を変更できます。

次の PowerShell コマンドレットを使用して、設定を設定または変更します。

### <a name="usage"></a>使用方法

```PowerShell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name <SettingName> -Value <Value>  
```

#### <a name="example"></a>例

```PowerShell
Get-StorageSubSystem Cluster* | Set-StorageHealthSetting -Name "System.Storage.Volume.CapacityThreshold.Warning" -Value 70
```

### <a name="common-settings"></a>共通設定

一部のよく変更される設定は、既定値と共に、以下に示します。

#### <a name="volume-capacity-threshold"></a>ボリューム容量のしきい値

```
"System.Storage.Volume.CapacityThreshold.Enabled"  = True
"System.Storage.Volume.CapacityThreshold.Warning"  = 80
"System.Storage.Volume.CapacityThreshold.Critical" = 90
```

#### <a name="pool-reserve-capacity-threshold"></a>プールの予約容量のしきい値

```
"System.Storage.StoragePool.CheckPoolReserveCapacity.Enabled" = True
```

#### <a name="physical-disk-lifecycle"></a>物理ディスクのライフ サイクル

```
"System.Storage.PhysicalDisk.AutoPool.Enabled"                             = True
"System.Storage.PhysicalDisk.AutoRetire.OnLostCommunication.Enabled"       = True
"System.Storage.PhysicalDisk.AutoRetire.OnUnresponsive.Enabled"            = True
"System.Storage.PhysicalDisk.AutoRetire.DelayMs"                           = 900000 (i.e. 15 minutes)
"System.Storage.PhysicalDisk.Unresponsive.Reset.CountResetIntervalSeconds" = 360 (i.e. 60 minutes)
"System.Storage.PhysicalDisk.Unresponsive.Reset.CountAllowed"              = 3
```

#### <a name="supported-components-document"></a>サポートされているコンポーネントのドキュメント

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

#### <a name="platform--quiescence"></a>プラットフォーム/休止

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

- [Windows Server 2016 でヘルス サービス](health-service-overview.md)
- [Windows Server 2016 での記憶域スペース ダイレクト](../storage/storage-spaces/storage-spaces-direct-overview.md)
