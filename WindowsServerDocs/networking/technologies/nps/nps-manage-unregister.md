---
title: Active Directory ドメインから NPS サーバーの登録を解除します。
description: このトピックを使用すると、または別のドメインに NPS サーバーの既定のドメインでの Windows Server 2016 でネットワーク ポリシー サーバーを実行しているサーバーを登録します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 68a94616-3c29-45bd-bd33-e4c578f119e1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 55c3b00146706831351ce63d1e5b74f45d7b9be1
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="unregister-an-nps-server-from-an-active-directory-domain"></a>Active Directory ドメインから NPS サーバーの登録を解除します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

NPS サーバーの展開を管理するには、処理中であるした可能性があります方を置き換える NPS サーバー、または NPS サーバーをインベントリから削除する別のドメインに NPS サーバーを移動すると便利です。 

移動するか、または NPS サーバーの使用を停止するときに、NPS サーバーが Active Directory 内のユーザー アカウントのプロパティを読み取るアクセス許可を持つ Active Directory ドメインに NPS サーバーの登録を解除することができます。

メンバーシップ**管理者**、またはそれと同等がこれらの手順を実行するために必要な最小値。

## <a name="to-unregister-an-nps-server"></a>NPS サーバーの登録を解除するには

1. ドメイン コントローラー、サーバー マネージャーで、クリックして**ツール**、] をクリックし、**Active Directory ユーザーとコンピューター**します。 Active Directory ユーザーとコンピューター コンソールが開きます。

2. をクリックして**ユーザー**、順にダブルクリック**RAS および IAS サーバー**します。

3. をクリックして、**メンバー**タブ、および NPS サーバーの登録を解除するを選択します。

4. をクリックして**削除**、] をクリックして**[はい]**、] をクリックし、**OK**します。

