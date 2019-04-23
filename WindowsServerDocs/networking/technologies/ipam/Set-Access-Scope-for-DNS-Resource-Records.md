---
title: DNS リソース レコードのアクセス スコープを設定する
description: このトピックでは、Windows Server 2016 での IP アドレス管理 (IPAM) の管理ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a96a8752-5678-49c5-b069-d2cce8042a51
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2e63c82ef0c58a9b4392ad8b9b1fc896d075ab71
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882913"
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
[IPAM を管理します。](Manage-IPAM.md)  
  


