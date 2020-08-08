---
title: 特定の IP アドレスの DNS リソース レコードを表示する
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.topic: article
ms.assetid: f590fb86-4195-4f90-98cb-e90459d4c1e3
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 211dcfdc17cfa81aad7adb1a424a9fadc0c932c6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944603"
---
# <a name="view-dns-resource-records-for-a-specific-ip-address"></a>特定の IP アドレスの DNS リソース レコードを表示する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、選択した IP アドレスに関連付けられている DNS リソースレコードを表示できます。

この手順を実行するには、**Administrators** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

### <a name="to-view-resource-records-for-an-ip-address"></a>IP アドレスのリソースレコードを表示するには

1.  サーバー マネージャーで、クリックして  **IPAM**します。 IPAM クライアントコンソールが表示されます。

2.  ナビゲーションウィンドウの [ **IP アドレス空間**] で、[ **ip アドレスインベントリ**] をクリックします。 下のナビゲーションウィンドウで、[ **IPv4** ] または [ **IPv6**] をクリックします。 IP アドレスインベントリは、表示ウィンドウの検索ビューに表示されます。 DNS リソースレコードを表示する IP アドレスを探して選択します。

    ![IP アドレスインベントリの表示](../../media/View-DNS-Resource-Records-for-a-Specific-IP-Address/ipam_IPInventory_01.jpg)

3.  表示ウィンドウの**詳細ビュー**で、[ **DNS リソースレコード**] をクリックします。 選択した IP アドレスに関連付けられているリソースレコードが表示されます。

    ![DNS リソースレコードの表示](../../media/View-DNS-Resource-Records-for-a-Specific-IP-Address/ipam_IPInventory_02.jpg)

## <a name="see-also"></a>参照
[DNS リソースレコードの管理](DNS-Resource-Record-Management.md) 
[IPAM の管理](Manage-IPAM.md)



