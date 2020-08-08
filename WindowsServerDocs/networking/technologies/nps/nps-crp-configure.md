---
title: 接続要求ポリシーを構成する
description: このトピックでは、Windows Server 2016 のネットワークポリシーサーバーで接続要求ポリシーを構成する方法について説明します。
manager: brianlic
ms.topic: article
ms.assetid: f62c6a67-4dda-47f8-8bdf-9b76c37953e6
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 422ef3238aac950b7d2808d8576b186aeb430767
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969419"
---
# <a name="configure-connection-request-policies"></a>接続要求ポリシーを構成する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用して、ローカル NPS が接続要求を処理するか、リモート RADIUS サーバーに転送して処理するかを指定する接続要求ポリシーを作成して構成できます。

接続要求ポリシーは一連の条件と設定で構成され、ネットワーク管理者は、ネットワークポリシーサーバー NPS を実行しているサーバーが \( radius クライアントから受信する接続要求の認証および承認を実行するリモート認証ダイヤルインユーザーサービス (radius) サーバーを指定でき \) ます。

既定の接続要求ポリシーは NPS を RADIUS サーバーとして使用し、すべての認証要求をローカルで処理します。

NPS を実行するサーバーを RADIUS プロキシとして機能させ、接続要求を他の NPS または RADIUS サーバーに転送するように構成するには、接続要求が満たすべき条件と設定を指定する新しい接続要求ポリシーを追加するだけでなく、リモート RADIUS サーバー グループを構成する必要もあります。

新しい接続要求ポリシーウィザードを使用して新しい接続要求ポリシーを作成するときに、新しいリモート RADIUS サーバーグループを作成できます。

NPS が RADIUS サーバーとして機能し、接続要求をローカルで処理しないようにする場合は、既定の接続要求ポリシーを削除できます。

NPS が RADIUS サーバーとして機能し、接続要求をローカルで処理し、RADIUS プロキシとして動作し、いくつかの接続要求をリモート RADIUS サーバーグループに転送する場合は、次の手順に従って新しいポリシーを追加し、既定の接続要求ポリシーが最後に処理されたポリシーであることを確認します。

## <a name="add-a-connection-request-policy"></a>接続要求ポリシーを追加する

この手順を完了するには、少なくとも、**Domain Admins** グループ、またはそれと同等の権限を持つグループのメンバである必要があります。

### <a name="to-add-a-new-connection-request-policy"></a>新しい接続要求ポリシーを追加するには

1. サーバーマネージャーで、[**ツール**] をクリックし、[**ネットワークポリシーサーバー** ] をクリックして NPS コンソールを開きます。
2. コンソールツリーで、[**ポリシー**] をダブルクリックします。
3. [**接続要求ポリシー**] を右クリックし、[**新しい接続要求ポリシー**] をクリックします。
4. 新しい接続要求ポリシー ウィザードを使用して接続要求ポリシーを構成し、リモート RADIUS サーバー グループが構成されていない場合はこれを構成します。


NPS の管理の詳細については、「 [Manage Network Policy Server](nps-manage-top.md)」を参照してください。

NPS の詳細については、「[ネットワークポリシーサーバー (nps)](nps-top.md)」を参照してください。

