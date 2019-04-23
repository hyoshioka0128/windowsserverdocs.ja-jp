---
title: Virtual Receive Side Scaling (vRSS)
description: Windows Server および VM で複数の論理プロセッサ コア間で負荷を受信ネットワーク トラフィックを分散する仮想ネットワーク アダプターを構成する方法は、仮想 Receive Side Scaling (vRSS) について説明します。 ホストの複数の物理コアを構成することもできます。 仮想ネットワーク インターフェイス カード (vNIC)。
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 9be477b3-f81d-4e84-a6b0-ac4c1ea97715
ms.date: 09/05/2018
ms.localizationpriority: medium
manager: dougkim
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0c1cb11cb8ce69463a31cfa5061290f79d8dda91
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875233"
---
# <a name="virtual-receive-side-scaling-vrss"></a>仮想 Receive Side Scaling \(vRSS\)

>適用対象:Windows Server 2016 の Windows Server (半期チャネル)

このトピックでは、仮想 Receive Side Scaling (vRSS) および VM で複数の論理プロセッサ コア間で負荷を受信ネットワーク トラフィックを分散する仮想ネットワーク アダプターを構成する方法について説明します。 ホストの複数の物理コアを構成する、vRSS を使用することもできます。 仮想ネットワーク インターフェイス カード\(vNIC\)します。

この構成により、負荷分散される仮想マシンで複数の仮想プロセッサの仮想ネットワーク アダプターから\(VM\)より多くのネットワーク トラフィックを 1 つをより迅速に処理する VM を許可します。論理プロセッサ。

>[!TIP]
>VRSS を使用するにはハイパースレッディング上の Vm で\-を複数のプロセッサ、1 つの複数のコア プロセッサを持つ V ホストまたは複数のコア プロセッサがインストールされ構成された VM を使用する 1 つ以上。

vRSS は他のすべてのハイパースレッディングと互換性のある\-V ネットワーク テクノロジ。 vRSS は仮想マシン キューに依存\(VMQ\) Hyper で\-V ホストとホスト vNIC のまたは VM で RSS です。

既定では vRSS、により、Windows Server が Windows PowerShell を使用して、VM で無効ことができます。 詳細については、次を参照してください。[管理 vRSS](vrss-manage.md)と[RSS および vRSS 用 Windows PowerShell コマンド](vrss-wps.md)します。



## <a name="operating-system-compatibility"></a>オペレーティング システムの互換性

RSS は、任意のマルチプロセッサまたはマルチコア コンピューターまたはマルチプロセッサまたはマルチコア VM - Windows Server 2016 を実行しているで vRSS で使用できます。

マルチプロセッサまたはマルチコア次の Microsoft オペレーティング システムを実行している Vm も vRSS をサポートします。

- Windows Server 2016
- Windows 10 Pro または Enterprise
- Windows Server 2012 R2
- Windows 8.1 Pro または Enterprise
- Windows Server 2012 R2 の統合コンポーネントがインストールされた Windows Server 2012。
- Windows 8、Windows Server 2012 R2 統合コンポーネントがインストールされているとします。

ゲスト オペレーティング システムとして、HYPER-V で FreeBSD または Linux を実行する仮想マシンに対する vRSS のサポートについては、次を参照してください。 [Windows 上の Hyper-v ではサポートされている Linux および FreeBSD の仮想マシン](https://docs.microsoft.com/windows-server/virtualization/hyper-v/Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows)します。
  
## <a name="hardware-requirements"></a>ハードウェア要件

VRSS のハードウェア要件を次に示します。
 
- 物理ネットワーク アダプターが仮想マシン キューをサポートする必要があります\(VMQ\)します。 VRSS が、ハイパースレッディングを無効になっているかどうかは、VMQ が無効またはサポートされていない、\-V ホストとホストで構成されているすべての Vm。
- ネットワーク アダプターは、10 Gbps のリンク速度以上が必要です。
- ハイパー\-V ホストは、複数のプロセッサまたは少なくとも 1 つのマルチで構成する必要があります\-コア vRSS を使用するプロセッサ。
- 仮想マシン\(Vm\) 2 つ以上の論理プロセッサを使用するように構成する必要があります。


## <a name="use-case-scenarios"></a>ユース ケース シナリオ

次の 2 つのユース ケース シナリオは、vRSS プロセッサの負荷分散とソフトウェアの負荷分散の一般的な使用方法を示しています。

### <a name="processor-load-balancing"></a>プロセッサの負荷分散
  
Anthony は、ネットワーク管理者は、単一ルート入出力仮想化をサポートする 2 つのネットワーク アダプターで新しい HYPER-V ホストをセットアップしている\(SR\-IOV\)します。 彼は、Windows Server 2016 VM のファイル サーバーをホストにデプロイします。

ハードウェアとソフトウェアをインストールした後は、Anthony は、8 つの仮想プロセッサを使用する VM と 4096 MB のメモリを構成します。 残念ながら、Anthony には記憶域レプリカを有効にするオプションがない\-IOV 彼の Vm は、ハイパースレッディングで作成した仮想スイッチを通じてポリシーの適用に依存するので\-仮想スイッチの V マネージャー。 このため、Anthony は記憶域レプリカではなく vRSS を使用する決定\-IOV します。

最初に、Anthony は、vRSS で使用できるように Windows PowerShell を使用して 4 つの仮想プロセッサを割り当てます。 1 週間後、ファイル サーバーの使用は、非常に一般的になるため、Anthony は、VM のパフォーマンスを確認します。 表示されていました。  彼は、次の 4 つの仮想プロセッサを最大限に利用します。

このため、Anthony は、vRSS で使用するため、VM にプロセッサを追加するが決定します。  彼は、大きなネットワーク負荷の処理に役立つ vRSS を自動的に利用すると、VM に 2 つの仮想プロセッサを割り当てます。 作業は、ネットワーク トラフィックの負荷を効率的に処理する 6 つのプロセッサを搭載した VM のファイル サーバーのパフォーマンスが向上結果します。


### <a name="software-load-balancing"></a>ソフトウェア負荷分散

ある Sandra は、ネットワーク管理者は、ソフトウェア ロード バランサーとして機能するシステムのいずれかで 1 つの高パフォーマンス VM の設定は。 使用可能なすべての論理プロセッサは、この 1 つの VM に割り当てられた彼女が。

Windows Server をインストールすると、彼女は、vRSS を使用、VM 内の複数の論理プロセッサで処理を並列のネットワーク トラフィックを取得します。 Windows Server では、vRSS できますが、構成変更を加える Sandra はありません。


## <a name="related-topics"></a>関連トピック

- [VRSS の使用を計画します。](vrss-plan.md)
- [仮想ネットワーク アダプターで vRSS を有効にします。](vrss-enable.md)
- [VRSS を管理します。](vrss-manage.md)
- [vRSS よく寄せられる質問](vrss-faq.md)
- [RSS および vRSS 用 Windows PowerShell コマンド](vrss-wps.md)

---
