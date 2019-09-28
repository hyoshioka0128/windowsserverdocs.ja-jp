---
ms.assetid: ''
title: Windows Server 2019 の HPN 機能の Insider Preview
description: Windows Server 2019 の新しい高パフォーマンスネットワーク機能について説明します。
manager: dougkim
author: shortpatti
ms.author: pashort
ms.date: 09/12/2018
ms.topic: article
ms.prod: windows-server
ms.technology: networking
ms.openlocfilehash: 7098e81f486a5b0b4974c19b47e2d48c6f98832b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355364"
---
# <a name="insider-preview"></a>Insider Preview


## <a name="dynamic-vrss-and-vmmq"></a>動的な vRSS と VMMQ

>適用対象:Windows Server 2019

以前は、仮想マシンのキューと仮想マシンのマルチキューを使用すると、ネットワークスループットは最初に 10GbE mark 以降に到達したため、個々の Vm へのスループットが大幅に向上しました。 残念ながら、成功に必要な計画、基準、チューニング、および監視が大きな作業になりました。多くの場合、IT 管理者が使用することを想定しています。 

Windows Server 2019 では、必要に応じて、ネットワークワークロードの処理を動的に拡散およびチューニングすることで、これらの最適化が向上しています。 Windows Server 2019 では、ピーク時の効率が確保され、IT 管理者の構成の負荷が排除されます。

詳細については、以下をご覧ください。

-   [お知らせのブログ](https://blogs.technet.microsoft.com/networking/2018/08/22/netperf4vw/)

-   [IT プロフェッショナル向けの検証ガイド](https://aka.ms/DVMMQ-Validation)

## <a name="receive-segment-coalescing-rsc-in-the-vswitch"></a>vSwitch の Receive Segment Coalescing (RSC)

>適用対象:Windows Server 2019 および Windows 10 バージョン1809

VSwitch での受信セグメント結合 (RSC) は、データが vSwitch を走査する前に、複数の TCP セグメントを大きなセグメントに分割する拡張機能です。 大きなセグメントを使用すると、仮想ワークロードのネットワークパフォーマンスが向上します。

以前は、これは NIC によって実装されたオフロードでした。 残念ながら、アダプターを仮想スイッチに接続した瞬間は無効になりました。 Windows Server 2019 および Windows 10 10 月2018更新プログラムの vSwitch では、この制限が解除されます。

既定では、vSwitch の RSC は外部仮想スイッチで有効になっています。

詳細については、以下をご覧ください。

-  [お知らせのブログ](https://blogs.technet.microsoft.com/networking/2018/08/22/netperf4vw/)

-  [IT プロフェッショナル向けの検証ガイド](https://aka.ms/RSC-Validation)
