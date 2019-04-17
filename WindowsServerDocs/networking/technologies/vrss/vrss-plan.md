---
title: VRSS の使用を計画します。
description: このトピックでは、Windows Server 2016 で vRSS を使用するため、仮想マシンと HYPER-V ホストの準備を使用できます。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 695e6192-5e84-4ab4-b33e-8ebf6b8f5cbb
ms.localizationpriority: medium
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/04/2018
ms.openlocfilehash: e6558b00e87721d8ab81c84946a14745c4faa812
ms.sourcegitcommit: e84e328c13a701e8039b16a4824a6e58a6e59b0b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2018
ms.locfileid: "4133388"
---
# VRSS の使用を計画します。

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

Windows Server 2016 で vRSS が有効になりますが既定では、仮想マシンで正しく動作する vRSS を許可する環境を準備する必要があります \(VM\) またはホスト仮想アダプター \(vNIC\) します。 Windows Server 2012 R2、vRSS は既定で無効にされました。

計画 vRSS の使用を準備すると、以下のことを確認します。

- 物理ネットワーク アダプターを使用して、仮想マシンのキュー \(VMQ\) 互換性が、10 gbps リンク速度以上します。
- Hyper \-v 仮想スイッチ ポートと物理 NIC で VMQ が有効になっています。
- 1 つのルート Input\ 出力の仮想化 \(SR\-IOV\) VM 用に構成することはありません。
- NIC チーミングが正しく構成されています。
- VM では、複数の論理プロセッサ \(LPs\) があります。

>[!NOTE]
>vRSS は既定では、ホスト Vnic を有効になっている RSS を持つのも有効にします。

これらの準備手順を完了する必要がある追加の情報を次に示します。
  
1. **ネットワーク アダプターの容量**。 ネットワーク アダプターが仮想マシンのキュー \(VMQ\) と互換性のあるリンクの速度が 10 Gbps 以上のことを確認します。 リンク速度がより小さい 10 Gbps の場合は、hyper \-v 仮想スイッチを無効にする VMQ 既定では、場合でも、表示されたまま VMQ **Get NetAdapterVmq**の Windows PowerShell コマンドの結果で有効にします。 VMQ が有効または無効になっていることを確認する場合に使用できる 1 つのメソッドでは、 **Get NetAdapterVmqQueue**コマンドを使用します。  VMQ を無効にした場合、このコマンドの結果は VM またはホストの仮想ネットワーク アダプターに割り当てられている QueueID がないことを示しています。 
  
2. **VMQ を有効に**します。 ホスト コンピューターで VMQ が有効になっていることを確認します。 vRSS では、ホストが VMQ をサポートしていない場合は機能しません。 **Get VMSwitch**を実行していると、仮想スイッチを使用しているアダプターを検索して VMQ が有効になっていることを確認できます。 次に、 **Get NetAdapterVmq**を実行し、アダプターが結果に表示される VMQ を有効になっていることを確認します。
  
3. **SR\ IOV がない場合**。 ことを確認する 1 つのルート Input\ 出力の仮想化 \(SR\-IOV\) 仮想関数 \(VF\) ドライバーは VM ネットワーク インターフェイスに接続されていません。 これは、 **Get NetAdapterSriov**コマンドを使用して確認できます。 VF ドライバーが読み込まれている場合、RSS は vRSS で構成されているものではなくこのドライバーからのスケーリングの設定を使用します。 VF ドライバーは、RSS をサポートしていない、vRSS が無効です。
  
4. **NIC チーミングの構成**。 NIC チーミングを使用している場合は、NIC チーミングの設定を操作する VMQ を正しく構成することが重要です。 NIC チーミングの展開と管理の詳細については、 [NIC チーミング](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)を参照してください。

5. **Lp の数**です。 VM には、複数の論理プロセッサがあることを確認 \(LP\) します。 vRSS は、VM の RSS やトラフィックの負荷分散を受信する複数の Lp 並列処理のために、HYPER-V ホスト上に依存します。 ホストで**Get VMProcessor**の Windows PowerShell コマンドを実行して、VM には多くの Lp を確認できます。 コマンドを実行した後、Lp の数のカウント列のエントリを確認できます。

ホスト vNIC 常にすべての物理プロセッサ; へのアクセスにはプロセッサの特定の数を使用するホスト vNIC を構成するには、設定を使用して **、BaseProcessorNumber**と **-MaxProcessors** **セット NetAdapterRss**の Windows PowerShell コマンドを実行するとします。

---