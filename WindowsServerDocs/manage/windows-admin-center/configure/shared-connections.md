---
title: Windows 管理センターゲートウェイのすべてのユーザーの共有接続を構成する
description: 管理者が Windows 管理センター (Project ホノルル) ゲートウェイを1回構成して、すべてのユーザーが1つの接続リストを共有できるようにする方法について説明します。
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/28/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: c632c178e91b92e0a80d8c72e8ea0ce3ce37b502
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357287"
---
# <a name="configure-shared-connections-for-all-users-of-the-windows-admin-center-gateway"></a>Windows 管理センターゲートウェイのすべてのユーザーの共有接続を構成する

> 適用先:Windows 管理センタープレビュー、Windows 管理センター

共有接続を構成する機能を使用すると、ゲートウェイ管理者は、特定の Windows 管理センターゲートウェイのすべてのユーザーに対して接続一覧を1回構成できます。 

ゲートウェイ管理者は、Windows 管理センターのゲートウェイ設定の **共有接続** タブから、すべての接続 ページの場合と同様に、サーバー、クラスター、および PC 接続を追加できます。接続にタグを付けることもできます。 [共有接続] の一覧に追加されたすべての接続とタグは、この Windows 管理センターゲートウェイのすべてのユーザーに対して [すべての接続] ページから表示されます。
    ![](../media/shared-cnxns-1.png)

共有接続を構成した後、Windows 管理センターのユーザーが [すべての接続] ページにアクセスすると、その接続は2つのセクションにグループ化されます。個人用接続と共有接続。 個人用グループは、特定のユーザーの接続リストであり、そのユーザーのブラウザーセッションをまたいで保持されます。 共有接続グループはすべてのユーザーに対して同じであり、[すべての接続] ページから変更することはできません。
![](../media/shared-cnxns-2.png)