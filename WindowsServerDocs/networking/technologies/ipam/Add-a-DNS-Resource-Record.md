---
title: DNS リソース レコードを追加する
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ipam
ms.topic: article
ms.assetid: 5379373f-a3d9-4f51-b6fc-bf0f6df1d244
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 67238c1546e8833298ec061cf6e05a038b9d474c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814845"
---
# <a name="add-a-dns-resource-record"></a>DNS リソース レコードを追加する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、IPAM クライアントコンソールを使用して、1つまたは複数の新しい DNS リソースレコードを追加する方法について説明します。  
  
この手順を実行するには、**Administrators** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。  
  
### <a name="to-add-a-dns-resource-record"></a>DNS リソースレコードを追加するには  
  
1.  サーバー マネージャーで、クリックして  **IPAM**します。 IPAM クライアントコンソールが表示されます。  
  
2.  ナビゲーションウィンドウの **[監視と管理]** で、 **[DNS ゾーン数]** をクリックします。  上部のナビゲーション ウィンドウと下のナビゲーション ウィンドウのナビゲーション ウィンドウに分割します。  
  
3.  下のナビゲーションウィンドウで、 **[前方参照]** をクリックします。 IPAM で管理されているすべての DNS 前方参照ゾーンが、表示ウィンドウの検索結果に表示されます。 リソースレコードを追加するゾーンを右クリックし、 **[DNS リソースレコードの追加]** をクリックします。  
  
    ![DNS リソースレコードの追加](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_01.jpg)
  
4.  **[DNS リソースレコードの追加]** ダイアログボックスが表示されます。 **[リソースレコードのプロパティ]** で、 **[dns サーバー]** をクリックし、1つまたは複数の新しいリソースレコードを追加する dns サーバーを選択します。 **[DNS リソースレコードの構成]** で、 **[新規]** をクリックします。  
  
    ![DNS リソースレコードを構成する](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_02.jpg)  
  
5.  ダイアログボックスが展開され、**新しいリソースレコード**が表示されます。 **[リソースレコードの種類]** をクリックします。  
  
    ![リソース レコードの種類](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_03.jpg)  
  
6.  リソースレコードの種類の一覧が表示されます。 追加するリソースレコードの種類をクリックします。  
  
    ![追加するレコードの種類を選択します](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_04.jpg)  
  
7.  [**新しいリソースレコード]** の **[名前]** に、リソースレコード名を入力します。 **[Ip アドレス]** に ip アドレスを入力し、展開に適したリソースレコードのプロパティを選択します。 **[リソースレコードの追加]** をクリックします。  
  
    ![リソースレコードの追加](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_06.jpg)  
  
8.  追加の新しいリソースレコードを作成しない場合は、[ **OK]** をクリックします。 追加の新しいリソースレコードを作成する場合は、 **[新規]** をクリックします。  
  
    ![[OK] または [新規] をクリック](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_01.jpg)
  
9. ダイアログボックスが展開され、**新しいリソースレコード**が表示されます。 **[リソースレコードの種類]** をクリックします。 リソースレコードの種類の一覧が表示されます。 追加するリソースレコードの種類をクリックします。  
  
10. [**新しいリソースレコード]** の **[名前]** に、リソースレコード名を入力します。 **[Ip アドレス]** に ip アドレスを入力し、展開に適したリソースレコードのプロパティを選択します。 **[リソースレコードの追加]** をクリックします。  
  
    ![リソースレコードの追加](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_02.jpg)  
  
11. リソースレコードをさらに追加する場合は、レコードを作成するプロセスを繰り返します。 新しいリソースレコードの作成が完了したら、 **[適用]** をクリックします。  
  
    ![リソースレコードの作成の完了](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_03.jpg)  
  
12. **[リソースレコードの追加]** ダイアログボックスには、リソースレコードの概要が表示されます。 IPAM は、指定した DNS サーバーにリソースレコードを作成します。 レコードが正常に作成されると、レコードの**状態**は "**成功**" になります。  
  
    ![レコード追加の状態](../../media/Add-a-DNS-Resource-Record/ipam_DNSrr_r2_04.jpg)  
  
13. **[OK]** をクリックすると、  
  
## <a name="see-also"></a>参照  
[DNS リソースレコードの管理](DNS-Resource-Record-Management.md)  
[IPAM の管理](Manage-IPAM.md)  
  


