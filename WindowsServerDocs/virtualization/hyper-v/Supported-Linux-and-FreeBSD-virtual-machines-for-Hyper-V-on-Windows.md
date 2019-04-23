---
title: Windows にインストールされた Hyper-v の Linux および FreeBSD 仮想マシンがサポートされています。
description: Linux integration services オブジェクトと各バージョンに含まれる機能を一覧表示します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 990ff94a-30fb-434b-b4a2-3804a5245ba6
author: shirgall
ms.author: kathydav
ms.date: 10/03/2016
ms.openlocfilehash: 9df495bdc67b06a675fec050fb4c2960337ce8ca
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832903"
---
# <a name="supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows"></a>Windows にインストールされた Hyper-v の Linux および FreeBSD 仮想マシンがサポートされています。

>適用先:Windows Server 2016、Hyper V Server 2016、Windows Server 2012 R2、Hyper-V Server 2012 R2、Windows Server 2012、Hyper-V Server 2012、Windows Server 2008 R2、Windows 10、Windows 8.1、Windows 8、Windows 7.1、Windows 7

HYPER-V では、Linux および FreeBSD の仮想マシンのエミュレートされたとハイパー V 固有の両方のデバイスをサポートします。 エミュレートされたデバイスを実行すると追加のソフトウェアをインストールする必要はありません。 ただしエミュレートされたデバイスは、高パフォーマンスを提供せず、HYPER-V テクノロジを提供する豊富な仮想マシンの管理インフラストラクチャを活用することはできません。 HYPER-V が提供するすべての利点を最大限に活用するために、Linux および FreeBSD のハイパー V 固有のデバイスを使用することをお勧めします。 ハイパースレッディング固有のデバイスを実行するために必要なドライバーのコレクションは、Linux Integration Services (LIS) または FreeBSD Integration Services (BIS) と呼ばれます。

LIS は Linux カーネルに追加されているされ、新しいリリースの更新されます。 以前のカーネルに基づく Linux ディストリビューションは、最新の機能強化または修正プログラムがない可能性が。 Microsoft では、これらの古いカーネルに基づいていくつか Linux のインストールのインストール可能なの LIS ドライバーが含まれるダウンロードを提供します。 配布のベンダーでは、Linux Integration Services のバージョンが含まれる、ため、必要に応じて、インストール、LIS のダウンロード可能な最新のバージョンをインストールすることをお勧めします。

他の Linux ディストリビューション LIS は個別のダウンロードやインストールは必要ありませんので変更をオペレーティング システムのカーネルおよびアプリケーションに統合されます定期的にします。

(10.0) の前に古い FreeBSD リリースには、マイクロソフトは、インストール可能な BIS ドライバーおよび FreeBSD の仮想マシンの対応するデーモンが含まれているポートを提供します。 それ以降の FreeBSD リリースの BIS、FreeBSD オペレーティング システムに組み込まれて、個別のダウンロードやインストールは FreeBSD 10.0 に必要な KVP ポート ダウンロード以外は必要ありません。

> [!TIP]
> - ダウンロード [Windows Server 2016](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016) Evaluation Center からです。
> - ダウンロード[Microsoft HYPER-V Server 2016](https://www.microsoft.com/evalcenter/evaluate-hyper-v-server-2016) Evaluation Center からです。

このコンテンツの目的は、情報が役立ちますが、HYPER-V 上の Linux または FreeBSD 展開を容易にするためです。 特定の詳細は次のとおりです。

* Linux ディストリビューションまたは FreeBSD のリリースをダウンロードし、LIS または BIS ドライバーのインストールを必要とします。

* Linux ディストリビューションまたは組み込みの LIS または BIS ドライバーを含む FreeBSD リリースします。

* 主要な Linux ディストリビューションまたは FreeBSD のリリースで機能を示す機能配布マップします。

* 既知の問題と回避策の各配布またはリリースします。

* LIS または BIS 機能ごとに機能の説明。

**特徴および機能に関する提案を送信しますか。** 適切か何かはありますか。 使用することができます、 [Windows Server の User Voice](https://windowsserver.uservoice.com/forums/295062-linux-support)サイト Linux と FreeBSD 仮想マシン、HYPER-V の新機能と機能を提案および他のユーザーの声を参照してください。

## <a name="in-this-section"></a>このセクションの内容

* [CentOS をサポートし、HYPER-V 上の Red Hat Enterprise Linux 仮想マシン](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)

* [HYPER-V でサポートされている Debian の仮想マシン](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [HYPER-V でサポートされている Oracle Linux 仮想マシン](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Hyper-v のサポートされている SUSE 仮想マシン](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Ubuntu 仮想マシンの HYPER-V でサポートされています。](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Hyper-v のサポートされている FreeBSD 仮想マシン](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [HYPER-V で Linux および FreeBSD の仮想マシンの機能の説明](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [HYPER-V で Linux を実行するためのベスト プラクティス](Best-Practices-for-running-Linux-on-Hyper-V.md)

* [HYPER-V で FreeBSD を実行するためのベスト プラクティス](Best-practices-for-running-FreeBSD-on-Hyper-V.md)
