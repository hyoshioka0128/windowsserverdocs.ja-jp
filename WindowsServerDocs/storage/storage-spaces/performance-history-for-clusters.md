---
title: クラスターのパフォーマンスの履歴
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: 68596cbdcf8593cd3017c8ae5d0836891c78229c
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2018
ms.locfileid: "1894321"
---
# <a name="performance-history-for-clusters"></a>クラスターのパフォーマンスの履歴

> 対象アプリケーション: Windows Server 内部のプレビュー

[記憶域スペースの直接のパフォーマンス履歴](performance-history.md)のサブこのトピックでは、クラスターの収集のパフォーマンス履歴について説明します。

系列クラスター レベルで発生することはありません。 代わりに、サーバー シリーズでは、次のような`clusternode.cpu.usage`、クラスター内のすべてのサーバーに集計されます。 ボリューム シリーズでは、次のような`volume.iops.total`、クラスター内のすべてのボリュームに集計されます。 系列の次のようなドライブと`physicaldisk.size.total`、クラスター内のすべてのドライブに集計されます。

## <a name="usage-in-powershell"></a>PowerShell での使用

[Get クラスター](https://docs.microsoft.com/powershell/module/failoverclusters/get-cluster)コマンドレットを使用します。

```PowerShell
Get-Cluster | Get-ClusterPerf
```

## <a name="see-also"></a>関連項目

- [記憶域スペースの直接のパフォーマンス履歴](performance-history.md)
