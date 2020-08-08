---
title: DNS ゾーンの DNS リソース レコードを表示する
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.topic: article
ms.assetid: 375feefc-949e-47c3-9e61-35b79e021966
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 0395033fe009a6bb787761ab3ec47604c94ba6b1
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944644"
---
# <a name="view-dns-resource-records-for-a-dns-zone"></a>DNS ゾーンの DNS リソース レコードを表示する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用して、IPAM クライアント コンソールで、DNS ゾーンの DNS リソース レコードを表示することができます。

この手順を実行するには、**Administrators** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

### <a name="to-view-dns-resource-records-for-a-zone"></a>ゾーンの DNS リソース レコードを表示するには

1.  サーバー マネージャーで、クリックして  **IPAM**します。 IPAM クライアントコンソールが表示されます。

2.  ナビゲーションウィンドウの [**監視と管理**] で、[ **DNS ゾーン数**] をクリックします。  上部のナビゲーション ウィンドウと下のナビゲーション ウィンドウのナビゲーション ウィンドウに分割します。

3.  下のナビゲーション ウィンドウで、クリックして **前方参照**, を検索して表示するゾーンを選択するドメインとゾーンの一覧を展開します。 たとえば、dublin という名前のゾーンがあれば、クリックして **dublin**します。

    ![表示するゾーンを選択します。](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01a.jpg)


4.  表示ウィンドウで、既定のビューは、ゾーンの DNS サーバーです。 ビューを変更する] をクリックして **現在のビュー**, 、クリックして **リソース レコード**します。

    ![リソース レコードに、ビューを変更します。](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_Zone_RR_02.jpg)

5.  ゾーンの DNS リソース レコードが表示されます。 レコードをフィルター処理するで検索するテキストを入力 **フィルター**します。

    ![レコードをフィルターするテキストを入力](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01c.jpg)

6.  レコードの種類、アクセス スコープ、またはその他の条件によって、リソース レコードをフィルター処理するにはクリックして **条件の追加**, 、リストの中から選択して、をクリックして **追加**します。

    ![レコードをフィルターする基準を使用してください。](../../media/View-DNS-Resource-Records-for-a-DNS-Zone/ipam_DNSzones_01d.jpg)

## <a name="see-also"></a>参照
[DNS ゾーンの管理](DNS-Zone-Management.md) 
[IPAM の管理](Manage-IPAM.md)



