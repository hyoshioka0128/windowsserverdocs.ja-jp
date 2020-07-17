---
title: レプリカ サーバーは、特定のプライマリ サーバーがレプリケーション トラフィックを送信する権限を特定するように構成する必要があります。
description: このベストプラクティスアナライザー規則によって報告された問題を解決するための手順を示します。
ms.prod: windows-server
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 0aeb1f4b-2e75-430b-9557-fe64738c4992
author: kbdazure
ms.date: 8/16/2016
ms.openlocfilehash: 649af22f615f2f36baceb1fa23b79c54b038f9c2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861835"
---
# <a name="replica-servers-should-be-configured-to-identify-specific-primary-servers-authorized-to-send-replication-traffic"></a>レプリカ サーバーは、特定のプライマリ サーバーがレプリケーション トラフィックを送信する権限を特定するように構成する必要があります。

>適用対象: Windows Server 2016

ベストプラクティスとスキャンの詳細については、「[ベストプラクティスアナライザースキャンの実行」および「スキャン結果の管理](https://go.microsoft.com/fwlink/p/?LinkID=223177)」を参照してください。  
  
|プロパティ|詳細|  
|-|-|  
|**オペレーティング システム**|Windows Server 2016|  
|**製品/機能**|Hyper-V|  
|**順**|［警告］|  
|**カテゴリ**|構成|  
  
次のセクションでは、斜体は、この問題のためのベスト プラクティス アナライザー ツールで表示される UI テキストを示します。  
  
## <a name="issue"></a>問題  
*構成されているように、このレプリカサーバーは、すべてのプライマリサーバーからのレプリケーショントラフィックを受け入れ、1つの場所に格納します。*  
  
### <a name="impact"></a>影響  
*すべてのプライマリサーバーからのすべてのレプリケーションは1つの場所に保存されるため、プライバシーやセキュリティの問題が発生する可能性があります。*  
  
## <a name="resolution"></a>解決方法  
*Hyper-v マネージャーを使用して、特定のプライマリサーバーの新しい承認エントリを作成し、それぞれに個別の記憶域の場所を指定します。ワイルドカード文字を使用すると、各承認エントリのセットにプライマリサーバーをグループ化できます。*  
  
#### <a name="create-authorization-entries-using-hyper-v-manager"></a>HYPER-V マネージャーを使用して承認エントリを作成します。  
  
1.  Hyper-V マネージャーを開きます。 (サーバー マネージャーで、クリックして **ツールの** > **Hyper V マネージャー**.)  
  
2.  ホストの一覧から、目的のホストを右クリックし、[Hyper-v の**設定**] をクリックします。  
  
3.  ナビゲーションウィンドウで、 **[レプリケーションの構成]** をクリックします。  
  
4.  **[承認と記憶域]** で、 **[指定したサーバーからレプリケーションを許可する]** をクリックします。  
  
5.  サーバーの一覧の下にある **[追加]** をクリックします。  
  
6.  **[承認エントリの追加]** で、次のようにします。  
  
    -   最初のサーバーの完全修飾名を入力します。  
  
    -   そのサーバーのファイルのみを格納する専用の場所を指定します。  
  
7.  **[OK]** をクリックすると、  
  
8.  各プライマリサーバーに対してこの手順を繰り返します。  
  
9. もう一度 **[OK]** をクリックして終了し、ウィンドウを閉じます。  
  
### <a name="create-authorization-entries-using-windows-powershell"></a>Windows PowerShell を使用して承認エントリを作成する  
  
1.  Windows PowerShell を開きます。 (デスクトップから [スタート] をクリックし、「 **Windows PowerShell**」と入力を開始します)。  
  
2.  右クリック **Windows PowerShell**  をクリック **管理者として実行**します。  
  
3.  次のようなコマンドを実行して、を置き換えます。  
  
    -   サーバーの完全修飾ドメイン名を使用した server01.domain01.contoso.com のプライマリサーバー名。  
  
    -   D:\ReplicaVMStorage の場所を指定します。  
  
    -   既定という名前の信頼グループが作成されている場合は、そのグループの名前。 それ以外の場合は、既定値を使用します。  
  
```  
New-VMReplicationAuthorizationEntry server01.domain01.contoso.com D:\ReplicaVMStorage DEFAULT  
```  
  
## <a name="see-also"></a>参照  
[New-vmreplicationauthorizationentry](https://technet.microsoft.com/library/hh848606.aspx)  
  


