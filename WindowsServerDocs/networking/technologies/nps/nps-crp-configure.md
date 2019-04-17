---
title: 接続要求ポリシーを構成します。
description: このトピックでは、Windows Server 2016 でのネットワーク ポリシー サーバーの接続要求ポリシーを構成する方法について説明します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: f62c6a67-4dda-47f8-8bdf-9b76c37953e6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9677e147bdaea4de71a054cd6c52d81126e005d1
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="configure-connection-request-policies"></a>接続要求ポリシーを構成します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックの「を使用して、作成しローカルの NPS サーバーが接続要求を処理するか、処理ためのリモート RADIUS サーバーに転送するかを指定する接続要求ポリシーを構成することができます。

接続要求ポリシーは、条件と、ネットワーク管理者が認証およびネットワーク ポリシー サーバー \(NPS\) を実行しているサーバーが RADIUS クライアントから受信接続要求の承認を実行するリモート認証ダイヤルイン ユーザー サービス (RADIUS) サーバーを指定する設定のセットです。

既定の接続要求ポリシーでは、NPS を RADIUS サーバーとして使用し、ローカルでのすべての認証要求を処理します。

RADIUS プロキシ、および転送要求を他の NPS または RADIUS サーバーとして機能するために NPS を実行しているサーバーを構成するのには、条件と、接続要求が一致する必要がある設定を指定する新しい接続要求ポリシーを追加するだけでなく、リモート RADIUS サーバー グループを構成する必要があります。

新しい接続要求ポリシー ウィザードを使用して新しい接続要求ポリシーを作成するときに、新しいリモート RADIUS サーバー グループを作成することができます。

NPS サーバーを RADIUS サーバーとプロセスの接続要求をローカルとして機能したくない場合は、既定の接続要求ポリシーを削除することができます。

NPS サーバーを RADIUS サーバーとして機能する場合は、接続要求の処理、ローカルとリモートの RADIUS サーバー グループにいくつかの接続要求を転送、RADIUS プロキシとして、次の手順を使用して新しいポリシーを追加し、既定の接続要求ポリシーが最後にポリシーによってポリシーの一覧の最後に配置処理であることを確認します。

## <a name="add-a-connection-request-policy"></a>接続要求ポリシーを追加します。

メンバーシップ**Domain Admins**、相当するものでは、この手順を完了するために必要な最低限またはします。

### <a name="to-add-a-new-connection-request-policy"></a>新しい接続要求ポリシーを追加するには 

1. サーバー マネージャーで、クリックして**ツール**、] をクリックし、**ネットワーク ポリシー サーバー** NPS コンソールを開きます。 
2. コンソール ツリーで、ダブルクリック**ポリシー**します。
3. 右クリック**接続要求ポリシー**、] をクリックし、**新しい接続要求ポリシー**します。
4. 使用して、新しい接続要求ポリシー ウィザードを接続を構成するのには、ポリシーを要求し、以前に構成されていない場合、リモート RADIUS サーバー グループ。


NPS の管理に関する詳細については、次を参照してください。[ネットワーク ポリシー サーバーの管理](nps-manage-top.md)します。

NPS の詳細については、次を参照してください。[ネットワーク ポリシー サーバー (NPS)](nps-top.md)します。

