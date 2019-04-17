---
title: "ヘルス サービス アクション"
ms.prod: windows-server-threshold
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: 
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: efdf8f04e68fcbdc7051e78d6725cb919e740ffa
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/17/2017
---
# <a name="health-service-actions"></a>ヘルス サービス アクション

> Windows Server 2016 に適用されます。

ヘルス サービスは、日常的な監視、改善する Windows Server 2016 と記憶域スペース ダイレクトを実行するクラスター操作エクスペリエンスの新機能です。

## <a name="actions"></a>アクション  

次のセクションでは、ヘルス サービスで自動化されるワークフローについて説明します。 操作が行われている自律的に、その進行状況や成果を追跡するため、ヘルス サービスは「アクション」を生成ことを確認します。 ログとは異なり直後に完了したら、パフォーマンスや容量 (回復性の復元またはデータの再調整など) に影響を与える可能性が進行中のアクティビティを把握するには、主には、アクションが消えます。  

### <a name="usage"></a>使用状況  

1 つの新しい PowerShell コマンドレットでは、すべてのアクションが表示されます。  

```PowerShell
Get-StorageHealthAction  
```

### <a name="coverage"></a>カバレッジ  

Windows Server 2016 で、 **Get StorageHealthAction**コマンドレットは、次の情報のいずれかを返すことができます。  

-   接続の障害が発生した、紛失した、または応答不能の物理ディスクの使用を中止します。  

-   代替物理ディスクを使用する記憶域プールの切り替え  

-   データを完全回復性を復元します。  

-   記憶域プールを再分配  

## <a name="see-also"></a>参照してください。

- [Windows Server 2016 のヘルス サービス](health-service-overview.md)
- [開発者向けドキュメント、サンプル コード、および (msdn) API リファレンス](https://msdn.microsoft.com/windowshealthservice)
