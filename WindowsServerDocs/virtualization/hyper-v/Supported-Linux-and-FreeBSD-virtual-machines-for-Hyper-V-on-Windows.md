---
title: Windows にインストールされた Hyper-v の Linux および FreeBSD 仮想マシンがサポートされています。
description: 各バージョンに含まれる Linux integration services と機能の一覧を示します。
manager: dongill
ms.topic: article
ms.assetid: 990ff94a-30fb-434b-b4a2-3804a5245ba6
author: shirgall
ms.author: kathydav
ms.date: 10/03/2016
ms.openlocfilehash: 3c971b3b802f1059454bc8935b638ddcc10c825c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87965629"
---
# <a name="supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows"></a>Windows にインストールされた Hyper-v の Linux および FreeBSD 仮想マシンがサポートされています。

>適用対象: Windows Server 2019、Windows Server 2016、Hyper-v Server 2016、Windows Server 2012 R2、Hyper-v Server 2012 R2、Windows Server 2012、Hyper-v Server 2012、Windows Server 2008 R2、Windows 10、Windows 8.1、Windows 8、Windows 7.1、Windows 7。

HYPER-V では、Linux および FreeBSD の仮想マシンのエミュレートされたとハイパー V 固有の両方のデバイスをサポートします。 エミュレートされたデバイスを実行すると追加のソフトウェアをインストールする必要はありません。 ただしエミュレートされたデバイスは、高パフォーマンスを提供せず、HYPER-V テクノロジを提供する豊富な仮想マシンの管理インフラストラクチャを活用することはできません。 HYPER-V が提供するすべての利点を最大限に活用するために、Linux および FreeBSD のハイパー V 固有のデバイスを使用することをお勧めします。 ハイパースレッディング固有のデバイスを実行するために必要なドライバーのコレクションは、Linux Integration Services (LIS) または FreeBSD Integration Services (BIS) と呼ばれます。

LIS は Linux カーネルに追加されているされ、新しいリリースの更新されます。 以前のカーネルに基づく Linux ディストリビューションは、最新の機能強化または修正プログラムがない可能性が。 Microsoft では、これらの古いカーネルに基づいていくつか Linux のインストールのインストール可能なの LIS ドライバーが含まれるダウンロードを提供します。 配布のベンダーでは、Linux Integration Services のバージョンが含まれる、ため、必要に応じて、インストール、LIS のダウンロード可能な最新のバージョンをインストールすることをお勧めします。

他の Linux ディストリビューション LIS は個別のダウンロードやインストールは必要ありませんので変更をオペレーティング システムのカーネルおよびアプリケーションに統合されます定期的にします。

(10.0) の前に古い FreeBSD リリースには、マイクロソフトは、インストール可能な BIS ドライバーおよび FreeBSD の仮想マシンの対応するデーモンが含まれているポートを提供します。 それ以降の FreeBSD リリースの BIS、FreeBSD オペレーティング システムに組み込まれて、個別のダウンロードやインストールは FreeBSD 10.0 に必要な KVP ポート ダウンロード以外は必要ありません。

> [!TIP]
> - 評価センターから[Windows Server 2019](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019)をダウンロードします。

このコンテンツの目的は、情報が役立ちますが、HYPER-V 上の Linux または FreeBSD 展開を容易にするためです。 特定の詳細は次のとおりです。

* Linux ディストリビューションまたは FreeBSD のリリースをダウンロードし、LIS または BIS ドライバーのインストールを必要とします。

* Linux ディストリビューションまたは組み込みの LIS または BIS ドライバーを含む FreeBSD リリースします。

* 主要な Linux ディストリビューションまたは FreeBSD のリリースで機能を示す機能配布マップします。

* 既知の問題と回避策の各配布またはリリースします。

* LIS または BIS 機能ごとに機能の説明。

**特徴および機能に関する提案を送信する場合は、** 適切か何かはありますか。 [Windows Server User Voice](https://windowsserver.uservoice.com/forums/295062-linux-support)サイトを使用して、hyper-v 上の Linux および FreeBSD Virtual Machines の新機能を提案したり、他のユーザーの意見を確認したりすることができます。

## <a name="in-this-section"></a>このセクションの内容

* [CentOS をサポートし、HYPER-V 上の Red Hat Enterprise Linux 仮想マシン](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [Debian の仮想マシンを HYPER-V でサポートされています。](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [HYPER-V でサポートされている Oracle Linux 仮想マシン](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [HYPER-V でサポートされている SUSE 仮想マシン](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [HYPER-V でサポートされている Ubuntu 仮想マシン](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [HYPER-V でサポートされている FreeBSD 仮想マシン](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Hyper-v 上の Linux および FreeBSD 仮想マシンの機能の説明](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [HYPER-V で Linux を実行するためのベスト プラクティス](Best-Practices-for-running-Linux-on-Hyper-V.md)

* [HYPER-V での FreeBSD の実行に関するベスト プラクティス](Best-practices-for-running-FreeBSD-on-Hyper-V.md)
