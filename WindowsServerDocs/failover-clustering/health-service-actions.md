---
title: ヘルス サービスの動作
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: ''
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: efdf8f04e68fcbdc7051e78d6725cb919e740ffa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843023"
---
# <a name="health-service-actions"></a>ヘルス サービスの動作

> 適用対象: Windows Server 2016

ヘルス サービスは、日常的な監視を強化する Windows Server 2016 で記憶域スペース ダイレクトを実行するクラスターの運用エクスペリエンスの新しい機能です。

## <a name="actions"></a>Actions  

以下のセクションでは、ヘルス サービスにより自動化されるワークフローについて説明します。 ある操作が自立的に行われていることを検証するため、またはこの操作の進行状況や成果を追跡するために、ヘルス サービスは "アクション" を生成します。 ログとは異なり、アクションは完了後すぐに表示されなくなります。アクションは主に、パフォーマンスや容量に影響を与える可能性がある進行中のアクティビティ (回復性やデータの再調整など) についての情報を提供するためのものです。  

### <a name="usage"></a>使用方法  

1 つの新しい PowerShell コマンドレットで、すべてのアクションを表示できます。  

```PowerShell
Get-StorageHealthAction  
```

### <a name="coverage"></a>対象範囲  

Windows Server 2016 で、 **Get StorageHealthAction**コマンドレットには、次の情報を返すことができます。  

-   障害が発生している、接続が損失している、または応答不能の物理ディスクの使用停止  

-   代替物理ディスクを使用するための記憶域プールの切り替え  

-   データへの完全回復性の復元  

-   記憶域プールの再調整  

## <a name="see-also"></a>関連項目

- [Windows Server 2016 でヘルス サービス](health-service-overview.md)
- [開発者向けドキュメント、サンプル コード、および msdn API リファレンス](https://msdn.microsoft.com/windowshealthservice)
