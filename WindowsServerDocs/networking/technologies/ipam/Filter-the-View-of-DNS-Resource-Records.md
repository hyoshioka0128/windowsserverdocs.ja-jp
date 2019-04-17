---
title: DNS リソース レコードのビューをフィルター処理します。
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
ms.assetid: 5b80294a-7325-476b-84eb-69f0d051e8b2
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 35c0e822daa9f2c8c49ae7e6f2f40ec0411cb6fa
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="filter-the-view-of-dns-resource-records"></a>DNS リソース レコードのビューをフィルター処理します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、IPAM クライアント コンソール内の DNS リソース レコードのビューをフィルター処理します。  
  
メンバーシップ**管理者**、相当するものでは、この手順を実行するために必要な最低限またはします。  
  
### <a name="to-filter-the-view-of-dns-resource-records"></a>DNS リソース レコードのビューをフィルター処理するには  
  
1.  サーバー マネージャーで、クリックして**IPAM**します。 IPAM クライアント コンソールに表示されます。  
  
2.  ナビゲーション ウィンドウで、[**監視と管理**、] をクリックして**DNS ゾーン**します。  上部ナビゲーション ウィンドウと下のナビゲーション ウィンドウのナビゲーション ウィンドウに分割します。  
  
3.  下のナビゲーション ウィンドウでをクリックして**前方参照**します。 表示ウィンドウの検索結果では、すべての IPAM で管理されたで DNS 前方参照ゾーンが表示されます。  
  
4.  ゾーンにレコードを表示およびフィルター処理をクリックします。  
  
5.  表示ウィンドウで、をクリックして**現在のビュー**、] をクリックし、**リソース レコード**します。 ゾーンのリソース レコードは、表示ウィンドウで表示されます。  
  
6.  表示ウィンドウで、をクリックして**条件の追加**します。  
  
    ![[条件を追加します。](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_01.jpg)  
  
7.  ドロップダウン リストから、条件を選択します。 たとえば、特定のレコードの種類を表示する場合は、クリックして**レコードの種類**します。  
  
    ![条件を選択します。](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_02.jpg)  
  
8.  をクリックして**追加**します。  
  
    ![条件を追加します。](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_03.jpg)  
  
9. **レコードの種類**検索パラメーターとして追加されます。 検索するレコードの種類のテキストを入力します。 たとえば、SRV レコードのみを表示する場合は、入力**SRV**します。  
  
    ![検索するレコードの種類を指定します。](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_04.jpg)  
  
10. ENTER キーを押します。 DNS リソース レコードは、条件に基づいてフィルター処理されたし、指定した語句を検索します。  
  
    ![フィルターを実行します。](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_05.jpg)  
  
## <a name="see-also"></a>参照してください。  
[DNS リソース レコードの管理](DNS-Resource-Record-Management.md)  
[IPAM を管理します。](Manage-IPAM.md)  
  


