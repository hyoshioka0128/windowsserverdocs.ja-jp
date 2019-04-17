---
title: 仮想ネットワークの暗号化
description: このトピックの「仮想ネットワーク暗号化に Windows Server でネットワーク定義ソフトウェア情報を提供します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 7da0f509-7b02-4a0f-90fb-d97c83a2bc4e
ms.author: pashort
author: grcusanz
ms.openlocfilehash: 425cc1cff8c7241aeec7764b60c89b4586fd323b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="virtual-network-encryption"></a>仮想ネットワークの暗号化

>Windows Server の適用対象:

仮想ネットワークの暗号化では、「暗号化を有効に」とマークされているサブネット内で相互に通信する仮想マシン間で暗号化する仮想ネットワーク トラフィックの機能を提供します。

この機能は、パケットの暗号化に仮想サブネットでデータグラム トランスポート層セキュリティ (DTLS) を利用します。  DTLS より、盗聴、改ざんや、物理ネットワークへのアクセスを持つユーザーが偽造に対する保護を提供します。

仮想ネットワークの暗号化 requries、SDN のそれぞれにインストールされている暗号化証明書有効になっている Hyper-V ホストでは、その証明書、および各仮想ネットワーク上の構成の拇印を参照する、ネットワーク コントローラーでの資格情報オブジェクト暗号化を必要とするサブネットを含みます。

サブネット上の暗号化を有効にする、そのサブネット内にあるすべてのネットワーク トラフィックは自動的に暗号化されます。  これは場所をかかる場合がありますもアプリケーション レベルの暗号化だけでなくなります。  暗号化はサブネットの両方が付いている場合でも、サブネット間の通過するトラフィックが暗号化されていない場合に自動的に送信されます。  仮想ネットワークの境界をまたぐするすべてのトラフィックは暗号化されていないも送信されます。

仮想ネットワークの暗号化を構成する方法については、次を参照してください。[仮想ネットワークの暗号化を構成する](sdn-config-vnet-encryption.md)します。

場合は、暗号化されたサブネットでのみ通信するためにアプリケーションを制限する必要があります。  現在のサブネット内での通信のみを許可するのにアクセス制御リスト (Acl) を使用できます。  

アクセス制御リストを構成する方法の詳細については、次を参照してください。[使用アクセス制御リスト (Acl) の管理データ センター ネットワーク トラフィック フローを](../manage/use-acls-for-traffic-flow.md)します。