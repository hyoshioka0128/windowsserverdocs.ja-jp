---
title: DNS リソース レコードのアクセス スコープを設定する
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ipam
ms.topic: article
ms.assetid: a96a8752-5678-49c5-b069-d2cce8042a51
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 613796c933498d104db4895733c9a9b1957cb952
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80860615"
---
# <a name="set-access-scope-for-dns-resource-records"></a>DNS リソース レコードのアクセス スコープを設定する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用して、IPAM クライアントコンソールを使用して DNS リソースレコードのアクセススコープを設定できます。  
  
この手順を実行するには、**Administrators** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。  
  
### <a name="to-set-access-scope-for-dns-resource-records"></a>DNS リソースレコードのアクセススコープを設定するには  
  
1.  サーバー マネージャーで、クリックして  **IPAM**します。 IPAM クライアントコンソールが表示されます。  
  
2.  ナビゲーションウィンドウで、 **[DNS ゾーン数]** をクリックします。  下のナビゲーションウィンドウで、 **[前方参照]** を展開し、アクセススコープを変更するリソースレコードが含まれているゾーンを参照して選択します。  
  
3.  表示ウィンドウで、アクセススコープを変更するリソースレコードを見つけて選択します。  
  
    ![リソースレコードを選択します](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_02.jpg)  
  
4.  選択した DNS リソースレコードを右クリックし、 **[アクセススコープの設定]** をクリックします。  
  
    ![アクセス スコープの設定](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_03.jpg)  
  
5.  **[アクセススコープの設定]** ダイアログボックスが表示されます。 デプロイに必要な場合は、 **[親からのアクセススコープの継承]** をクリックして選択を解除します。 **[アクセススコープの選択]** で項目を選択し、 **[OK]** をクリックします。  
  
    ![アクセススコープの選択](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_04.jpg)  
  
## <a name="see-also"></a>参照  
[ロールベースの Access Control](Role-based-Access-Control.md)  
[IPAM の管理](Manage-IPAM.md)  
  


