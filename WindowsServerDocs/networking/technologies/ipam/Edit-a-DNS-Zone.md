---
title: DNS ゾーンを編集する
description: このトピックでは、Windows Server 2016 での IP アドレス管理 (IPAM) の管理ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a35164e1-11ad-47c8-9843-580d30c70d07
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d688790828cb58b9fca2a17c95212c064532bb22
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282168"
---
# <a name="edit-a-dns-zone"></a>DNS ゾーンを編集する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用するには、IPAM クライアント コンソールでの DNS ゾーンを編集します。  
  
メンバーシップ **管理者**, 、同等の権限をこの手順を実行するために必要な最低限のですか。  
  
### <a name="to-edit-a-dns-zone"></a>DNS ゾーンを編集するには  
  
1.  サーバー マネージャーで、 **IPAM**します。 IPAM クライアント コンソールに表示されます。  
  
2.  ナビゲーション ウィンドウで [**監視と管理**、] をクリックして**DNS ゾーン**。 上部のナビゲーション ウィンドウと下のナビゲーション ウィンドウのナビゲーション ウィンドウに分割します。  
  
3.  下のナビゲーション ウィンドウでは、次の選択肢の 1 つを行います。  
  
    -   前方参照  
  
    -   IPv4 逆引き参照  
  
    -   IPv6 逆引き参照  
  
4.  たとえば、IPv4 逆引き参照を選択します。  
  
    ![ゾーンの種類を選択します。](../../media/Edit-a-DNS-Zone/ipam_EditZone_01.jpg)  
  
5.  表示ウィンドウで、編集、およびクリックするゾーンを右クリックして**Edit DNS Zone**します。  
  
    ![DNS ゾーンの編集](../../media/Edit-a-DNS-Zone/ipam_EditZone_02.jpg)  
  
6.  **編集 DNS ゾーン**ダイアログ ボックスが開き、**全般**選択ページ。 必要な場合は、一般的なゾーンのプロパティを編集します。**DNS サーバー**、**ゾーン カテゴリ**と**ゾーンの種類**、順にクリックします**適用**または、編集が完了すると、 **OK**します。  
  
    ![ゾーンのプロパティを編集および保存](../../media/Edit-a-DNS-Zone/ipam_EditZone_03a.jpg)  
  
7.  **編集 DNS ゾーン**ダイアログ ボックスで、をクリックして **[詳細設定]** します。 **詳細**ゾーンのプロパティ ページが開きます。 必要な場合は、変更し、クリックするプロパティの編集**適用**または、編集が完了すると、 **OK**します。  
  
    ![高度なゾーンのプロパティを編集します。](../../media/Edit-a-DNS-Zone/ipam_EditZone_04a.jpg)  
  
8.  必要な場合、に加えて、ゾーン プロパティのページ名 (ネーム サーバー、SOA、ゾーン転送) を選択、編集を行っておよび をクリックして**適用**または**OK**します。 すべての編集はゾーンを確認する**概要**、順にクリックします**OK**します。  
  
## <a name="see-also"></a>関連項目  
[DNS ゾーンの管理](DNS-Zone-Management.md)  
[IPAM の管理](Manage-IPAM.md)  
  


