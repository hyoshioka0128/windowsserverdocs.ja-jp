---
title: Virtual Receive Side Scaling (vRSS)
description: Windows Server とトラフィックの負荷分散着信ネットワーク VM で複数の論理プロセッサ コアを仮想ネットワーク アダプターを構成する方法、Virtual Receive Side Scaling (vRSS) について説明します。 ホストの複数の物理コアを構成することもできます。 仮想ネットワーク インターフェイス カード (vNIC)。
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
ms.sourcegitcommit: e84e328c13a701e8039b16a4824a6e58a6e59b0b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2018
ms.locfileid: "4133688"
---
# 仮想受信側 \(vRSS\) のスケーリング

>適用対象: Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、Virtual Receive Side Scaling (vRSS) とトラフィックの負荷分散着信ネットワーク VM で複数の論理プロセッサ コアを仮想ネットワーク アダプターを構成する方法について説明します。 ホストの仮想ネットワーク インターフェイス カード \(vNIC\) の複数の物理コアを構成するのに vRSS を使用することもできます。

この構成では、負荷分散される仮想マシンで複数の仮想プロセッサの仮想ネットワーク アダプターから \(VM\) より多くのネットワーク トラフィックを 1 つの論理プロセッサを搭載したことよりも迅速に処理する VM を許可します。

>[!TIP]
>Vm で vRSS を使用するには、1 つの複数のプロセッサが複数のコア プロセッサが hyper \-v ホストで複数のコア プロセッサがインストールされているし、VM 用に構成された 1 つ以上またはします。

vRSS は、その他の hyper \-v ネットワーク テクノロジはすべてと互換性が。 vRSS では、hyper \-v ホストの仮想マシンのキュー \(VMQ\) と RSS VM またはホスト vNIC に依存します。

既定では、Windows Server により、vRSS が Windows PowerShell を使用して VM で無効ことができます。 詳細については、[管理 vRSS](vrss-manage.md)し、 [RSS や vRSS 用の Windows PowerShell コマンド](vrss-wps.md)を参照してください。



## オペレーティング システムの互換性

任意のマルチプロセッサまたはマルチコア コンピューターまたは vRSS マルチプロセッサまたはマルチコア VM - Windows Server 2016 を実行しているのでは、RSS を使用できます。

マルチプロセッサまたはマルチコア以下の Microsoft のオペレーティング システムを実行している Vm も vRSS をサポートします。

- Windows Server 2016
- Windows 10 Pro または Enterprise
- Windows Server 2012 R2
- Windows 8.1 Pro または Enterprise
- Windows Server 2012 R2 の統合コンポーネントがインストールされた Windows Server 2012 です。
- Windows Server 2012 R2 の統合コンポーネントがインストールされた Windows 8 します。

HYPER-V でゲスト オペレーティング システムとして FreeBSD または Linux を実行して Vm の vRSS サポートについては、 [Windows 上の HYPER-V のサポートされる Linux と FreeBSD の仮想マシン](https://docs.microsoft.com/windows-server/virtualization/hyper-v/Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows)を参照してください。
  
## ハードウェア要件

VRSS のハードウェア要件を次に示します。
 
- 物理ネットワーク アダプターには、仮想マシンのキュー \(VMQ\) をサポートする必要があります。 VMQ が無効またはサポートされていない場合は、hyper \-v ホストとホストで構成されているすべての Vm の vRSS が無効です。
- ネットワーク アダプターは、10 gbps リンク速度以上が必要です。
- Hyper \-v ホストは、複数のプロセッサまたは vRSS を使用する 1 つ以上の multi\ コア プロセッサで構成する必要があります。
- 仮想マシン \(VMs\) は、2 つまたは複数の論理プロセッサを使用するように構成する必要があります。


## 使用事例

次の 2 つの使用事例では、プロセッサの負荷分散とソフトウェア負荷分散 vRSS の一般的な使用量を表します。

### プロセッサの負荷分散
  
仮想化の 1 つのルート入力出力 \(SR\-IOV\) をサポートする 2 つのネットワーク アダプターで、新しい HYPER-V ホストをアンソニー、ネットワーク管理者が設定されています。 彼は、VM のファイル サーバーをホストする Windows Server 2016 を展開します。

ハードウェアとソフトウェアをインストールした後は、アンソニーは、8 つの仮想プロセッサを使用する VM と 4096 MB のメモリを構成します。 残念ながら、アンソニーには、自分の Vm は、hyper \-v 仮想スイッチ マネージャーで作成した仮想スイッチを介したポリシーの適用に依存するために、SR\ IOV を有効にするオプションはありません。 このため、代わりに使う vRSS SR\ IOV アンソニーを決定します。

最初に、アンソニーは vRSS で使用するために利用可能な Windows PowerShell を使用して、4 つの仮想プロセッサを割り当てます。 1 週間後、ファイル サーバーの使用は、アンソニー VM のパフォーマンスを確認するために、非常に一般的に表示されます。  彼は、4 つの仮想プロセッサの完全な使用率を検出します。

このため、vRSS を使用するため、VM をプロセッサを追加するアンソニーを決定します。  彼は、vRSS 大規模なネットワークの負荷を処理するために自動的に提供すると、VM に 2 つ以上の仮想プロセッサを割り当てます。 作業が発生するネットワーク トラフィックの負荷を効率的に処理 6 つのプロセッサを搭載した VM ファイル サーバーのパフォーマンスが向上します。


### ソフトウェア負荷分散

平野、ネットワーク管理者は、ソフトウェア ロード バランサーとして動作する、1 つのパフォーマンスの高い VM を自分のシステムのいずれかの設定です。 この 1 つの VM には、利用可能なすべての論理プロセッサが割り当てられます。

Windows Server をインストールすると、彼女を使って vRSS VM 内の複数の論理プロセッサで処理並列のネットワーク トラフィックを取得します。 Windows Server では、vRSS できますが、構成を変更する平野はありません。


## 関連トピック

- [VRSS の使用を計画します。](vrss-plan.md)
- [仮想ネットワーク アダプターで vRSS を有効にします。](vrss-enable.md)
- [VRSS を管理します。](vrss-manage.md)
- [vRSS よく寄せられる質問](vrss-faq.md)
- [RSS および vRSS 用の Windows PowerShell コマンド](vrss-wps.md)

---
