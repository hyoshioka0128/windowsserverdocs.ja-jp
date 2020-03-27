---
title: ネットワーク ワークロードに関するパフォーマンス ツール
description: このトピックは、Windows Server 2016 のネットワークサブシステムのパフォーマンスチューニングガイドに含まれています。
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: c7789781-87e8-464e-981b-af887d01badd
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 07/16/2018
ms.openlocfilehash: bcf179484718aa029302281ea91c99588ad2857a
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80316553"
---
# <a name="performance-tools-for-network-workloads"></a>ネットワーク ワークロードに関するパフォーマンス ツール

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、パフォーマンスツールについて説明します。

このトピックでは、クライアントとサーバー間のトラフィックツール、TCP/IP ウィンドウのサイズ、および Microsoft Server Performance Advisor について説明します。

##  <a name="client-to-server-traffic-tool"></a><a name="bkmk_tuning"></a>クライアントからサーバーへのトラフィックツール

クライアントとサーバー間のトラフィック \(Ctstrの\) ツールを使用すると、ネットワークトラフィックを作成および検証することができます。

詳細については、ツールをダウンロードするには、「 [ctc (クライアントとサーバー間のトラフィック)](https://github.com/Microsoft/ctsTraffic)」を参照してください。
  
##  <a name="tcpip-window-size"></a><a name="bkmk_size"></a>TCP/IP ウィンドウのサイズ

1 GB のアダプターの場合は、前の表に示した設定で最適なスループットが得られます。 NTttcp では、接続の\) SO_RCVBUF \(特定の論理プロセッサオプションを使用して、既定の TCP ウィンドウサイズが 64 K に設定されるためです。 これにより、待機時間の短いネットワークで優れたパフォーマンスが得られます。  

これに対し、待機時間の長いネットワークまたは 10 GB のアダプターの場合、NTttcp の既定の TCP ウィンドウサイズの値によって、最適なパフォーマンスが得られません。 どちらの場合も、帯域幅の遅延が大きくなるように、TCP ウィンドウのサイズを調整する必要があります。  

**-Rb**オプションを使用すると、TCP ウィンドウサイズを大きな値に静的に設定できます。 このオプションを選択すると、TCP ウィンドウ自動調整が無効になります。ユーザーが TCP/IP 動作の結果変更を完全に理解している場合にのみ、このオプションを使用することをお勧めします。 既定では、TCP ウィンドウのサイズは十分な値で設定され、負荷が高い場合、または待機時間の長いリンクの場合にのみ調整されます。  

##  <a name="microsoft-server-performance-advisor"></a><a name="bkmk_advisor"></a>Microsoft Server Performance Advisor

Microsoft Server Performance Advisor \(SPA\) を使用すると、IT 管理者は Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、または Windows Server 2008 の展開で発生する可能性のあるパフォーマンスの問題を特定、比較、診断するためのメトリックを収集できます。 

SPA は、包括的な診断レポートとグラフを生成します。また、問題を迅速に分析し、是正措置を開発するために役立つ推奨事項を提供します。  
  
 Advisor の詳細とダウンロードについては、Windows ハードウェアデベロッパーセンターの「 [Microsoft Server Performance advisor](https://msdn.microsoft.com/library/windows/hardware/dn481522.aspx) 」を参照してください。

このガイドのすべてのトピックへのリンクについては、「[ネットワークサブシステムのパフォーマンスチューニング](net-sub-performance-top.md)」を参照してください。