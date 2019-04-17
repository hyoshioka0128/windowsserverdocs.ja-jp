---
title: コンテナー ネットワークの概要
description: このトピックでは、Windows コンテナーのネットワー キング スタックの概要を説明し、作成、構成、およびコンテナーのネットワークの管理についての追加情報へのリンクが含まれています。
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
ms.openlocfilehash: fd2f022948208d4aacce2994ff053e77384b28fc
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="container-networking-overview"></a>コンテナー ネットワークの概要

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Windows コンテナーのネットワー キング スタックの概要を説明し、作成、構成、およびコンテナーのネットワークの管理についての追加情報へのリンクが含まれています。

Windows Server コンテナーは、軽量のオペレーティング システム仮想化の方法が、同じコンテナー ホストで実行されているその他のサービスからのアプリケーションまたはサービスを分離するために使用します。 これを有効にするのには、それぞれのコンテナーは、オペレーティング システム、プロセス、ファイル システム、レジストリ、および IP アドレスの独自のビューがします。

Windows コンテナーの機能はネットワークに関して言えば内の仮想マシンと同じようにします。 各コンテナーは、受信と送信トラフィックを転送する、仮想スイッチに接続されている仮想ネットワーク アダプターを持ちます。 同じホスト上のコンテナー間の分離を強制するには、各 Windows Server と HYPER-V コンテナーをコンテナーのネットワーク アダプターがインストールされているネットワーク コンパートメントが作成されます。 Windows Server のコンテナーでは、ホスト vNIC を使用して、仮想スイッチに接続します。 HYPER-V コンテナーは、(ユーティリティ VM に公開されません) 統合 VM NIC を使用して、仮想スイッチに接続します。 

コンテナーのエンドポイントは、ローカル ホストのネットワーク (例: NAT)、物理ネットワーク、または、Microsoft ソフトウェアによるネットワーク制御 (SDN) スタックによって作成されたオーバーレイの仮想ネットワークに接続することができます。 

作成とオーバーレイ/SDN 以外の場合のコンテナー ネットワークを管理する方法の詳細についてを参照してください、 [Windows コンテナーのネットワーク](https://msdn.microsoft.com/en-us/virtualization/windowscontainers/management/container_networking)ガイド (msdn)。

作成と SDN とオーバーレイの仮想ネットワークのコンテナー ネットワークを管理する方法の詳細についてを参照してください[コンテナー エンドポイントをテナントの仮想ネットワークに接続](../../manage/Connect-container-endpoints-to-a-Tenant-Virtual-Network.md)します。 