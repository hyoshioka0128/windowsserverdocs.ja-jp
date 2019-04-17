---
title: 集約型の NIC 構成のトラブルシューティング
description: このトピックでは、集約型の NIC 構成ガイドの Windows Server 2016 の一部です。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0bc6746f-2adb-43d8-a503-52f473833164
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 373ecd9b9fff62aaabd8caa176ff091ec98ad81c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="troubleshooting-converged-nic-configurations"></a>集約型の NIC 構成のトラブルシューティング

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

RDMA 構成が Hyper-V ホスト上で正しいかどうかを確認するのには、次のスクリプトを使用できます。

- [スクリプト Test-Rdma .ps1 をダウンロードします。](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1)

次の Windows PowerShell コマンドを使用して、トラブルシューティングを実行し、コンバージド Nic の構成を確認するもことができます。

## <a name="get-netadapterrdma"></a>Get-NetAdapterRdma

ネットワーク アダプターの RDMA 構成を確認するには、Hyper-V サーバー上で、次の Windows PowerShell コマンドを実行します。

    
    Get-NetAdapterRdma | fl *
    

下記の期待と予期しない結果を使用するには、識別し、Hyper-V ホスト上でこのコマンドを実行した後、問題を解決します。

### <a name="get-netadapterrdma-expected-results"></a>予想される結果を Get-NetAdapterRdma

ホスト vNIC と物理 NIC は、0 以外の RDMA 機能を示しています。

![Windows PowerShell が期待どおりの結果](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-01.jpg)

### <a name="get-netadapterrdma-unexpected-results"></a>Get-NetAdapterRdma 予期しない結果

実行するときに予期しない結果を受け取った場合は、次の手順を実行、**Get NetAdapterRdma**コマンド。

1. Mlnx ミニポートと Mlnx バス ドライバーが最新であることを確認してください。 Mellanox、使用するには、42 少なくともドロップします。 
2. デバイス マネージャーを使ってドライバーのバージョンをチェックして Mlnx ミニポートとバス ドライバーと一致していることを確認します。 [システム デバイスは、バス ドライバーを検索できます。 名前を開始 Mellanox Connect-X 3 PRO VPI、ネットワーク アダプターのプロパティのスクリーン ショットを次に示すようにします。

![ネットワーク アダプターのプロパティ](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-02.jpg)

4. 物理 NIC とホスト vNIC の両方で、ネットワーク ダイレクト (RDMA) を有効にすることを確認します。
5. VSwitch が、RDMA 機能を確認して、右物理アダプター上で作成することを確認します。
6. イベント ビューアーのシステム ログとソース"ハイパー V VmSwitch"でフィルタ処理を確認します。

## <a name="get-smbclientnetworkinterface"></a>SmbClientNetworkInterface を取得します。

RDMA 構成の確認に追加の手順として、Hyper-V サーバー上で、次の Windows PowerShell コマンドを実行します。


    Get SmbClientNetworkInterface

### <a name="get-smbclientnetworkinterface-expected-results"></a>SmbClientNetworkInterface 期待どおりの結果を取得します。

ホスト vNIC として表示されます RDMA 対応の SMB の観点からもします。

![ネットワーク アダプターのプロパティ](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-03.jpg)


### <a name="get-smbclientnetworkinterface-unexpected-results"></a>SmbClientNetworkInterface を取得する予期しない結果

1. Mlnx ミニポートと Mlnx バス ドライバーが最新であることを確認してください。 Mellanox、使用するには、42 少なくともドロップします。 
2. デバイス マネージャーを使ってドライバーのバージョンをチェックして Mlnx ミニポートとバス ドライバーと一致していることを確認します。 [システム デバイスは、バス ドライバーを検索できます。 名前を開始 Mellanox Connect-X 3 PRO VPI、ネットワーク アダプターのプロパティのスクリーン ショットを次に示すようにします。
3. 物理 NIC とホスト vNIC の両方で、ネットワーク ダイレクト (RDMA) を有効にすることを確認します。
4. 右の物理アダプタ上での RDMA 機能をチェックして、Hyper-V 仮想スイッチが作成されたことを確認します。
5. 「SMB クライアント」のイベント ビューアー ログを確認**アプリケーションとサービス |Microsoft |Windows**します。

## <a name="get-netadapterqos"></a>Get-NetAdapterQos

サービス \(QoS\) 構成のネットワーク アダプターの品質を表示するには、次の Windows PowerShell コマンドを実行します。

    Get-NetAdapterQos

### <a name="get-netadapterqos-expected-results"></a>予想される結果を Get-NetAdapterQos

優先順位とトラフィック クラスは、このガイドを使用してを実行する最初の構成手順に従って表示する必要があります。

![サービスの優先度クラスおよびクラスの品質](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-04.jpg)

### <a name="get-netadapterqos-unexpected-results"></a>Get-NetAdapterQos 予期しない結果

結果が予想される場合は、次の手順を実行します。

1. 物理ネットワーク アダプターには、データ センター ブリッジング \(DCB\) と QoS がサポートしていることを確認します。
2. ネットワーク アダプターのドライバーが最新の状態であることを確認します。


## <a name="get-smbmultichannelconnection"></a>Get-SmbMultiChannelConnection

次の Windows PowerShell コマンドを使用すると、リモート ノードの IP アドレスが RDMA\ 対応であることを確認します。

    Get-SmbMultiChannelConnection


### <a name="get-smbmultichannelconnection-expected-results"></a>予想される結果を Get-SmbMultiChannelConnection

リモート ノードの IP アドレスが対応 RDMA として表示されます。

![RDMA 対応のリモート ノードの IP アドレス](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-05.jpg)

### <a name="get-smbmultichannelconnection-unexpected-results"></a>Get-SmbMultiChannelConnection 予期しない結果

結果が予想される場合は、次の手順を実行します。

1. Ping 機能の両方の方法を確認します。
2. ファイアウォールが SMB 接続の開始をブロックしていないことを確認します。 具体的には、SMB ダイレクト ポート 5445 iWARP 用のファイアウォール規則と ROCE の 445 を有効にします。

## <a name="get-smbclientnetworkinterface"></a>Get-SmbClientNetworkInterface

次のコマンドを使用すると、SMB で RDMA を有効になっている仮想 NIC が RDMA\ 対応として報告されることを確認します。

    Get-SmbClientNetworkInterface


### <a name="get-smbclientnetworkinterface-expected-results"></a>予想される結果を Get-SmbClientNetworkInterface

RDMA が有効になっている仮想 NIC は、SMB で RDMA 対応と見なす必要があります。

![Nic が RDMA 対応である SMB をレポートします。](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-06.jpg)

### <a name="get-smbclientnetworkinterface-unexpected-results"></a>Get-SmbClientNetworkInterface 予期しない結果

結果が予想される場合は、次の手順を実行します。

1. Ping 機能の両方の方法を確認します。
2. ファイアウォールが SMB 接続の開始をブロックしていないことを確認します。

## <a name="vstat-mellanox-specific"></a>Vstat \(Mellanox specific\)

ネットワークの Mellanox アダプターを使用している場合を使用できます、**vstat**コマンドを RDMA を over Converged Ethernet \(RoCE\) バージョンの Hyper-V ノードを確認します。

### <a name="vstat-expected-results"></a>予想 vstat 結果

両方のノードで、RoCE バージョンは同じである必要があります。 これは、両方のノードにファームウェアのバージョンが最新であることを確認する効果的な方法ではまたです。

![RoCE バージョン チェックの結果の例](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-07.jpg)

### <a name="vstat-unexpected-results"></a>Vstat 予期しない結果

結果が予想される場合は、次の手順を実行します。

1. Set-MlnxDriverCoreSetting を使用して、正しい RoCE バージョンを設定します。
2. Mellanox の Web サイトから最新のファームウェアをインストールします。


## <a name="perfmon-counters"></a>パフォーマンス モニター カウンター

構成の RDMA のアクティビティを確認するパフォーマンス モニター カウンターを確認することができます。

![パフォーマンス モニターの結果の例](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-08.jpg)

## <a name="all-topics-in-this-guide"></a>このガイドのすべてのトピック

このガイドには、次のトピックが含まれています。

- [単一のネットワーク アダプターに収束の NIC 構成](cnic-single.md)
- [収束の NIC チーム化された NIC の構成](cnic-datacenter.md)
- [収束の NIC の物理スイッチの構成](cnic-app-switch-config.md)
- [集約型の NIC 構成のトラブルシューティング](cnic-app-troubleshoot.md)
