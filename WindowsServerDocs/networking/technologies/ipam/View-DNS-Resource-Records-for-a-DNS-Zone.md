---
title: DNS ゾーンの DNS リソース レコードを表示する
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
ms.assetid: 375feefc-949e-47c3-9e61-35b79e021966
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9cd1184c9f9d603b82ac43829d4c8f7946f26561
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867983"
---
# <a name="view-dns-resource-records-for-a-dns-zone"></a>DNS ゾーンの DNS リソース レコードを表示する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用して、IPAM クライアント コンソールで、DNS ゾーンの DNS リソース レコードを表示することができます。  
  
メンバーシップ **管理者**, 、同等の権限をこの手順を実行するために必要な最低限のですか。  
  
### <a name="to-view-dns-resource-records-for-a-zone"></a>ゾーンの DNS リソース レコードを表示するには  
  
1.  サーバー マネージャーで、クリックして  **IPAM**します。 IPAM クライアント コンソールに表示されます。  
  
2.  ナビゲーション ウィンドウで [**監視と管理**、] をクリックして**DNS ゾーン**。  上部のナビゲーション ウィンドウと下のナビゲーション ウィンドウのナビゲーション ウィンドウに分割します。  
  
3.  下のナビゲーション ウィンドウで、クリックして **前方参照**, を検索して表示するゾーンを選択するドメインとゾーンの一覧を展開します。 たとえば、dublin という名前のゾーンがあれば、クリックして **dublin**します。  
  
    ![表示するゾーンを選択します。](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01a.jpg)  

  
4.  表示ウィンドウで、既定のビューは、ゾーンの DNS サーバーです。 ビューを変更する をクリックして **現在のビュー**, 、クリックして **リソース レコード**します。  
  
    ![リソース レコードに、ビューを変更します。](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_Zone_RR_02.jpg)  
  
5.  ゾーンの DNS リソース レコードが表示されます。 レコードをフィルター処理するで検索するテキストを入力 **フィルター**します。  
  
    ![レコードをフィルターするテキストを入力](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01c.jpg)  
  
6.  レコードの種類、アクセス スコープ、またはその他の条件によって、リソース レコードをフィルター処理するにはクリックして **条件の追加**, 、リストの中から選択して、をクリックして **追加**します。  
  
    ![レコードをフィルターする基準を使用してください。](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01d.jpg)  
  
## <a name="see-also"></a>関連項目  
[DNS ゾーンの管理](DNS-Zone-Management.md)  
[IPAM を管理します。](Manage-IPAM.md)  
  


