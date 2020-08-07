---
title: DNS ゾーンを作成する
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.topic: article
ms.assetid: a030ff51-a815-4fc4-b26d-aae41c3e4ce5
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 0635c91b3dd61db6df41c2836cc5efc65d9de520
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87970789"
---
# <a name="create-a-dns-zone"></a>DNS ゾーンを作成する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用して、IPAM クライアントコンソールを使用して DNS ゾーンを作成できます。

この手順を実行するには、**Administrators** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

### <a name="to-create-a-dns-zone"></a>DNS ゾーンを作成するには

1.  サーバー マネージャーで、クリックして  **IPAM**します。 IPAM クライアントコンソールが表示されます。

2.  ナビゲーションウィンドウの [**監視と管理**] で、[ **DNS および DHCP サーバー**] をクリックします。 表示ウィンドウで、[**サーバーの種類**] をクリックし、[ **DNS**] をクリックします。 IPAM によって管理されているすべての DNS サーバーが検索結果に一覧表示されます。

3.  ゾーンを追加するサーバーを見つけて、サーバーを右クリックします。  [ **DNS ゾーンの作成**] をクリックします。

    ![DNS ゾーンの作成](../../media/Create-a-DNS-Zone/ipam_CreateDNSZone_01a.jpg)

4.  [ **DNS ゾーンの作成**] ダイアログボックスが表示されます。 **[全般プロパティ**] で、ゾーンカテゴリとゾーンの種類を選択し、[**ゾーン名**] に名前を入力します。 また、[**詳細プロパティ**] で、展開に適した値を選択し、[ **OK**] をクリックします。

    ![高度なプロパティ](../../media/Create-a-DNS-Zone/ipam_CreateDNSZone_02a.jpg)

## <a name="see-also"></a>参照
[DNS ゾーンの管理](DNS-Zone-Management.md) 
[IPAM の管理](Manage-IPAM.md)



