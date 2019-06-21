---
title: DNS リソース レコードを追加する
description: このトピックでは、Windows Server 2016 での IP アドレス管理 (IPAM) の管理ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5379373f-a3d9-4f51-b6fc-bf0f6df1d244
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 36773525187229e498b9addf4b1e6532fd413701
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282322"
---
# <a name="add-a-dns-resource-record"></a>DNS リソース レコードを追加する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用して、IPAM クライアント コンソールを使用して 1 つまたは複数の新しい DNS リソース レコードを追加することができます。  
  
メンバーシップ **管理者**, 、同等の権限をこの手順を実行するために必要な最低限のですか。  
  
### <a name="to-add-a-dns-resource-record"></a>DNS リソース レコードを追加するには  
  
1.  サーバー マネージャーで、クリックして  **IPAM**します。 IPAM クライアント コンソールに表示されます。  
  
2.  ナビゲーション ウィンドウで [**監視と管理**、] をクリックして**DNS ゾーン**。  上部のナビゲーション ウィンドウと下のナビゲーション ウィンドウのナビゲーション ウィンドウに分割します。  
  
3.  下部のナビゲーション ウィンドウで次のようにクリックします。**前方参照**します。 表示ウィンドウの検索結果には、すべての IPAM で管理されたで DNS 前方参照ゾーンが表示されます。 クリックして、リソース レコードを追加するゾーンを右クリックして**追加の DNS リソース レコード**します。  
  
    ![DNS リソース レコードを追加します。](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_01.jpg)
  
4.  **DNS リソース レコードの追加** ダイアログ ボックスが表示されます。 **リソース レコードのプロパティ**、 をクリックして**DNS server** 1 つまたは複数の新しいリソース レコードを追加する DNS サーバーを選択します。 **構成の DNS リソース レコード**、 をクリックして**新規**します。  
  
    ![DNS リソース レコードを構成します。](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_02.jpg)  
  
5.  ダイアログ ボックスを展開する**新しいリソース レコード**します。 クリックして**リソース レコードの種類**します。  
  
    ![リソース レコードの種類](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_03.jpg)  
  
6.  リソース レコードの種類の一覧が表示されます。 追加するリソース レコードの種類をクリックします。  
  
    ![追加するレコードの種類を選択します。](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_04.jpg)  
  
7.  **、新しいリソース レコード**で**名前**、リソース レコードの名前を入力します。 **IP アドレス**IP アドレスを入力して、デプロイの適切なリソース レコードのプロパティを選択します。 クリックして**リソース レコードを追加**します。  
  
    ![リソース レコードを追加します。](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_06.jpg)  
  
8.  その他の新しいリソース レコードを作成したくない場合にクリックします**OK**します。 その他の新しいリソース レコードを作成する場合は、クリックして**新規**します。  
  
    ![[OK] または [新規] をクリックします。](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_01.jpg)
  
9. ダイアログ ボックスを展開する**新しいリソース レコード**します。 クリックして**リソース レコードの種類**します。 リソース レコードの種類の一覧が表示されます。 追加するリソース レコードの種類をクリックします。  
  
10. **、新しいリソース レコード**で**名前**、リソース レコードの名前を入力します。 **IP アドレス**IP アドレスを入力して、デプロイの適切なリソース レコードのプロパティを選択します。 クリックして**リソース レコードを追加**します。  
  
    ![リソース レコードを追加します。](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_02.jpg)  
  
11. 複数のリソース レコードを追加する場合は、レコードを作成するため、プロセスを繰り返します。 新しいリソース レコードを作成したら、クリックして**適用**します。  
  
    ![完全なリソース レコードの作成](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_03.jpg)  
  
12. **リソース レコードの追加** ダイアログ ボックスでは、IPAM は、指定した DNS サーバーでリソース レコードを作成中にリソース レコードの概要が表示されます。 レコードが正常に作成される、**状態**のレコードが**成功**します。  
  
    ![レコードの追加の状態](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_04.jpg)  
  
13. **[OK]** をクリックします。  
  
## <a name="see-also"></a>関連項目  
[DNS リソース レコードの管理](DNS-Resource-Record-Management.md)  
[IPAM の管理](Manage-IPAM.md)  
  


