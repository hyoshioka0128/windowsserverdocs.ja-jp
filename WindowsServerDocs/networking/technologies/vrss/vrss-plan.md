---
title: VRSS の使用を計画します。
description: VRSS を使用して、Windows Server 2016 での仮想マシンと HYPER-V ホストを準備するのにには、このトピックを使用します。
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850443"
---
# <a name="plan-the-use-of-vrss"></a>VRSS の使用を計画します。

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

Windows Server 2016 で vRSS は有効になりますが既定では、仮想マシンで正しく機能する vRSS を許可する環境を準備する必要があります\(VM\)またはホストの仮想アダプター \(vNIC\)します。 Windows Server 2012 R2 では、vRSS は既定で無効にされました。

計画 vRSS の使用を準備すると、以下のことを確認します。

- 物理ネットワーク アダプターが仮想マシン キューと互換性のある\(VMQ\) 10 Gbps のリンク速度以上であるとします。
- Hyper と物理 NIC で VMQ が有効になっている\-V 仮想スイッチ ポート
- ルートの 1 つの入力がない\-出力 Virtualization \(SR\-IOV\) VM 用に構成します。
- NIC チーミングが正しく構成されます。
- VM が複数の論理プロセッサ\(LPs\)します。

>[!NOTE]
>vRSS は既定では、RSS が有効になっているホスト Vnic のも有効にします。

これらの準備手順を完了する必要がある追加の情報を次に示します。
  
1. **ネットワーク アダプターのキャパシティ**します。 ネットワーク アダプターが仮想マシン キューと互換性があることを確認\(VMQ\) 10 Gbps のリンク速度以上であるとします。 リンク速度がより小さい 10 Gbps、Hyper\-場合でも、Windows PowerShell コマンドの結果に有効になっている VMQ がまだ表示 V 仮想スイッチに既定で VMQ が無効に**Get-netadaptervmq**します。 VMQ を有効または無効になっていることを確認するための 1 つの方法は、コマンドを使用する**Get-netadaptervmqqueue**します。  VMQ が無効になっている場合、このコマンドの結果は VM またはホストの仮想ネットワーク アダプターに割り当てられている QueueID がないことを示しています。 
  
2. **VMQ を有効にする**します。 ホスト マシン上で VMQ が有効であることを確認します。 vRSS では、ホストで VMQ がサポートされていない場合は機能しません。 実行して VMQ が有効であることを確認できます**Get-vmswitch**および仮想スイッチを使用しているアダプターを検索します。 次に、 **Get-NetAdapterVmq** を実行して、結果にアダプターが表示されていること、および VMQ が有効であることを確認します。
  
3. **記憶域レプリカの休暇\-IOV**します。 単一のルートを入力することを確認\-出力の仮想化\(SR\-IOV\)仮想関数\(VF\)ドライバーは、VM ネットワーク インターフェイスにアタッチされていません。 これを確認するにを使用して、 **Get-netadaptersriov**コマンド。 VF ドライバーが読み込まれている場合、RSS は、vRSS によって構成された設定ではなくこのドライバーからのスケール設定を使用します。 VF ドライバーは、RSS をサポートしていない、vRSS は無効です。
  
4. **NIC チーミングの構成**します。 NIC チーミングを使用している場合は、NIC チーミングの設定を使用するために VMQ を正しく構成することが重要です。 NIC チーミングの展開と管理の詳細については、次を参照してください。 [NIC チーミング](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)します。

5. **LPs 数**します。 VM に 1 つ以上の論理プロセッサがあることを確認\(LP\)します。 vRSS では、VM で rss または受信トラフィックを負荷分散する並列処理のための複数の LPs を HYPER-V ホストに依存しています。 VM が Windows PowerShell コマンドを実行している数 LPs を観察できます**Get-vmprocessor**でホストします。 コマンドを実行した後、LPs の数のカウント列のエントリを確認できます。

ホスト vNIC が常にすべての物理プロセッサ; へのアクセスを持っています特定のプロセッサ数を使用するホスト vNIC を構成するには、設定を使用して **- BaseProcessorNumber**と **- MaxProcessors**を実行すると、 **Set-netadapterrss**Windows PowerShell コマンド。

---