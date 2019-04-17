---
title: NPS で NAS 通知の転送を無効にします。
description: このトピックでは、Windows Server 2016 でのネットワーク ポリシー サーバーの同時認証の構成手順について説明します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: a09bfb03-95fc-4534-bf3c-97078ef6b07e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c25f3b5a94624a35099e84ede3296f7ab860da7c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="disable-nas-notification-forwarding-in-nps"></a>NPS で NAS 通知の転送を無効にします。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

スタート画面の転送を無効にして、NPS で構成されている、リモート RADIUS サーバー グループのメンバーへのネットワーク アクセス サーバー (Nas) からメッセージを停止するこの手順を使用することができます。

リモート RADIUS サーバー グループを構成した場合、NPS で**接続要求ポリシー**、オフにする、**このリモート RADIUS サーバー グループにアカウンティング要求を転送**チェック ボックスをこれらのグループにも適用されます NAS 開始し、停止の通知メッセージ。 

これにより、不要なネットワーク トラフィックが作成されます。 このトラフィックを排除するには、各リモート RADIUS サーバー グループの個々 のサーバーに転送 NAS 通知を無効にします。

この手順を完了するには、メンバーである、**管理者**グループ。

### <a name="to-disable-nas-notification-forwarding"></a>NAS 通知の転送を無効にするには

1. サーバー マネージャーで、クリックして**ツール**、] をクリックし、**ネットワーク ポリシー サーバー**します。 NPS コンソールが開きます。

2. NPS コンソールで、ダブルクリック**RADIUS クライアントとサーバー**、] をクリックして**リモート RADIUS サーバー グループ**、し、構成するのとリモート RADIUS サーバー グループをダブルクリックします。 リモート RADIUS サーバー グループ**プロパティ**] ダイアログ ボックスが開きます。

3. 構成、およびをクリックするグループのメンバーをダブルクリックして、**認証またはアカウンティング**] タブ。

4. **アカウンティング**をオフ、**転送のネットワーク アクセス サーバーの開始と停止のこのサーバーに通知**チェック ボックスをオンにし**OK**します。

5. 構成するすべてのグループ メンバーの手順 3. および 4. を繰り返します。

NPS の管理に関する詳細については、次を参照してください。[ネットワーク ポリシー サーバーの管理](nps-manage-top.md)します。

NPS の詳細については、次を参照してください。[ネットワーク ポリシー サーバー (NPS)](nps-top.md)します。
