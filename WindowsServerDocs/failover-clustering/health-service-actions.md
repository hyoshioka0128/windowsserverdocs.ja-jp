---
title: ヘルスサービスアクション
ms.prod: windows-server
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
ms.assetid: ''
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: 519f0321f36fb7afc86962950aeab729d7a38adb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361100"
---
# <a name="health-service-actions"></a>ヘルスサービスアクション

> 適用対象:Windows Server 2019、Windows Server 2016

ヘルスサービスは、Windows Server 2016 の新機能であり、記憶域スペースダイレクトを実行しているクラスターの日常的な監視と操作エクスペリエンスを向上させます。

## <a name="actions"></a>Actions  

以下のセクションでは、ヘルス サービスにより自動化されるワークフローについて説明します。 ある操作が自立的に行われていることを検証するため、またはこの操作の進行状況や成果を追跡するために、ヘルス サービスは "アクション" を生成します。 ログとは異なり、アクションは完了後すぐに表示されなくなります。アクションは主に、パフォーマンスや容量に影響を与える可能性がある進行中のアクティビティ (回復性やデータの再調整など) についての情報を提供するためのものです。  

### <a name="usage"></a>使用方法  

1 つの新しい PowerShell コマンドレットで、すべてのアクションを表示できます。  

```PowerShell
Get-StorageHealthAction  
```

### <a name="coverage"></a>対象範囲  

Windows Server 2016 では、 **StorageHealthAction**コマンドレットは次のいずれかの情報を返すことができます。  

-   障害が発生している、接続が損失している、または応答不能の物理ディスクの使用停止  

-   代替物理ディスクを使用するための記憶域プールの切り替え  

-   データへの完全回復性の復元  

-   記憶域プールの再調整  

## <a name="see-also"></a>関連項目

- [Windows Server 2016 のヘルスサービス](health-service-overview.md)
- [MSDN の開発者向けドキュメント、サンプルコード、API リファレンス](https://msdn.microsoft.com/windowshealthservice)
