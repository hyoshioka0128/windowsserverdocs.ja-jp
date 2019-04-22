---
title: クラスターのパフォーマンス履歴
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
Keywords: 記憶域スペース ダイレクト
ms.localizationpriority: medium
ms.openlocfilehash: 68596cbdcf8593cd3017c8ae5d0836891c78229c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818773"
---
# <a name="performance-history-for-clusters"></a>クラスターのパフォーマンス履歴

> 適用先:Windows Server Insider Preview

このサブ トピックの[記憶域スペース ダイレクトのパフォーマンスの履歴](performance-history.md)クラスター用に収集されたパフォーマンスの履歴について説明します。

クラスター レベルで発生する系列がありません。 代わりに、server シリーズなど`clusternode.cpu.usage`クラスター内のすべてのサーバーごとに集計します。 ボリュームの系列など`volume.iops.total`クラスター内のすべてのボリュームごとに集計します。 など、系列をドライブと`physicaldisk.size.total`クラスター内のすべてのドライブごとに集計します。

## <a name="usage-in-powershell"></a>PowerShell での使用法

使用して、 [Get クラスター](https://docs.microsoft.com/powershell/module/failoverclusters/get-cluster)コマンドレット。

```PowerShell
Get-Cluster | Get-ClusterPerf
```

## <a name="see-also"></a>関連項目

- [記憶域スペース ダイレクトのパフォーマンスの履歴](performance-history.md)
