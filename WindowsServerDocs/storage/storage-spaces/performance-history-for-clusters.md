---
title: クラスターのパフォーマンス履歴
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: e013295364ae2951ffe8a963fb61a85d7863f5b6
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/23/2020
ms.locfileid: "86962054"
---
# <a name="performance-history-for-clusters"></a>クラスターのパフォーマンス履歴

> 適用対象:Windows Server 2019

[記憶域スペースダイレクトのパフォーマンス履歴](performance-history.md)のこのサブトピックでは、クラスターに対して収集されたパフォーマンス履歴について説明します。

クラスターレベルで生成されたシリーズはありません。 代わりに、などのサーバーシリーズ `clusternode.cpu.usage` がクラスター内のすべてのサーバーに対して集計されます。 ボリュームシリーズ (など) `volume.iops.total` は、クラスター内のすべてのボリュームに対して集計されます。 また、などのドライブシリーズ `physicaldisk.size.total` は、クラスター内のすべてのドライブに対して集計されます。

## <a name="usage-in-powershell"></a>PowerShell での使用法

[Get クラスター](/powershell/module/failoverclusters/get-cluster)コマンドレットを使用します。

```PowerShell
Get-Cluster | Get-ClusterPerf
```

## <a name="additional-references"></a>その他のリファレンス

- [記憶域スペース ダイレクトのパフォーマンス履歴](performance-history.md)
