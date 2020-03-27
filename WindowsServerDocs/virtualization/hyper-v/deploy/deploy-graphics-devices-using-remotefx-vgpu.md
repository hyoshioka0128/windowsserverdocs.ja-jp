---
title: RemoteFX vGPU を使用してグラフィックスデバイスをデプロイする
description: Windows Server で RemoteFX vGPU をデプロイして構成する方法について説明します。
ms.prod: windows-server
ms.reviewer: rickman
author: rick-man
ms.author: rickman
manager: stevelee
ms.topic: article
ms.date: 08/21/2019
ms.openlocfilehash: 4ae185232ec39d92997929f8f916ff49caf26dcf
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/26/2020
ms.locfileid: "80310511"
---
# <a name="deploy-graphics-devices-using-remotefx-vgpu"></a>RemoteFX vGPU を使用してグラフィックスデバイスをデプロイする

> 適用対象: Windows Server 2016、Microsoft Hyper-V Server 2016

RemoteFX の vGPU 機能を使用すると、複数の仮想マシンが物理 GPU を共有できるようになります。 レンダリングとコンピューティングリソースは仮想マシン間で動的に共有されるため、専用 GPU リソースが必要ではない高バーストワークロードに適した RemoteFX vGPU になります。 たとえば、VDI サービスでは、RemoteFX vGPU を使用してアプリのレンダリングコストを GPU にオフロードできます。これにより、CPU の負荷が減少し、サービスのスケーラビリティが向上します。

## <a name="remotefx-vgpu-requirements"></a>RemoteFX vGPU の要件

ホストシステムの要件:

- Windows Server 2016
- WDDM 1.2 互換のドライバーを使用した DirectX 11.0 互換の GPU
- 第2レベルのアドレス変換 (SLAT) をサポートする CPU

ゲスト VM の要件:

- サポートされているゲスト OS。 詳細については、「 [RemoteFX 3D ビデオアダプター (vGPU) のサポート](../../../remote/remote-desktop-services/rds-supported-config.md#remotefx-3d-video-adapter-vgpu-support)」を参照してください。

ゲスト VM に関するその他の考慮事項:

- OpenGL および OpenCL 機能は、Windows 10 または Windows Server 2016 を実行しているゲストでのみ使用できます。  
- DirectX 11.0 は、Windows 8 以降を実行しているゲストでのみ使用できます。

## <a name="enable-remotefx-vgpu"></a>RemoteFX vGPU を有効にする

Windows Server 2016 ホストで RemoteFX vGPU を構成するには、次のようにします。

1. Windows Server 2016 の GPU ベンダーによって推奨されているグラフィックスドライバーをインストールします。
2. RemoteFX vGPU でサポートされているゲスト OS を実行している VM を作成します。 詳細については、「 [RemoteFX 3D ビデオアダプター (vGPU) のサポート](../../../remote/remote-desktop-services/rds-supported-config.md#remotefx-3d-video-adapter-vgpu-support)」を参照してください。
3. RemoteFX 3D グラフィックスアダプターを VM に追加します。 詳細については、「 [RemoteFX VGPU 3d アダプターの構成](#configure-the-remotefx-vgpu-3d-adapter)」を参照してください。

既定では、RemoteFX vGPU は使用可能なすべての Gpu を使用します。 RemoteFX vGPU が使用する Gpu を制限するには、次の手順を実行します。

1. Hyper-V マネージャーで Hyper-V 設定に移動します。
2. Hyper-v の設定 で **物理 gpu** を選択します。
3. 使用しない GPU を選択し、 **[この GPU を RemoteFX で使用する]** をオフにします。

### <a name="configure-the-remotefx-vgpu-3d-adapter"></a>RemoteFX vGPU 3D アダプターを構成する

RemoteFX vGPU 3D グラフィックス アダプターを構成するには、Hyper-V マネージャーの UI または PowerShell コマンドレットを使用できます。

#### <a name="configure-remotefx-vgpu-with-hyper-v-manager"></a>Hyper-v マネージャーを使用して RemoteFX vGPU を構成する

1. 現在実行中の場合は、VM を停止します。
2. Hyper-v マネージャーを開き、VM の **[設定]** に移動して、 **[ハードウェアの追加]** を選択します。
3. **[RemoteFX 3D グラフィックスアダプター]** を選択し、 **[追加]** を選択します。
4. 最大モニター数、最大モニター解像度、および専用ビデオ メモリを設定するか、既定値のままにします。

   > [!NOTE]
   > - これらのオプションのいずれかに高い値を設定するとサービスのスケールに影響するため、必要なもののみを設定する必要があります。
   > - 1 GB の専用 VRAM を使用する必要がある場合は、最適な結果を得るために32ビット (x86) ではなく、64ビットのゲスト VM を使用します。

5. **[OK]** を選択して構成を完了します。

#### <a name="configure-remotefx-vgpu-with-powershell-cmdlets"></a>PowerShell コマンドレットを使用して RemoteFX vGPU を構成する

次の PowerShell コマンドレットを使用して、アダプターを追加、確認、および構成します。

- [VMRemoteFx3dVideoAdapter](https://docs.microsoft.com/powershell/module/hyper-v/add-vmremotefx3dvideoadapter?view=win10-ps)
- [VMRemoteFx3dVideoAdapter](https://docs.microsoft.com/powershell/module/hyper-v/get-vmremotefx3dvideoadapter?view=win10-ps)
- [VMRemoteFx3dVideoAdapter](https://docs.microsoft.com/powershell/module/hyper-v/set-vmremotefx3dvideoadapter?view=win10-ps)
- [取得-VMRemoteFXPhysicalVideoAdapter](https://docs.microsoft.com/powershell/module/hyper-v/get-vmremotefxphysicalvideoadapter?view=win10-ps)

## <a name="monitor-performance"></a>パフォーマンスを監視する

RemoteFX vGPU が有効になっているサービスのパフォーマンスとスケールは、システム上の Gpu の数、合計 GPU メモリ、システムメモリとメモリ速度、CPU コア数と CPU クロック周波数、記憶域速度、NUMA などのさまざまな要因によって決まります。ション.

### <a name="host-system-memory"></a>ホストシステムメモリ

VGPU で有効になっているすべての VM について、RemoteFX はゲストオペレーティングシステムとホストサーバーの両方でシステムメモリを使用します。 ハイパーバイザーは、ゲストオペレーティングシステムのシステムメモリの可用性を保証します。 ホスト上で、vGPU が有効な各仮想デスクトップは、そのシステムのメモリ要件をハイパーバイザーに提供する必要があります。 VGPU が有効な仮想デスクトップが起動すると、ハイパーバイザーはホストに追加のシステムメモリを予約します。

Remotefx が有効になっているサーバーで消費されるメモリの量は、vGPU が有効な仮想デスクトップに関連付けられているモニターの数と、の最大解像度に依存しているため、RemoteFX が有効になっているサーバーのメモリ要件は動的です。これらのモニター。

### <a name="host-gpu-video-memory"></a>ホスト GPU ビデオメモリ

VGPU が有効なすべての仮想デスクトップでは、ホストサーバー上の GPU ハードウェアビデオメモリを使用してデスクトップがレンダリングされます。 さらに、コーデックはビデオメモリを使用して、レンダリングされた画面を圧縮します。 レンダリングと圧縮に必要なメモリの量は、仮想マシンに対してプロビジョニングされたモニターの数に直接基づいています。 予約されているビデオメモリの量は、システムの画面解像度とモニターの数によって異なります。 ユーザーによっては、特定のタスクに対して画面の解像度が高くなることがありますが、他のすべての設定が変わらない場合は、低い解像度の設定でスケーラビリティが向上します。

### <a name="host-cpu"></a>ホストの CPU

ハイパーバイザーは、CPU 上のホストと Vm をスケジュールします。 システムでは、vGPU が有効な仮想デスクトップごとに追加のプロセス (rdvgm) が実行されるため、RemoteFX 対応ホストのオーバーヘッドが増加します。 このプロセスでは、グラフィックスデバイスドライバーを使用して、GPU 上でコマンドを実行します。 また、コーデックは CPU を使用して、クライアントに送り返す必要がある画面データを圧縮します。

より多くの仮想プロセッサは、より優れたユーザーエクスペリエンスを意味します。 VGPU が有効な仮想デスクトップごとに少なくとも2つの仮想 Cpu を割り当てることをお勧めします。 また、vGPU が有効な仮想デスクトップには x64 アーキテクチャを使用することをお勧めします。 x64 仮想マシンでは、x86 仮想マシンと比較してパフォーマンスが向上するためです。

### <a name="gpu-processing-power"></a>GPU 処理能力

VGPU が有効なすべての仮想デスクトップには、ホストサーバーで実行される対応する DirectX プロセスがあります。 このプロセスでは、RemoteFX 仮想デスクトップから受信したすべてのグラフィックスコマンドが物理 GPU に再生されます。 これは、同じ物理 GPU で複数の DirectX アプリケーションを同時に実行するのと似ています。

通常、グラフィックスデバイスとドライバーは、デスクトップ上で一度に少数のアプリケーションのみを実行するようにチューニングされていますが、RemoteFX によってさらに多くの Gpu がストレッチされます。 vGPUs には、RemoteFX 要求に対する GPU 応答を測定するパフォーマンスカウンターが付属しています。また、Gpu があまり拡張されていないことを確認するのに役立ちます。

GPU のリソースが不足している場合、読み取りと書き込みの操作が完了するまでに時間がかかります。 管理者は、パフォーマンスカウンターを使用して、リソースを調整してユーザーのダウンタイムを回避するタイミングを知ることができます。

RemoteFX vGPU 動作を監視するためのパフォーマンスカウンターの詳細については、「[リモートデスクトップでのグラフィックスパフォーマンスの問題の診断」](https://docs.microsoft.com/azure/virtual-desktop/remotefx-graphics-performance-counters)を参照してください。
