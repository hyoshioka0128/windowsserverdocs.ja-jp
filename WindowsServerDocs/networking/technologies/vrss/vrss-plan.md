---
title: VRSS の使用を計画する
description: このトピックを使用して、Windows Server 2016 で vRSS を使用するように仮想マシンと Hyper-v ホストを準備できます。
ms.topic: article
ms.assetid: 695e6192-5e84-4ab4-b33e-8ebf6b8f5cbb
ms.localizationpriority: medium
manager: dougkim
ms.author: lizross
author: eross-msft
ms.date: 09/04/2018
ms.openlocfilehash: 9457a1763f92e7f2571040c1c6e8e323d96ee598
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87951941"
---
# <a name="plan-the-use-of-vrss"></a>VRSS の使用を計画する

>適用先:Windows Server (半期チャネル)、Windows Server 2016

Windows Server 2016 では、vRSS は既定で有効になっていますが、vRSS が仮想マシン \( VM \) またはホスト仮想アダプター vNIC で正しく機能するように環境を準備する必要があり \( \) ます。 Windows Server 2012 R2 では、既定では、vRSS は無効になっていました。

VRSS の使用を計画および準備するときは、次のことを確認してください。

- 物理ネットワークアダプターは仮想マシンキュー VMQ と互換性があり、 \( \) 10 Gbps 以上のリンク速度を備えています。
- 物理 NIC と Hyper-v \- 仮想スイッチポートで VMQ が有効になっています。
- \- \( \- \) VM 用に構成された単一のルート入力出力仮想化 SR がありません。
- NIC チーミングが正しく構成されている。
- VM には複数の論理プロセッサがあり \( \) ます。

>[!NOTE]
>また、RSS が有効になっているすべてのホスト vNICs に対して、vRSS も既定で有効になっています。

これらの準備手順を実行するために必要な追加情報を次に示します。

1. **ネットワークアダプターの容量**。 ネットワークアダプターが仮想マシンキュー VMQ と互換性があり \( 、 \) 10 Gbps 以上のリンク速度があることを確認します。 リンク速度が 10 Gbps 未満の場合、 \- Windows PowerShell コマンド**get-netadaptervmq**の結果で vmq が有効と表示されていても、hyper-v 仮想スイッチは既定で vmq を無効にします。 VMQ が有効または無効になっていることを確認するために使用できる方法の1つは、 **get-netadaptervmqqueue**コマンドを使用することです。  VMQ が無効になっている場合、このコマンドの結果は、VM またはホスト仮想ネットワークアダプターに QueueID が割り当てられていないことを示します。

2. **VMQ を有効に**します。 ホスト マシン上で VMQ が有効であることを確認します。 ホストで VMQ がサポートされていない場合、vRSS は機能しません。 VMQ が有効になっていることを確認するには、 **Get VMSwitch**を実行し、仮想スイッチが使用しているアダプターを探します。 次に、**Get-NetAdapterVmq** を実行して、結果にアダプターが表示されていること、および VMQ が有効であることを確認します。

3. **SR \- の欠如SR-IOV**。 単一のルート入力 \- 出力仮想化 \( SR \- \) 仮想関数 \( VF \) ドライバーが VM ネットワークインターフェイスに接続されていないことを確認してください。 これを確認するには、 **get-netadaptersriov**コマンドを使用します。 VF ドライバーが読み込まれると、RSS は、vRSS で構成されているものではなく、このドライバーからのスケーリング設定を使用します。 VF ドライバーが RSS をサポートしていない場合、vRSS は無効になります。

4. **NIC チーミングの構成**。 NIC チーミングを使用している場合は、NIC チーミング設定と連動するように VMQ を正しく構成することが重要です。 NIC チーミングの展開と管理の詳細については、「 [Nic チーミング](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)」を参照してください。

5. **LPs の数**。 VM に複数の論理プロセッサ LP があることを確認し \( \) ます。 vRSS は、VM または Hyper-v ホストの RSS に依存して、受信したトラフィックを並列処理のために複数の LPs に負荷分散します。 ホストで Windows PowerShell コマンドの**Get VMProcessor**を実行すると、VM で使用されている lps の数を確認できます。 コマンドを実行した後、LPs の数の Count 列のエントリを確認できます。

ホスト vNIC は、常にすべての物理プロセッサにアクセスできます。特定の数のプロセッサを使用するようにホスト vNIC を構成するには、 **Set-netadapterrss** Windows PowerShell コマンドを実行するときに、設定 **-baseprocessornumber**と **-maxprocessors**を使用します。

---