---
title: 仮想ネットワークと Vlan の動作についてください。
description: このトピックでは、テナント ワークロードを管理および Windows Server 2016 での仮想ネットワークに方法について、ソフトウェア定義ネットワーク ガイドの一部です。
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 84ac2458-3fcf-4c4f-acfe-6105443dd83f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fcf84c5c1f0be2fa1c7524592f8d02e4b11d3a2b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="understanding-usage-of-virtual-networks-and-vlans"></a>仮想ネットワークと Vlan の動作についてください。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、Hyper-V ネットワーク仮想化の仮想ネットワークと仮想ローカル エリア ネットワーク (Vlan) との違いについて説明します。  
  
ソフトウェアによるネットワーク制御 (SDN) Windows Server 2016 では、Hyper-V 仮想スイッチに仮想ネットワークのオーバーレイのポリシーのプログラミングに基づいています。 オーバーレイの仮想ネットワーク、仮想ネットワークと、Hyper-V ネットワーク仮想化とも呼ばれます。を作成することができます。   
  
Hyper-V ネットワーク仮想化を展開するときにオーバーレイまたはトンネル ヘッダーなど、VXLAN (NVGRE) とレイヤー 3 IP とイーサネットのレイヤー 2 ヘッダー アンダーレイ (または物理) からネットワークを使用して、元のテナント仮想マシンのレイヤー 2 イーサネット フレームをカプセル化してオーバーレイ ネットワークが作成されます。 によって、24 ビット仮想ネットワーク識別子 (VNI) と重複する IP アドレスを許可するようにテナント トラフィックの分離を維持するために、仮想ネットワークのオーバーレイが識別されます。 VNI は仮想サブネット ID (VSID)、論理スイッチの ID、およびトンネル ID で構成されます。  
  
さらに、各テナントが割り当てられている (仮想ルーティングおよび転送 - VRF に似ています)、ルーティング ドメイン (各は、VNI によって表される) 複数の仮想サブネット プレフィックスは相互に直接ルーティングできるようにします。 クロス テナント (またはルーティング ドメインを越えた) ゲートウェイを経由せずにルーティングはサポートされていません。   
  
各テナントのカプセル化されたトラフィックがトンネルは、物理ネットワークは、プロバイダーの論理ネットワークと呼ばれる論理ネットワークで表されます。 このプロバイダーの論理ネットワークは 1 つまたは複数のサブネットの構成され、それぞれ、IP プレフィックスと、必要に応じて、802.1 q VLAN で表されますタグ。  
  
追加の論理ネットワークを作成して、サブネットの管理トラフィック、記憶域トラフィックを実行するために、インフラストラクチャの目的でライブ マイグレーション トラフィックなど。  
  
Microsoft SDN は、Vlan を使用してテナントのネットワークの分離をサポートしていません。 テナントの分離は、Hyper-V ネットワーク仮想化のオーバーレイの仮想ネットワークとのカプセル化を使用するだけで実現します。 


