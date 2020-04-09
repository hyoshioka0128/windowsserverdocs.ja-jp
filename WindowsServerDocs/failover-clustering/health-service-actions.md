---
title: ヘルスサービスアクション
ms.prod: windows-server
manager: eldenc
ms.author: cosdar
ms.technology: storage-health-service
ms.topic: article
author: cosmosdarwin
ms.date: 08/14/2017
ms.openlocfilehash: a4ef08a4ca552211b64d11677153775d6b18b4fa
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80827625"
---
# <a name="health-service-actions"></a>ヘルスサービスアクション

> 適用対象: Windows Server 2019、Windows Server 2016

ヘルスサービスは、Windows Server 2016 の新機能であり、記憶域スペースダイレクトを実行しているクラスターの日常的な監視と操作エクスペリエンスを向上させます。

## <a name="actions"></a>操作  

以下のセクションでは、ヘルス サービスにより自動化されるワークフローについて説明します。 ある操作が自立的に行われていることを検証するため、またはこの操作の進行状況や成果を追跡するために、ヘルス サービスは "アクション" を生成します。 ログとは異なり、アクションは完了後すぐに表示されなくなります。アクションは主に、パフォーマンスや容量に影響を与える可能性がある進行中のアクティビティ (回復性やデータの再調整など) についての情報を提供するためのものです。  

### <a name="usage"></a>使用法  

1 つの新しい PowerShell コマンドレットで、すべてのアクションを表示できます。  

```PowerShell
Get-StorageHealthAction  
```

### <a name="coverage"></a>カバレッジ  

Windows Server 2016 では、 **StorageHealthAction**コマンドレットは次のいずれかの情報を返すことができます。  

-   障害が発生している、接続が損失している、または応答不能の物理ディスクの使用停止  

-   代替物理ディスクを使用するための記憶域プールの切り替え  

-   データへの完全回復性の復元  

-   記憶域プールの再調整  

## <a name="see-also"></a>参照

- [Windows Server 2016 のヘルスサービス](health-service-overview.md)
- [MSDN の開発者向けドキュメント、サンプルコード、API リファレンス](https://msdn.microsoft.com/windowshealthservice)
