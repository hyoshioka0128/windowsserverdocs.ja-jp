---
title: クラスターのパフォーマンス履歴
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7a5eec986d6e7d633f1917c599ab6fcd244c7008
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856205"
---
# <a name="performance-history-for-clusters"></a>クラスターのパフォーマンス履歴

> 適用対象: Windows Server 2019

[記憶域スペースダイレクトのパフォーマンス履歴](performance-history.md)のこのサブトピックでは、クラスターに対して収集されたパフォーマンス履歴について説明します。

クラスターレベルで生成されたシリーズはありません。 代わりに、`clusternode.cpu.usage`などのサーバーシリーズがクラスター内のすべてのサーバーに対して集計されます。 `volume.iops.total`などのボリュームシリーズは、クラスター内のすべてのボリュームについて集計されます。 また、`physicaldisk.size.total`などのドライブシリーズは、クラスター内のすべてのドライブについて集計されます。

## <a name="usage-in-powershell"></a>PowerShell での使用法

[Get クラスター](https://docs.microsoft.com/powershell/module/failoverclusters/get-cluster)コマンドレットを使用します。

```PowerShell
Get-Cluster | Get-ClusterPerf
```

## <a name="see-also"></a>参照

- [記憶域スペースダイレクトのパフォーマンス履歴](performance-history.md)
