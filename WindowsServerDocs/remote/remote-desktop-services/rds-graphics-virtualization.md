---
title: RDS - どちらのグラフィックス仮想化テクノロジが適切か
description: お使いの RDS 展開に適したグラフィックス仮想化オプションの選択に役立つ計画情報。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 03/16/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d6ff5b22-7695-4fee-b1bd-6c9dce5bd0e8
author: lizap
manager: scottman
ms.openlocfilehash: ce10575d38bccc0b22dadf55bd89156c6ce5ea7b
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871052"
---
# <a name="which-graphics-virtualization-technology-is-right-for-you"></a>どちらのグラフィックス仮想化テクノロジが適切か

リモート デスクトップ サービスでグラフィックス レンダリングを有効にする場合、さまざまなオプションがあります。 仮想化環境を計画する際に、次の考慮事項によって、どちらのグラフィックス レンダリング テクノロジを選択するかが決まります。

![グラフィックス レンダリングに関する考慮事項 - ユーザーの規模と GPU の要件を比較して、お使いの環境に最適な GPU テクノロジを判断します](media/rds-gpu.png)

Windows Server 2016 では、GPU ハードウェアを活用するための、Hyper-V で使用可能な 2 つのグラフィックス仮想化テクノロジがあります。

- [個別のデバイスの割り当て (DDA)](#discrete-device-assignment) - VM 内部でネイティブな GPU ドライバーのサポートを提供する VM 専用の 1 つ以上の GPU を使用して最高のパフォーマンスを得る場合。 サーバーで利用できる物理的な GPU の数によって制限されるので、密度は低いです。 
- [リモート FX vGPU](#remotefx-vgpu) - 複数の VM が準仮想化を通じて 1 つ以上の GPU を利用する、ナレッジ ワーカーおよび高バースト GPU シナリオの場合。 このソリューションでは、サーバーあたりのユーザー密度が高くなります。

次の図では、Windows Server 2016 のグラフィックス仮想化のオプションを示しています。

![RDS を使用した Windows Server 2016 のグラフィックス仮想化オプション - 使用可能な 3 つのテクノロジと、それらが規模とパフォーマンスについてどのように異なるかを示します](media/rds-graphics-virtualization.png)

## <a name="discrete-device-assignment"></a>個別のデバイスの割り当て
個別のデバイスの割り当て (DDA) は、VM がネイティブ ドライバーを使用して GPU にフル アクセスできる場合は、最高のパフォーマンスをもたらすハードウェア パススルー ソリューションです。 VM ユーザーは、デバイスのネイティブ ドライバーと同様、デバイスの全機能にアクセスできます。 つまり、VM 内のデバイスを実行する機能は、ベア メタルで同じデバイスを実行することを反映します。

DDA の詳細については、[個別のデバイスの割り当ての展開の計画](../../virtualization/hyper-v/plan/plan-for-deploying-devices-using-discrete-device-assignment.md)に関するページを参照してください。

## <a name="remotefx-vgpu"></a>RemoteFX vGPU 
RemoteFX vGPU は、ナレッジ ワーカー シナリオ (上記の最初の図を参照) を有効にするために、GPU の処理能力をさまざまなゲスト オペレーティング システムに分割可能にするグラフィックス仮想化テクノロジです。 Windows Server 2016 での進歩により、デザイナー アプリケーションやデータの可視化など、GPU バースト シナリオ用のさらなる機能強化が可能になっています。 その他の機能強化は次のとおりです。

- 第 2 世代のゲスト VM、Windows Server 2016 ゲスト VM、および Windows Client Hyper-V ホストのサポート。
  >[!NOTE] 
  > リモート デスクトップ セッション ホストは、Windows Server 2016 ゲスト VM ではサポートされていません。Windows Server 2016 ゲスト VM につき 1 セッションだけをホストできます。

- アプリケーションの互換性と安定性の向上。
- VM 接続拡張セッション モード。RemoteFX vGPU に対して有効になっている VM への VM 接続を通じた、USB とクリップボードのリダイレクトを可能にします。

詳細については、「[リモート デスクトップ サービスに RemoteFX vGPU をセットアップして構成](rds-remotefx-vgpu.md)」を参照してください。

## <a name="which-should-you-use"></a>どちらを使用すべきか

仮想化テクノロジの選択に関する重要な考慮事項は、お使いの環境でのハードウェアの仕様やアプリケーションの要件によって異なる場合があります。 DDA および RemoteFX vGPU の機能に関する簡単な表を次に示します。

| 機能               | RemoteFX vGPU                                                                       | 個別のデバイスの割り当て                                             |
|-----------------------|-------------------------------------------------------------------------------------|------------------------------------------------------------------------|
| デバイス GPU の割り当て | 準仮想化済み (多数の VM 対 1 つ以上の GPU)                                     | 1 つ以上の GPU 対 1 つの VM                                                  |
| Scale                 | 最適なスケール/1 つの GPU 対多数の VM                                                      | 低いスケール/1 つ以上の GPU 対 1 つの VM                                     |
| アプリの互換性     | DX 11.1、OpenGL 4.4、OpenCL 1.1                                                     | ベンダーから提供されるすべての GPU 機能 (DX 12、OpenGL、CUDA)          |
| AVC444                | 既定で有効 (Windows 10 および Windows Server 2016)                             | グループ ポリシーを通じて使用可能 (Windows 10 および Windows Server 2016)    |
| GPU VRAM              | 最大 1 GB の専用 VRAM                                                           | GPU でサポートされている VRAM まで                                        |
| フレーム レート            | 最大 30 fps                                                                         | 最大 60 fps                                                            |
| ゲスト内の GPU ドライバー   | RemoteFX 3D アダプター ディスプレイ ドライバー (Microsoft)                                      | GPU ベンダー ドライバー (Nvidia、AMD、Intel)                                 |
| ゲスト OS のサポート      |  Windows Server 2012 R2  Windows Server 2016  Windows 7 SP1  Windows 8.1 Windows 10 |  Windows Server 2012 R2  Windows Server 2016  Windows 10 Linux         |
| ハイパーバイザー            | Microsoft Hyper-V                                                                   | Microsoft Hyper-V                                                      |
| ホスト OS の可用性  |  Windows Server 2012 R2  Windows Server 2016 Windows 10                             | Windows Server 2016                                                    |
| GPU ハードウェア          | エンタープライズ GPU (Nvidia Quadro/GRID または AMD FirePro)                         | エンタープライズ GPU (Nvidia Quadro/GRID または AMD FirePro)            |
| サーバー ハードウェア       | 特別な要件なし                                                             | 最新のサーバー、OS に IOMMU を公開 (通常は SR-IOV 準拠のハードウェア) |

一般的な経験則としては、仮想マシンは GPU に直接アクセスできるので、アプリケーションの互換性を最適にするには DDA を使用します。 アプリケーションまたはワークロードに GPU の厳格な要件がなく、さらに広範なユーザー ベースに対応しようとする場合、RemoteFX vGPU が最適である可能性があります。