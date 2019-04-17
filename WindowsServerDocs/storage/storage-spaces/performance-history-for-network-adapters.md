---
title: ネットワーク アダプターのパフォーマンスの履歴
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
Keywords: Storage Spaces Direct
ms.localizationpriority: medium
ms.openlocfilehash: 340999a8f440975d3736277b1a30dddbb942785d
ms.sourcegitcommit: d31e266130b3b082372f7af4024e6089cb347d74
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/28/2018
ms.locfileid: "4239239"
---
# ネットワーク アダプターのパフォーマンスの履歴

> Windows Server Insider Preview の適用対象:

[記憶域スペース ダイレクトのパフォーマンスの履歴](performance-history.md)のサブこのトピックでは、ネットワーク アダプターのパフォーマンスの履歴を収集するために詳しく説明します。 ネットワーク アダプターのパフォーマンスの履歴はすべて物理ネットワーク アダプターで、クラスター内のすべてのサーバーで利用できます。 リモート ダイレクト メモリ アクセス (RDMA) のパフォーマンスの履歴は、RDMA 対応のすべての物理ネットワーク アダプター利用できます。

   > [!NOTE]
   > 下にあるサーバーのネットワーク アダプターのパフォーマンスの履歴を収集することはできません。 コレクションは、、サーバーが戻ってきた自動的に再開されます。

## 一連の名前と単位

これらの系列に対してすべての対象となるネットワーク アダプターが収集されます。

| シリーズ                               | Unit            |
|--------------------------------------|-----------------|
| `netadapter.bandwidth.inbound`       | 1 秒あたりのビット |
| `netadapter.bandwidth.outbound`      | 1 秒あたりのビット |
| `netadapter.bandwidth.total`         | 1 秒あたりのビット |
| `netadapter.bandwidth.rdma.inbound`  | 1 秒あたりのビット |
| `netadapter.bandwidth.rdma.outbound` | 1 秒あたりのビット |
| `netadapter.bandwidth.rdma.total`    | 1 秒あたりのビット |

   > [!NOTE]
   > ネットワーク アダプターのパフォーマンスの履歴は、1 秒あたりのバイトではなく、1 秒あたり**のビット**に記録されます。 1 つの 10 GbE ネットワーク アダプターが約 1,000,000, 000 ビットを送受信できる 125,000,000 バイト = 1.25 GB、理論上の最大で 1 秒あたりの = します。

## 解釈する方法

| シリーズ                               | 解釈する方法                                                      |
|--------------------------------------|-----------------------------------------------------------------------|
| `netadapter.bandwidth.inbound`       | ネットワーク アダプターで受信したデータの数です。                         |
| `netadapter.bandwidth.outbound`      | ネットワーク アダプターが送信されるデータの数です。                             |
| `netadapter.bandwidth.total`         | データの合計レートの受信またはネットワーク アダプターで送信します。           |
| `netadapter.bandwidth.rdma.inbound`  | ネットワーク アダプターで RDMA 経由で受信したデータの数です。               |
| `netadapter.bandwidth.rdma.outbound` | ネットワーク アダプターで RDMA 経由で送信されるデータの数です。                   |
| `netadapter.bandwidth.rdma.total`    | データの合計レートの受信またはネットワーク アダプターで RDMA 経由で送信します。 |

## どこから取得します。

`bytes.*`からシリーズを収集、`Network Adapter`ネットワーク アダプターがインストールされているサーバーの設定のパフォーマンス カウンター、ネットワーク アダプターあたり 1 つのインスタンスです。

| シリーズ                           | ソース カウンター           |
|----------------------------------|--------------------------|
| `netadapter.bandwidth.inbound`   | 8 × `Bytes Received/sec` |
| `netadapter.bandwidth.outbound`  | 8 × `Bytes Sent/sec`     |
| `netadapter.bandwidth.total`     | 8 × `Bytes Total/sec`    |

`rdma.*`からシリーズを収集、`RDMA Activity`ネットワーク アダプターがインストールされているサーバーの設定のパフォーマンス カウンターを有効になっている RDMA ネットワーク アダプターあたり 1 つのインスタンスです。

| シリーズ                               | ソース カウンター           |
|--------------------------------------|--------------------------|
| `netadapter.bandwidth.rdma.inbound`  | 8 × `Inbound bytes/sec`  |
| `netadapter.bandwidth.rdma.outbound` | 8 × `Outbound bytes/sec` |
| `netadapter.bandwidth.rdma.total`    | 8 ×*上記の合計*   |

   > [!NOTE]
   > カウンターは、サンプリングされたいない全体の間隔で測定されます。 たとえば、ネットワーク アダプターがアイドル状態 9 秒転送 200 ビットは 10 秒間、その`netadapter.bandwidth.total`この 10 秒間の平均 1 秒あたり 20 ビットとして記録されます。 これにより、パフォーマンスの履歴は、すべてのアクティビティをキャプチャでき、ノイズに堅牢です。

## PowerShell の使用状況

[Get-netadapter](https://docs.microsoft.com/powershell/module/netadapter/get-netadapter)コマンドレットを使用します。

```PowerShell
Get-NetAdapter <Name> | Get-ClusterPerf
```

## 関連項目

- [記憶域スペース ダイレクトのパフォーマンスの履歴](performance-history.md)
