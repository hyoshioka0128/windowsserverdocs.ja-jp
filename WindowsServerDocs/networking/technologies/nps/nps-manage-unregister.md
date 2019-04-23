---
title: Active Directory ドメインから NPS の登録を解除する
description: このトピックでは、NPS の既定のドメインまたは別のドメイン内の Windows Server 2016 でネットワーク ポリシー サーバーを実行しているサーバーの登録を使用できます。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 68a94616-3c29-45bd-bd33-e4c578f119e1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8fe4773efd89aeb413b3793f874ad6a1b030294a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864353"
---
# <a name="unregister-an-nps-from-an-active-directory-domain"></a>Active Directory ドメインから NPS の登録を解除する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

NPS の展開を管理するには、処理した方を置き換える、NPS または NPS をインベントリから削除する別のドメインに NPS を移動すると便利です。 

移動または NPS の使用を停止すると、NPS が Active Directory 内のユーザー アカウントのプロパティを読み取るアクセス許可を持つ Active Directory ドメインに NPS の登録を解除することができます。

これらの手順を実行するには、**Administrators** のメンバーシップ、またはそれと同等のメンバーシップが最低限必要です。

## <a name="to-unregister-an-nps"></a>NPS の登録を解除するには

1. ドメイン コント ローラーで、サーバー マネージャーで、次のようにクリックします。**ツール**、 をクリックし、 **Active Directory ユーザーとコンピューター**します。 Active Directory ユーザーとコンピューター コンソールが開きます。

2. クリックして**ユーザー**、し、ダブルクリック**RAS および IAS サーバー**します。

3. をクリックして、**メンバー**タブをクリックし、登録を解除する NPS を選択します。

4. をクリックして**削除**、 をクリックして**はい**、順にクリックします**OK**します。

