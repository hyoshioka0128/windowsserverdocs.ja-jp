---
title: Datacenter Firewall の概要
description: このトピックを使用すると、ネットワーク層、5 組 (プロトコル、ソースと宛先のポート番号、ソースおよび宛先の IP アドレス)、Windows Server 2016 でのステートフルなマルチ テナント ファイアウォールのあるデータ センターのファイアウォールについて説明します。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 67576533-206b-428a-956c-ed8c53218d9b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f1de50dc61639f4985c9d28fdde6072af650f42e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59890833"
---
# <a name="datacenter-firewall-overview"></a>Datacenter Firewall の概要

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

データ センターのファイアウォールは、Windows Server 2016 に含まれている新しいサービスです。 ネットワーク層、5 組 (プロトコル、ソースと宛先のポート番号、ソースおよび宛先の IP アドレス)、ステートフルなマルチ テナント ファイアウォールです。 デプロイし、サービス プロバイダーによって、サービスとして提供されている、ときに、テナント管理者はインストールして、そのインターネットからの不要なトラフィックからの仮想ネットワークおよびイントラネットのネットワークを保護するためのファイアウォール ポリシーを構成できます。  
  
![ネットワーク スタック内のデータ センターのファイアウォール](../../../media/Datacenter-Firewall-Overview/MultitenantFirewallOverview2.png)  
  
サービス プロバイダーの管理者またはテナント管理者は、ネットワーク コント ローラーおよび northbound Api 経由でデータ センターのファイアウォール ポリシーを管理できます。  
  
データ センターのファイアウォールでは、クラウド サービス プロバイダーの次の利点を提供しています。  
  
-   テナントに提供できる高いスケーラビリティ、管理性、および診断可能なソフトウェア ベースのファイアウォール ソリューション  
  
-   自由テナント ファイアウォールのポリシーを損なうことがなく、さまざまなコンピューティング ホストにテナントの仮想マシンを移動するには  
  
    -   VSwitch ポート ホスト エージェントのファイアウォールとしてデプロイされています。  
  
    -   テナントの仮想マシンの vSwitch ホスト エージェントのファイアウォールに割り当てられているポリシーを取得します。  
  
    -   仮想マシンを実行している実際のホストに依存せずに各 vSwitch ポートでファイアウォール規則が構成されています。  
  
-   テナント仮想マシンを別のテナントのゲスト オペレーティング システムへの保護を提供しています  
  
データ センターのファイアウォールには、テナント用の次の利点が提供しています。  
  
-   インターネットへの仮想ネットワーク上のワークロードを保護するためにファイアウォール規則を定義する機能  
  
-   同じ L2 仮想サブネットにも仮想マシンを別の L2 仮想サブネット間で仮想マシン間のトラフィックを保護するためにファイアウォール規則を定義する機能  
  
-   保護やテナント間のネットワーク トラフィックを分離するためのファイアウォール規則を定義する機能、オンプレミス ネットワークとその仮想ネットワーク サービス プロバイダー  
  


