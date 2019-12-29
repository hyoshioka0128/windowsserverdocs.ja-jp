---
title: DNS リソース レコードの表示をフィルター処理する
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5b80294a-7325-476b-84eb-69f0d051e8b2
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 541645a274481bb8b044c37df572d7746c5da30e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405670"
---
# <a name="filter-the-view-of-dns-resource-records"></a>DNS リソース レコードの表示をフィルター処理する

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用して、IPAM クライアントコンソールで DNS リソースレコードのビューをフィルター処理できます。  
  
メンバーシップ **管理者**, 、同等の権限をこの手順を実行するために必要な最低限のですか。  
  
### <a name="to-filter-the-view-of-dns-resource-records"></a>DNS リソースレコードのビューをフィルター処理するには  
  
1.  サーバー マネージャーで、クリックして  **IPAM**します。 IPAM クライアントコンソールが表示されます。  
  
2.  ナビゲーションウィンドウの **[監視と管理]** で、 **[DNS ゾーン数]** をクリックします。  上部のナビゲーション ウィンドウと下のナビゲーション ウィンドウのナビゲーション ウィンドウに分割します。  
  
3.  下のナビゲーションウィンドウで、 **[前方参照]** をクリックします。 IPAM で管理されているすべての DNS 前方参照ゾーンが、表示ウィンドウの検索結果に表示されます。  
  
4.  レコードを表示およびフィルター処理するゾーンをクリックします。  
  
5.  表示ウィンドウで、 **[現在のビュー]** をクリックし、 **[リソースレコード]** をクリックします。 ゾーンのリソースレコードが表示ウィンドウに表示されます。  
  
6.  表示ウィンドウで、 **[条件の追加]** をクリックします。  
  
    ![条件の追加](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_01.jpg)  
  
7.  ドロップダウンリストから条件を選択します。 たとえば、特定のレコードの種類を表示する場合は、 **[レコードの種類]** をクリックします。  
  
    ![条件を選択してください](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_02.jpg)  
  
8.  **[追加]** をクリックします。  
  
    ![条件を追加する](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_03.jpg)  
  
9. **レコードの種類**は、検索パラメーターとして追加されます。 検索するレコードの種類のテキストを入力します。 たとえば、SRV レコードのみを表示する場合は、「 **srv**」と入力します。  
  
    ![検索するレコードの種類を指定します。](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_04.jpg)  
  
10. Enter キーを押します。 DNS リソースレコードは、指定した条件と検索語句に従ってフィルター処理されます。  
  
    ![フィルターを実行する](../../media/Filter-the-View-of-DNS-Resource-Records/ipam_FilterRR_05.jpg)  
  
## <a name="see-also"></a>関連項目  
[DNS リソースレコードの管理](DNS-Resource-Record-Management.md)  
[IPAM の管理](Manage-IPAM.md)  
  


