---
title: DNS リソース レコードのアクセス スコープを設定する
description: このトピックでは、Windows Server 2016 での IP アドレス管理 (IPAM) の管理ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a96a8752-5678-49c5-b069-d2cce8042a51
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c79e1f63b9bcb43520a57defca8228b76db68a31
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283872"
---
# <a name="set-access-scope-for-dns-resource-records"></a>DNS リソース レコードのアクセス スコープを設定する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、IPAM クライアント コンソールを使用して DNS リソース レコードのアクセス スコープの設定を使用できます。  
  
メンバーシップ **管理者**, 、同等の権限をこの手順を実行するために必要な最低限のですか。  
  
### <a name="to-set-access-scope-for-dns-resource-records"></a>DNS リソース レコードのアクセス スコープを設定するには  
  
1.  サーバー マネージャーで、クリックして  **IPAM**します。 IPAM クライアント コンソールに表示されます。  
  
2.  ナビゲーション ウィンドウで、 **DNS ゾーン**します。  下のナビゲーション ウィンドウで **前方参照**とを参照して、リソース レコードを変更するアクセス スコープが含まれるゾーンを選択します。  
  
3.  表示ウィンドウで検索し、リソース レコードを変更するアクセス スコープを選択します。  
  
    ![リソース レコードを選択します。](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_02.jpg)  
  
4.  選択された DNS リソース レコードを右クリックし、をクリックし、**アクセス スコープの設定**します。  
  
    ![アクセス スコープの設定](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_03.jpg)  
  
5.  **アクセス スコープの設定** ダイアログ ボックスが表示されます。 展開に、必要な場合は、選択を解除する をクリックして**親から継承されたアクセス スコープ**します。 **アクセス スコープの選択**、項目を選択し、をクリックし、 **OK**します。  
  
    ![アクセス スコープを選択します。](../../media/Set-Access-Scope-for-DNS-Resource-Records/ipam_RestrictUserToRRControl_04.jpg)  
  
## <a name="see-also"></a>関連項目  
[ロール ベース Access Control](Role-based-Access-Control.md)  
[IPAM の管理](Manage-IPAM.md)  
  


