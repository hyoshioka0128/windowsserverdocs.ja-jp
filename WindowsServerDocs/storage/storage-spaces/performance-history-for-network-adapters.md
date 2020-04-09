---
title: ネットワークアダプターのパフォーマンス履歴
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: e2379ce540cb26c02bc79f591d2a597874ab287c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856215"
---
# <a name="performance-history-for-network-adapters"></a>ネットワークアダプターのパフォーマンス履歴

> 適用対象: Windows Server 2019

[記憶域スペースダイレクトのパフォーマンス履歴](performance-history.md)のこのサブトピックでは、ネットワークアダプターについて収集されるパフォーマンス履歴の詳細について説明します。 ネットワークアダプターのパフォーマンス履歴は、クラスター内のすべてのサーバーのすべての物理ネットワークアダプターで使用できます。 リモートダイレクトメモリアクセス (RDMA) のパフォーマンス履歴は、RDMA が有効になっているすべての物理ネットワークアダプターで使用できます。

   > [!NOTE]
   > ダウンしているサーバーのネットワークアダプターのパフォーマンス履歴を収集することはできません。 コレクションは、サーバーが復帰すると自動的に再開されます。

## <a name="series-names-and-units"></a>系列の名前と単位

これらのシリーズは、対象となるすべてのネットワークアダプターについて収集されます。

| 系列                               | Unit            |
|--------------------------------------|-----------------|
| `netadapter.bandwidth.inbound`       | 1秒あたりのビット数 |
| `netadapter.bandwidth.outbound`      | 1秒あたりのビット数 |
| `netadapter.bandwidth.total`         | 1秒あたりのビット数 |
| `netadapter.bandwidth.rdma.inbound`  | 1秒あたりのビット数 |
| `netadapter.bandwidth.rdma.outbound` | 1秒あたりのビット数 |
| `netadapter.bandwidth.rdma.total`    | 1秒あたりのビット数 |

   > [!NOTE]
   > ネットワークアダプターのパフォーマンス履歴は、1秒あたりのバイト数ではなく、**ビット**単位で記録されます。 1 10 GbE ネットワークアダプターは、理論的に最大で約10億ビット = 1億2500万バイト = 1.25 GB/秒を送受信できます。

## <a name="how-to-interpret"></a>解釈する方法

| 系列                               | 解釈する方法                                                      |
|--------------------------------------|-----------------------------------------------------------------------|
| `netadapter.bandwidth.inbound`       | ネットワークアダプターによって受信されたデータの比率。                         |
| `netadapter.bandwidth.outbound`      | ネットワークアダプターによって送信されたデータの比率。                             |
| `netadapter.bandwidth.total`         | ネットワークアダプターによって受信または送信されたデータの合計速度。           |
| `netadapter.bandwidth.rdma.inbound`  | ネットワークアダプターが RDMA 経由で受信したデータの比率。               |
| `netadapter.bandwidth.rdma.outbound` | ネットワークアダプターによって RDMA 経由で送信されたデータの比率。                   |
| `netadapter.bandwidth.rdma.total`    | ネットワークアダプターによって RDMA 経由で送受信されたデータの合計速度。 |

## <a name="where-they-come-from"></a>どこから来ているか

`bytes.*` シリーズは、ネットワークアダプターがインストールされているサーバーの `Network Adapter` パフォーマンスカウンターセット (ネットワークアダプターごとに1つのインスタンス) から収集されます。

| 系列                           | ソースカウンター           |
|----------------------------------|--------------------------|
| `netadapter.bandwidth.inbound`   | 8× `Bytes Received/sec` |
| `netadapter.bandwidth.outbound`  | 8× `Bytes Sent/sec`     |
| `netadapter.bandwidth.total`     | 8× `Bytes Total/sec`    |

`rdma.*` シリーズは、ネットワークアダプターがインストールされているサーバーの `RDMA Activity` パフォーマンスカウンターセットから収集されます。これは、RDMA が有効になっているネットワークアダプターごとに1つのインスタンスです。

| 系列                               | ソースカウンター           |
|--------------------------------------|--------------------------|
| `netadapter.bandwidth.rdma.inbound`  | 8× `Inbound bytes/sec`  |
| `netadapter.bandwidth.rdma.outbound` | 8× `Outbound bytes/sec` |
| `netadapter.bandwidth.rdma.total`    | *上記の8倍の合計*   |

   > [!NOTE]
   > カウンターは、サンプリングされるのではなく、間隔全体にわたって測定されます。 たとえば、ネットワークアダプターが9秒間アイドル状態で200ビットを10秒間転送する場合、その `netadapter.bandwidth.total` は、この10秒間に平均で1秒あたり20ビットとして記録されます。 これにより、パフォーマンス履歴がすべてのアクティビティをキャプチャし、ノイズに対して堅牢になります。

## <a name="usage-in-powershell"></a>PowerShell での使用法

[Get NetAdapter](https://docs.microsoft.com/powershell/module/netadapter/get-netadapter)コマンドレットを使用します。

```PowerShell
Get-NetAdapter <Name> | Get-ClusterPerf
```

## <a name="see-also"></a>参照

- [記憶域スペースダイレクトのパフォーマンス履歴](performance-history.md)
