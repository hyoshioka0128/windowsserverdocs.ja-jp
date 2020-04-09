---
title: AD フォレストの回復-グローバルカタログを削除します。
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 60087a62-11e6-4750-a70e-510f35315688
ms.technology: identity-adds
ms.openlocfilehash: 9c16d25c3e749062bdcb2531960c17be434cf615
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80823725"
---
# <a name="ad-forest-recovery---removing-the-global-catalog"></a>AD フォレストの回復-グローバルカタログの削除  

>適用対象: Windows Server 2016、Windows Server 2012、および 2012 R2、Windows Server 2008 および 2008 R2

 DC からグローバルカタログを削除するには、次の手順に従います。 
  
 グローバルカタログサーバーをバックアップから復元すると、その部分レプリカに対して権威を持つ対応するドメインよりも、その部分的なレプリカの1つについて、新しいデータがグローバルカタログに保持される可能性があります。 このような場合、新しいデータはグローバルカタログから削除されず、他のグローバルカタログサーバーにレプリケートされることもあります。 その結果、グローバルカタログサーバーである DC を誤って復元した場合や、信頼されている唯一のバックアップであった場合でも、復元操作が完了した直後にグローバルカタログを削除する必要があります。 グローバルカタログを削除すると、そのすべての部分レプリカが削除されます。 
  
## <a name="to-remove-the-global-catalog-using-active-directory-sites-and-services"></a>Active Directory サイトとサービスを使用してグローバルカタログを削除するには  
 
1. サーバーマネージャーを開き、 **[ツール]** をクリックして **[Active Directory サイトとサービス]** をクリックします。 
2. コンソールツリーで、 **[サイト]** コンテナを展開し、対象サーバーが含まれている適切なサイトを選択します。 
3. **[サーバー]** コンテナーを展開し、グローバルカタログを削除する DC の*サーバー*オブジェクトを展開します。 
4. **[NTDS 設定]** を右クリックし、 **[プロパティ]** をクリックします。 
5. **[グローバルカタログ]** チェックボックスをオフにします。 
   GC](media/AD-Forest-Recovery-Remove-GC/removegc1.png) を削除 ![には
6. **[適用]** をクリックします。
  
## <a name="to-remove-the-global-catalog-using-repadmin"></a>Repadmin を使用してグローバルカタログを削除するには  
  
管理者特権でのコマンドプロンプトを開き、次のコマンドを入力して、enter キーを押します。  

   ```
   repadmin.exe /options DC_NAME –IS_GC  
   ```  

## <a name="next-steps"></a>次の手順

- [AD フォレストの回復ガイド](AD-Forest-Recovery-Guide.md)
- [AD フォレストの回復 - 手順](AD-Forest-Recovery-Procedures.md)
