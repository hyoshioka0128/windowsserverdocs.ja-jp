---
ms.assetid: ''
title: Windows Server 2019 HPN 機能の insider Preview
description: Windows Server 2019 で高パフォーマンスのネットワークの新機能について説明します。
manager: dougkim
author: shortpatti
ms.author: pashort
ms.date: 09/12/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: 3d3e974472f28c30d093fbd1094ef3693d984d19
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886273"
---
# <a name="insider-preview"></a>Insider Preview


## <a name="dynamic-vrss-and-vmmq"></a>動的 vRSS と VMMQ

>適用対象:Windows Server 2019

以前は、仮想マシン キュー、および仮想マシンの複数キュー有効になっている個々 の Vm に高いスループットが著しく以降としてネットワーク スループットの最初の 10 gbe のマークに到達します。 残念ながら、計画、ベースライン設定で、チューニング、および監視に必要な成功なりましたは大規模な作業でした。多くの場合、IT 管理者以上の使用権をプレゼントもの。 

Windows Server 2019 は、動的に分散することと、必要に応じてネットワーク ワークロードの処理をチューニングしてこれらの最適化を向上します。 Windows Server 2019 では、により、効率を最大化し、IT 管理者の構成の負担を削除します。

詳しくは、次のトピックをご覧ください。

-   [発表に関するブログ](https://blogs.technet.microsoft.com/networking/2018/08/22/netperf4vw/)

-   [IT 向けの検証ガイド Pro](https://aka.ms/DVMMQ-Validation)

## <a name="receive-segment-coalescing-rsc-in-the-vswitch"></a>vSwitch の Receive Segment Coalescing (RSC)

>適用対象:Windows Server 2019 および Windows 10、バージョンは 1809

受信セグメント Coalescing (RSC)、vSwitch では、拡張機能データ、vSwitch を走査する前に大きなセグメントに複数の TCP セグメントの連結です。 大規模なセグメントでは、仮想ワークロード用のネットワークのパフォーマンスが向上します。

NIC によって実装されるオフロードは、これは以前は、 残念ながら、これは、アダプターを仮想スイッチに接続した時点を無効にされました。 Windows Server 2019 および Windows 上の vSwitch で RSC 10 年 2018年 10 月の更新がこの制限を削除します。

外部仮想スイッチでは既定では、vSwitch で RSC が有効にします。

詳しくは、次のトピックをご覧ください。

-  [発表に関するブログ](https://blogs.technet.microsoft.com/networking/2018/08/22/netperf4vw/)

-  [IT 向けの検証ガイド Pro](https://aka.ms/RSC-Validation)
