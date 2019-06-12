---
title: ネットワーク関連のパフォーマンス カウンター
description: このトピックでは、Windows Server 2016 は、ネットワーク サブシステムのパフォーマンス チューニング ガイドの一部です。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 7ebaa271-2557-4c24-a679-c3d863e6bf9e
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bcb0c1c5a08a306fbd9b419d0c458c3bc54e1786
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446207"
---
# <a name="network-related-performance-counters"></a>ネットワーク関連のパフォーマンス カウンター

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、ネットワークのパフォーマンスの管理に関連して、次のセクションが含まれて カウンターを使用します。  
  
-   [リソース使用率](#bkmk_ru)  
  
-   [潜在的なネットワークの問題](#bkmk_np)  
  
-   [受信側 Coalescing (RSC) のパフォーマンス](#bkmk_rsc)  
  
##  <a name="bkmk_ru"></a> リソース使用率  

次のパフォーマンス カウンターは、ネットワーク リソースの使用率に関連します。  
  
- IPv4、IPv6  
  
  -   データグラムの受信/秒  
  
  -   データグラムの送信/秒  
  
- TCPv4, TCPv6  
  
  -   セグメントの受信/秒  
  
  -   セグメントの送信/秒  
  
  -   セグメントの再送信/秒  
  
- Network Interface(*), Network Adapter(\*)  
  
  - 受信バイト数/秒  
  
  - 送信バイト数/秒  
  
  - パケットの受信/秒  
  
  - パケットの送信/秒  
  
  - 出力キューの長さ  
  
    このカウンターは、出力パケット キューの長さ\(パケット\)します。 これが 2 より長い場合は、遅延が発生します。 ボトルネックを見つけるし、可能な場合は、排除する必要があります。 NDIS は、要求をキューであるために、この長さは 0 を必ずします。  
  
- プロセッサ情報  
  
  - [% プロセッサ時間]  
  
  - 割り込み/秒  
  
  - DPCs Queued/sec  
  
    このカウンターは、位置、Dpc が論理プロセッサの DPC キューに追加された、平均レートです。 各論理プロセッサには、独自の DPC キューがあります。 このカウンターは、Dpc は、キュー内の Dpc の数ではなく、キューに追加される割合を測定します。 最後の 2 つのサンプルでは、サンプル間隔の時間で割った値で検出された値の差が表示されます。  
  
##  <a name="bkmk_np"></a> 潜在的なネットワークの問題  

次のパフォーマンス カウンターは、潜在的なネットワークの問題に関連します。  
  
-   Network Interface(*), Network Adapter(\*)  
  
    -   破棄された受信パケット数  
  
    -   パケットの受信エラー  
  
    -   破棄されたパケットの送信  
  
    -   パケットの送信エラー  
  
-   WFPv4、WFPv6  
  
    -   パケットの破棄/秒

-   を通じて、UDPv4、UDPv6

    -   Datagrams Received エラー  
  
-   TCPv4, TCPv6  
  
    -   接続エラー  
  
    -   接続のリセット  
  
-   ネットワーク QoS ポリシー  
  
    -   破棄されたパケット  
  
    -   パケットの破棄/秒  
  
-   Processor Network Interface Card Activity ごと  
  
    -   低リソースがない/秒を受信します。  
  
    -   低リソース受信パケット/秒  
  
-   Microsoft Winsock BSP  
  
    -   ドロップされたデータグラム  
  
    -   1 秒あたりの破棄されたデータグラム  
  
    -   Rejected Connections  
  
    -   1 秒あたりに拒否された接続  
  
##  <a name="bkmk_rsc"></a> 受信側 Coalescing (RSC) のパフォーマンス  

次のパフォーマンス カウンターは、RSC のパフォーマンスに関連します。  
  
-   ネットワーク Adapter(*)  
  
    -   アクティブな RSC の TCP 接続  
  
    -   TCP RSC パケットの平均サイズ  
  
    -   TCP RSC パケット/秒の結合  
  
    -   TCP RSC Exceptions/sec

このガイドのすべてのトピックへのリンクを参照してください。[ネットワーク サブシステムのパフォーマンス チューニング](net-sub-performance-top.md)します。