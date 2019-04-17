---
title: ネットワーク ワークロードに関するパフォーマンス ツール
description: このトピックは、Windows Server 2016 のネットワーク サブシステムのパフォーマンス チューニング ガイドの一部です。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: c7789781-87e8-464e-981b-af887d01badd
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 81c31871b3dfa4644690fe074ae15eaaa680d7f2
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="performance-tools-for-network-workloads"></a>ネットワーク ワークロードに関するパフォーマンス ツール

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックを使用すると、パフォーマンス ツールについて説明します。

このトピックには、サーバーのトラフィック ツール、TCP/IP ウィンドウ サイズ、および Microsoft Server Performance Advisor のクライアントに関するセクションが含まれています。

##  <a name="bkmk_tuning"></a>サーバーのトラフィックのツールをクライアント

サーバーのトラフィック \(ctsTraffic\) ツールに、クライアントは、作成し、ネットワーク トラフィックを検証する機能を提供します。

詳細については、およびツールをダウンロードするには、「[ctsTraffic (クライアントとサーバーのトラフィック)](http://ctstraffic.codeplex.com/)します。
  
##  <a name="bkmk_size"></a>TCP/IP のウィンドウのサイズ

1 GB のアダプターを前の表に示すように設定する必要があります提供の良好なスループット NTttcp 64 K に特定の論理プロセッサを既定の TCP ウィンドウ サイズを設定するためオプション \(SO_RCVBUF\) 接続します。 これは、低待機時間のネットワーク上で優れたパフォーマンスを提供します。  

これに対し、大規模なネットワークまたは 10 GB のアダプターでは、NTttcp の既定 TCP ウィンドウのサイズの値が得られます最適なパフォーマンスのよりも少ないリソースです。 どちらの場合も、大規模な帯域幅の遅延の製品の許可するように TCP ウィンドウ サイズを調整する必要があります。  

使用して、大きい値に TCP ウィンドウ サイズを設定できます静的に、**-rb**オプションです。 このオプションは、TCP ウィンドウの自動調整を無効にし、ユーザーについて十分に理解 TCP/IP の動作の結果として変更する場合にのみ使用することをお勧めします。 既定では、TCP ウィンドウのサイズが十分な値に設定されてし、または高待機時間リンク経由では、負荷を調整します。  

##  <a name="bkmk_advisor"></a>Microsoft Server Performance Advisor

Microsoft Server Performance Advisor \(SPA\) では、IT 管理者が識別、比較、および Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2、または Windows Server 2008 の展開で潜在的なパフォーマンスの問題の診断へのメトリックを収集することができます。 

SPA は包括的な診断レポートとグラフを生成し、すぐに始めるための推奨事項は、問題を分析し、是正措置を開発を提供します。  
  
 詳細については、および、アドバイザーをダウンロードするには、「[Microsoft Server Performance Advisor](https://msdn.microsoft.com/library/windows/hardware/dn481522.aspx) Windows ハードウェア デベロッパー センターでします。

このガイドのすべてのトピックへのリンクを参照してください。[ネットワーク サブシステムのパフォーマンス チューニング](net-sub-performance-top.md)します。