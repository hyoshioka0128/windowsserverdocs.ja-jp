---
title: 仮想ネットワークの暗号化
description: 仮想ネットワークの暗号化では、' 暗号化を有効にします ' としてマークされているサブネット内で互いと通信する仮想マシン間の仮想ネットワーク トラフィックの暗号化
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 7da0f509-7b02-4a0f-90fb-d97c83a2bc4e
ms.author: pashort
author: shortpatti
ms.date: 08/08/2018
ms.openlocfilehash: f2f50ae3146854e2ef6081b0c400a474b53dcf66
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851083"
---
# <a name="virtual-network-encryption"></a>仮想ネットワークの暗号化

>適用対象:Windows Server

仮想ネットワークの暗号化では、' 暗号化を有効にします ' としてマークされているサブネット内で互いと通信する仮想マシン間の仮想ネットワーク トラフィックの暗号化 また、この機能は、仮想サブネットのデータグラム トランスポート層セキュリティ (DTLS) を利用して、パケットを暗号化します。 DTLS は、物理ネットワークへのアクセスを持つユーザーによる盗聴、改ざん、偽造に対する保護を提供します。

仮想ネットワークの暗号化が必要です。
- 各 SDN 対応の HYPER-V ホストにインストールされている暗号化証明書。
- その証明書の拇印を参照しているネットワーク コント ローラー内の資格情報オブジェクト。
- 各仮想ネットワークの構成には、暗号化が必要なサブネットが含まれます。

サブネット上の暗号化を有効にすると場合がありますも行われるアプリケーション レベルの暗号化に加えて、そのサブネット内のすべてのネットワーク トラフィックが自動的に暗号化されます。  暗号化された、としてマークされている場合でも、サブネット間を通過するトラフィックは、自動的に暗号化されていないに送信されます。 仮想ネットワークの境界を越える任意のトラフィックも送信される暗号化されていません。

>[!TIP]
>暗号化されたサブネット上でのみ通信するのにアプリケーションを制限する必要があります場合、アクセス制御リスト (Acl) を使用だけが、現在のサブネット内の通信を許可できます。 詳細については、次を参照してください。[使用へのアクセス制御リスト (Acl) を管理データ センター ネットワーク トラフィックのフローを](https://docs.microsoft.com/windows-server/networking/sdn/manage/use-acls-for-traffic-flow)します。

### <a name="next-steps"></a>次のステップ

[仮想ネットワークの暗号化を構成します。](https://docs.microsoft.com/windows-server/networking/sdn/vnet-encryption/sdn-config-vnet-encryption)

