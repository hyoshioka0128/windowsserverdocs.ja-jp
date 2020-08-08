---
title: Virtual Receive Side Scaling (vRSS)
description: Windows Server での仮想 Receive Side Scaling (vRSS) について説明します。また、仮想ネットワークアダプターを構成して、VM 内の複数の論理プロセッサコア間で着信ネットワークトラフィックを負荷分散する方法についても説明します。 また、ホスト仮想ネットワークインターフェイスカード (vNIC) の複数の物理コアを構成することもできます。
ms.topic: article
ms.assetid: 9be477b3-f81d-4e84-a6b0-ac4c1ea97715
ms.date: 09/05/2018
ms.localizationpriority: medium
manager: dougkim
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 135008db9f8a5f6b1238c18df64e89ed8c71180c
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955529"
---
# <a name="virtual-receive-side-scaling-vrss"></a>仮想 Receive Side Scaling \( vRSS\)

>適用先:Windows Server (半期チャネル)、Windows Server 2016

このトピックでは、仮想 Receive Side Scaling (vRSS) について説明します。また、仮想ネットワークアダプターを構成して、VM 内の複数の論理プロセッサコア間で着信ネットワークトラフィックを負荷分散する方法について説明します。 また、vRSS を使用して、ホスト仮想ネットワークインターフェイスカード vNIC の複数の物理コアを構成することもでき \( \) ます。

この構成により、仮想ネットワークアダプターからの負荷を仮想マシン VM の複数の仮想プロセッサに分散できるため \( \) 、vm は、1つの論理プロセッサを使用する場合よりも高速により多くのネットワークトラフィックを処理することができます。

>[!TIP]
>\-複数のプロセッサ、1つのマルチコアプロセッサ、または複数のコアプロセッサがインストールされ、vm で使用するように構成されている hyper-v ホスト上の vm では、vRSS を使用できます。

vRSS は、他のすべての Hyper-v ネットワークテクノロジと互換性が \- あります。 vRSS は、 \( \) \- VM またはホスト vNIC の HYPER-V ホストと RSS の仮想マシンキュー VMQ に依存しています。

既定では、Windows Server では vRSS が有効になりますが、Windows PowerShell を使用して VM で無効にすることができます。 詳細については、「 [RSS および vrss 用の vRSS および Windows PowerShell コマンドの](vrss-wps.md)[管理](vrss-manage.md)」を参照してください。



## <a name="operating-system-compatibility"></a>オペレーティング システムの互換性

RSS は、Windows Server 2016 を実行しているマルチプロセッサまたはマルチコアの VM 上のマルチプロセッサまたはマルチコアのコンピューターまたは vRSS で使用できます。

次の Microsoft オペレーティングシステムを実行しているマルチプロセッサまたはマルチコア Vm では、vRSS もサポートされています。

- Windows Server 2016
- Windows 10 Pro または Enterprise
- Windows Server 2012 R2
- Windows 8.1 Pro または Enterprise
- Windows server 2012 R2 統合コンポーネントがインストールされている windows Server 2012。
- Windows Server 2012 R2 統合コンポーネントがインストールされている windows 8。

Hyper-v でゲストオペレーティングシステムとして FreeBSD または Linux を実行する Vm の vRSS サポートの詳細については、「 [Windows 上の hyper-v でサポートされている Linux および FreeBSD 仮想マシン](https://docs.microsoft.com/windows-server/virtualization/hyper-v/Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows)」を参照してください。

## <a name="hardware-requirements"></a>ハードウェア要件

次に、vRSS のハードウェア要件を示します。

- 物理ネットワークアダプターは仮想マシンキュー VMQ をサポートする必要があり \( \) ます。 VMQ が無効になっているか、サポートされていない場合、Hyper-v \- ホストとホスト上に構成されているすべての vm に対して、vRSS は無効になります。
- ネットワークアダプターのリンク速度は 10 Gbps 以上である必要があります。
- \-複数のプロセッサまたは少なくとも1つのマルチコアプロセッサを使用して、vRSS を使用するように hyper-v ホストを構成する必要があり \- ます。
- 仮想マシン \( vm \) は、2つ以上の論理プロセッサを使用するように構成する必要があります。


## <a name="use-case-scenarios"></a>ユースケースシナリオ

次の2つのユースケースシナリオでは、プロセッサの負荷分散とソフトウェアの負荷分散のための vRSS の一般的な使用方法を示しています。

### <a name="processor-load-balancing"></a>プロセッサの負荷分散

ネットワーク管理者である Anthony は、1つのルート入出力仮想化 SR Sr-iov をサポートする2つのネットワークアダプターを備えた新しい Hyper-v ホストをセットアップしてい \( \- \) ます。 Windows Server 2016 をデプロイして、VM ファイルサーバーをホストします。

ハードウェアとソフトウェアをインストールした後、Anthony は8個の仮想プロセッサと 4096 MB のメモリを使用するように VM を構成します。 残念ながら、Anthony には、 \- Hyper-v 仮想スイッチマネージャーを使用して作成した仮想スイッチを通じて、vm がポリシーの適用に依存しているため、sr-iov を有効にするオプションはありません \- 。 このため、Anthony は、sr-iov ではなく、vRSS を使用することを決定し \- ます。

最初に、Anthony は、Windows PowerShell を使用して4つの仮想プロセッサを割り当てて、vRSS で使用できるようにします。 1週間後にファイルサーバーを使用することは非常に一般的なものであるため、Anthony は VM のパフォーマンスをチェックします。  4つの仮想プロセッサの全使用を検出します。

このため、Anthony は、vRSS で使用するためにプロセッサを VM に追加することを決定します。  VM に2つ以上の仮想プロセッサを割り当てます。これは、大きなネットワーク負荷の処理に役立つように、自動的に vRSS で利用できます。 彼の取り組みにより、VM ファイルサーバーのパフォーマンスが向上し、6つのプロセッサでネットワークトラフィックの負荷が効率的に処理されるようになります。


### <a name="software-load-balancing"></a>ソフトウェア負荷分散

ネットワーク管理者である Sandra は、1つのシステム上に1つの高パフォーマンス VM をセットアップし、ソフトウェアロードバランサーとして機能します。 この単一 VM には、使用可能なすべての論理プロセッサが割り当てられています。

Windows Server をインストールした後は、vRSS を使用して、VM 内の複数の論理プロセッサ上で並列ネットワークトラフィックを処理します。 Windows Server では vRSS が有効になっているため、Sandra では構成を変更する必要はありません。


## <a name="related-topics"></a>関連トピック

- [VRSS の使用を計画する](vrss-plan.md)
- [Virtual Network アダプターでの vRSS の有効化](vrss-enable.md)
- [vRSS の管理](vrss-manage.md)
- [vRSS に関してよく寄せられる質問](vrss-faq.md)
- [RSS および vRSS 用の Windows PowerShell コマンド](vrss-wps.md)

---
