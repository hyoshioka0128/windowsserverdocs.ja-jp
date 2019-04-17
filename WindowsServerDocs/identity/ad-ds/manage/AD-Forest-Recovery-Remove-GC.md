---
title: "AD フォレストの回復 - グローバル カタログを削除します。"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 60087a62-11e6-4750-a70e-510f35315688
ms.technology: identity-adfs
ms.openlocfilehash: b7da7c03cbae4691e8f902f1be0cb33c0c912248
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2017
---
# <a name="ad-forest-recovery---removing-the-global-catalog"></a>AD フォレストの回復 - グローバル カタログを削除します。  

>Windows Server 2016、Windows Server 2012 および 2012 R2、Windows Server 2008 および 2008 の R2 を適用対象:

 DC からグローバル カタログを削除するのにには、次の手順を使用します。  
  
 グローバル カタログ サーバーをバックアップから復元すると、グローバル カタログのいずれかの部分的なレプリカは部分的なレプリカに対する権限を対応するドメインとの新しいデータを保持している可能性があります。 このような場合より新しいデータは、グローバル カタログからは削除されませんされ、その他のグローバル カタログ サーバーにもレプリケート可能性があります。 その結果、れた、グローバル カタログ サーバーか、誤って DC を復元、または信頼されている単独のバックアップであるため、場合でも、復元操作が完了した後すぐにグローバル カタログを削除する必要があります。 グローバル カタログが削除されると、コンピューターは、すべての部分的なレプリカを削除します。  
  
## <a name="to-remove-the-global-catalog-using-active-directory-sites-and-services"></a>Active Directory サイトとサービスを使用してグローバル カタログを削除するには  
 
1.  サーバー マネージャーを開き、[**ツール**] をクリック**Active Directory サイトとサービス**します。  
2.  コンソール ツリーで、展開、**サイト**コンテナー、およびターゲット サーバーが含まれている適切なサイトを選択します。  
3.  展開、**サーバー**コンテナー、し、展開、*サーバー*グローバル カタログを削除する DC のオブジェクトです。  
4.  右クリック**NTDS 設定**、] をクリックし、**プロパティ**します。  
5.  クリア、**グローバル カタログ**チェック ボックスをオンします。  
![GC を削除します。](media/AD-Forest-Recovery-Remove-GC/removegc1.png)
6.  をクリックして**適用**します。
  
## <a name="to-remove-the-global-catalog-using-repadmin"></a>Repadmin を使用してグローバル カタログを削除するには  
  
1.  管理者特権でコマンド プロンプトを開き、次のコマンドを入力し、Enter キーを押します。  
  
    ```  
    repadmin.exe /options DC_NAME –IS_GC  
    ```  
  
 ## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復の手順](AD-Forest-Recovery-Procedures.md)
