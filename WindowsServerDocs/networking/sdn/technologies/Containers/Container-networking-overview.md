---
title: コンテナー ネットワークの概要
description: このトピックでは、Windows コンテナーのネットワーク スタックの概要については、し、詳細なガイダンスについては、作成、構成、およびコンテナーのネットワークの管理へのリンクが含まれています。
manager: ravirao
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 318659e5-e4a5-4e46-99d6-211dfc46f6b8
ms.author: pashort
author: jmesser81
ms.date: 09/04/2018
ms.openlocfilehash: 72b1ac739d9012ac7b90e97abe22e5f321ddba63
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886143"
---
# <a name="container-networking-overview"></a>コンテナー ネットワークの概要

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでされ提供いたしますネットワー キング スタックの概要 Windows コンテナーの作成、構成、およびコンテナーのネットワークの管理に関するその他のガイダンスへのリンクが含まれています。

Windows Server コンテナーは、軽量のオペレーティング システム仮想化の方法が、同じコンテナー ホスト上で実行される他のサービスからアプリケーションやサービスを分離します。 Windows コンテナーの機能は、仮想マシンと同じようにします。 有効な場合、各コンテナーはオペレーティング システム、プロセス、ファイル システム、レジストリ、および IP アドレスは、仮想ネットワークに接続できるは個別のビューには。 

Windows コンテナーは、コンテナー ホストとホストで実行されているすべてのコンテナーとカーネルを共有します。 これらのコンテナーはカーネルを共有しているため、カーネルのバージョンと構成を同一にする必要があります。 コンテナーは、プロセスと名前空間の分離テクノロジを使用してアプリケーションの分離を提供します。

>[!IMPORTANT]
>Windows コンテナーは、悪意のあるセキュリティの境界を指定しないと、信頼できないコードを分離する未使用する必要があります。 

Windows コンテナーでは、VM のホスト上の 1 つまたは複数の仮想マシンを作成する、HYPER-V ホストを展開できます。 VM のホスト内でコンテナーを作成し、ネットワーク アクセスは、仮想マシン内で実行されている仮想スイッチを介して。 リポジトリに格納されている再利用可能なイメージを使用すると、オペレーティング システムとサービスをコンテナーにデプロイします。 各コンテナーでは、受信および送信トラフィックを転送する、仮想ネットワーク アダプターを仮想スイッチに接続するには。 コンテナーのエンドポイントは、(NAT) などのローカル ホストのネットワークでは、物理ネットワークまたは SDN スタックを使って作成された仮想ネットワークをオーバーレイにアタッチできます。

同じホスト上のコンテナー間の分離を強制するには、Windows Server と HYPER-V コンテナーごとにネットワーク コンパートメントを作成します。 Windows Server コンテナーでは、仮想スイッチへの接続に Host vNIC を使用します。 HYPER-V コンテナーでは、仮想スイッチへの接続に (ユーティリティ VM には公開されていない) 統合 VM NIC を使用します。 

## <a name="related-topics"></a>関連トピック 

- [Windows コンテナーのネットワーク](https://docs.microsoft.com/virtualization/windowscontainers/container-networking/architecture):作成してコンテナー ネットワークのオーバーレイ/SDN の展開を管理する方法について説明します。

- [コンテナーのエンドポイントをテナントの仮想ネットワークに接続](../../manage/Connect-container-endpoints-to-a-Tenant-Virtual-Network.md):作成して sdn 仮想ネットワークのオーバーレイのコンテナー ネットワークを管理する方法について説明します。 