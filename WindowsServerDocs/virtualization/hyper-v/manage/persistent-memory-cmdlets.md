---
title: Hyper-v Vm 用の永続メモリデバイスを構成するためのコマンドレット
description: Hyper-v Vm の永続メモリデバイスを構成する方法
ms.prod: windows-server
ms.service: na
manager: jasgroce
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5715c02-a90f-4de9-a71e-0fc08039ba1d
author: coreyp-at-msft
ms.author: coreyp
ms.openlocfilehash: ecae1fe96bc5088fa840c6e2e24a75bb72a9e8f3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392534"
---
# <a name="cmdlets-for-configuring-persistent-memory-devices-for-hyper-v-vms"></a>Hyper-v Vm 用の永続メモリデバイスを構成するためのコマンドレット

>適用先:Windows Server 2019

この記事では、システム管理者および IT プロフェッショナルに、永続メモリ (ストレージクラスメモリまたは NVDIMM) を使用した Hyper-v Vm の構成に関する情報を提供します。 JDEC に準拠している NVDIMM-N 永続メモリデバイスは、Windows Server 2016 と Windows 10 でサポートされており、非常に短い待機時間の少ない非揮発性デバイスへのバイトレベルのアクセスを提供します。 VM 永続メモリデバイスは、Windows Server 2019 でサポートされています。 

## <a name="create-a-persistent-memory-device-for-a-vm"></a>VM の永続メモリデバイスを作成する

VM の永続メモリデバイスを作成するには、 **[新しい VHD](https://docs.microsoft.com/powershell/module/hyper-v/new-vhd?view=win10-ps)** コマンドレットを使用します。 デバイスは、既存の NTFS DAX ボリューム上に作成する必要があります。  新しいファイル名拡張子 (. vhdpmem) は、デバイスが永続的なメモリデバイスであることを指定するために使用されます。 固定の VHD ファイル形式のみがサポートされています。

**例:** `New-VHD d:\VMPMEMDevice1.vhdpmem -Fixed -SizeBytes 4GB`

## <a name="create-a-vm-with-a-persistent-memory-controller"></a>永続的なメモリコントローラーを備えた VM を作成する



**新しい vm コマンドレット**を使用して、指定されたメモリサイズと VHDX イメージへのパスを持つ第2世代 vm を作成します。 次に、 **VMPmemController**を使用して、永続的なメモリコントローラーを VM に追加します。

**例:** 
    
    New-VM -Name "ProductionVM1" -MemoryStartupBytes 1GB -VHDPath c:\vhd\BaseImage.vhdx

    Add-VMPmemController ProductionVM1x

## <a name="attach-a-persistent-memory-device-to-a-vm"></a>永続メモリデバイスを VM に接続する

**[Add-vmharddiskdrive](https://docs.microsoft.com/powershell/module/hyper-v/add-vmharddiskdrive?view=win10-ps)** を使用して永続メモリデバイスを VM に接続する

**例:** `Add-VMHardDiskDrive ProductionVM1 PMEM -ControllerLocation 1 -Path D:\VPMEMDevice1.vhdpmem`

Hyper-v VM 内の永続メモリデバイスは、ゲストオペレーティングシステムによって使用および管理される永続的なメモリデバイスとして表示されます。 ゲストオペレーティングシステムでは、デバイスをブロックまたは DAX ボリュームとして使用できます。 VM 内の永続的なメモリデバイスが DAX ボリュームとして使用されている場合、ホストデバイスの低待機時間のバイトレベルのアドレス機能 (コードパスに i/o 仮想化が存在しない) の恩恵を受けられます。 

>[!NOTE] 
>永続メモリは、Hyper-v Gen2 Vm でのみサポートされます。 ライブマイグレーションと記憶域の移行は、永続メモリを持つ Vm ではサポートされていません。 Vm の運用チェックポイントには、永続メモリの状態は含まれません。 