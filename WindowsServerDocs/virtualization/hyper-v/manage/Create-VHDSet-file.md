---
title: HYPER-V VHD 設定ファイルを作成します。
description: Hyper-v 2016 VHDset ファイルを作成する手順
author: jiwool
ms.author: jiwool
manager: senthilr
ms.date: 01/26/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: compute-hyper-v
ms.assetid: 444e1496-9e5a-41cf-bfbc-306e2ed8e00a
audience: IT Pros
ms.reviewer: kathydav
ms.openlocfilehash: 61f2450857cbeaffd7f75f7b259e9f9de06ba5c6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870403"
---
# <a name="create-hyper-v-vhd-set-files"></a>HYPER-V VHD 設定ファイルを作成します。
ファイルの VHD の設定は、Windows Server 2016 でのゲスト クラスター用の新しい共有仮想ディスク モデルです。 ファイルの VHD の設定を共有の仮想ディスクのオンライン サイズ変更をサポート、HYPER-V レプリカをサポート、およびアプリケーション整合性のチェックポイントに含めることができます。 

ファイルの VHD の設定は、新しい VHD ファイルの種類を使用します。VHD をします。 ファイルの VHD の設定は、メタデータの形式でのゲスト クラスターで使用されるグループのバーチャル ディスクに関するチェックポイント情報を格納します。

HYPER-V がチェックポイントのチェーンを管理するすべての側面を処理し、設定、共有 VHD をマージします。 場合と同様に VHD の設定ファイルのオンライン サイズ変更などのディスク操作を実行できるは、管理ソフトウェア。VHDX ファイル。 これは、管理ソフトウェアが、VHD の設定ファイルの形式について知っておく必要があることを意味します。

## <a name="create-a-vhd-set-file-from-hyper-v-manager"></a>HYPER-V マネージャーから VHD の設定ファイルを作成します。

1.  Hyper-V マネージャーを開きます。 **[スタート]** ボタンをクリックし、**[管理ツール]** をポイントして **[Hyper-V マネージャー]** をクリックします。
2.  操作ウィンドウで次のようにクリックします。**新規**、順にクリックします**ハード_ディスク**します。
3.  **ディスク フォーマットの選択**] ページで、[ **VHD 設定**バーチャル ハード ディスクのフォーマットとします。
4.  仮想ハード_ディスクをカスタマイズするウィザードの各ページの手順を続行します。 クリックすることができます**次**間を移動するか、ウィザードの各ページの左側のウィンドウにそのページに直接移動するページの名前をクリックできます。
5.  仮想ハード_ディスクの構成が完了したら後でクリックして**完了**します。

## <a name="create-a-vhd-set-file-from-windows-powershell"></a>Windows PowerShell から VHD の設定ファイルを作成します。

使用して、 [NEW-VHD](https://technet.microsoft.com/library/hh848503.aspx)コマンドレットは、ファイルの種類にします。VHD ファイルのパス。 この例では、10 ギガバイトのサイズは base.vhds をという名前の VHD 設定ファイルを作成します。

``` PowerShell
PS c:\>New-VHD -Path c:\base.vhds -SizeBytes 10GB
```

## <a name="migrate-a-shared-vhdx-file-to-a-vhd-set-file"></a>共有 VHDX ファイルを VHD に設定ファイルに移行します。

VHD に既存の共有 VHDX を移行するには、VM をオフラインにする必要があります。 これは、Windows PowerShell を使用して、推奨されるプロセスです。

1.  VHDX を VM から削除します。 たとえばを実行します。 
  ``` PowerShell
  PS c:\>Remove-VMHardDiskDrive existing.vhdx
  ```
  
2.  VHDX を VHD に変換します。 たとえばを実行します。
  ``` PowerShell
  PS c:\>Convert-VHD existing.vhdx new.vhds
  ```
  
3.  VM に VHD を追加します。 たとえばを実行します。
  ``` PowerShell
  PS c:\>Add-VMHardDiskDrive new.vhds
  ```
  



