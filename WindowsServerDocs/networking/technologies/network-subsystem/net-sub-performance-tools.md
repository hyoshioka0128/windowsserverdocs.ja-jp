---
title: ネットワーク ワークロードに関するパフォーマンス ツール
description: このトピックでは、Windows Server 2016 は、ネットワーク サブシステムのパフォーマンス チューニング ガイドの一部です。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: c7789781-87e8-464e-981b-af887d01badd
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 07/16/2018
ms.openlocfilehash: e71c5f34041145907c30b279dc91a94c03c2abed
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59824933"
---
# <a name="performance-tools-for-network-workloads"></a>ネットワーク ワークロードに関するパフォーマンス ツール

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックを使用すると、パフォーマンス ツールについて説明します。

このトピックには、クライアント サーバー トラフィック ツール、TCP/IP ウィンドウのサイズ、および Microsoft Server Performance Advisor に関するセクションが含まれています。

##  <a name="bkmk_tuning"></a> クライアント サーバー トラフィック ツールに

クライアント サーバー トラフィックを\(ctsTraffic\)ツールを作成し、ネットワーク トラフィックを確認する機能を提供します。

詳細については、およびツールをダウンロードするには、「 [ctsTraffic (クライアントからサーバーへのトラフィック)](https://github.com/Microsoft/ctsTraffic)します。
  
##  <a name="bkmk_size"></a> TCP/IP のウィンドウのサイズ

1 GB アダプターの場合、前の表に示すように設定する必要があります提供に十分なスループット NTttcp 64 K に特定の論理プロセッサ オプションを使用して既定の TCP ウィンドウ サイズを設定するため\(SO_RCVBUF\)接続します。 これは、待機時間の短いネットワーク上で良好なパフォーマンスを提供します。  

これに対し、待機時間の長いネットワークまたは 10 GB アダプターでは、NTttcp の既定の TCP ウィンドウ サイズ値が最適なパフォーマンスをより小さい生成されます。 どちらの場合も、大規模な帯域幅遅延積を許可する TCP ウィンドウ サイズを調整する必要があります。  

使用して TCP ウィンドウ サイズを大きい値に静的に設定することができます、 **-rb**オプション。 TCP ウィンドウ自動チューニングにより、このオプションを無効にし、ユーザーが完全に TCP/IP 動作の結果の変更を認識する場合にのみ使用することをお勧めします。 します。 既定は、TCP ウィンドウ サイズは、十分な値に設定し、負荷の下でのみ、または待機時間の長いリンクでを調整します。  

##  <a name="bkmk_advisor"></a> Microsoft Server Performance Advisor

Microsoft Server Performance Advisor \(SPA\) IT 管理者は、識別するためにメトリックを収集することは、比較、および Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows での潜在的なパフォーマンス問題を診断Server 2008 R2、または Windows Server 2008 の展開。 

SPA は包括的な診断レポートとグラフを生成し、すぐに始めるための推奨事項は、問題を分析し、是正措置を開発を提供します。  
  
 詳細については、および、アドバイザーをダウンロードするには、「 [Microsoft Server Performance Advisor](https://msdn.microsoft.com/library/windows/hardware/dn481522.aspx) Windows ハードウェア デベロッパー センターでします。

このガイドのすべてのトピックへのリンクを参照してください。[ネットワーク サブシステムのパフォーマンス チューニング](net-sub-performance-top.md)します。