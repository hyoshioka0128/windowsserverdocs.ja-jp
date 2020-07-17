---
title: コンテナー ネットワークの概要
description: このトピックでは、Windows コンテナーのネットワークスタックの概要について説明し、コンテナーネットワークの作成、構成、および管理に関するその他のガイダンスへのリンクを示します。
manager: grcusanz
ms.prod: windows-server
ms.technology: networking-sdn
ms.topic: article
ms.assetid: 318659e5-e4a5-4e46-99d6-211dfc46f6b8
ms.author: anpaul
author: AnirbanPaul
ms.date: 09/04/2018
ms.openlocfilehash: 8e2f10c7577f6f271c3766cff9a4fb1cc9d41140
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80854315"
---
# <a name="container-networking-overview"></a>コンテナー ネットワークの概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Windows コンテナーのネットワークスタックの概要について説明し、コンテナーネットワークの作成、構成、管理に関するその他のガイダンスへのリンクを示します。

Windows Server のコンテナーは、同じコンテナーホストで実行されている他のサービスからアプリケーションやサービスを分離する、オペレーティングシステムの簡易仮想化の方法です。 Windows コンテナーは、仮想マシンと同様に機能します。 有効にすると、各コンテナーには、仮想ネットワークに接続できるオペレーティングシステム、プロセス、ファイルシステム、レジストリ、および IP アドレスが個別に表示されます。 

Windows コンテナーは、ホスト上で実行されているコンテナーホストとすべてのコンテナーを使用してカーネルを共有します。 これらのコンテナーはカーネルを共有しているため、カーネルのバージョンと構成を同一にする必要があります。 コンテナーは、プロセスと名前空間の分離テクノロジによってアプリケーションの分離を提供します。

>[!IMPORTANT]
>Windows コンテナーは、悪意のあるセキュリティ境界を提供しないため、信頼されていないコードを分離するために使用しないでください。 

Windows コンテナーを使用すると、Hyper-v ホストを展開して、VM ホスト上に1つ以上の仮想マシンを作成することができます。 VM ホスト内では、コンテナーが作成され、ネットワークアクセスは仮想マシン内で実行されている仮想スイッチを介して行われます。 リポジトリに格納されている再利用可能なイメージを使用して、オペレーティングシステムとサービスをコンテナーに展開できます。 各コンテナーには、仮想スイッチに接続し、受信トラフィックと送信トラフィックを転送する仮想ネットワークアダプターがあります。 コンテナーエンドポイントをローカルホストネットワーク (NAT など)、物理ネットワーク、または SDN スタックを介して作成されたオーバーレイ仮想ネットワークに接続できます。

同じホスト上のコンテナー間の分離を強制するために、Windows Server と Hyper-v コンテナーごとにネットワークコンパートメントを作成します。 Windows Server コンテナーでは、仮想スイッチへの接続に Host vNIC を使用します。 HYPER-V コンテナーでは、仮想スイッチへの接続に (ユーティリティ VM には公開されていない) 統合 VM NIC を使用します。 

## <a name="related-topics"></a>関連トピック 

- [Windows コンテナーネットワーク](https://docs.microsoft.com/virtualization/windowscontainers/container-networking/architecture): 非オーバーレイ/SDN デプロイ用のコンテナーネットワークを作成および管理する方法について説明します。

- [テナントの仮想ネットワークにコンテナーのエンドポイントを接続](../../manage/Connect-container-endpoints-to-a-Tenant-Virtual-Network.md)する: SDN を使用してオーバーレイ仮想ネットワークのコンテナーネットワークを作成および管理する方法について説明します。 