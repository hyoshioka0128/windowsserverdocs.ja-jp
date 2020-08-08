---
title: DNS ゾーンのアクセス スコープを設定する
description: このトピックは、Windows Server 2016 の IP アドレス管理 (IPAM) 管理ガイドに含まれています。
manager: brianlic
ms.topic: article
ms.assetid: 6a211dde-80eb-4888-b5bb-4e28fe8dc7df
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 155e21bae4045f094696a8193966469f09a8b6ea
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944664"
---
# <a name="set-access-scope-for-a-dns-zone"></a>DNS ゾーンのアクセス スコープを設定する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用して、IPAM クライアントコンソールを使用して DNS ゾーンのアクセススコープを設定できます。

この手順を実行するには、**Administrators** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

### <a name="to-set-the-access-scope-for-a-dns-zone"></a>DNS ゾーンのアクセススコープを設定するには

1.  サーバー マネージャーで、クリックして  **IPAM**します。 IPAM クライアントコンソールが表示されます。

2.  ナビゲーションウィンドウで、[ **DNS ゾーン数**] をクリックします。 表示ウィンドウで、アクセススコープを変更する DNS ゾーンを右クリックし、[**アクセススコープの設定**] をクリックします。

    ![アクセス スコープの設定](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_02.jpg)

3.  [**アクセススコープの設定**] ダイアログボックスが表示されます。 デプロイに必要な場合は、[**親からのアクセススコープの継承**] をクリックして選択を解除します。 [**アクセススコープの選択**] で項目を選択し、[ **OK**] をクリックします。

    ![アクセススコープの選択](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_03.jpg)

4.  IPAM クライアントコンソールの表示ウィンドウで、ゾーンのアクセススコープが変更されていることを確認します。

    ![ゾーンのアクセススコープが変更されていることを確認します。](../../media/Set-Access-Scope-for-a-DNS-Zone/ipam_SetAccessScopeOfZone_04.jpg)

## <a name="see-also"></a>参照
[ロールベースの Access Control](Role-based-Access-Control.md) 
[IPAM の管理](Manage-IPAM.md)



