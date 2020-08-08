---
title: HYPER-V テクノロジの概要
description: Hyper-v とは何か、それを取得する方法、主な機能、および一般的な使用方法について説明します。
manager: dongill
ms.topic: article
ms.assetid: ac069fed-7bf5-4cc3-aff5-25a2766040b8
author: kbdazure
ms.author: kathydav
ms.date: 11/29/2016
ms.openlocfilehash: 2d69a16dc49c34872d3787338a1fd130aaf7241d
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997042"
---
# <a name="hyper-v-technology-overview"></a>HYPER-V テクノロジの概要

>適用先:Windows Server 2016、Microsoft Hyper-V Server 2016、Windows Server 2019、Microsoft Hyper-V Server 2019

Hyper-v は、Microsoft のハードウェア仮想化製品です。 これにより、*仮想マシン*と呼ばれるソフトウェアバージョンのコンピューターを作成および実行できます。 各仮想マシンは、オペレーティングシステムとプログラムを実行する完全なコンピューターのように機能します。 コンピューティングリソースが必要な場合、virtual machines を使用すると、柔軟性が向上し、時間とコストを節約できます。また、物理ハードウェア上で1つのオペレーティングシステムを実行するよりも、ハードウェアをより効率的に使用することができます。

Hyper-v では、各仮想マシンが独自の分離された領域で実行されるため、同じハードウェア上で複数の仮想マシンを同時に実行することができます。 これは、他のワークロードに影響を与えるクラッシュや、異なるユーザー、グループ、またはサービスに異なるシステムへのアクセスを許可するなどの問題を回避するために必要になる場合があります。

## <a name="some-ways-hyper-v-can-help-you"></a>Hyper-v が役に立ちます。

Hyper-v は、次のことを支援します。

- **プライベート クラウド環境の確立または拡大。** 共有リソースの使用を拡大したり拡張したり、需要の変化に応じて使用率を調整したりして、より柔軟なオンデマンドの IT サービスを提供します。

- **ハードウェアをより効果的に使用できます。** サーバーとワークロードをより少ない数の強力な物理コンピューターに統合することで、電力と物理領域を節約できます。

- **ビジネス継続性の向上。** ワークロードのスケジュールされたダウンタイムと予定外のダウンタイムの両方の影響を最小限に抑えます。

- **仮想デスクトップ インフラストラクチャ (VDI) の確立または拡大。** VDI で集中管理されたデスクトップ戦略を使用すると、ビジネスの機敏性とデータのセキュリティを向上させることができます。また、法令順守を簡素化し、デスクトップオペレーティングシステムとアプリケーションを管理することもできます。 個人用仮想デスクトップまたは仮想デスクトッププールをユーザーが使用できるようにするには、Hyper-v とリモートデスクトップ仮想化ホスト (RD 仮想化ホスト) を同じサーバーに展開します。

- **開発とテストの効率を高めます。** 物理システムのみを使用している場合は、必要なハードウェアを購入したり保守したりしなくても、さまざまなコンピューティング環境を再現できます。

## <a name="hyper-v-and-other-virtualization-products"></a>Hyper-v とその他の仮想化製品

Windows および Windows Server の hyper-v は、以前のハードウェア仮想化製品 (Microsoft Virtual PC、Microsoft Virtual Server、Windows Virtual PC など) に代わるものです。 Hyper-v では、これらの古い製品では利用できないネットワーク、パフォーマンス、ストレージ、およびセキュリティ機能を提供しています。

Hyper-v と、同じプロセッサの機能を必要とするほとんどのサードパーティの仮想化アプリケーションには互換性がありません。 これは、ハードウェア仮想化拡張機能と呼ばれるプロセッサ機能が共有されないように設計されているためです。 詳細については、「[仮想化アプリケーションが hyper-v、Device guard、および Credential guard と連携](https://support.microsoft.com/kb/3204980)して動作しない」を参照してください。

## <a name="what-features-does-hyper-v-have"></a>Hyper-v にはどのような機能がありますか。

Hyper-v には、多くの機能が用意されています。 これは、機能によって提供または支援される概要です。

**コンピューティング環境**-hyper-v 仮想マシンには、メモリ、プロセッサ、記憶域、ネットワークなど、物理コンピューターと同じ基本部分が含まれています。 これらのすべての部分には、さまざまなニーズを満たすためにさまざまな方法を構成できる機能とオプションがあります。 ストレージとネットワークは、さまざまな方法で構成できるため、それぞれが独自のカテゴリと考えることができます。

**ディザスターリカバリーとバックアップ**-ディザスターリカバリーのために、hyper-v レプリカは仮想マシンのコピーを作成します。これは別の物理的な場所に格納することを目的としています。そのため、仮想マシンをコピーから復元することができます。 バックアップの場合、Hyper-v では2種類が提供されます。 1つは保存された状態を使用し、もう1つはボリュームシャドウコピーサービス (VSS) を使用して、VSS をサポートするプログラムのアプリケーション整合性バックアップを作成できるようにします。

**最適化**-サポートされる各ゲストオペレーティングシステムには、*統合サービス*と呼ばれる、カスタマイズされたサービスとドライバーのセットがあり、hyper-v 仮想マシンでのオペレーティングシステムの使用が簡単になります。

**移植性**-ライブマイグレーション、記憶域の移行、インポート/エクスポートなどの機能により、仮想マシンを簡単に移動または配布することができます。

**リモート接続**-hyper-v には、Windows と Linux の両方で使用するリモート接続ツールである仮想マシン接続が含まれています。 リモートデスクトップとは異なり、このツールはコンソールへのアクセスを提供します。そのため、オペレーティングシステムがまだ起動していない場合でも、ゲストで何が起こっているかを確認できます。

**セキュリティ**-セキュアブートとシールドされた仮想マシンは、仮想マシンとそのデータへのマルウェアやその他の承認されていないアクセスから保護するのに役立ちます。

このバージョンで導入された機能の概要については、「 [Windows Server の hyper-v の新](What-s-new-in-Hyper-V-on-Windows.md)機能」を参照してください。 一部の機能やパーツには、構成できる数に制限があります。 詳細については、「 [Windows Server 2016 での hyper-v のスケーラビリティの計画](./plan/plan-hyper-v-scalability-in-windows-server.md)」を参照してください。

## <a name="how-to-get-hyper-v"></a>Hyper-v を取得する方法

Hyper-v は、windows server および Windows では、x64 バージョンの Windows Server で使用できるサーバーの役割として使用できます。 サーバーの手順については、「 [Windows server に hyper-v の役割をインストールする](get-started/Install-the-Hyper-V-role-on-Windows-Server.md)」を参照してください。 Windows では、一部の64ビットバージョンの Windows で[機能](/virtualization/hyper-v-on-windows/index)として使用できます。 また、ダウンロード可能なスタンドアロンサーバー製品である[Microsoft Hyper-V サーバー](https://www.microsoft.com/evalcenter/evaluate-hyper-v-server-2019)としても利用できます。

## <a name="supported-operating-systems"></a>サポートされるオペレーティング システム

多くのオペレーティングシステムは、仮想マシン上で実行されます。 一般に、x86 アーキテクチャを使用するオペレーティングシステムは、Hyper-v 仮想マシン上で実行されます。 ただし、実行できるすべてのオペレーティングシステムが Microsoft によってテストおよびサポートされているわけではありません。 サポートされる内容の一覧については、以下を参照してください。

- [Windows にインストールされた Hyper-v の Linux および FreeBSD 仮想マシンがサポートされています。](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)

- [Windows Server 上の Hyper-v でサポートされている Windows ゲストオペレーティングシステム](Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows.md)

## <a name="how-hyper-v-works"></a>Hyper-v の動作

Hyper-v は、ハイパーバイザーベースの仮想化テクノロジです。 Hyper-v では、特定の機能を搭載した物理プロセッサを必要とする Windows ハイパーバイザーを使用します。 ハードウェアの詳細については、「 [Windows Server の hyper-v のシステム要件](System-requirements-for-Hyper-V-on-Windows.md)」を参照してください。

ほとんどの場合、ハイパーバイザーはハードウェアと仮想マシン間の相互作用を管理します。 このハイパーバイザーによって制御されたハードウェアへのアクセスは、仮想マシンが実行される分離された環境を提供します。 一部の構成では、仮想マシンまたは仮想マシンで実行されているオペレーティングシステムが、グラフィックス、ネットワーク、または記憶域のハードウェアに直接アクセスできます。

## <a name="what-does-hyper-v-consist-of"></a>Hyper-v の構成要素

Hyper-v には、仮想マシンを作成して実行できるようにするために必要な部分があります。 これらの部分は、仮想化プラットフォームと呼ばれます。 これらは、Hyper-v の役割をインストールするときにセットとしてインストールされます。 必要な部分には、Windows ハイパーバイザー、Hyper-v 仮想マシン管理サービス、仮想化 WMI プロバイダー、仮想マシンバス (VMbus)、仮想化サービスプロバイダー (VSP)、仮想インフラストラクチャドライバー (VID) などがあります。

Hyper-v には、管理と接続のためのツールも用意されています。 これらは、Hyper-v の役割がインストールされているのと同じコンピューター、および Hyper-v の役割がインストールされていないコンピューターにインストールできます。 これらのツールは次のとおりです。

- Hyper-V マネージャーは
- [Windows PowerShell 用 Hyper-V モジュール](/powershell/module/hyper-v/index)
- [仮想マシン接続](./learn-more/hyper-v-virtual-machine-connect.md) \(VMConnect と呼ばれることもあります。\)
- [Windows PowerShell ダイレクト](manage/Manage-Windows-virtual-machines-with-PowerShell-Direct.md)

## <a name="related-technologies"></a>関連テクノロジ

次に、Hyper-v でよく使用される Microsoft のテクノロジをいくつか示します。

- [フェールオーバー クラスタリング](../../failover-clustering/whats-new-in-failover-clustering.md)
- [リモート デスクトップ サービス](../../remote/remote-desktop-services/welcome-to-rds.md)
- [System Center Virtual Machine Manager](/system-center/vmm/overview)

さまざまな記憶域テクノロジ: クラスターの共有ボリューム、SMB 3.0、記憶域スペースダイレクト

Windows コンテナーは、仮想化にもう1つのアプローチを提供します。 MSDN の[Windows コンテナー](/virtualization/windowscontainers/index)ライブラリを参照してください。