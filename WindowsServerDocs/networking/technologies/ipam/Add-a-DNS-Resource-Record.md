---
title: DNS リソース レコードを追加します。
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
ms.assetid: 5379373f-a3d9-4f51-b6fc-bf0f6df1d244
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e14a59e9f172b20e85a34d2299e3733a796adafc
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="add-a-dns-resource-record"></a>DNS リソース レコードを追加します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用して、IPAM クライアント コンソールを使用して 1 つまたは複数の新しい DNS リソース レコードを追加することができます。  
  
メンバーシップ**管理者**、相当するものでは、この手順を実行するために必要な最低限またはします。  
  
### <a name="to-add-a-dns-resource-record"></a>DNS リソース レコードを追加するには  
  
1.  サーバー マネージャーで、クリックして**IPAM**します。 IPAM クライアント コンソールに表示されます。  
  
2.  ナビゲーション ウィンドウで、[**監視と管理**、] をクリックして**DNS ゾーン**します。  上部ナビゲーション ウィンドウと下のナビゲーション ウィンドウのナビゲーション ウィンドウに分割します。  
  
3.  下のナビゲーション ウィンドウでをクリックして**前方参照**します。 表示ウィンドウの検索結果では、すべての IPAM で管理されたで DNS 前方参照ゾーンが表示されます。 クリックして、リソース レコードを追加する場合、ゾーンを右クリックして**追加 DNS リソース レコード**します。  
  
    ![DNS リソース レコードを追加します。](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_01.jpg)
  
4.  **DNS リソース レコードの追加**] ダイアログ ボックスが開きます。 **リソース レコード プロパティ**、] をクリックして**DNS サーバー**を 1 つまたは複数の新しいリソース レコードを追加する DNS サーバーを選択します。 **DNS リソース レコードを構成**、] をクリックして**新規**します。  
  
    ![DNS リソース レコードを構成します。](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_02.jpg)  
  
5.  ダイアログ ボックスを展開する**新しいリソース レコード**します。 をクリックして**リソース レコードの種類**します。  
  
    ![リソース レコードの種類](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_03.jpg)  
  
6.  リソース レコードの種類の一覧が表示されます。 追加するリソース レコードの種類をクリックします。  
  
    ![追加するレコードの種類を選択します。](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_04.jpg)  
  
7.  **新しいリソース レコード**で**名**、リソース レコード名を入力します。 **IP アドレス**、IP アドレスを入力し、展開に適切なリソース レコードのプロパティ。 をクリックして**リソース レコードを追加**します。  
  
    ![リソース レコードを追加します。](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_06.jpg)  
  
8.  その他の新しいリソース レコードを作成しない場合、以下の] をクリックして**OK**します。 その他の新しいリソース レコードを作成する場合は、クリックして**新規**します。  
  
    ![[OK] または [新規] をクリックします。](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_01.jpg)
  
9. ダイアログ ボックスを展開する**新しいリソース レコード**します。 をクリックして**リソース レコードの種類**します。 リソース レコードの種類の一覧が表示されます。 追加するリソース レコードの種類をクリックします。  
  
10. **新しいリソース レコード**で**名**、リソース レコード名を入力します。 **IP アドレス**、IP アドレスを入力し、展開に適切なリソース レコードのプロパティ。 をクリックして**リソース レコードを追加**します。  
  
    ![リソース レコードを追加します。](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_02.jpg)  
  
11. 複数のリソース レコードを追加する場合は、レコードを作成するため、プロセスを繰り返します。 新しいリソース レコードの作成が完了したら、クリックして**適用**します。  
  
    ![完全なリソース レコードの作成](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_03.jpg)  
  
12. **リソース レコードの追加**] ダイアログ ボックスでは、IPAM は、指定した DNS サーバーで、リソース レコードを作成中にリソース レコードの概要が表示されます。 レコードを正常に作成するとき、**ステータス**レコードの名前を**成功**します。  
  
    ![レコードの追加の状態](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_04.jpg)  
  
13. をクリックして**OK**します。  
  
## <a name="see-also"></a>参照してください。  
[DNS リソース レコードの管理](DNS-Resource-Record-Management.md)  
[IPAM を管理します。](Manage-IPAM.md)  
  


