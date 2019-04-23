---
title: ソフトウェア定義ネットワーク (SDN)
description: ソフトウェア定義ネットワーク (SDN) は、データ センター内のルーター、スイッチ、およびゲートウェイなどの物理および仮想ネットワーク デバイスを一元的に構成・管理する手段を提供します。 このトピックを使用して、Windows Server、System Center、および Microsoft Azure で提供されるソフトウェア定義ネットワーク (SDN) テクノロジについて説明します。
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 9a1ea73c-20cd-42c5-95ad-b003b9cc6d64
ms.author: pashort
author: shortpatti
ms.date: 08/09/2018
ms.openlocfilehash: a6c4db97b1c55d5114eba09251685ef0f2b840bc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59855233"
---
# <a name="sdn-in-windows-server-overview"></a>Windows Server の SDN の概要

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)


ソフトウェア定義ネットワーク (SDN) は、データ センター内のルーター、スイッチ、およびゲートウェイなどの物理および仮想ネットワーク デバイスを一元的に構成・管理する手段を提供します。 仮想ネットワークと物理ネットワークの間の緊密な統合を実現するために、既存の SDN と互換性のあるデバイスを使用することができます。 SDN インフラストラクチャの不可欠な要素は、HYPER-V 仮想スイッチ、HYPER-V ネットワーク仮想化、および RAS ゲートウェイなどの仮想ネットワーク要素が設計されています。 

>[!Note]
>HYPER-V ホストと SDN インフラストラクチャ サーバー、ネットワーク コント ローラーとソフトウェアの負荷分散のノードなどを実行する仮想マシン (Vm) には、Windows Server 2016 Datacenter edition がインストールされている必要があります。 
>
>SDN 管理ネットワークに接続されているコンテナーのみテナント ワークロード Vm、HYPER-V ホストには、Windows Server 2016 Standard edition を使用できます。

SDN は、ネットワーク プレーンは、ネットワーク デバイス自体にバインドされていないため、可能性があります。 ただし、System Center 2016 のようなデータ センター管理ソフトウェアなどの他のエンティティは、ネットワーク面を使用します。 SDN を使用すると、データ センター ネットワークを動的に管理、アプリケーションとワークロードの要件を満たすために自動で一元的な手段を提供します。 

SDN を使用することができます。

- 動的に作成、保護、およびアプリのニーズを満たすためにネットワーク接続
- 非破壊的な方法で、ワークロードのデプロイを高速化します。
- ネットワーク経由で分散することから、セキュリティの脆弱性を含む
- 定義し、物理および仮想ネットワークを管理するポリシーを制御します。 
- スケールで一貫してネットワーク ポリシーを実装します。

SDN も、全体的なインフラストラクチャ コストを削減しながらすべてこれを実現することができます。



## <a name="contact-the-datacenter-and-cloud-networking-product-team"></a>データ センターとクラウド ネットワークの製品チームにお問い合わせください。

Microsoft やその他の SDN 顧客 SDN テクノロジについても説明して知りたい場合は、さまざまなメソッドを行うのためにお問い合わせください。

詳細については、次を参照してください。[データ センターとクラウド ネットワーク チームにお問い合わせください](contact-sdn-team.md)します。
