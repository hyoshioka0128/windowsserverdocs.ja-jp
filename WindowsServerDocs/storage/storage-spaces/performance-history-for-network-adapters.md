---
title: ネットワーク アダプターのパフォーマンス履歴
ms.author: cosdar
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 02/02/2018
Keywords: 記憶域スペース ダイレクト
ms.localizationpriority: medium
ms.openlocfilehash: 340999a8f440975d3736277b1a30dddbb942785d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849983"
---
# <a name="performance-history-for-network-adapters"></a>ネットワーク アダプターのパフォーマンス履歴

> 適用先:Windows Server Insider Preview

このサブ トピックの[記憶域スペース ダイレクトのパフォーマンスの履歴](performance-history.md)ネットワーク アダプター用に収集されたパフォーマンスの履歴の詳細について説明します。 ネットワーク アダプターのパフォーマンス履歴は、クラスター内のすべてのサーバーですべての物理ネットワーク アダプター使用できます。 リモート ダイレクト メモリ アクセス (RDMA) のパフォーマンス履歴は、RDMA 対応のすべての物理ネットワーク アダプター使用できます。

   > [!NOTE]
   > 停止しているサーバーのネットワーク アダプターのパフォーマンスの履歴を収集できません。 コレクションは、ときに、サーバーが復帰自動的に再開されます。

## <a name="series-names-and-units"></a>系列名とユニット

すべての対象となるネットワーク アダプターではこれらの系列が収集されます。

| シリーズ                               | Unit            |
|--------------------------------------|-----------------|
| `netadapter.bandwidth.inbound`       | 1 秒あたりのビット数 |
| `netadapter.bandwidth.outbound`      | 1 秒あたりのビット数 |
| `netadapter.bandwidth.total`         | 1 秒あたりのビット数 |
| `netadapter.bandwidth.rdma.inbound`  | 1 秒あたりのビット数 |
| `netadapter.bandwidth.rdma.outbound` | 1 秒あたりのビット数 |
| `netadapter.bandwidth.rdma.total`    | 1 秒あたりのビット数 |

   > [!NOTE]
   > ネットワーク アダプターのパフォーマンス履歴が記録された**ビット**1 秒間、1 秒あたりのバイトではありません。 1 つの 10 GbE ネットワーク アダプターが約 1,000,000, 000 ビットを送受信できる 125,000,000 バイト = 1.25 GB、理論上最大で 1 秒あたりの = です。

## <a name="how-to-interpret"></a>解釈する方法

| シリーズ                               | 解釈する方法                                                      |
|--------------------------------------|-----------------------------------------------------------------------|
| `netadapter.bandwidth.inbound`       | ネットワーク アダプターで受信したデータの比率。                         |
| `netadapter.bandwidth.outbound`      | ネットワーク アダプターから送信されたデータの比率。                             |
| `netadapter.bandwidth.total`         | 送受信ネットワーク アダプターから送信されたデータの合計の割合。           |
| `netadapter.bandwidth.rdma.inbound`  | Over RDMA ネットワーク アダプターで受信したデータの比率。               |
| `netadapter.bandwidth.rdma.outbound` | ネットワーク アダプターで RDMA 経由で送信されるデータの比率。                   |
| `netadapter.bandwidth.rdma.total`    | データの合計の割合の受信または over RDMA ネットワーク アダプターで送信します。 |

## <a name="where-they-come-from"></a>来た

`bytes.*`シリーズがから収集された、`Network Adapter`パフォーマンス カウンターのネットワーク アダプターがインストールされているサーバーの設定、ネットワーク アダプターごとに 1 つのインスタンス。

| シリーズ                           | ソースのカウンター           |
|----------------------------------|--------------------------|
| `netadapter.bandwidth.inbound`   | 8 × `Bytes Received/sec` |
| `netadapter.bandwidth.outbound`  | 8 × `Bytes Sent/sec`     |
| `netadapter.bandwidth.total`     | 8 × `Bytes Total/sec`    |

`rdma.*`シリーズがから収集された、`RDMA Activity`パフォーマンス カウンターのネットワーク アダプターがインストールされているサーバーの設定、RDMA 対応ネットワーク アダプターごとに 1 つのインスタンス。

| シリーズ                               | ソースのカウンター           |
|--------------------------------------|--------------------------|
| `netadapter.bandwidth.rdma.inbound`  | 8 × `Inbound bytes/sec`  |
| `netadapter.bandwidth.rdma.outbound` | 8 × `Outbound bytes/sec` |
| `netadapter.bandwidth.rdma.total`    | 8 ×*上記の合計*   |

   > [!NOTE]
   > カウンターは、サンプリングされなかった、全体の間隔で測定されます。 たとえば、ネットワーク アダプターがアイドル状態 9 秒ですが 200 の bits 転送の 10 日の 1 秒間、その`netadapter.bandwidth.total`この 10 秒間に平均で 1 秒あたりのビット数 20 として記録されます。 これにより、そのパフォーマンス履歴がすべてのアクティビティをキャプチャしがノイズに堅牢になりました。

## <a name="usage-in-powershell"></a>PowerShell での使用法

使用して、 [Get-netadapter](https://docs.microsoft.com/powershell/module/netadapter/get-netadapter)コマンドレット。

```PowerShell
Get-NetAdapter <Name> | Get-ClusterPerf
```

## <a name="see-also"></a>関連項目

- [記憶域スペース ダイレクトのパフォーマンスの履歴](performance-history.md)
