---
title: DNS ゾーンを編集する
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a35164e1-11ad-47c8-9843-580d30c70d07
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2175cf9c740d7b727ba017922a77c94d4379c891
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355277"
---
# <a name="edit-a-dns-zone"></a>DNS ゾーンを編集する

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、IPAM クライアントコンソールで DNS ゾーンを編集する方法について説明します。  
  
メンバーシップ **管理者**, 、同等の権限をこの手順を実行するために必要な最低限のですか。  
  
### <a name="to-edit-a-dns-zone"></a>DNS ゾーンを編集するには  
  
1.  サーバーマネージャーで、 **[IPAM]** をクリックします。 IPAM クライアントコンソールが表示されます。  
  
2.  ナビゲーションウィンドウの **[監視と管理]** で、 **[DNS ゾーン数]** をクリックします。 上部のナビゲーション ウィンドウと下のナビゲーション ウィンドウのナビゲーション ウィンドウに分割します。  
  
3.  下のナビゲーションウィンドウで、次のいずれかの選択を行います。  
  
    -   前方参照  
  
    -   IPv4 逆引き参照  
  
    -   IPv6 逆引き参照  
  
4.  たとえば、[IPv4 逆引き参照] を選択します。  
  
    ![ゾーンの種類を選択してください](../../media/Edit-a-DNS-Zone/ipam_EditZone_01.jpg)  
  
5.  表示ウィンドウで、編集するゾーンを右クリックし、 **[DNS ゾーンの編集]** をクリックします。  
  
    ![DNS ゾーンの編集](../../media/Edit-a-DNS-Zone/ipam_EditZone_02.jpg)  
  
6.  **[DNS ゾーンの編集]** ダイアログボックスが開き、 **[全般**] ページが選択された状態で表示されます。 必要に応じて、一般的なゾーンのプロパティを編集します。**DNS サーバー**、**ゾーンカテゴリ**、**ゾーンの種類**を選択し、 **[適用]** をクリックします。編集が完了したら、[ **OK]** をクリックします。  
  
    ![ゾーンのプロパティを編集して保存する](../../media/Edit-a-DNS-Zone/ipam_EditZone_03a.jpg)  
  
7.  **[DNS ゾーンの編集]** ダイアログボックスで、 **[詳細設定]** をクリックします。 **[高度な**ゾーンのプロパティ] ページが開きます。 必要に応じて、変更するプロパティを編集し、 **[適用]** をクリックします。編集が完了したら、[ **OK]** をクリックします。  
  
    ![高度なゾーンのプロパティの編集](../../media/Edit-a-DNS-Zone/ipam_EditZone_04a.jpg)  
  
8.  必要に応じて、追加のゾーンプロパティページ名 (ネームサーバー、SOA、ゾーン転送) を選択し、編集を行い、 **[適用]** または [ **OK]** をクリックします。 ゾーンの編集をすべて確認するには、 **[概要]** をクリックし、 **[OK]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
[DNS ゾーンの管理](DNS-Zone-Management.md)  
[IPAM の管理](Manage-IPAM.md)  
  


