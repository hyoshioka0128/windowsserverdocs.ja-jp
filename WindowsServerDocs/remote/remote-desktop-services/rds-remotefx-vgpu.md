---
title: RDS - RemoteFX vGPU の設定と構成
description: RemoteFX vGPU グラフィックスの仮想化を構成するための計画情報。
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 03/23/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0263fa6b-2185-4cc3-99ef-3588e2f4ada5
author: lizap
manager: scottman
ms.openlocfilehash: 3e189d9ac059136b40d8ee5d93a4eea5b788cdd1
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70870850"
---
# <a name="set-up-and-configure-remotefx-vgpu-for-remote-desktop-services"></a>リモート デスクトップ サービスに RemoteFX vGPU をセットアップして構成


RemoteFX の vGPU 機能を利用すると、複数の仮想マシンが物理グラフィックス アダプターを共有できるようになります。 仮想マシンによって、グラフィックス情報のレンダリングをプロセッサから専用グラフィックス アダプターにオフロードできます。 これで CPU 負荷が軽減され、VDI 仮想マシンで実行されるグラフィックスを多用するワークロードのスケーラビリティが向上します。 

## <a name="remotefx-vgpu-requirements"></a>RemoteFX vGPU の要件

ホスト システムの要件: 

- Windows Server 2016 または Windows 10
- WDDM 1.2 互換ドライバーを搭載した DX 11.0 互換 GPU 
- Windows Server RD 仮想化ホストの役割が有効 (Hyper-V の役割を有効にする) 
- SLAT (Second Level Address Translation) をサポートする CPU を搭載したサーバー 

ゲスト VM の要件:

- Windows Enterprise クライアント (Windows 7 Service Pack 1、Windows 8.1、Windows 10) または Windows Server (Windows Server 2012 R2 または Windows Server 2016) を実行しているゲスト VM。 その他の OS のサポートについては、[リモート デスクトップ サービスでのサポートされる構成](rds-supported-config.md)に関するページを参照してください。

ゲスト VM に関するその他の考慮事項:

- OpenGL および OpenCL の機能は、Windows 10 または Windows Server 2016 でのみ使用できます。  
- DirectX 11.0 は、Windows 8 以降のゲスト VM でのみ使用できます。 
- リモート デスクトップ セッション ホストは、[個人用セッション デスクトップ](rds-personal-session-desktops.md)として実行されている場合にのみ RemoteFX vGPU でサポートされます。

ゲスト VMS については、「[VDI 展開 - サポートされるゲスト OS](rds-supported-config.md#vdi-deployment--supported-guest-oss)」を必ず確認してください。

## <a name="install-remotefx-vgpu"></a>RemoteFX vGPU をインストールする

Windows Server 2016 および Windows 10 のホスト上で RemoteFX をインストールおよび構成するには、次の手順を使用します。

1. オペレーティング システムをインストールする。
2. グラフィックス カードのベンダー サイトから入手できる最新の Windows 10/Windows Server 2016 GPU ドライバーをインストールします。
3. Windows 10/Windows Server 2016 ホストに RemoteFX vGPU をインストールします。
   1. Windows 10 ホストで、コントロール パネルの Hyper-V 機能を有効にします ([コントロール パネル]、[プログラムと機能]、[Windows の機能の有効化または無効化] の順に移動します)。

      ![Hyper-V 機能を有効にするための Windows の機能ウィンドウ](media/rds-hyperv-settings.png)

   2. Windows Server 2016 ホストに、リモート デスクトップ仮想化ホスト (RDVH) の役割をインストールします。
   

4. 次にゲスト VM を作成して構成します。
   1. Windows 10 Enterprise または Windows Server 2016 で VM を作成します。
   2. RemoteFX 3D グラフィックス アダプターを追加します。 Hyper-V マネージャーまたは PowerShell コマンドレットを使用してこれを行う方法については、「[RemoteFX vGPU 3D アダプターを構成する](#configure-the-remotefx-vgpu-3d-adapter)」を参照してください。 

複数の GPU がある場合、RemoteFX vGPU ではすべての GPU が使用されます。 ただし、場合によっては、RemoteFX から使用される GPU が制限されることがあります。 Hyper-V 環境でこれを制御するには、RemoteFX が使用すべきでは "*ない*" GPU を具体的に選択します。 次の手順を使用します。 

   1. Hyper-V マネージャーで Hyper-V 設定に移動します。
   2. [Hyper-V の設定] で **[物理 GPU]** をクリックします。
   3. 使用しない GPU を選択し、 **[この GPU を RemoteFX で使用する]** をオフにします。


### <a name="configure-the-remotefx-vgpu-3d-adapter"></a>RemoteFX vGPU 3D アダプターを構成する
RemoteFX vGPU 3D グラフィックス アダプターを構成するには、Hyper-V マネージャーの UI または PowerShell コマンドレットを使用できます。 

#### <a name="through-hyper-v-manager"></a>Hyper-V マネージャーの使用:

1. システムが Hyper-V で設定され、VM が構成されていることを確認します。  
2. VM が実行中の場合は停止します。 
3. Hyper-V マネージャーで **[VM 設定]** に移動し、 **[ハードウェアの追加]** をクリックします。
4. **[RemoteFX 3D Graphics Adapter]\(RemoteFX 3D グラフィックス アダプター\)** を選択し、 **[追加]** をクリックします。 
5. 最大モニター数、最大モニター解像度、および専用ビデオ メモリを設定するか、既定値のままにします。

   > [!NOTE]
   > - これらのオプションのいずれかに高い値を設定すると、スケールに影響するため、絶対に必要なもののみを設定します。
   >
   > - 1 GB の専用 VRAM を使用する必要がある場合は、最高の結果を得るために 32 ビット (x86) ではなく 64 ビットのゲスト VM を使用します。
6. **[OK]** をクリックして構成を完了します。

#### <a name="with-powershell-cmdlets"></a>PowerShell コマンドレットの使用:

次のコマンドレットを実行して、アダプターを追加、確認、および構成します。 

```powershell
Add-VMRemoteFx3dVideoAdapter [-CimSession <CimSession[]>] [-ComputerName <String[]>] [-Credential <PSCredential[]>] [-VMName] <String[]> [-Passthru] [-WhatIf] [-Confirm] [<CommonParameters>]
```

詳細については、「[Add-VMRemoteFx3dVideoAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/add-vmremotefx3dvideoadapter)」を参照してください。

```powershell
Get-VMRemoteFx3dVideoAdapter [-CimSession <CimSession[]>] [-ComputerName <String[]>]  [-Credential <PSCredential[]>] [-VMName] <String[]> [<CommonParameters>]
```

詳細については、「[Get-VMRemoteFx3dVideoAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/get-vmremotefx3dvideoadapter)」を参照してください

```powershell
Set-VMRemoteFx3dVideoAdapter [-CimSession <CimSession[]>] [-ComputerName <String[]>] [-Credential <PSCredential[]>] [-VMName] <String[]> [[-MonitorCount] <Byte>] [[-MaximumResolution] <String>] [[-VRAMSizeBytes] <UInt64>] [-Passthru] [-WhatIf] [-Confirm] [<CommonParameters>]
```

詳細については、「[Set-VMRemoteFx3dVideoAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/set-vmremotefx3dvideoadapter)」を参照してください。

次のコマンドレットを実行して物理 GPU を確認します。

```powershell
Get-VMRemoteFXPhysicalVideoAdapter [-ComputerName <String[]>] [-Credential <PSCredential[]>] [[-Name] <String[]>] [<CommonParameters>]  
```

詳細については、「[Get-VMRemoteFXPhysicalVideoAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/get-vmremotefxphysicalvideoadapter)」を参照してください。

## <a name="monitor-performance"></a>パフォーマンスを監視する

VDI システムのパフォーマンスとスケールは、GPU の合計メモリ、システム メモリの量とメモリ速度、CPU コアの数と CPU クロック周波数、ストレージ速度、NUMA の実装など、さまざまな要因によって決まります。

RDS でのリモート vGPU のサポートには、次のパフォーマンス カウンターが含まれています。これらをパフォーマンス モニター (perfmon.exe) で表示して、フレーム レートのスループットに関する情報を収集できます。

- [RemoteFX Graphics]\(RemoteFX グラフィックス\) - リモート デスクトップ プロトコル グラフィックス圧縮用のカウンター。 たとえば、圧縮のために RDP に提示されているフレーム数を調べる場合は、 **[Input Frames/Second]\(入力フレーム/秒\)** カウンターを確認します。
- [RemoteFX Network]\(RemoteFX ネットワーク\) - リモート デスクトップ プロトコル ネットワーク トラフィックのカウンター。 たとえば、**往復時間 (RTT)** です。
- [RemoteFX Root GPU Management]\(RemoteFX ルート GPU 管理\) - 使用可能で予約済みの VRAM を測定します。
- [RemoteFX Software]\(RemoteFX ソフトウェア\) - キャプチャ レート、GPU 応答時間などのカウンターを提供します。

特にトラブルシューティングのために、より低レベルのパフォーマンス監視を行うには、次の追加のパフォーマンス カウンターを使用できます。

- RemoteFX Synth3D VSC VM Device (RemoteFX Synth3D VSC VM デバイス) 
- RemoteFX Synth3D VSC VM Transport Channel (RemoteFX Synth3D VSC VM トランスポート チャネル) 
- RemoteFX Synth3D VSP 
- RemoteFX Synth3D VSP VM Device (RemoteFX Synth3D VSP VM デバイス) 
- RemoteFX Synth3D VSP VM Channel (RemoteFX Synth3D VSP VM チャネル)
