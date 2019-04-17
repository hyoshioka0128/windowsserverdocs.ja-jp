---
title: DNS ゾーンの DNS リソース レコードを表示します。
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
ms.openlocfilehash: 786c1ee8fd673bd17465ab9586dd1e0bcfd7971c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="view-dns-resource-records-for-a-dns-zone"></a>DNS ゾーンの DNS リソース レコードを表示します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用して、IPAM クライアント コンソールで DNS ゾーンの DNS リソース レコードを表示することができます。  
  
メンバーシップ**管理者**、相当するものでは、この手順を実行するために必要な最低限またはします。  
  
### <a name="to-view-dns-resource-records-for-a-zone"></a>ゾーンの DNS リソース レコードを表示するには  
  
1.  サーバー マネージャーで、クリックして**IPAM**します。 IPAM クライアント コンソールに表示されます。  
  
2.  ナビゲーション ウィンドウで、[**監視と管理**、] をクリックして**DNS ゾーン**します。  上部ナビゲーション ウィンドウと下のナビゲーション ウィンドウのナビゲーション ウィンドウに分割します。  
  
3.  下のナビゲーション ウィンドウでをクリックして**前方参照**、し、検索して表示するゾーンを選択するドメインとゾーンの一覧を展開します。 たとえば、dublin という名前のゾーンがあれば、クリックして**dublin**します。  
  
    ![表示するゾーンを選択します。](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01a.jpg)  

  
4.  表示ウィンドウで、既定のビューは、ゾーンに対する DNS サーバーです。 ビューを変更する] をクリックして**現在のビュー**、] をクリックし、**リソース レコード**します。  
  
    ![リソース レコードに、ビューを変更します。](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_Zone_RR_02.jpg)  
  
5.  ゾーンの DNS リソース レコードが表示されます。 レコードをフィルター処理するで検索するテキストを入力**フィルター**します。  
  
    ![レコードをフィルターするテキストを入力](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01c.jpg)  
  
6.  レコードの種類、アクセス スコープ、またはその他の条件によって、リソース レコードをフィルターするには、次のようにクリックします。**条件の追加**、条件一覧からオプションを選択すると、] をクリック**追加**します。  
  
    ![レコードをフィルターする条件を使用します。](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01d.jpg)  
  
## <a name="see-also"></a>参照してください。  
[DNS ゾーン管理](DNS-Zone-Management.md)  
[IPAM を管理します。](Manage-IPAM.md)  
  


