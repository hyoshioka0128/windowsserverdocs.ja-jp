---
title: Virtual Network 暗号化
description: 仮想ネットワーク暗号化を使用すると、"暗号化が有効になっている" とマークされているサブネット内で相互に通信する仮想マシン間で仮想ネットワークトラフィックを暗号化できます。
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 7da0f509-7b02-4a0f-90fb-d97c83a2bc4e
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/08/2018
ms.openlocfilehash: 63daea02ec00593504383ce071d3f9454a37956b
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853575"
---
# <a name="virtual-network-encryption"></a>Virtual Network 暗号化

>適用対象: Windows Server

仮想ネットワーク暗号化を使用すると、"暗号化が有効になっている" とマークされているサブネット内で相互に通信する仮想マシン間で仮想ネットワークトラフィックを暗号化できます。 また、この機能は、仮想サブネットのデータグラム トランスポート層セキュリティ (DTLS) を利用して、パケットを暗号化します。 DTLS は、物理ネットワークへのアクセスを持つユーザーによる盗聴、改ざん、偽造に対する保護を提供します。

仮想ネットワークの暗号化には次のものが必要です。
- SDN が有効になっている各 Hyper-v ホストにインストールされている暗号化証明書。
- ネットワークコントローラーの資格情報オブジェクト。この証明書の拇印を参照しています。
- 各仮想ネットワークの構成には、暗号化が必要なサブネットが含まれています。

サブネットで暗号化を有効にすると、そのサブネット内のすべてのネットワークトラフィックが自動的に暗号化されます。また、アプリケーションレベルの暗号化も行われることになります。  暗号化済みとしてマークされていても、サブネット間を通過するトラフィックは暗号化されずに自動的に送信されます。 仮想ネットワークの境界を越えるすべてのトラフィックも、暗号化されずに送信されます。

>[!TIP]
>暗号化されたサブネット上でのみアプリケーションを通信するように制限する必要がある場合は、現在のサブネット内での通信のみを許可するように Access Control リスト (Acl) のみを使用できます。 詳細については、「 [Access Control リスト (acl) を使用してデータセンターのネットワークトラフィックフローを管理する」を](https://docs.microsoft.com/windows-server/networking/sdn/manage/use-acls-for-traffic-flow)参照してください。

### <a name="next-steps"></a>次のステップ:

[仮想ネットワークの暗号化の構成](https://docs.microsoft.com/windows-server/networking/sdn/vnet-encryption/sdn-config-vnet-encryption)

