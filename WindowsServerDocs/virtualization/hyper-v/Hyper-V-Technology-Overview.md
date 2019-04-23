---
title: HYPER-V テクノロジの概要
description: HYPER-V はについて説明します、主要な機能、および一般的な使用法を取得する方法。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ac069fed-7bf5-4cc3-aff5-25a2766040b8
author: KBDAzure
ms.author: kathydav
ms.date: 11/29/2016
ms.openlocfilehash: 9ae3c9dce36ad7d67a19ce167c9cb875b3c91810
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864313"
---
# <a name="hyper-v-technology-overview"></a>HYPER-V テクノロジの概要

>適用先:Windows Server 2016、Microsoft HYPER-V Server 2016、Windows Server 2019、Microsoft HYPER-V Server 2019

HYPER-V は、Microsoft のハードウェア仮想化製品です。 作成しと呼ばれる、コンピューターのソフトウェア バージョンを実行することができます、*仮想マシン*します。 各仮想マシンは、オペレーティング システムとプログラムを実行する、完全なコンピューターのように機能します。 コンピューティング リソースを必要があるときに仮想マシンは、柔軟性が向上、時間とコストを節約でき、同じ物理ハードウェア上で 1 つのオペレーティング システムを実行するよりもハードウェアを使用するより効率的な方法です。

HYPER-V は、同時に同じハードウェア上で 1 つ以上の仮想マシンを実行することを意味する独自の独立した領域で各仮想マシンを実行します。 このまたは他のワークロードに影響を与えるクラッシュなどの問題を避けるために、さまざまなシステムに別のユーザー、グループ、またはサービスのアクセス権を付与する可能性があります。

## <a name="some-ways-hyper-v-can-help-you"></a>いくつかの方法、HYPER-V が役立つ

HYPER-V には、するのに役立ちます。

- **確立またはプライベート クラウド環境を拡大します。** 移動または共有リソースの使用を拡張してより柔軟で、オンデマンドの IT サービスを提供し、需要の変化に使用率を調整します。

- **ご使用のハードウェアをより効果的に使用します。** サーバーとワークロードをより少ない電源と物理領域を使用するより少ないより強力な物理コンピューターに統合します。

- **ビジネス継続性を向上します。** ワークロードのおよび予定外のダウンタイムの影響を最小限に抑えます。

- **確立または仮想デスクトップ インフラストラクチャ (VDI) を展開します。** Vdi の一元化されたデスクトップ戦略の使用は、ビジネスの機敏性とデータのセキュリティを向上させるだけでなく法令遵守を簡素化およびデスクトップ オペレーティング システムとアプリケーションの管理に役立ちます。 個人用仮想デスクトップまたは仮想デスクトップ プールをユーザーに使用できるようにする同じサーバー上の Hyper-v ホストとリモート デスクトップ仮想化ホスト (RD 仮想化ホスト) をデプロイします。

- **開発を行いより効率的にテストします。** 購入や保守が必要になりますのみ、物理システムを使用した場合、すべてのハードウェアをしなくても、異なるコンピューティング環境を再現します。

## <a name="hyper-v-and-other-virtualization-products"></a>Hyper-v ホストとその他の仮想化製品

Windows および Windows Server HYPER-V では、Microsoft Virtual PC、Microsoft Virtual Server、Windows Virtual PC などの古いハードウェア仮想化製品が置き換えられます。 HYPER-V には、これらの古い製品では使用できないネットワーク、パフォーマンス、ストレージ、およびセキュリティの機能が提供されます。

Hyper-v ホストと同じプロセッサ機能を必要とするほとんどのサード パーティ製の仮想化アプリケーションは、互換性がありません。 ハードウェア仮想化拡張機能と呼ばれる、プロセッサの機能は、共有できないためにです。 詳細については、次を参照してください。[仮想化アプリケーションは、Hyper-v、Device Guard、Credential Guard とは動作しません](https://support.microsoft.com/kb/3204980)します。

## <a name="what-features-does-hyper-v-have"></a>HYPER-V には、どのような機能はありますか。

HYPER-V では、多くの機能を提供します。 これは、概要については、機能が提供または操作に役立つどのようなグループ化します。

**コンピューティング環境**-A HYPER-V 仮想マシンには、メモリ、プロセッサ、ストレージ、およびネットワー キングなどの物理コンピューターと同じ基本的なパーツが含まれています。 これらすべての部分がある機能とオプションのさまざまなニーズを満たすためにさまざまな方法を構成することができます。 記憶域やネットワーク見なすことができるそれぞれ独自のカテゴリ、さまざまな方法により、それらを構成できます。

**ディザスター リカバリーとバックアップ**-ディザスター リカバリーを HYPER-V レプリカは、コピーから、仮想マシンを復元できるように、別の物理的な場所に格納するためのもので、仮想マシンのコピーを作成します。 バックアップの場合は、HYPER-V は、2 つの型を提供します。 いずれかで保存された状態が使用して、VSS をサポートするプログラムのアプリケーション整合性バックアップを作成するため、ボリューム シャドウ コピー サービス (VSS) を使用して、その他

**最適化**-各サポートされているゲスト オペレーティング システムが、カスタマイズされた一連のサービスとドライバーと呼ばれる*統合サービス*、簡単に、HYPER-V 仮想マシンでオペレーティング システムを使用するようにします。

**移植性**- などの機能のライブ マイグレーション、記憶域の移行し、インポート/エクスポートでは、移動、または仮想マシンの配布に簡単です。

**リモート接続**-HYPER-V には仮想マシンの接続、Windows と Linux の両方で使用するためのリモート接続ツールが含まれています。 リモート デスクトップでこのツールで、アクセスのコンソールは、ご覧のようで起きているゲスト オペレーティング システムがまだ起動されていない場合でもです。

**セキュリティ**-マルウェアやその他の不正アクセス、仮想マシンとそのデータをセキュリティで保護された boot とシールドされた仮想マシンを保護します。

このバージョンで導入された機能の概要については、次を参照してください。[新機能については、Hyper-v で Windows Server](What-s-new-in-Hyper-V-on-Windows.md)します。 一部の機能やパーツが構成されている数に制限があります。 詳細については、次を参照してください。[の Windows Server 2016 で Hyper-v のスケーラビリティの計画](plan/Plan-for-Hyper-V-scalability-in-Windows-Server-2016.md)します。

## <a name="how-to-get-hyper-v"></a>HYPER-V を取得する方法

X64 の使用可能なサーバーの役割として HYPER-V は Windows Server および Windows では、使用可能なバージョンの Windows Server。 サーバーの手順については、次を参照してください。 [Windows server、Hyper-v の役割をインストール](get-started/Install-the-Hyper-V-role-on-Windows-Server.md)します。 として使用できますが、Windows で[機能](https://docs.microsoft.com/virtualization/hyper-v-on-windows/index)64 ビット バージョンの Windows でします。 ダウンロード可能なスタンドアロンのサーバー製品で使用可能なも[Microsoft HYPER-V Server](https://www.microsoft.com/evalcenter/evaluate-hyper-v-server-2019)します。

## <a name="supported-operating-systems"></a>サポートされるオペレーティング システム

多くのオペレーティング システムは、仮想マシンで実行されます。 一般に、オペレーティング システムを使用する、x86 アーキテクチャは、HYPER-V 仮想マシンで実行されます。 実行できるすべてのオペレーティング システムがテストされ、ただし、Microsoft によってサポートされています。 サポートされている機能の一覧を参照してください。

- [Windows 上の HYPER-V ではサポートされている Linux および FreeBSD 仮想マシン](Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)

- [Windows server、HYPER-V 用の Windows ゲスト オペレーティング システムがサポートされています。](Supported-Windows-guest-operating-systems-for-Hyper-V-on-Windows.md)

## <a name="how-hyper-v-works"></a>HYPER-V のしくみ

HYPER-V は、ハイパーバイザー ベースの仮想化テクノロジです。 HYPER-V では、特定機能を持つ物理プロセッサを必要とする Windows ハイパーバイザーを使用します。 ハードウェアの詳細については、次を参照してください。 [Windows server、Hyper-v のシステム要件](System-requirements-for-Hyper-V-on-Windows.md)します。

ほとんどの場合は、ハイパーバイザーはハードウェアと仮想マシン間の相互作用を管理します。 このハイパーバイザー制御のアクセス、ハードウェアには、実行される分離された環境の仮想マシンを示します。 一部の構成で仮想マシンまたは仮想マシンで実行されているオペレーティング システムは、グラフィックス、ネットワーク、または記憶域のハードウェアに直接アクセスを持っています。

## <a name="what-does-hyper-v-consist-of"></a>HYPER-V が構成しますか。

HYPER-V を作成して仮想マシンを実行できるように連携する部分が必要です。 同時に、これらの部分は、仮想化プラットフォームと呼ばれます。 セットとしてインストールされている HYPER-V の役割をインストールするときにします。 必要な部分は、Windows ハイパーバイザー、HYPER-V 仮想マシン管理サービス、仮想化 WMI プロバイダーを仮想マシン バス (VMbus)、仮想化サービス プロバイダー (VSP) および仮想インフラストラクチャ ドライバー (VID)。

HYPER-V では、管理および接続するためのツールもあります。 同じコンピューターで HYPER-V ロールがインストールされている、およびコンピューター上で HYPER-V ロールをインストールせずにこれらをインストールすることができます。 これらのツールは次のとおりです。

- Hyper-V マネージャー
- [Windows PowerShell 用 HYPER-V モジュール](https://docs.microsoft.com/powershell/module/hyper-v/index)
- [仮想マシン接続](https://docs.microsoft.com/windows-server/virtualization/hyper-v/learn-more/hyper-v-virtual-machine-connect) \(VMConnect とも呼ばれます。\)
- [Windows PowerShell ダイレクト](manage/Manage-Windows-virtual-machines-with-PowerShell-Direct.md)

## <a name="related-technologies"></a>関連テクノロジ

これらは、マイクロソフトの HYPER-V でよく使用されるいくつかのテクノロジ

- [フェールオーバー クラスタ リング](../../failover-clustering/whats-new-in-failover-clustering.md)
- [リモート デスクトップ サービス](../../remote/remote-desktop-services/Host-desktops-and-apps-in-Remote-Desktop-Services.md)
- [System Center Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/overview)

さまざまなストレージ テクノロジ: クラスターの共有ボリューム、SMB 3.0 では、記憶域スペース ダイレクト

Windows コンテナーは、仮想化する別のアプローチを提供します。 参照してください、 [Windows コンテナー](https://docs.microsoft.com/virtualization/windowscontainers/index) msdn ライブラリ。
