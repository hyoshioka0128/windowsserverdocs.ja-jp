---
title: クラスターのパフォーマンス履歴
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8ee2e85723cc2449e8cb9c42ccb7d6b761482e3a
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85474869"
---
# <a name="performance-history-for-clusters"></a>クラスターのパフォーマンス履歴

> 適用対象:Windows Server 2019

[記憶域スペースダイレクトのパフォーマンス履歴](performance-history.md)のこのサブトピックでは、クラスターに対して収集されたパフォーマンス履歴について説明します。

クラスターレベルで生成されたシリーズはありません。 代わりに、などのサーバーシリーズ `clusternode.cpu.usage` がクラスター内のすべてのサーバーに対して集計されます。 ボリュームシリーズ (など) `volume.iops.total` は、クラスター内のすべてのボリュームに対して集計されます。 また、などのドライブシリーズ `physicaldisk.size.total` は、クラスター内のすべてのドライブに対して集計されます。

## <a name="usage-in-powershell"></a>PowerShell での使用法

[Get クラスター](https://docs.microsoft.com/powershell/module/failoverclusters/get-cluster)コマンドレットを使用します。

```PowerShell
Get-Cluster | Get-ClusterPerf
```

## <a name="additional-references"></a>その他のリファレンス

- [記憶域スペース ダイレクトのパフォーマンス履歴](performance-history.md)
