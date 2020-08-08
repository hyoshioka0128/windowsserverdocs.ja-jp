---
title: Windows Server での GPU アクセラレーションの計画
description: DDA や RemoteFX vGPU など、GPU アクセラレーション用のさまざまな Hyper-v テクノロジについて説明します。
ms.reviewer: rickman
author: rick-man
ms.author: rickman
manager: stevelee
ms.topic: article
ms.date: 07/14/2020
ms.openlocfilehash: 8cba3ac4d2e4680f480ff76db12c10553c1857d3
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87996958"
---
# <a name="plan-for-gpu-acceleration-in-windows-server"></a>Windows Server での GPU アクセラレーションの計画

> 適用対象: Windows Server 2016、Microsoft Hyper-V Server 2016、Windows Server 2019、Microsoft Hyper-V Server 2019

この記事では、Windows Server で使用できるグラフィックス仮想化機能について説明します。

## <a name="when-to-use-gpu-acceleration"></a>GPU アクセラレーションを使用する場合

ワークロードによっては、GPU アクセラレータを考慮する必要がある場合があります。 GPU アクセラレーションを選択する前に、次の点を考慮する必要があります。

- **アプリとデスクトップのリモート処理 (VDI/DaaS) ワークロード**: Windows Server を使用してアプリまたはデスクトップリモート処理サービスを構築している場合は、ユーザーが実行する予定のアプリのカタログを検討してください。 CAD/CAM アプリ、シミュレーションアプリ、ゲーム、レンダリング/視覚化アプリなど、一部の種類のアプリは、スムーズで応答性の高い対話機能を提供するために、3D レンダリングに大きく依存しています。 ほとんどのお客様は、これらの種類のアプリで適切なユーザーエクスペリエンスを実現するために Gpu を使用することを検討しています。
- **リモートでのレンダリング、エンコード、および視覚化ワークロード**: これらのグラフィック指向のワークロードは、コスト効果とスループットの目標を達成するために、効率的な3d レンダリングやフレームエンコード/デコードなど、GPU の特殊な機能に大きく依存する傾向があります。 この種類のワークロードでは、1つの GPU 対応 VM が、多くの CPU 専用 Vm のスループットと一致することができます。
- **HPC ワークロードと ML ワークロード**: ハイパフォーマンスコンピューティングおよび機械学習モデルのトレーニングや推論など、データ並列計算の高度なワークロードについては、gpu によって、結果への時間、推定時間、トレーニング時間が大幅に短縮されます。 また、同等のパフォーマンスレベルでは、CPU のみのアーキテクチャよりもコスト効果が高くなる可能性があります。 多くの HPC および機械学習フレームワークには、GPU アクセラレーションを有効にするオプションがあります。これが特定のワークロードにメリットをもたらす可能性があるかどうかを検討します。

## <a name="gpu-virtualization-in-windows-server"></a>Windows Server での GPU 仮想化

GPU 仮想化テクノロジは、仮想化された環境 (通常は仮想マシン内) で GPU アクセラレーションを有効にします。 ワークロードが Hyper-v で仮想化されている場合は、物理 GPU から仮想化されたアプリまたはサービスに GPU アクセラレーションを提供するために、グラフィックス仮想化を使用する必要があります。 ただし、ワークロードが物理的な Windows Server ホスト上で直接実行されている場合、グラフィックスの仮想化は不要です。アプリとサービスは、既に Windows Server でネイティブにサポートされている GPU 機能と Api にアクセスできます。

次のグラフィックス仮想化テクノロジは、Windows Server の Hyper-v Vm で使用できます。

- [個別のデバイスの割り当て (DDA)](#discrete-device-assignment-dda)
- [RemoteFX vGPU](#remotefx-vgpu)

Windows Server では、VM ワークロードに加えて、Windows コンテナー内のコンテナー化されたワークロードの GPU アクセラレーションもサポートしています。 詳細については、「 [Windows コンテナーの GPU 高速化](/virtualization/windowscontainers/deploy-containers/gpu-acceleration)」を参照してください。

## <a name="discrete-device-assignment-dda"></a>個別のデバイスの割り当て (DDA)

個別のデバイスの割り当て (DDA) は、GPU パススルーとも呼ばれ、1つまたは複数の物理 Gpu を1つの仮想マシンに専用にすることができます。 DDA デプロイでは、仮想化されたワークロードはネイティブドライバー上で実行され、通常は GPU の機能へのフルアクセスが可能です。 DDA は、最高レベルのアプリの互換性と潜在的なパフォーマンスを提供します。 DDA は、サポートの対象となる Linux Vm への GPU アクセラレーションも提供します。

DDA の展開では、仮想マシンの数を制限することができます。これは、各物理 GPU が最大1つの VM にアクセラレーションを提供できるためです。 共有仮想マシンをサポートするアーキテクチャを持つサービスを開発している場合は、VM ごとに複数の高速ワークロードをホストすることを検討してください。 たとえば、RDS でデスクトップリモート処理サービスを構築している場合、Windows Server のマルチセッション機能を利用して、各 VM で複数のユーザーデスクトップをホストすることにより、ユーザーの規模を向上させることができます。 これらのユーザーは、GPU アクセラレーションの利点を共有します。

詳細については、以下のトピックを参照してください。

- [個別のデバイス割り当ての展開の計画](plan-for-deploying-devices-using-discrete-device-assignment.md)
- [Discrete Device Assignment を使用したグラフィックス デバイスのデプロイ](../deploy/Deploying-graphics-devices-using-dda.md)

## <a name="remotefx-vgpu"></a>RemoteFX vGPU

> [!NOTE]
> セキュリティ上の問題のため、2020 年 7 月 14 日以降のセキュリティ更新プログラムでは、すべてのバージョンの Windows において RemoteFX vGPU は既定で無効になっています。 詳しくは、[KB 4570006](https://support.microsoft.com/help/4570006) をご覧ください。

RemoteFX vGPU は、1つの物理 GPU を複数の仮想マシン間で共有することを可能にするグラフィックス仮想化テクノロジです。 RemoteFX vGPU デプロイでは、仮想化されたワークロードは Microsoft の RemoteFX 3D アダプターで実行されます。これにより、ホストとゲスト間の GPU 処理要求が調整されます。 RemoteFX vGPU は、専用 GPU リソースを必要としない、ナレッジワーカーおよび高度なバーストワークロードに最適です。 RemoteFX vGPU では、Windows Vm への GPU アクセラレーションのみを行うことができます。

詳細については、以下のトピックを参照してください。

- [RemoteFX vGPU を使ったグラフィックス デバイスの展開](../deploy/deploy-graphics-devices-using-remotefx-vgpu.md)
- [RemoteFX 3D ビデオ アダプター (vGPU) のサポート](../../../remote/remote-desktop-services/rds-supported-config.md#remotefx-3d-video-adapter-vgpu-support)

## <a name="comparing-dda-and-remotefx-vgpu"></a>DDA と RemoteFX vGPU の比較

展開を計画する際には、次の機能を検討し、グラフィックス仮想化テクノロジ間の相違点をサポートします。

| 説明 | RemoteFX vGPU | 個別のデバイスの割り当て |
|--|--|--|
| GPU リソースモデル | 専用または共有 | 専用 |
| VM 密度 | 高 (1 つ以上の Gpu から多数の Vm) | 低 (1 つの VM に1つ以上の Gpu) |
| アプリの互換性 | DX 11.1、OpenGL 4.4、OpenCL 1.1 | ベンダーから提供されるすべての GPU 機能 (DX 12、OpenGL、CUDA) |
| AVC444 | 既定で有効 | 使用可能なグループポリシー |
| GPU VRAM | 最大 1 GB の専用 VRAM | GPU でサポートされている VRAM まで |
| フレーム レート | 最大 30 fps | 最大 60 fps |
| ゲスト内の GPU ドライバー | RemoteFX 3D アダプター ディスプレイ ドライバー (Microsoft) | GPU ベンダードライバー (NVIDIA、AMD、Intel) |
| ホスト OS のサポート | Windows Server 2016 | Windows Server 2016;Windows Server 2019 |
| ゲスト OS のサポート | Windows Server 2012 R2Windows Server 2016;Windows 7 SP1、Windows 8.1;Windows 10 | Windows Server 2012 R2Windows Server 2016;Windows Server 2019;Windows 10;マシン |
| ハイパーバイザー | Microsoft Hyper-V | Microsoft Hyper-V |
| GPU ハードウェア | エンタープライズ GPU (Nvidia Quadro/GRID または AMD FirePro) | エンタープライズ GPU (Nvidia Quadro/GRID または AMD FirePro) |
| サーバー ハードウェア | 特別な要件なし | 最新のサーバー、OS に IOMMU を公開 (通常は SR-IOV 準拠のハードウェア) |