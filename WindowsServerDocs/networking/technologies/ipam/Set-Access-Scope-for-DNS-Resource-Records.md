---
title: DNS リソース レコードのアクセス スコープを設定する
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a96a8752-5678-49c5-b069-d2cce8042a51
ms.author: lizross
author: eross-msft
ms.openlocfilehash: fd084c856b4f78810ce732fd64b801d6b0f7b67d
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316783"
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
  


