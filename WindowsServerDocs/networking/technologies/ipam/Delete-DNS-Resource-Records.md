---
title: DNS リソース レコードを削除する
description: このトピックでは、Windows Server 2016 での IP アドレス管理 (IPAM) の管理ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 366e6fd5-d563-4de3-9551-5614cbb8f2cb
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ecbe5dcc452aa39a9afca7e1c8d5fe70d8d4528d
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67283976"
---
# <a name="delete-dns-resource-records"></a>DNS リソース レコードを削除する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用して、IPAM クライアント コンソールを使用して 1 つまたは複数の DNS リソース レコードを削除することができます。  
  
メンバーシップ **管理者**, 、同等の権限をこの手順を実行するために必要な最低限のですか。  
  
### <a name="to-delete-dns-resource-records"></a>DNS リソース レコードを削除するには  
  
1.  サーバー マネージャーで、クリックして  **IPAM**します。 IPAM クライアント コンソールに表示されます。  
  
2.  ナビゲーション ウィンドウで [**監視と管理**、] をクリックして**DNS ゾーン**。  上部のナビゲーション ウィンドウと下のナビゲーション ウィンドウのナビゲーション ウィンドウに分割します。  
  
3.  クリックして展開**前方参照**とドメインを削除するゾーンとリソースのレコードが存在します。 ゾーン、および表示ウィンドウをクリックし**現在のビュー**します。 クリックして**リソース レコード**します。  
  
4.  表示ウィンドウで検索し、削除するリソース レコードを選択します。  
  
    ![削除するリソース レコードを選択します。](../../media/Delete-DNS-Resource-Records/ipam_DeleteRR_01.jpg)  
  
5.  選択されたレコードを右クリックし、をクリックし、**削除 DNS リソース レコード**します。  
  
    ![レコードを削除します。](../../media/Delete-DNS-Resource-Records/ipam_DeleteRR_02.jpg)  
  
6.  **DNS リソース レコードの削除** ダイアログ ボックスが表示されます。 適切な DNS サーバーが選択されていることを確認します。 そうでない場合はクリックして**DNS server**リソース レコードを削除するサーバーを選択します。 **[OK]** をクリックします。 IPAM では、DNS サーバーからリソース レコードを削除します。  
  
    ![正しい DNS サーバーが選択されていることを確認し、レコードの削除](../../media/Delete-DNS-Resource-Records/ipam_DeleteRR_03.jpg)  
  
## <a name="see-also"></a>関連項目  
[DNS リソース レコードの管理](DNS-Resource-Record-Management.md)  
[IPAM の管理](Manage-IPAM.md)  
  


