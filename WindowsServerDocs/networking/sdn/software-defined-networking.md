---
title: ソフトウェア定義ネットワーク (SDN)
description: ソフトウェア定義ネットワーク (SDN) は、データ センター内のルーター、スイッチ、およびゲートウェイなどの物理および仮想ネットワーク デバイスを一元的に構成・管理する手段を提供します。 このトピックでは、Windows Server、System Center、および Microsoft Azure で提供されるソフトウェア定義ネットワーク (SDN) テクノロジについて説明します。
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 9a1ea73c-20cd-42c5-95ad-b003b9cc6d64
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/09/2018
ms.openlocfilehash: 355375b17132a46f070d5ef34cd6ea02a36868e0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854335"
---
# <a name="sdn-in-windows-server-overview"></a>Windows Server の SDN の概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2016


ソフトウェア定義ネットワーク (SDN) は、データ センター内のルーター、スイッチ、およびゲートウェイなどの物理および仮想ネットワーク デバイスを一元的に構成・管理する手段を提供します。 既存の SDN と互換性のあるデバイスを使用して、仮想ネットワークと物理ネットワークの間の統合をさらに強化することができます。 Hyper-v 仮想スイッチ、Hyper-v ネットワーク仮想化、RAS ゲートウェイなどの仮想ネットワーク要素は、SDN インフラストラクチャの不可欠な要素として設計されています。 

>[!Note]
>ネットワークコントローラーやソフトウェアの負荷分散ノードなど、SDN インフラストラクチャサーバーを実行する hyper-v ホストと仮想マシン (Vm) には、Windows Server 2016 Datacenter edition がインストールされている必要があります。 
>
>SDN で制御されるネットワークに接続されているテナントワークロード Vm のみを含む hyper-v ホストでは、Windows Server 2016 Standard edition を使用できます。

ネットワークプレーンがネットワークデバイス自体にバインドされなくなったため、SDN が可能です。 ただし、System Center 2016 のようなデータセンター管理ソフトウェアなどの他のエンティティは、ネットワークプレーンを使用します。 SDN を使用すると、データセンターネットワークを動的に管理できるため、アプリケーションとワークロードの要件を満たすための自動化された一元的な方法を実現できます。 

SDN を使用して、次のことを行うことができます。

- アプリの進化するニーズに合わせて、ネットワークを動的に作成、セキュリティ保護、接続します
- 中断のない方法でワークロードのデプロイを高速化する
- ネットワーク全体に分散することによるセキュリティの脆弱性を含む
- 物理ネットワークと仮想ネットワークの両方を管理するポリシーを定義および制御する 
- 大規模なネットワークポリシーの実装

SDN を使用すると、インフラストラクチャ全体のコストを削減しながら、すべてを実現できます。



## <a name="contact-the-datacenter-and-cloud-networking-product-team"></a>データセンターとクラウドネットワークの製品チームに問い合わせてください

SDN テクノロジと Microsoft またはその他の SDN 顧客との話し合いに関心がある場合は、さまざまな方法で連絡を取ることができます。

詳細については、「[データセンターとクラウドネットワークチームに問い合わせる](contact-sdn-team.md)」を参照してください。
