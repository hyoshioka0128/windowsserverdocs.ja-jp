---
title: 接続要求ポリシーを構成する
description: このトピックでは、Windows Server 2016 でネットワーク ポリシー サーバーで接続要求ポリシーを構成する方法について説明します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: f62c6a67-4dda-47f8-8bdf-9b76c37953e6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4f80f9fb8be0c44cfb5685e5b9cc489282e4961d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884513"
---
# <a name="configure-connection-request-policies"></a>接続要求ポリシーを構成する

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

作成およびローカルの NPS 接続要求を処理するか、処理用のリモート RADIUS サーバーに転送するかどうかを指定している接続要求ポリシーを構成するには、このトピックを使用します。

接続要求ポリシーは条件のセットと、ネットワーク管理者がリモート認証ダイヤルイン ユーザー サービス (RADIUS) サーバーを指定する設定は、認証を実行し、接続の承認を要求する、ネットワーク ポリシー サーバーを実行しているサーバー \(NPS\) RADIUS クライアントから受信します。

既定の接続要求ポリシーは NPS を RADIUS サーバーとして使用し、すべての認証要求をローカルで処理します。

RADIUS プロキシ、および転送接続要求を他の NPS または RADIUS サーバーとして機能する NPS を実行するサーバーを構成するには、条件と設定を指定する新しい接続要求ポリシーを追加するだけでなく、リモート RADIUS サーバー グループを構成する必要がありますが接続要求に一致する必要があります。

新しい接続要求ポリシー ウィザードを使用して新しい接続要求ポリシーを作成するときに、新しいリモート RADIUS サーバー グループを作成することができます。

RADIUS サーバーとプロセスの接続要求をローカルとして機能する NPS したくない場合は、既定の接続要求ポリシーを削除できます。

既定値を NPS を RADIUS サーバー、接続要求をローカルでの処理として動作させをリモート RADIUS サーバー グループでは、一部の接続要求を転送する RADIUS プロキシとして、次の手順を使用して新しいポリシーを追加してとことを確認する場合接続要求ポリシーは、ポリシーの一覧の最後に配置することによって処理された最後のポリシーです。

## <a name="add-a-connection-request-policy"></a>接続要求ポリシーを追加します。

この手順を完了するには、少なくとも **Domain Admins** グループ、またはそれと同等のメンバーシップが必要です。

### <a name="to-add-a-new-connection-request-policy"></a>新しい接続要求ポリシーを追加するには 

1. サーバー マネージャーで、**ツール**、 をクリックし、**ネットワーク ポリシー サーバー** NPS コンソールを開きます。 
2. コンソール ツリーで、ダブルクリック**ポリシー**します。
3. 右クリックして**接続要求ポリシー**、 をクリックし、**新しい接続要求ポリシー**します。
4. 使用して接続を構成する新しい接続要求ポリシー ウィザードは、ポリシーを要求し、以前に構成しない場合、リモート RADIUS サーバー グループ。


NPS の管理に関する詳細については、次を参照してください。[ネットワーク ポリシー サーバーの管理](nps-manage-top.md)します。

NPS の詳細については、次を参照してください。[ネットワーク ポリシー サーバー (NPS)](nps-top.md)します。

