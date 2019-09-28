---
title: 接続要求ポリシーを構成する
description: このトピックでは、Windows Server 2016 のネットワークポリシーサーバーで接続要求ポリシーを構成する方法について説明します。
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: f62c6a67-4dda-47f8-8bdf-9b76c37953e6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: d62beb3106141d4683c957020bc96e4a7dfb306f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405473"
---
# <a name="configure-connection-request-policies"></a>接続要求ポリシーを構成する

>適用対象:Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用して、ローカル NPS が接続要求を処理するか、リモート RADIUS サーバーに転送して処理するかを指定する接続要求ポリシーを作成して構成できます。

接続要求ポリシーは、ネットワーク管理者が接続要求の認証と承認を実行するリモート認証ダイヤルインユーザーサービス (RADIUS) サーバーを指定できるようにするための条件と設定のセットです。ネットワークポリシーサーバーを実行しているサーバー \(NPS @ no__t は RADIUS クライアントから受信します。

既定の接続要求ポリシーでは、NPS を RADIUS サーバーとして使用し、すべての認証要求をローカルで処理します。

NPS を実行するサーバーが RADIUS プロキシとして機能し、接続要求を他の NPS または RADIUS サーバーに転送するように構成するには、新しい接続要求ポリシーを追加するだけでなく、リモート RADIUS サーバーグループを構成する必要があります。接続要求が一致している必要があります。

新しい接続要求ポリシーウィザードを使用して新しい接続要求ポリシーを作成するときに、新しいリモート RADIUS サーバーグループを作成できます。

NPS が RADIUS サーバーとして機能し、接続要求をローカルで処理しないようにする場合は、既定の接続要求ポリシーを削除できます。

NPS を RADIUS サーバーとして機能させ、接続要求をローカルで処理し、RADIUS プロキシとして使用して、一部の接続要求をリモート RADIUS サーバーグループに転送する場合は、次の手順に従って新しいポリシーを追加して、既定のポリシーであることを確認します。接続要求ポリシーは、ポリシーの一覧の最後に配置することによって最後に処理されるポリシーです。

## <a name="add-a-connection-request-policy"></a>接続要求ポリシーを追加する

この手順を完了するには、少なくとも **Domain Admins** グループ、またはそれと同等のメンバーシップが必要です。

### <a name="to-add-a-new-connection-request-policy"></a>新しい接続要求ポリシーを追加するには 

1. サーバーマネージャーで、 **[ツール]** をクリックし、 **[ネットワークポリシーサーバー]** をクリックして NPS コンソールを開きます。 
2. コンソールツリーで、 **[ポリシー]** をダブルクリックします。
3. **[接続要求ポリシー]** を右クリックし、 **[新しい接続要求ポリシー]** をクリックします。
4. 新しい接続要求ポリシーウィザードを使用して、接続要求ポリシーを構成します。これを構成していない場合は、リモート RADIUS サーバーグループを構成します。


NPS の管理の詳細については、「 [Manage Network Policy Server](nps-manage-top.md)」を参照してください。

NPS の詳細については、「[ネットワークポリシーサーバー (nps)](nps-top.md)」を参照してください。

