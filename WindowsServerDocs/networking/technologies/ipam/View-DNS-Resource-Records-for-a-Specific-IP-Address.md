---
title: 特定の IP アドレスの DNS リソース レコードを表示する
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ipam
ms.topic: article
ms.assetid: f590fb86-4195-4f90-98cb-e90459d4c1e3
ms.author: lizross
author: eross-msft
ms.openlocfilehash: d3694d3e551f3b9d38e2b7ea879b84ae07270b0f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854825"
---
# <a name="view-dns-resource-records-for-a-specific-ip-address"></a>特定の IP アドレスの DNS リソース レコードを表示する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、選択した IP アドレスに関連付けられている DNS リソースレコードを表示できます。  
  
この手順を実行するには、**Administrators** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。  
  
### <a name="to-view-resource-records-for-an-ip-address"></a>IP アドレスのリソースレコードを表示するには  
  
1.  サーバー マネージャーで、クリックして  **IPAM**します。 IPAM クライアントコンソールが表示されます。  
  
2.  ナビゲーションウィンドウの **[IP アドレス空間]** で、 **[ip アドレスインベントリ]** をクリックします。 下のナビゲーションウィンドウで、 **[IPv4]** または **[IPv6]** をクリックします。 IP アドレスインベントリは、表示ウィンドウの検索ビューに表示されます。 DNS リソースレコードを表示する IP アドレスを探して選択します。  
  
    ![IP アドレスインベントリの表示](../../media/View-DNS-Resource-Records-for-a-Specific-IP-Address/ipam_IPInventory_01.jpg)  
  
3.  表示ウィンドウの**詳細ビュー**で、 **[DNS リソースレコード]** をクリックします。 選択した IP アドレスに関連付けられているリソースレコードが表示されます。  
  
    ![DNS リソースレコードの表示](../../media/View-DNS-Resource-Records-for-a-Specific-IP-Address/ipam_IPInventory_02.jpg)  
  
## <a name="see-also"></a>参照  
[DNS リソースレコードの管理](DNS-Resource-Record-Management.md)  
[IPAM の管理](Manage-IPAM.md)  
  


