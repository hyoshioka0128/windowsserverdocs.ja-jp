---
title: 接続要求ポリシーを構成する
description: このトピックでは、Windows Server 2016 のネットワークポリシーサーバーで接続要求ポリシーを構成する方法について説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: f62c6a67-4dda-47f8-8bdf-9b76c37953e6
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 7b42dd9470b44b0f1c7d25627d491cd6f2a2dfae
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316279"
---
# <a name="configure-connection-request-policies"></a>接続要求ポリシーを構成する

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用して、ローカル NPS が接続要求を処理するか、リモート RADIUS サーバーに転送して処理するかを指定する接続要求ポリシーを作成して構成できます。

接続要求ポリシーは一連の条件と設定で構成され、ネットワーク管理者は、ネットワークポリシーサーバー \(NPS\) 実行しているサーバーが RADIUS クライアントから受信する接続要求の認証と承認を、ネットワーク管理者がリモート認証ダイヤルインユーザーサービス指定できます。

既定の接続要求ポリシーは NPS を RADIUS サーバーとして使用し、すべての認証要求をローカルで処理します。

NPS を実行するサーバーを RADIUS プロキシとして機能させ、接続要求を他の NPS または RADIUS サーバーに転送するように構成するには、接続要求が満たすべき条件と設定を指定する新しい接続要求ポリシーを追加するだけでなく、リモート RADIUS サーバー グループを構成する必要もあります。

新しい接続要求ポリシーウィザードを使用して新しい接続要求ポリシーを作成するときに、新しいリモート RADIUS サーバーグループを作成できます。

NPS が RADIUS サーバーとして機能し、接続要求をローカルで処理しないようにする場合は、既定の接続要求ポリシーを削除できます。

NPS を RADIUS サーバーとして機能させ、接続要求をローカルで処理し、RADIUS プロキシとして使用して、一部の接続要求をリモート RADIUS サーバーグループに転送する場合は、次の手順に従って新しいポリシーを追加して、既定のポリシーであることを確認します。接続要求ポリシーは、ポリシーの一覧の最後に配置することによって最後に処理されるポリシーです。

## <a name="add-a-connection-request-policy"></a>接続要求ポリシーを追加する

この手順を完了するには、少なくとも、**Domain Admins** グループ、またはそれと同等の権限を持つグループのメンバである必要があります。

### <a name="to-add-a-new-connection-request-policy"></a>新しい接続要求ポリシーを追加するには 

1. サーバーマネージャーで、 **[ツール]** をクリックし、 **[ネットワークポリシーサーバー]** をクリックして NPS コンソールを開きます。 
2. コンソールツリーで、 **[ポリシー]** をダブルクリックします。
3. **[接続要求ポリシー]** を右クリックし、 **[新しい接続要求ポリシー]** をクリックします。
4. 新しい接続要求ポリシー ウィザードを使用して接続要求ポリシーを構成し、リモート RADIUS サーバー グループが構成されていない場合はこれを構成します。


NPS の管理の詳細については、「 [Manage Network Policy Server](nps-manage-top.md)」を参照してください。

NPS の詳細については、「[ネットワークポリシーサーバー (nps)](nps-top.md)」を参照してください。

