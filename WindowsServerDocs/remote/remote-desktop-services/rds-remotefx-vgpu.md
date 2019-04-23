---
title: RDS で RemoteFX vGPU のセットアップと構成
description: RemoteFX vGPU グラフィックスの仮想化を構成する情報を計画します。
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
ms.openlocfilehash: 3e7da1a70826dc720a96ceb3fe5d04868943f163
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59876843"
---
# <a name="set-up-and-configure-remotefx-vgpu-for-remote-desktop-services"></a>リモート デスクトップ サービスに RemoteFX vGPU をセットアップして構成


RemoteFX vGPU 機能により、物理グラフィックス アダプターを共有する複数の仮想マシンのことです。 仮想マシンは、専用のグラフィックス アダプター、プロセッサからグラフィックス情報のレンダリングをオフロードできます。 CPU の負荷を軽減され、VDI の仮想マシンで実行されるグラフィックを多用するワークロードのスケーラビリティが向上します。 

## <a name="remotefx-vgpu-requirements"></a>RemoteFX vGPU の要件

ホスト システムの要件: 

- Windows Server 2016 または Windows 10
- WDDM 1.2 互換性のあるドライバーを使用した互換性のある GPU を DX 11.0 
- Windows Server の RD 仮想化ホスト ロールが有効になっている (Hyper-v の役割を有効に) 
- SLAT (第 2 レベルのアドレス変換) をサポートする CPU を持つサーバー 

ゲスト VM の要件:

- ゲスト VM が Windows エンタープライズ クライアント (Windows 7 Service Pack 1、Windows 8.1、Windows 10) または Windows Server (Windows Server 2012 R2 または Windows Server 2016) を実行します。 その他の OS のサポートを参照してください[for Remote Desktop Services のサポートされている構成](rds-supported-config.md)します。

ゲスト Vm の追加の考慮事項:

- OpenGL と OpenCL 機能には、Windows 10 または Windows Server 2016 ではできるだけです。  
- DirectX 11.0 には、Windows 8 または新しいゲスト Vm にできるだけです。 
- として実行されている場合、リモート デスクトップ セッション ホストが RemoteFX vGPU のサポートされているのみ、[個人用セッション デスクトップ](rds-personal-session-desktops.md)します。

ゲスト VM のことを確認することを確認して[VDI 展開 - サポートされるゲスト Os](rds-supported-config.md#vdi-deployment--supported-guest-oss)します。

## <a name="install-remotefx-vgpu"></a>RemoteFX vGPU をインストールします。

インストールして Windows Server 2016 および Windows 10 ホストで RemoteFX を構成するには、次の手順を使用します。

1. オペレーティング システムをインストールする。
2. グラフィックス カード ベンダー サイトから、最新 Windows 10/Windows Server 2016 の GPU ドライバーの使用をインストールします。
3. Windows 10/Windows Server 2016 ホスト上の RemoteFX vGPU をインストールします。
   1. Windows 10 ホストでは、コントロール パネル (go コントロール パネルのプログラムと機能を Windows の機能をオンまたはオフ) に HYPER-V の機能を有効にします。

      ![HYPER-V の機能を有効にする Windows 機能 ウィンドウ](media/rds-hyperv-settings.png)

   2. Windows Server 2016 ホストでは、リモート デスクトップ仮想化ホスト (RDVH) の役割をインストールします。
   

4. ここで、作成し、ゲスト VM を構成します。
   1. Windows 10 Enterprise または Windows Server 2016 では、VM を作成します。
   2. RemoteFX 3D グラフィックス アダプターを追加します。 参照してください[RemoteFX vGPU の 3D アダプターを構成する](#configure-the-remotefx-vgpu-3d-adapter)については、HYPER-V マネージャーまたは PowerShell コマンドレットを使用する実行する方法。 

使用可能な 1 つ以上が場合、RemoteFX vGPU はすべての Gpu を使用します。 ただし、今後も RemoteFX でどの Gpu を制限する特定のケースでは使用します。 HYPER-V 環境でこの機能を制御具体的には Gpu がこれを選択して*いない*RemoteFX で使用します。 次の手順を使用します。 

   1. HYPER-V マネージャーで、HYPER-V の設定に移動します。
   2. クリックして**物理 Gpu** Hyper V の設定にします。
   3. 選択し、オフにしたくない GPU**この GPU を使用して、RemoteFX の**します。


### <a name="configure-the-remotefx-vgpu-3d-adapter"></a>RemoteFX vGPU の 3D アダプターを構成します。
RemoteFX vGPU の 3D グラフィックス アダプターを構成するのには、HYPER-V マネージャーの UI または PowerShell コマンドレットを使用できます。 

#### <a name="through-hyper-v-manager"></a>Hyper V マネージャー。

1. Hyper-v を使用した、システムがセットアップされており、VM が構成されていることを確認します。  
2. 実行されている場合、VM を停止します。 
3. HYPER-V マネージャーに移動、 **VM 設定**、順にクリックします**ハードウェアの追加**します。
4. 選択**RemoteFX 3D グラフィックス アダプター**、 をクリック**追加**します。 
5. モニター、モニターの最大解像度、および専用のビデオ メモリの最大数を設定または既定値のままにします。

   > [!NOTE]
   > - これらのオプションのいずれかのより高い値を設定するため、絶対に必要なだけ設定する必要があります、スケール変更の影響があります。
   >
   > - 専用 VRAM の 1 GB を使用する必要がある場合は、32 ビット (x86) の代わりに、64 ビットのゲスト仮想マシンを使用して、最適な結果をします。
6. クリックして**OK**構成を終了します。

#### <a name="with-powershell-cmdlets"></a>PowerShell コマンドレット。

追加、確認、およびアダプターを構成するのには、次のコマンドレットを実行します。 

```powershell
Add-VMRemoteFx3dVideoAdapter [-CimSession <CimSession[]>] [-ComputerName <String[]>] [-Credential <PSCredential[]>] [-VMName] <String[]> [-Passthru] [-WhatIf] [-Confirm] [<CommonParameters>]
```

詳細を参照してください[追加 VMRemoteFx3dVideoAdapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/add-vmremotefx3dvideoadapter)します。

```powershell
Get-VMRemoteFx3dVideoAdapter [-CimSession <CimSession[]>] [-ComputerName <String[]>]  [-Credential <PSCredential[]>] [-VMName] <String[]> [<CommonParameters>]
```

詳細を参照してください[Get-vmremotefx3dvideoadapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/get-vmremotefx3dvideoadapter)

```powershell
Set-VMRemoteFx3dVideoAdapter [-CimSession <CimSession[]>] [-ComputerName <String[]>] [-Credential <PSCredential[]>] [-VMName] <String[]> [[-MonitorCount] <Byte>] [[-MaximumResolution] <String>] [[-VRAMSizeBytes] <UInt64>] [-Passthru] [-WhatIf] [-Confirm] [<CommonParameters>]
```

詳細を参照してください[Set-vmremotefx3dvideoadapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/set-vmremotefx3dvideoadapter)します。

物理 Gpu を確認するのには、次のコマンドレットを実行します。

```powershell
Get-VMRemoteFXPhysicalVideoAdapter [-ComputerName <String[]>] [-Credential <PSCredential[]>] [[-Name] <String[]>] [<CommonParameters>]  
```

詳細を参照してください[Get-vmremotefxphysicalvideoadapter](https://technet.microsoft.com/itpro/powershell/windows/hyper-v/get-vmremotefxphysicalvideoadapter)します。

## <a name="monitor-performance"></a>パフォーマンスの監視

VDI システムのスケールとパフォーマンスについては、さまざまなシステム メモリ、およびメモリの速度、CPU コアと CPU のクロック周波数、記憶域の速度と NUMA の実装の数の量、GPU の合計メモリなどの要因によって決まります。

RDS でのリモート vGPU のサポートには、フレーム レートのスループットに関する情報を収集するパフォーマンス モニター (perfmon.exe) で表示することができます、次のパフォーマンス カウンターが含まれています。

- RemoteFX グラフィックス - リモート デスクトップ プロトコルのグラフィックスの圧縮のカウンター。 たとえば、圧縮、RDP に表示されているフレームの数を確認する場合を見て、**入力 Frames/Second**カウンター。
- RemoteFX ネットワーク - リモート デスクトップ プロトコルのネットワーク トラフィック用のカウンター。 たとえば、**ラウンド トリップ時間 (RTT)** します。
- RemoteFX ルート GPU 管理 - VRAM 使用と予約済みのメジャー。
- RemoteFX ソフトウェア - キャプチャ レート、GPU の応答時間、およびその他のユーザーのカウンターを提供します。

特に、トラブルシューティングの場合、パフォーマンスの監視がより低レベルの次の追加のパフォーマンス カウンターを使用できます。

- RemoteFX Synth3D VSC VM デバイス 
- RemoteFX Synth3D VSC VM トランスポート チャネル 
- RemoteFX Synth3D VSP 
- RemoteFX Synth3D VSP VM デバイス 
- RemoteFX Synth3D VSP VM チャネル
