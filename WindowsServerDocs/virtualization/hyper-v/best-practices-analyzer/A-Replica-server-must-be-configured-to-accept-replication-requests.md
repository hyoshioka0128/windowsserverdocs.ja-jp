---
title: レプリカ サーバーはレプリケーション要求を受け入れるように構成する必要があります。
description: このベスト プラクティス アナライザー ルールによって報告された問題を解決する方法を説明します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: c5e30ddc50b176b83db081a29c6427356ab946c8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827523"
---
# <a name="a-replica-server-must-be-configured-to-accept-replication-requests"></a>レプリカ サーバーはレプリケーション要求を受け入れるように構成する必要があります。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|エラー|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。
  
## <a name="issue"></a>問題  
*このコンピューターでは、HYPER-V レプリカ サーバーとして指定されてがプライマリ サーバーからの受信レプリケーション データを受け入れるように構成されていません。*  
  
## <a name="impact"></a>影響  
*このサーバーでは、プライマリ サーバーからレプリケーション トラフィックを受け入れることはできません。*  
  
## <a name="resolution"></a>解決方法  
*HYPER-V マネージャーを使用すると、プライマリ サーバーからレプリケーション データがこのレプリカ サーバーに受け入れる必要がありますを指定します。*  
  
#### <a name="create-authorization-entries-using-hyper-v-manager"></a>HYPER-V マネージャーを使用して承認エントリを作成します。  
  
1.  Hyper-V マネージャーを開きます。 (サーバー マネージャーで、クリックして **ツールの** > **Hyper V マネージャー**.)  
  
2.  選択し、クリックして 1 つを右クリックし、ホストの一覧から**HYPER-V 設定**します。  
  
3.  ナビゲーション ウィンドウで、**レプリケーション構成**します。  
  
4.  [**承認と記憶域**、] をクリックして **、指定したサーバーからレプリケーションを許可する**します。  
  
5.  以下のサーバーの一覧で、次のようにクリックします。**追加**します。  
  
6.  **承認エントリを追加**:  
  
    -   最初のサーバーの完全修飾名を入力します。  
  
    -   そのサーバーのファイルのみを格納する専用の場所を指定します。  
  
7.  **[OK]** をクリックします。  
  
8.  各プライマリ サーバーを繰り返します。  
  
9. クリックして**OK**もう一度を完了し、ウィンドウを閉じます。  
  
### <a name="create-authorization-entries-using-windows-powershell"></a>Windows PowerShell を使用して承認エントリを作成します。  
  
1.  Windows PowerShell を開きます。 (デスクトップで、[スタート] をクリックし、入力を開始**Windows PowerShell**)。  
  
2.  右クリック **Windows PowerShell**  をクリック **管理者として実行**します。  
  
3.  次のようなコマンドを実行して、置換します。  
  
    -   サーバーの完全修飾ドメイン名と server01.domain01.contoso.com のプライマリ サーバーの名前。  
  
    -   場所 D:\ReplicaVMStorage の場所。  
  
    -   信頼グループに 1 つを作成した場合に、グループの名前を持つ DEFAULT という名前です。 それ以外の場合は、既定値を使用します。  
  
```  
New-VMReplicationAuthorizationEntry server01.domain01.contoso.com D:\ReplicaVMStorage DEFAULT  
```  
  


