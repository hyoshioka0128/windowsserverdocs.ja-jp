---
title: Windows Admin Center ゲートウェイのすべてのユーザーに対して共有接続を構成する
description: 管理者が Windows Admin Center (Project Honolulu) ゲートウェイを一度に構成して、すべてのユーザーが接続の単一のリストを共有できるようにする方法を説明します。
ms.technology: manage
ms.topic: article
author: haley-rowland
ms.author: harowl
ms.date: 03/28/2019
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: e0e78ac8feb4e008e060ba318bd5693e841b91b2
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2020
ms.locfileid: "87518599"
---
# <a name="configure-shared-connections-for-all-users-of-the-windows-admin-center-gateway"></a>Windows Admin Center ゲートウェイのすべてのユーザーに対して共有接続を構成する

> 適用先:Windows Admin Center Preview、Windows Admin Center

共有接続を構成する機能により、ゲートウェイ管理者は特定の Windows Admin Center ゲートウェイのすべてのユーザーに対して、接続リストを一度に構成することができます。 この機能は、Windows Admin Center のサービス モードでのみ利用可能です。

ゲートウェイ管理者は Windows Admin Center ゲートウェイの [設定] にある **[Shared Connections]\(共有接続\)** タブから、[すべての接続] ページの場合と同じように、サーバー、クラスター、PC 接続を追加できます。接続のタグ付けも可能です。 共有接続のリストで追加された接続とタグは、この Windows Admin Center ゲートウェイのすべてのユーザーに対し、[すべての接続] ページで表示されます。

![Windows Admin Center - 共有接続のページ](../media/shared-cnxns-1.png)

共有接続が構成された後に Windows Admin Center ユーザーが [すべての接続] ページにアクセスすると、接続は 2 つのセクションにグループ化されて表示されます。[個人] と [共有] の接続です。 [個人] のグループは特定のユーザーの接続のリストであり、そのユーザーのブラウザー セッションをまたいで保持されます。 [共有] 接続のグループはすべてのユーザーに対して同じであり、[すべての接続] ページから変更することはできません。

![Windows Admin Center - すべての接続のページ](../media/shared-cnxns-2.png)