---
title: ネットワーク関連のパフォーマンス カウンター
description: このトピックは、Windows Server 2016 のネットワーク サブシステムのパフォーマンス チューニング ガイドの一部です。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 7ebaa271-2557-4c24-a679-c3d863e6bf9e
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 33551dfd4f76bc13ba69863b782ddae279e0ad16
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="network-related-performance-counters"></a>ネットワーク関連のパフォーマンス カウンター

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、ネットワークのパフォーマンスの管理に関連して、次のセクションが含まれて カウンターを示します。  
  
-   [リソース使用率](#bkmk_ru)  
  
-   [潜在的なネットワークの問題](#bkmk_np)  
  
-   [受信側 Coalescing (RSC) のパフォーマンス](#bkmk_rsc)  
  
##  <a name="bkmk_ru"></a>リソース使用率  

次のパフォーマンス カウンターは、ネットワーク リソース使用率に関連します。  
  
-   IPv4、IPv6  
  
    -   データグラム受信パケット/秒  
  
    -   データグラム送信パケット/秒  
  
-   TCPv4、TCPv6  
  
    -   セグメントの受信パケット/秒  
  
    -   セグメント送信パケット/秒  
  
    -   再送信セグメントの数/秒  
  
-   ネットワークの Interface(*)、Adapter(\*) のネットワーク  
  
    -   Bytes received/sec  
  
    -   Bytes sent/sec  
  
    -   受信パケットの数/秒  
  
    -   送信パケットの数/秒  
  
    -   出力キューの長さ  
  
     このカウンタは、出力パケット キュー \(in packets\) の長さです。 これが 2 よりも長い場合は、遅延が発生します。 ボトルネックを見つけるし、可能な場合は、それを排除する必要があります。 NDIS 要求をキューに入れます、ためこの長さは 0 を常にする必要があります。  
  
-   プロセッサ情報  
  
    -   プロセッサ時間の割合  
  
    -   割り込み/秒  
  
    -   キューに入れられた Dpc の数/秒  
  
     このカウンタは、Dpc が論理プロセッサの DPC キューに追加される平均レートです。 論理プロセッサは、独自の DPC キュー。 このカウンタは、Dpc がキュー内の Dpc の数ではなく、キューに追加される速度を測定します。 最後の 2 つのサンプルでは、サンプリング間隔の時間で割った値で観察された値の差が表示されます。  
  
##  <a name="bkmk_np"></a>潜在的なネットワークの問題  

次のパフォーマンス カウンターは、潜在的なネットワークの問題に関連します。  
  
-   ネットワークの Interface(*)、Adapter(\*) のネットワーク  
  
    -   受信破棄されたパケット  
  
    -   パケットは受信エラー  
  
    -   破棄されたパケットの送信  
  
    -   パケットの送信エラー  
  
-   WFPv4、WFPv6  
  
    -   パケットは破棄/秒

-   を通じて、UDPv4、UDPv6

    -   データグラムの受信エラー  
  
-   TCPv4、TCPv6  
  
    -   接続エラー  
  
    -   接続のリセット  
  
-   ネットワーク QoS ポリシー  
  
    -   破棄されたパケット  
  
    -   破棄されたパケットの数/秒  
  
-   プロセッサのネットワーク インターフェイス カードのアクティビティごと  
  
    -   低リソース受信兆候/秒  
  
    -   リソース不足の受信パケット/秒  
  
-   Microsoft Winsock BSP  
  
    -   破棄されたデータグラム  
  
    -   破棄されたデータグラム/秒  
  
    -   拒否された接続  
  
    -   拒否された接続数/秒  
  
##  <a name="bkmk_rsc"></a>受信側 Coalescing (RSC) のパフォーマンス  

次のパフォーマンス カウンターは、RSC のパフォーマンスに関連します。  
  
-   ネットワーク Adapter(*)  
  
    -   TCP RSC がアクティブな接続  
  
    -   TCP RSC パケットの平均サイズ  
  
    -   TCP RSC に結合されたパケット数/秒  
  
    -   TCP RSC 例外/秒

このガイドのすべてのトピックへのリンクを参照してください。[ネットワーク サブシステムのパフォーマンス チューニング](net-sub-performance-top.md)します。