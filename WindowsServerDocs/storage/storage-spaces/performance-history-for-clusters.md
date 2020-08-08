---
title: クラスターのパフォーマンス履歴
ms.author: cosdar
manager: eldenc
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: ea80be97e3940850f9892c50c534c3449fd3ecdb
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954669"
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

## <a name="additional-references"></a>その他の参照情報

- [記憶域スペース ダイレクトのパフォーマンス履歴](performance-history.md)
