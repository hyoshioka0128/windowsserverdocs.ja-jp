---
title: 集約型のない NIC 構成のトラブルシューティング
description: このトピックでは、コンバージド NIC 構成ガイドの Windows Server 2016 の一部です。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 0bc6746f-2adb-43d8-a503-52f473833164
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3004ff9d6fe874410c24d174755a6d26f99f8f2a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59876483"
---
# <a name="troubleshooting-converged-nic-configurations"></a>集約型のない NIC 構成のトラブルシューティング

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

RDMA 構成が HYPER-V ホストに正しいかどうかを確認するのには、次のスクリプトを使用することができます。

- [テスト Rdma.ps1 スクリプトをダウンロードします。](https://github.com/Microsoft/SDN/blob/master/Diagnostics/Test-Rdma.ps1)

トラブルシューティングについては、コンバージド Nic の構成を確認する、次の Windows PowerShell コマンドを使用することもできます。

## <a name="get-netadapterrdma"></a>Get-NetAdapterRdma

ネットワーク アダプターの RDMA 構成を確認するには、HYPER-V サーバーで次の Windows PowerShell コマンドを実行します。

    
    Get-NetAdapterRdma | fl *
    

次が必要ですし、予期しない結果を使用するを特定し、HYPER-V ホストでこのコマンドを実行した後、問題を解決します。

### <a name="get-netadapterrdma-expected-results"></a>Get NetAdapterRdma 期待どおりの結果

ホスト vNIC 物理 NIC は、0 以外の RDMA 機能を紹介します。

![Windows PowerShell が期待どおりの結果](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-01.jpg)

### <a name="get-netadapterrdma-unexpected-results"></a>Get NetAdapterRdma 予期しない結果

実行するときに予期しない結果が発生した場合は、次の手順を実行、 **Get NetAdapterRdma**コマンド。

1. Mlnx ミニポートと Mlnx バス ドライバーが最新かどうか確かめてください。 Mellanox では、使用は、少なくとも 42 をドロップします。 
2. Mlnx ミニポートとバス ドライバーがデバイス マネージャーでドライバーのバージョンを確認して一致することを確認します。 システム デバイスは、バス ドライバーを確認できます。 名前は、ネットワーク アダプターのプロパティの次のスクリーン ショットに示すように、Mellanox Connect X 3 PRO VPI で始まらなければなりません。

![ネットワーク アダプターのプロパティ](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-02.jpg)

4. 物理 NIC とホスト vNIC の両方でネットワーク ダイレクト (RDMA) が有効になっていることを確認します。
5. VSwitch が適切な物理アダプターの RDMA 機能を確認して作成することを確認します。
6. イベント ビューアーのシステム ログとソース"ハイパー V VmSwitch"でフィルター処理を確認します。

--- 

## <a name="get-smbclientnetworkinterface"></a>Get SmbClientNetworkInterface

RDMA 構成の確認に追加の手順として、HYPER-V サーバーで、次の Windows PowerShell コマンドを実行します。


    Get-SmbClientNetworkInterface

### <a name="get-smbclientnetworkinterface-expected-results"></a>Get SmbClientNetworkInterface 期待どおりの結果

ホスト vNIC は、同様の SMB の観点から RDMA 対応として表示されます。

![ネットワーク アダプターのプロパティ](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-03.jpg)


### <a name="get-smbclientnetworkinterface-unexpected-results"></a>Get SmbClientNetworkInterface 予期しない結果

1. Mlnx ミニポートと Mlnx バス ドライバーが最新かどうか確かめてください。 Mellanox では、使用は、少なくとも 42 をドロップします。 
2. Mlnx ミニポートとバス ドライバーがデバイス マネージャーでドライバーのバージョンを確認して一致することを確認します。 システム デバイスは、バス ドライバーを確認できます。 名前は、ネットワーク アダプターのプロパティの次のスクリーン ショットに示すように、Mellanox Connect X 3 PRO VPI で始まらなければなりません。
3. 物理 NIC とホスト vNIC の両方でネットワーク ダイレクト (RDMA) が有効になっていることを確認します。
4. RDMA 機能を確認して、適切な物理アダプター上で HYPER-V 仮想スイッチを作成することを確認します。
5. SMB「クライアント」のイベント ビューアー ログを確認**アプリケーションとサービス |Microsoft |Windows**します。

--- 

## <a name="get-netadapterqos"></a>Get-NetAdapterQos

サービスのネットワーク アダプターの品質を表示する\(QoS\)次の Windows PowerShell コマンドを実行して構成します。

    Get-NetAdapterQos

### <a name="get-netadapterqos-expected-results"></a>Get-NetAdapterQos expected results

優先順位とトラフィック クラスは、このガイドを使用してを実行する最初の構成手順に従って表示されます。

![サービスの優先度、およびクラスの品質](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-04.jpg)

### <a name="get-netadapterqos-unexpected-results"></a>Get-NetAdapterQos unexpected results

結果が予想される場合は、次の手順を実行します。

1. 物理ネットワーク アダプターがデータ センター ブリッジングをサポートしていることを確認\(DCB\)と QoS
2. ネットワーク アダプターのドライバーが最新であることを確認します。

--- 

## <a name="get-smbmultichannelconnection"></a>Get-SmbMultiChannelConnection

次の Windows PowerShell コマンドを使用するには、リモート ノードの IP アドレスが RDMA であることを確認する\-対応します。

    Get-SmbMultiChannelConnection


### <a name="get-smbmultichannelconnection-expected-results"></a>Get SmbMultiChannelConnection 期待どおりの結果

リモート ノードの IP アドレスが可能な RDMA として表示されます。

![RDMA 対応のリモート ノードの IP アドレス](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-05.jpg)

### <a name="get-smbmultichannelconnection-unexpected-results"></a>Get SmbMultiChannelConnection 予期しない結果

結果が予想される場合は、次の手順を実行します。

1. Ping 機能の両方の方法を確認します。
2. ファイアウォールがブロックしていない場合、SMB 接続の開始に使用することを確認します。 具体的には、SMB ダイレクト ポート 5445 iWARP 用のファイアウォール規則と ROCE の 445 を有効にします。

--- 

## <a name="get-smbclientnetworkinterface"></a>Get SmbClientNetworkInterface

次のコマンドを使用するには、仮想 NIC を有効になっている RDMA が RDMA として報告されることを確認する\-SMB で対応します。

    Get-SmbClientNetworkInterface


### <a name="get-smbclientnetworkinterface-expected-results"></a>Get SmbClientNetworkInterface 期待どおりの結果

RDMA が有効になっている仮想 NIC は、SMB で RDMA 対応と見なす必要があります。

![Nic は、RDMA 対応である SMB を報告します。](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-06.jpg)

### <a name="get-smbclientnetworkinterface-unexpected-results"></a>Get SmbClientNetworkInterface 予期しない結果

結果が予想される場合は、次の手順を実行します。

1. Ping 機能の両方の方法を確認します。
2. ファイアウォールがブロックしていない場合、SMB 接続の開始に使用することを確認します。

--- 

## <a name="vstat-mellanox-specific"></a>vstat \(Mellanox 固有\)

使用すること Mellanox ネットワーク アダプターを使用している場合、 **vstat** over Converged Ethernet、RDMA を確認するコマンド\(RoCE\) HYPER-V ノード上のバージョン。

### <a name="vstat-expected-results"></a>vstat が期待どおりの結果

両方のノードで、RoCE バージョンは同じである必要があります。 これは、また、両方のノード上のファームウェア バージョンが最新であることを確認する良い方法です。

![RoCE バージョン チェックの結果の例](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-07.jpg)

### <a name="vstat-unexpected-results"></a>vstat 予期しない結果

結果が予想される場合は、次の手順を実行します。

1. セット MlnxDriverCoreSetting を使用して正しい RoCE のバージョンを設定します。
2. Mellanox web サイトから最新のファームウェアをインストールします。

--- 

## <a name="perfmon-counters"></a>パフォーマンス モニター カウンター

構成の RDMA のアクティビティを確認するパフォーマンス モニターのカウンターを確認できます。

![パフォーマンス モニターの結果の例](../../media/Converged-NIC/CNIC-Troubleshooting/cnic-tshoot-08.jpg)

--- 

## <a name="related-topics"></a>関連トピック

- [1 つのネットワーク アダプターに収束の NIC の構成](cnic-single.md)
- [収束の NIC チーミングされた NIC の構成](cnic-datacenter.md)
- [収束の NIC の物理スイッチの構成](cnic-app-switch-config.md)

---
