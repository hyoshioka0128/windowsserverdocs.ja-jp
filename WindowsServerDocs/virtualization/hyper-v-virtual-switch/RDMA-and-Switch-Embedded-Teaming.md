---
title: リモート ダイレクト メモリ アクセス (RDMA) とスイッチ埋め込みチーミング (SET)
description: このトピックでは、情報に関するスイッチ埋め込みチーミング (SET) に加え、Windows Server 2016 で HYPER-V をリモート ダイレクト メモリ アクセス (RDMA) インターフェイスの構成に関する情報を提供します。
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 68c35b64-4d24-42be-90c9-184f2b5f19be
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c945144194ac86623bfa8ce60a306f0202df0874
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881663"
---
# <a name="remote-direct-memory-access-rdma-and-switch-embedded-teaming-set"></a>リモート ダイレクト メモリ アクセス\(RDMA\)スイッチ埋め込みチーミングと\(設定\)

>適用先:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、リモート ダイレクト メモリ アクセスの構成に関する情報を提供します\(RDMA\)スイッチ埋め込みチーミングについては、さらに、Windows Server 2016 で HYPER-V とのインターフェイス\(設定\)します。  

> [!NOTE]
> このトピックに加え、次のスイッチ埋め込みチーミング コンテンツは使用できます。 
> - TechNet ギャラリーのダウンロード:[Windows Server 2016 の NIC とスイッチ埋め込みチーミング ユーザー ガイド](https://gallery.technet.microsoft.com/Windows-Server-2016-839cb607?redir=0)

## <a name="bkmk_rdma"></a>Hyper V と RDMA インターフェイスを構成  

Windows Server 2012 R2 では、RDMA サービスが HYPER-V 仮想スイッチにバインドされていないことができますを提供するネットワーク アダプターと同じコンピューターに RDMA と HYPER-V の両方を使用します。 これにより、HYPER-V ホストにインストールするために必要な物理ネットワーク アダプターの数が増加します。

>[!TIP]
>Windows Server 2016 より前の Windows Server のエディションでは、NIC チームまたは HYPER-V 仮想スイッチにバインドされているネットワーク アダプターで RDMA を構成することはできません。 Windows Server 2016 では、セットの有無、HYPER-V 仮想スイッチにバインドされているネットワーク アダプターで RDMA を有効にできます。

Windows Server 2016 では、セットの有無、RDMA を使用しているときに以下のネットワーク アダプターを使用できます。

次の図は、Windows Server 2012 R2 と Windows Server 2016 の間でのソフトウェア アーキテクチャの変更を示しています。

![アーキテクチャの変更](../media/RDMA-and-SET/rdma_over.jpg)

次のセクションで、RDMA 仮想 NIC で、HYPER-V 仮想スイッチを作成するデータ センター ブリッジング (DCB) を有効にする Windows PowerShell コマンドを使用する方法の手順を提供する\(vNIC\)セットで、HYPER-V 仮想スイッチを作成RDMA Vnic を選択します。

### <a name="enable-data-center-bridging-dcb"></a>有効にするデータ センター ブリッジング\(DCB\)

Over Converged Ethernet、RDMA を使用する前に\(RoCE\)バージョン RDMA の DCB を有効にする必要があります。  インターネット ワイド エリア RDMA プロトコルは必要ありません、 \(iWARP\)ネットワークでは、テストが判別されましたすべて RDMA のイーサネット ベースのテクノロジが DCB でより適切に動作します。 このため、DCB を使用して、iWARP RDMA の展開についても検討してください。

次の Windows PowerShell コマンド例では、有効にして SMB ダイレクトの DCB を構成する方法を示します。

DCB を有効にします。

    Install-WindowsFeature Data-Center-Bridging

SMB ダイレクトのポリシーを設定します。

    New-NetQosPolicy "SMB" -NetDirectPortMatchCondition 445 -PriorityValue8021Action 3

SMB のフロー制御をオンにします。

    Enable-NetQosFlowControl  -Priority 3

フロー制御は、他のトラフィックがオフすることを確認します。

    Disable-NetQosFlowControl  -Priority 0,1,2,4,5,6,7

ターゲットのアダプターにポリシーが適用されます。

    Enable-NetAdapterQos  -Name "SLOT 2"

SMB 帯域幅の最小の直接の 30% を与えます。

`New-NetQosTrafficClass "SMB"  -Priority 3  -BandwidthPercentage 30  -Algorithm ETS`  

カーネル デバッガーがシステムにインストールした場合は、QoS では、次のコマンドを実行して設定を許可するようにデバッガーを構成する必要があります。

デバッガーをオーバーライド - 既定では、デバッガーは NetQos をブロックします。
 
    Set-ItemProperty HKLM:"\SYSTEM\CurrentControlSet\Services\NDIS\Parameters" AllowFlowControlUnderDebugger -type DWORD -Value 1 -Force

### <a name="create-a-hyper-v-virtual-switch-with-an-rdma-vnic"></a>RDMA vNIC での HYPER-V 仮想スイッチの作成します。

セットで展開に必要ない場合、次の Windows PowerShell コマンドを使用して、RDMA vNIC で HYPER-V 仮想スイッチを作成することができます。

> [!NOTE]
> チームのセットを使用して、RDMA 対応の物理 Nic を持つ消費 Vnic の他の RDMA リソースを提供します。

    New-VMSwitch -Name RDMAswitch -NetAdapterName "SLOT 2"

ホスト Vnic を追加し、RDMA できるようにします。

    Add-VMNetworkAdapter -SwitchName RDMAswitch -Name SMB_1
    Enable-NetAdapterRDMA "vEthernet (SMB_1)" "SLOT 2"

RDMA 機能を確認します。

    Get-NetAdapterRdma

###  <a name="bkmk_set-rdma"></a>SET と RDMA Vnic で HYPER-V 仮想スイッチの作成します。

仮想ネットワーク アダプターをホストする hyper-v capabilies RDMA を使用するよう\(Vnic\) RDMA のチーミングをサポートする HYPER-V 仮想スイッチでは、これらの例の Windows PowerShell コマンドを使用できます。

    New-VMSwitch -Name SETswitch -NetAdapterName "SLOT 2","SLOT 3" -EnableEmbeddedTeaming $true

ホスト Vnic を追加します。

    Add-VMNetworkAdapter -SwitchName SETswitch -Name SMB_1 -managementOS
    Add-VMNetworkAdapter -SwitchName SETswitch -Name SMB_2 -managementOS

多くのスイッチは VLAN のタグなしトラフィックをトラフィック クラス情報を渡すしません、RDMA 用ホスト アダプターが Vlan であることを確認しておきます。 この例には、2 つ SMB_ * ホスト仮想アダプターの VLAN 42 が割り当て。
    
    Set-VMNetworkAdapterIsolation -ManagementOS -VMNetworkAdapterName SMB_1  -IsolationMode VLAN -DefaultIsolationID 42
    Set-VMNetworkAdapterIsolation -ManagementOS -VMNetworkAdapterName SMB_2  -IsolationMode VLAN -DefaultIsolationID 42
    

ホスト Vnic で RDMA を有効にします。

    Enable-NetAdapterRDMA "vEthernet (SMB_1)","vEthernet (SMB_2)" "SLOT 2", "SLOT 3"

RDMA 機能を確認します。機能が 0 以外であることを確認します。

    Get-NetAdapterRdma | fl *


## <a name="bkmk_sswitchembedded"></a>スイッチ埋め込みチーミング (SET)  

このセクションでは、スイッチ埋め込みチーミング (SET) Windows Server 2016 の概要について説明し、次のセクションが含まれています。

- [セットの概要](#bkmk_over)

- [セットの可用性](#bkmk_avail)

- [セットのサポートされているとサポート非対象の Nic](#bkmk_nics)

- [Windows Server ネットワーク テクノロジとの互換性を設定します。](#bkmk_compat)

- [セットのモードと設定](#bkmk_modes)

- [セットと仮想マシン キュー (VMQs)](#bkmk_vmq)

- [セットと HYPER-V ネットワーク仮想化 (HNV)](#bkmk_hnv)

- [設定とライブ移行](#bkmk_live)

- [転送されたパケットの MAC アドレスの使用](#bkmk_mac)

- [セット チームを管理します。](#bkmk_manage)

## <a name="bkmk_over"></a>セットの概要

セットは、Hyper-v ホストとソフトウェア定義ネットワークに含まれる環境で使用できる代替 NIC チーミング ソリューション\(SDN\) Windows Server 2016 でのスタック。 セットは、HYPER-V 仮想スイッチにいくつかの NIC チーミング機能を統合します。

セットには、1 つまたは 8 物理イーサネット ネットワーク アダプター間で 1 つまたは複数のソフトウェア ベースの仮想ネットワーク アダプターにグループ化することができます。 これらの仮想ネットワーク アダプターは、高速なパフォーマンスに加え、ネットワーク アダプターに障害が発生した場合のフォールト トレランスを提供します。

チームに配置する同じ物理的な HYPER-V ホスト上で、セットのメンバーのネットワーク アダプターをすべてにインストールする必要があります。

> [!NOTE]
> セットの使用は Windows Server 2016 で HYPER-V 仮想スイッチでのみサポートされます。 Windows Server 2012 R2 のセットを展開することはできません。

同じ物理スイッチまたはさまざまな物理スイッチ、Nic のチーミングを接続できます。 Nic を別々 のスイッチに接続する場合、同じサブネットに両方のスイッチを引き起こすことがあります。

次の図は、一連のアーキテクチャを示しています。

![セット アーキテクチャ](../media/RDMA-and-SET/set_architecture.jpg)

セットは、HYPER-V 仮想スイッチに統合されているので、仮想マシン (VM) の内部セットを使用することはできません。 Vm 内の NIC チーミングを使用すること、ただしします。

詳細については、次を参照してください。 [仮想マシン (Vm) での NIC チーミング](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nict-vms)します。

さらに、一連のアーキテクチャは、チームのインターフェイスを公開しません。 代わりに、HYPER-V 仮想スイッチ ポートを構成する必要があります。

## <a name="bkmk_avail"></a>セットの可用性

セットは、Hyper-v ホストと SDN スタックを含む Windows Server 2016 のすべてのバージョンで使用できます。 さらに、ツールがサポートされているクライアントのオペレーティング システムを実行しているリモート コンピューターからセットを管理するのに Windows PowerShell コマンドとリモート デスクトップ接続を使用することができます。

## <a name="bkmk_nics"></a>セットのサポートされている Nic

Windows ハードウェア認定およびロゴを経過した任意のイーサネット NIC を使用する\(WHQL\)で Windows Server 2016 でセット チームをテストします。 セットは、セット チームのメンバーであるすべてのネットワーク アダプターが同一でなければならないことが必要です\(つまり、同じ製造元で同じモデル、同じファームウェアとドライバー\)します。 セットは、チーム内の 1 つまたは 8 のネットワーク アダプター間でサポートします。
  
## <a name="bkmk_compat"></a>Windows Server ネットワーク テクノロジとの互換性を設定します。

セットは、Windows Server 2016 では、次のネットワーク テクノロジとの互換性です。

- データ センター ブリッジング\(DCB\)
  
- Windows Server 2016 では HYPER-V ネットワーク仮想化 - NV GRE と VxLAN がサポートされます。  
- 受信側のチェックサム オフロード\(IPv4、IPv6、TCP\) -サポート チームのメンバーのセットのいずれかの場合にサポートされています。

- リモート ダイレクト メモリ アクセス\(RDMA\)

- シングル ルート I/O 仮想化\(SR-IOV\)

- 送信側のチェックサム オフロード\(IPv4、IPv6、TCP\) -すべてのチーム メンバーのセットをサポートしている場合にサポートされています。

- 仮想マシン キュー \(VMQ\)

- 仮想 Receive Side Scaling \(RSS\)

セットは、Windows Server 2016 では、次のネットワーク テクノロジと互換性がありません。

- 802.1 X 認証します。 802.1 x Extensible Authentication Protocol \(EAP\)パケットはハイパーによって自動的に削除\-セットのシナリオで仮想スイッチの概要。
 
- IPsec タスク オフロード\(IPsecTO\)します。 これは、ほとんどのネットワーク アダプターでサポートされていないレガシ テクノロジと、存在して、既定で無効です。

- QoS を使用して\(pacer.exe\)ホストまたはネイティブのオペレーティング システムでします。 これらの QoS のシナリオがハイパー\-V シナリオ、テクノロジが交差しないようにします。 さらに、QoS には、使用できますが、既定で有効になっていません - QoS を意図的に有効にする必要があります。

- 受信側 coalescing \(RSC\)します。 RSC は自動的にハイパースレッディングを無効になっている\-仮想スイッチの概要。

- 受信側のスケーリング\(RSS\)します。 HYPER-V では、VMQ と VMMQ にキューを使用しているため、RSS は仮想スイッチを作成するときに常に無効です。

- TCP Chimney オフロードします。 このテクノロジは既定で無効になっています。

- 仮想マシンの QoS \(VM QoS\)します。 VM QoS は、使用できますが、既定では無効です。 セットの環境で VM の QoS を構成する QoS の設定に予期しない結果が発生します。

## <a name="bkmk_modes"></a>セットのモードと設定

NIC チーミングとは異なり、セット チームを作成するときに、チーム名インストールを構成することはできません。 さらに、NIC チーミングでサポートされてスタンバイ アダプターを使用してはセットではサポートされていません。 セットを展開するときに、すべてのネットワーク アダプターがアクティブとスタンバイ モードでは [なし] です。

NIC チーミングとセットのもう 1 つ重要な違いは、NIC チーミングが提供する 3 つの異なるチーミング モードの選択のみセットをサポートしている **スイッチに依存しない** モードです。 独立したスイッチのモードでは、スイッチまたはスイッチの設定のチーム メンバーが接続されているセット チームの存在に対応していないし、チーム メンバーを設定するネットワーク トラフィックを分散する方法を特定できません - セット チームが一連のチーム メンバー間で受信ネットワーク トラフィックを分散する代わりに、します。

新しいセット チームを作成するときに、次のチームのプロパティを構成する必要があります。

- メンバーのアダプター

- 負荷分散モード

### <a name="member-adapters"></a>メンバーのアダプター

セットのチームを作成する場合は、一連のチーム メンバーのアダプターとして、HYPER-V 仮想スイッチにバインドされている最大 8 つの同一のネットワーク アダプターを指定する必要があります。

### <a name="load-balancing-mode"></a>負荷分散モード

オプション セットをチームの負荷分散の分散モードは **HYPER-V ポート** と **動的**します。

**HYPER-V ポート**

Vm は、HYPER-V 仮想スイッチのポートに接続されます。 セット チームの HYPER-V ポートのモードを使用している場合、HYPER-V 仮想スイッチ ポートと関連付けられている MAC アドレスは、チーム メンバーのセット間のネットワーク トラフィックを分割に使用されます。

> [!NOTE]
> パケット ダイレクトでは、チーミング モードと組み合わせてセットを使用すると  **スイッチに依存しない** と負荷分散モード **HYPER-V ポート** が必要です。

隣接するスイッチは、指定したポートで、特定の MAC アドレスを常には、あるため、スイッチは、MAC アドレスのポートに受信負荷 (ホストのスイッチのトラフィック) を配布します。 これは特に便利ですバーチャル マシン キュー (VMQs) を使用している場合、キューは、トラフィックが到着する期待される場所で特定の NIC で配置できるためです。

ただし、ホストにいくつかの Vm がある場合は、このモードはありませんな負荷分散を実現するために必要なレベルです。 このモードは、単一のインターフェイスで利用できる帯域幅を 1 つの VM (つまり、1 つのスイッチ ポートからのトラフィック) を常にも制限されます。

**動的**

この負荷分散モードでは、次の利点を提供します。

- TCP ポートと IP アドレスのハッシュに基づいて、送信の負荷が分散されます。  動的モードもバランスが再調整負荷をリアルタイムに特定の送信フローは、チーム メンバーのセット間で双方向に移動できるようにします。

- HYPER-V ポートのモードと同じ方法では、着信負荷が分散されます。

このモードでの送信の負荷が flowlets の概念に基づいて動的に分散します。 人間の音声認識に単語や文の末尾にある自然な改行がある場合と同様 TCP フロー (TCP 通信ストリーム) が自然に発生した中断もあります。 このような 2 つの区切りの間の TCP フローの一部を flowlet と呼びます。

動的モード アルゴリズムは、十分な長さの中断が TCP フロー - で発生した場合などに flowlet 境界が検出されたことを検出すると、アルゴリズムで該当する場合は、別のチーム メンバーへの流れが自動的に再分散します。  一般的でない状況によっては、アルゴリズム可能性があります、flowlets が含まれていないフローを再調整も定期的にします。 このため、TCP フローとチーム メンバー間のアフィニティは動的な分散アルゴリズムは、チーム メンバーの作業負荷のバランスを取る動作いつでも変更できます。

## <a name="bkmk_vmq"></a>セットと仮想マシン キュー (VMQs)

VMQ と連携して動作、および Hyper-v ホストと設定を使用しているときに、VMQ を有効にする必要があります。

> [!NOTE]
> チーム メンバーには、すべての設定で使用するキューの合計数は常に設定します。 NIC チーミングには、キューの合計モードこの呼び出されます。

ほとんどのネットワーク アダプターがあるか Receive Side Scaling に使用できるキュー \(RSS\)または VMQ、両方ではなく同時にします。
  
VMQ 設定の一部では、RSS のキューの設定に見えますが、どの機能によって RSS および VMQ の両方の使用は現在使用されている一般的なキューの設定で、実際には。 各 NIC に、高度なプロパティでは、値の`*RssBaseProcNumber`と`*MaxRssProcessors`します。

システムのパフォーマンスを高めるいくつかの VMQ 設定を次に示します。

- 理想的に各 NIC が必要、`*RssBaseProcNumber`偶数を以上に設定の 2 つ (2)。 これは最初の物理プロセッサ コア 0 \(0 と 1 の論理プロセッサ\)、通常この物理プロセッサからネットワーク処理を送る必要があるために、システム処理の大部分を行います。 

>[!NOTE]
>一部のコンピューターのアーキテクチャは、ので、そのようなマシン ベースのプロセッサが 1 以上、物理プロセッサごとの 2 つの論理プロセッサを必要はありません。 不明な場合に、物理プロセッサのアーキテクチャごとの 2 つの論理プロセッサの使用には、ホストを想定しています。

- それが実用的で、重複しないする範囲内にチーム メンバー全員のプロセッサ必要があります。 たとえば、4 コアのホストで\(8 個の論理プロセッサ\)10 gbps の 2 つの Nic のチームが、2 の基本のプロセッサを使用して、4 つのコアを使用する最初の 1 つを設定できます。 2 つ目は基本プロセッサ 6 を使用し、2 コアの使用に設定されます。

## <a name="bkmk_hnv"></a>セットと HYPER-V ネットワーク仮想化\(HNV\)

セットは、Windows Server 2016 で HYPER-V ネットワーク仮想化の完全な互換性です。 HNV の管理システムでは、HNV トラフィック用に最適化された方法でネットワーク トラフィックの負荷を配布する設定は、セットのドライバーに情報を提供します。
  
## <a name="bkmk_live"></a>設定とライブ移行

ライブ マイグレーションは、Windows Server 2016 でサポートされます。

## <a name="bkmk_mac"></a>転送されたパケットの MAC アドレスの使用

動的な負荷分散により、1 つのソースからのパケットをセット チームを構成するとき\(など、単一の VM\)に同時に複数のチーム メンバー間で分散されます。 

スイッチが混乱するを防止し、MAC のひらひらとアラームを防ぐために次のように設定します。 ソース MAC アドレスを使用すると、関連付けられている所与のチーム メンバー以外のチーム メンバーに送信されるフレームで異なる MAC アドレスに置き換えます。 このため、各チーム メンバーが別の MAC アドレスを使用して、MAC アドレスの競合はしない限り、エラーが発生したためにできませんでした。

チーミング ソフトウェア セットを開始、一時のアフィニティを設定したチーム メンバーとして選択されているチーム メンバーに、VM の MAC アドレスを使用してプライマリ NIC で障害が検知されると、\(として、VM のスイッチに表示されるようになりましたもの、つまりインターフェイス\)します。

この変更は、MAC アドレスをソースとして VM の MAC アドレスを持つ VM のアフィニティを設定したチーム メンバーに送信するとしたトラフィックのみに適用されます。 その他のトラフィックは、どのようなソースは、障害発生前に使用した MAC アドレスと送信されます。

チームの構成方法に基づいて MAC アドレスの置き換え動作のチーム化のセットを記述する一覧を以下にします。

- HYPER-V ポート分布でスイッチに依存しないモードで

    - 各 vmSwitch ポートが、チーム メンバーに関連付けられます
  
    - ポートが関連付けられ、そのチーム メンバーにすべてのパケットを送信します。  
  
    - ソース MAC の置換は行われません  
  
- スイッチに依存しないモード動的配布と
  
    - 各 vmSwitch ポートが、チーム メンバーに関連付けられます  
  
    - ARP/NS のすべてのパケットが、ポートが関連付けられ、そのチーム メンバーに送信されます。  
  
    - アフィニティを設定したチーム メンバーは、チーム メンバーに送信されるパケットがソース MAC アドレスの置き換えが行われますを持っていません  
  
    - アフィニティを設定したチーム メンバー以外のチーム メンバーに送信されるパケットがソース MAC アドレスの置換が完了には  
  
## <a name="bkmk_manage"></a>セット チームを管理します。

System Center Virtual Machine Manager を使用することをお勧め\(VMM\)セットを管理するチームは、ただしできますも Windows PowerShell を使用して設定を管理します。 次のセクションでは、Windows PowerShell コマンド セットの管理に使用できるを提供します。

VMM を使用して、チームのセットを作成する方法については、System Center VMM ライブラリのトピックの「論理スイッチのセットアップ」セクションを参照してください[論理スイッチを作成](https://docs.microsoft.com/system-center/vmm/network-switch)です。
  
### <a name="create-a-set-team"></a>セット チームを作成します。

使用して、HYPER-V 仮想スイッチを作成するのと同時に、セット チームを作成する必要があります、 **New-vmswitch** Windows PowerShell コマンド。

HYPER-V 仮想スイッチを作成するときに、新しいあります**EnableEmbeddedTeaming**コマンドの構文のパラメーター。 HYPER-V スイッチでは、次の例では、名前**TeamedvSwitch**埋め込みチーミングと 2 つの初期のチーム メンバーが作成されます。
  
```  
New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 2" -EnableEmbeddedTeaming $true  
```  
  
**EnableEmbeddedTeaming**パラメーターは Windows PowerShell によってと見なされますときに引数**NetAdapterName**は 1 つの nic ではなく Nic の配列です。 その結果、次のように前のコマンドを変更する可能性があります。

```  
New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 2"  
```  

作成する場合は、セットに対応したスイッチと 1 つのチーム メンバーは後で、チーム メンバーを追加できるように EnableEmbeddedTeaming パラメーターを使用する必要があります。

```  
New-VMSwitch -Name TeamedvSwitch -NetAdapterName "NIC 1" -EnableEmbeddedTeaming $true  
```  

### <a name="adding-or-removing-a-set-team-member"></a>追加または SET チーム メンバーを削除します。

**セット VMSwitchTeam**コマンドが含まれています、 **NetAdapterName**オプション。 セット チームのチーム メンバーを変更するには、後のチーム メンバーの目的のリストを入力、 **NetAdapterName**オプション。 場合**TeamedvSwitch**最初に作成した NIC 1 と NIC 2 では、次のコマンド例チーム メンバーのセット"2 NIC"が削除され、新しいセット チームのメンバーを追加します"NIC 3"。
  
```  
Set-VMSwitchTeam -Name TeamedvSwitch -NetAdapterName "NIC 1","NIC 3"  
```  

### <a name="removing-a-set-team"></a>セットのチームを削除します。

セット チームを削除するには、セット チームを含む、HYPER-V 仮想スイッチを削除します。  トピックを使用して[Remove-vmswitch](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/remove-vmswitch)については、HYPER-V 仮想スイッチを削除する方法。 次の例では、という名前の仮想スイッチを削除する**では、SETvSwitch**します。

```  
Remove-VMSwitch "SETvSwitch"  
```  

### <a name="changing-the-load-distribution-algorithm-for-a-set-team"></a>セット チームの負荷分散アルゴリズムを変更します。

**セット VMSwitchTeam**コマンドレットは、 **LoadBalancingAlgorithm**オプション。 このオプションは、2 つの値のいずれかを取ります。**HyperVPort**または**動的**します。 を設定またはスイッチに組み込まれたチームの負荷分散アルゴリズムを変更するには、このオプションを使用します。 

次の例では、VMSwitchTeam が名前付き**TeamedvSwitch**を使用して、**動的**負荷分散アルゴリズム。  
```  
Set-VMSwitchTeam -Name TeamedvSwitch -LoadBalancingAlgorithm Dynamic  
```  
### <a name="affinitizing-virtual-interfaces-to-physical-team-members"></a>仮想インターフェイス物理チーム メンバーに関係付けることができます。

セットでは、仮想インターフェイス間のアフィニティを作成できます。\(つまり、Hyper-v 仮想スイッチ ポート\)物理 Nic チーム内の 1 つ。 

などを作成する場合は、2 つのホスト Vnic の SMB\-ダイレクト」のセクションでは、 [SET と RDMA Vnic で HYPER-V 仮想スイッチを作成する](#bkmk_set-rdma)、2 つの Vnic が別のチーム メンバーを使用することを確認することができます。 

そのセクション内スクリプトに追加すると、次の Windows PowerShell コマンドを使用できます。

    Set-VMNetworkAdapterTeamMapping -VMNetworkAdapterName SMB_1 –ManagementOS –PhysicalNetAdapterName “SLOT 2”
    Set-VMNetworkAdapterTeamMapping -VMNetworkAdapterName SMB_2 –ManagementOS –PhysicalNetAdapterName “SLOT 3”

このトピックでの 4.2.5」セクションで詳しく調べて、 [Windows Server 2016 の NIC とスイッチ埋め込みチーミング ユーザー ガイド](https://gallery.technet.microsoft.com/Windows-Server-2016-839cb607?redir=0)します。
