---
title: DNS リソース レコードの表示をフィルター処理する
description: このトピックでは、Windows Server 2016 での IP アドレス管理 (IPAM) の管理ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b80294a-7325-476b-84eb-69f0d051e8b2
ms.author: pashort
author: shortpatti
ms.openlocfilehash: cc3f2b8ec6e7c5149ef6351639fbbf8f0def8be8
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283933"
---
# <a name="filter-the-view-of-dns-resource-records"></a>DNS リソース レコードの表示をフィルター処理する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用するには、IPAM クライアント コンソールでの DNS リソース レコードのビューをフィルター処理します。  
  
メンバーシップ **管理者**, 、同等の権限をこの手順を実行するために必要な最低限のですか。  
  
### <a name="to-filter-the-view-of-dns-resource-records"></a>DNS リソース レコードのビューをフィルター処理  
  
1.  サーバー マネージャーで、クリックして  **IPAM**します。 IPAM クライアント コンソールに表示されます。  
  
2.  ナビゲーション ウィンドウで [**監視と管理**、] をクリックして**DNS ゾーン**。  上部のナビゲーション ウィンドウと下のナビゲーション ウィンドウのナビゲーション ウィンドウに分割します。  
  
3.  下部のナビゲーション ウィンドウで次のようにクリックします。**前方参照**します。 表示ウィンドウの検索結果には、すべての IPAM で管理されたで DNS 前方参照ゾーンが表示されます。  
  
4.  表示およびフィルター処理レコードがゾーンをクリックします。  
  
5.  表示ウィンドウで次のようにクリックします。**現在のビュー**、 をクリックし、**リソース レコード**します。 表示ウィンドウで、ゾーンのリソース レコードが表示されます。  
  
6.  表示ウィンドウで次のようにクリックします。**条件の追加**します。  
  
    ![条件の追加](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_01.jpg)  
  
7.  ドロップダウン リストから条件を選択します。 たとえば、特定のレコードの種類を表示する場合は、クリックして**レコードの種類**します。  
  
    ![基準を選択します。](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_02.jpg)  
  
8.  **[追加]** をクリックします。  
  
    ![条件を追加します。](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_03.jpg)  
  
9. **レコードの種類**検索パラメーターとして追加されます。 検索するレコードの種類のテキストを入力します。 たとえば、SRV レコードのみを表示する場合は、「 **SRV**します。  
  
    ![検索するレコードの種類を指定します。](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_04.jpg)  
  
10. Enter キーを押します。 DNS リソース レコードは、条件に従ってフィルター処理し、指定した語句を検索します。  
  
    ![フィルターを実行します。](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_05.jpg)  
  
## <a name="see-also"></a>関連項目  
[DNS リソース レコードの管理](DNS-Resource-Record-Management.md)  
[IPAM の管理](Manage-IPAM.md)  
  


