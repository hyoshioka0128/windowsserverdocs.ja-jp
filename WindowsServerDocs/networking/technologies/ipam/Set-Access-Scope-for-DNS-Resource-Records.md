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
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b1790f2cbf84fd68f33ca30d2fe7663dde824240
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405646"
---
# <a name="set-access-scope-for-dns-resource-records"></a>DNS リソース レコードのアクセス スコープを設定する

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用して、IPAM クライアントコンソールを使用して DNS リソースレコードのアクセススコープを設定できます。  
  
メンバーシップ **管理者**, 、同等の権限をこの手順を実行するために必要な最低限のですか。  
  
### <a name="to-set-access-scope-for-dns-resource-records"></a>DNS リソースレコードのアクセススコープを設定するには  
  
1.  サーバー マネージャーで、クリックして  **IPAM**します。 IPAM クライアントコンソールが表示されます。  
  
2.  ナビゲーションウィンドウで、 **[DNS ゾーン数]** をクリックします。  下のナビゲーションウィンドウで、 **[前方参照]** を展開し、アクセススコープを変更するリソースレコードが含まれているゾーンを参照して選択します。  
  
3.  表示ウィンドウで、アクセススコープを変更するリソースレコードを見つけて選択します。  
  
    ![リソースレコードを選択します](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_02.jpg)  
  
4.  選択した DNS リソースレコードを右クリックし、 **[アクセススコープの設定]** をクリックします。  
  
    ![アクセス スコープの設定](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_03.jpg)  
  
5.  **[アクセススコープの設定]** ダイアログボックスが表示されます。 デプロイに必要な場合は、 **[親からのアクセススコープの継承]** をクリックして選択を解除します。 **[アクセススコープの選択]** で項目を選択し、 **[OK]** をクリックします。  
  
    ![アクセススコープの選択](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_04.jpg)  
  
## <a name="see-also"></a>関連項目  
[ロールベースの Access Control](Role-based-Access-Control.md)  
[IPAM の管理](Manage-IPAM.md)  
  


