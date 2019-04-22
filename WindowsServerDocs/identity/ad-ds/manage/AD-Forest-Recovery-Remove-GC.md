---
title: AD フォレストの回復 - グローバル カタログの削除
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 60087a62-11e6-4750-a70e-510f35315688
ms.technology: identity-adds
ms.openlocfilehash: d730ce65fc179aee6a98f7cfc1a5b693bfcd6c93
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817073"
---
# <a name="ad-forest-recovery---removing-the-global-catalog"></a>AD フォレストの回復 - グローバル カタログを削除します。  

>適用先:Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 R2

 DC からグローバル カタログを削除するのにには、次の手順を使用します。 
  
 グローバル カタログ サーバーをバックアップから復元すると、グローバル カタログの部分的なレプリカがその権限のある、対応するドメインよりも、部分的なレプリカの 1 つの新しいデータを保持する可能性があります。 このような場合は、新しいデータはグローバル カタログからは削除されませんし、他のグローバル カタログ サーバーにもレプリケート場合があります。 その結果、グローバル カタログ サーバーをいずれかが誤っていた DC を復元、または信頼されたバックアップを単独であったため、場合でも、復元操作が完了した後すぐにグローバル カタログを削除する必要があります。 グローバル カタログが削除されると、コンピューターは、その部分のすべてのレプリカを削除します。 
  
## <a name="to-remove-the-global-catalog-using-active-directory-sites-and-services"></a>Active Directory サイトとサービスを使用してグローバル カタログを削除するには  
 
1. サーバー マネージャーを開き、**ツール**クリック**Active Directory サイトとサービス**します。 
2. コンソール ツリーで、展開、**サイト**コンテナー、およびターゲット サーバーを含む適切なサイトを選択します。 
3. 展開、**サーバー**コンテナーの順に展開し、*サーバー*の DC をグローバル カタログを削除するオブジェクト。 
4. 右クリックして**NTDS 設定**、 をクリックし、**プロパティ**します。 
5. クリア、**グローバル カタログ**チェック ボックスをオンします。 
   ![GC を削除します。](media/AD-Forest-Recovery-Remove-GC/removegc1.png)
6. **[適用]** をクリックします。
  
## <a name="to-remove-the-global-catalog-using-repadmin"></a>Repadmin を使用してグローバル カタログを削除するには  
  
管理者特権でコマンド プロンプトを開きます次のコマンドを入力し、ENTER キーを押します。  

   ```
   repadmin.exe /options DC_NAME –IS_GC  
   ```  

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
