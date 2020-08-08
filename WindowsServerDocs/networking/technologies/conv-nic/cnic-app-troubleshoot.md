---
title: 収束 NIC 構成のトラブルシューティング
description: このトピックは、Windows Server 2016 用の収束 NIC 構成ガイドに含まれています。
ms.topic: article
ms.assetid: 0bc6746f-2adb-43d8-a503-52f473833164
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 7868861d33392e954b64064e3f748f742293b9af
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955839"
---
# <a name="troubleshooting-converged-nic-configurations"></a>収束 NIC 構成のトラブルシューティング

>適用先:Windows Server (半期チャネル)、Windows Server 2016

次のスクリプトを使用して、Hyper-v ホストで RDMA 構成が正しいかどうかを確認できます。

- [スクリプトのダウンロード Test-Rdma.ps1](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1)

また、次の Windows PowerShell コマンドを使用して、収束 Nic の構成をトラブルシューティングし、検証することもできます。

## <a name="get-netadapterrdma"></a>NetAdapterRdma

ネットワークアダプターの RDMA 構成を確認するには、Hyper-v サーバーで次の Windows PowerShell コマンドを実行します。

```powershell
Get-NetAdapterRdma | fl *
```

Hyper-v ホストでこのコマンドを実行した後、次の予期される結果と予期しない結果を使用して問題を特定し、解決することができます。

### <a name="get-netadapterrdma-expected-results"></a>NetAdapterRdma の予想される結果

ホスト vNIC と物理 NIC には、ゼロ以外の RDMA 機能が表示されます。

![Windows PowerShell の予期される結果](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-01.jpg)

### <a name="get-netadapterrdma-unexpected-results"></a>NetAdapterRdma の予期しない結果

**NetAdapterRdma**コマンドを実行したときに予期しない結果が表示される場合は、次の手順を実行します。

1. Mlnx ミニポートおよび Mlnx バスドライバーが最新であることを確認します。 Mellanox の場合は、少なくとも drop 42 を使用します。
2. デバイスマネージャーでドライバーのバージョンを確認して、Mlnx ミニポートとバスドライバーが一致することを確認します。 バスドライバーは、システムデバイスにあります。 ネットワークアダプターのプロパティの次のスクリーンショットに示すように、名前は Mellanox Connect-X 3 PRO VPI で始まる必要があります。

![ネットワーク アダプターのプロパティ](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-02.jpg)

4. 物理 NIC とホスト vNIC の両方でネットワークダイレクト (RDMA) が有効になっていることを確認します。
5. RDMA 機能をチェックして、適切な物理アダプターに vSwitch が作成されていることを確認します。
6. EventViewer システムログを確認し、ソース "Hyper-v-VmSwitch" でフィルター処理します。

## <a name="get-smbclientnetworkinterface"></a>SmbClientNetworkInterface

RDMA 構成を確認するための追加の手順として、Hyper-v サーバーで次の Windows PowerShell コマンドを実行します。

```powershell
Get-SmbClientNetworkInterface
```

### <a name="get-smbclientnetworkinterface-expected-results"></a>SmbClientNetworkInterface の予想される結果

ホスト vNIC は、SMB の観点からも RDMA 対応として表示されます。

![ネットワーク アダプターのプロパティ](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-03.jpg)

### <a name="get-smbclientnetworkinterface-unexpected-results"></a>SmbClientNetworkInterface の予期しない結果

1. Mlnx ミニポートおよび Mlnx バスドライバーが最新であることを確認します。 Mellanox の場合は、少なくとも drop 42 を使用します。
2. デバイスマネージャーでドライバーのバージョンを確認して、Mlnx ミニポートとバスドライバーが一致することを確認します。 バスドライバーは、システムデバイスにあります。 ネットワークアダプターのプロパティの次のスクリーンショットに示すように、名前は Mellanox Connect-X 3 PRO VPI で始まる必要があります。
3. 物理 NIC とホスト vNIC の両方でネットワークダイレクト (RDMA) が有効になっていることを確認します。
4. RDMA 機能をチェックして、適切な物理アダプターで Hyper-v 仮想スイッチが作成されていることを確認します。
5. アプリケーションとサービスの "SMB クライアント" の EventViewer ログを確認します。 **Microsoft |Windows**。

## <a name="get-netadapterqos"></a>Get-netadapterqos

\(次の Windows PowerShell コマンドを実行して、ネットワークアダプターのサービス品質 (QoS) 構成を表示でき \) ます。

```powershell
Get-NetAdapterQos
```

### <a name="get-netadapterqos-expected-results"></a>Get-netadapterqos の予想される結果

優先順位とトラフィッククラスは、このガイドを使用して実行した最初の構成手順に従って表示されます。

![サービスの品質の優先度とクラス](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-04.jpg)

### <a name="get-netadapterqos-unexpected-results"></a>Get-netadapterqos の予期しない結果

予期しない結果が発生した場合は、次の手順を実行します。

1. 物理ネットワークアダプターがデータセンターブリッジング \( DCB \) と QoS をサポートしていることを確認する
2. ネットワークアダプターのドライバーが最新であることを確認します。

## <a name="get-smbmultichannelconnection"></a>SmbMultiChannelConnection

次の Windows PowerShell コマンドを使用して、リモートノードの IP アドレスが RDMA に対応していることを確認でき \- ます。

```powershell
Get-SmbMultiChannelConnection
```

### <a name="get-smbmultichannelconnection-expected-results"></a>SmbMultiChannelConnection の予想される結果

リモートノードの IP アドレスは、RDMA 対応として表示されます。

![RDMA 対応リモートノード IP アドレス](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-05.jpg)

### <a name="get-smbmultichannelconnection-unexpected-results"></a>SmbMultiChannelConnection の予期しない結果

予期しない結果が発生した場合は、次の手順を実行します。

1. Ping が両方の方法で動作することを確認します。
2. ファイアウォールが SMB 接続の開始をブロックしていないことを確認します。 具体的には、iWARP の場合は SMB ダイレクトポート5445のファイアウォール規則を有効にし、ROCE の場合は445を有効にします。

## <a name="get-smbclientnetworkinterface"></a>SmbClientNetworkInterface

次のコマンドを使用して、RDMA に対して有効にした仮想 NIC が SMB で RDMA 対応として報告されていることを確認でき \- ます。

```powershell
Get-SmbClientNetworkInterface
```

### <a name="get-smbclientnetworkinterface-expected-results"></a>SmbClientNetworkInterface の予想される結果

RDMA に対して有効にされた仮想 NIC は、SMB で RDMA 対応として認識される必要があります。

![Nic が RDMA 対応であることを示す SMB レポート](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-06.jpg)

### <a name="get-smbclientnetworkinterface-unexpected-results"></a>SmbClientNetworkInterface の予期しない結果

予期しない結果が発生した場合は、次の手順を実行します。

1. Ping が両方の方法で動作することを確認します。
2. ファイアウォールが SMB 接続の開始をブロックしていないことを確認してください。

## <a name="vstat-mellanox-specific"></a>\(Mellanox 固有の vst\)

Mellanox ネットワークアダプターを使用している場合は、 **vstat**コマンドを使用して、hyper-v ノードでの RDMA Over 収束イーサネット \( roce バージョンを確認でき \) ます。

### <a name="vstat-expected-results"></a>期待される結果の vst

両方のノードの RoCE バージョンは同じである必要があります。 これは、両方のノードのファームウェアのバージョンが最新であることを確認するための良い方法でもあります。

![RoCE バージョンチェックの結果の例](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-07.jpg)

### <a name="vstat-unexpected-results"></a>vstat 予期しない結果)

予期しない結果が発生した場合は、次の手順を実行します。

1. MlnxDriverCoreSetting を使用して正しい RoCE バージョンを設定する
2. Mellanox web サイトから最新のファームウェアをインストールします。

## <a name="perfmon-counters"></a>Perfmon カウンター

パフォーマンスモニターのカウンターを確認して、構成の RDMA アクティビティを確認できます。

![パフォーマンスモニターの結果の例](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-08.jpg)

## <a name="related-topics"></a>関連トピック

- [単一のネットワークアダプターを使用した収束 NIC 構成](cnic-single.md)
- [収束 NIC チーミング NIC 構成](cnic-datacenter.md)
- [収束 NIC の物理スイッチ構成](cnic-app-switch-config.md)
