---
title: レプリカ サーバーは、特定のプライマリ サーバーがレプリケーション トラフィックを送信する権限を特定するように構成する必要があります。
description: このベスト プラクティス アナライザー ルールによって報告された問題を解決する方法を説明します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 0aeb1f4b-2e75-430b-9557-fe64738c4992
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 47b215d4c84e68d93ae1189ddd370358e2781eff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822243"
---
# <a name="replica-servers-should-be-configured-to-identify-specific-primary-servers-authorized-to-send-replication-traffic"></a>レプリカ サーバーは、特定のプライマリ サーバーがレプリケーション トラフィックを送信する権限を特定するように構成する必要があります。

>適用先:Windows Server 2016

ベスト プラクティスとスキャンの詳細については、次を参照してください。 [Run Best Practices Analyzer Scans and Manage Scan Results](https://go.microsoft.com/fwlink/p/?LinkID=223177)します。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**重要度**|警告|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*上記の構成でこのレプリカ サーバーはすべてのプライマリ サーバーからのレプリケーション トラフィックを受信しを 1 か所で保存します。*  
  
### <a name="impact"></a>影響  
*すべてのプライマリ サーバーからのすべてのレプリケーションは、プライバシーやセキュリティ上の問題を導入する可能性がありますが、1 つの場所に格納されます。*  
  
## <a name="resolution"></a>解決方法  
*HYPER-V マネージャーを使用して、特定のプライマリ サーバーの新しい承認エントリを作成し、それぞれの個別の記憶域の場所を指定します。ワイルドカード文字を使用すると、プライマリ サーバーを承認の各エントリのセットにグループ化します。*  
  
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
  
## <a name="see-also"></a>関連項目  
[New-VMReplicationAuthorizationEntry](https://technet.microsoft.com/library/hh848606.aspx)  
  


