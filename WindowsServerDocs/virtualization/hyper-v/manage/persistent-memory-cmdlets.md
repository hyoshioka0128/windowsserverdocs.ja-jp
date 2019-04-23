---
title: HYPER-V Vm の永続的なメモリ デバイスを構成するためのコマンドレット
description: HYPER-V Vm の永続的なメモリ デバイスを構成する方法
ms.prod: windows-server-threshold
ms.service: na
manager: jasgroce
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5715c02-a90f-4de9-a71e-0fc08039ba1d
author: coreyp-at-msft
ms.author: coreyp
ms.openlocfilehash: fd1b04ce74f0b8d490529d2a7f65091f5847d0f4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59878183"
---
# <a name="cmdlets-for-configuring-persistent-memory-devices-for-hyper-v-vms"></a>HYPER-V Vm の永続的なメモリ デバイスを構成するためのコマンドレット

>適用先:Windows Server 2019

この記事では、永続的なメモリ (記憶域クラス メモリまたは NVDIMM とも呼ばれます) での HYPER-V Vm の構成に関する情報をシステム管理者および IT プロフェッショナルを提供します。 JDEC 準拠 NVDIMM-N の永続的なメモリ デバイスは、Windows Server 2016 と Windows 10 でサポートされ、バイト レベルのアクセスを非常に低待機時間の非揮発性のデバイスを指定します。 VM の永続的なメモリ デバイスは、Windows Server 2019 でサポートされます。 

## <a name="create-a-persistent-memory-device-for-a-vm"></a>VM の永続的なメモリ デバイスを作成します。

使用して、 **[NEW-VHD](https://docs.microsoft.com/powershell/module/hyper-v/new-vhd?view=win10-ps)** コマンドレットで VM の永続的なメモリ デバイスを作成します。 既存の NTFS DAX ボリュームでは、デバイスを作成する必要があります。  新しいファイル名拡張子 (.vhdpmem) を使用して、デバイスが、永続的なメモリ デバイスを指定します。 固定の VHD ファイル形式のみがサポートされています。

**例:** `New-VHD d:\VMPMEMDevice1.vhdpmem -Fixed -SizeBytes 4GB`

## <a name="create-a-vm-with-a-persistent-memory-controller"></a>永続的なメモリのコント ローラー VM を作成します。



使用して、 **NEW-VM コマンドレット**指定されたメモリ サイズと VHDX イメージのパスを持つ 2 世代の VM を作成します。 使用して、**追加 VMPmemController** VM に永続的なメモリのコント ローラーを追加します。

**例:** 
    
    New-VM -Name "ProductionVM1" -MemoryStartupBytes 1GB -VHDPath c:\vhd\BaseImage.vhdx

    Add-VMPmemController ProductionVM1x

## <a name="attach-a-persistent-memory-device-to-a-vm"></a>VM に永続的なメモリ デバイスを接続します。

使用**[Add-vmharddiskdrive](https://docs.microsoft.com/powershell/module/hyper-v/add-vmharddiskdrive?view=win10-ps)** を VM に永続的なメモリ デバイスを接続するには

**例:** `Add-VMHardDiskDrive ProductionVM1 PMEM -ControllerLocation 1 -Path D:\VPMEMDevice1.vhdpmem`

HYPER-V VM 内で永続的なメモリ デバイスは、永続的なメモリ消費およびゲスト オペレーティング システムによって管理されるデバイスとして表示されます。 ゲスト オペレーティング システムは、デバイスをブロックまたは DAX ボリュームとして使用できます。 DAX ボリュームとして、VM 内で永続的なメモリ デバイスを使用している場合は、低待機時間バイト レベル アドレス-機能のホスト デバイス (しないコード パスに I/O virtualization) からに活用します。 

>[!NOTE] 
>永続的なメモリは HYPER-V Gen2 Vm にのみサポートされます。 ライブ マイグレーションと記憶域の移行はサポートされていません Vm の永続的なメモリとします。 Vm の運用チェックポイントは、永続的なメモリの状態を含めないでください。 