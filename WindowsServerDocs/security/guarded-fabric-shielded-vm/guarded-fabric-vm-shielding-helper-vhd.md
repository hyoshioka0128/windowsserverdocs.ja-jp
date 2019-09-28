---
title: シールドされた Vm-VM シールドヘルパー VHD の準備
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 0e3414cf-98ca-4e91-9e8d-0d7bce56033b
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 7984d1c965c15f7d8c3f3abfdc99f01e3adc215f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403422"
---
# <a name="shielded-vms---preparing-a-vm-shielding-helper-vhd"></a>シールドされた Vm-VM シールドヘルパー VHD の準備

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

> [!IMPORTANT]
> これらの手順を開始する前に、Windows Server 2016 用の最新の累積的な更新プログラムがインストールされていること、または最新の Windows 10[リモートサーバー管理ツール](https://www.microsoft.com/en-us/download/details.aspx?id=45520)を使用していることを確認してください。 それ以外の場合、プロシージャは機能しません。 

このセクションでは、既存の Vm をシールドされた Vm に変換するためのサポートを有効にするホスティングサービスプロバイダーによって実行される手順の概要を説明します。

このトピックがシールドされた Vm のデプロイプロセス全体にどのように適合するかを理解するには、「保護された[ホストとシールドされた vm のホスティングサービスプロバイダーの構成手順](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)」を参照してください。

## <a name="which-vms-can-be-shielded"></a>どの Vm をシールドすることができますか。

既存の Vm のシールドプロセスは、次の前提条件を満たす Vm でのみ使用できます。

- ゲスト OS は、Windows Server 2012、2012 R2、2016、または半期チャネルリリースです。 既存の Linux Vm をシールドされた Vm に変換することはできません。
- VM は第2世代の VM (UEFI ファームウェア)
- VM では、OS ボリュームに差分ディスクは使用されません。

## <a name="prepare-helper-vhd"></a>ヘルパー VHD の準備

1.  Hyper-v がインストールされているコンピューターとリモートサーバー管理ツール機能のシールドされた**VM ツール**がインストールされているコンピューターで、空の VHDX を使用して新しい第2世代の vm を作成し、WINDOWS server ISO のインストールメディアを使用して windows server 2016 をインストールします。 この VM はシールドされていないため、Server Core またはデスクトップエクスペリエンス搭載サーバーを実行する必要があります。

    > [!IMPORTANT]
    > VM シールドヘルパー VHD は、[ホスティングサービスプロバイダー](guarded-fabric-create-a-shielded-vm-template.md)によって作成されたテンプレートディスクに関連付けられていないと、シールドされた vm テンプレートが作成され**ません**。 テンプレートディスクを再利用すると、シールドプロセス中にディスク署名の競合が発生します。これは、両方のディスクの GPT ディスク識別子が同じであるためです。 これを回避するには、新しい (空の) VHD を作成し、ISO のインストールメディアを使用して Windows Server 2016 をインストールします。

2.  VM を起動し、セットアップ手順を完了して、デスクトップにログインします。 VM が動作中の状態であることを確認したら、VM をシャットダウンします。

3.  管理者特権の Windows PowerShell ウィンドウで、次のコマンドを実行して、以前に作成した VHDX を VM シールドヘルパーディスクにする準備をします。 環境の正しいパスでパスを更新してください。

    ```powershell
    Initialize-VMShieldingHelperVHD -Path 'C:\VHD\shieldingHelper.vhdx'
    ```

4.  コマンドが正常に完了したら、VHDX を VMM ライブラリ共有にコピーします。 手順 1. で VM を再起動しない**で**ください。 この操作を行うと、ヘルパーディスクが破損します。

5.  これで、Hyper-v の手順 1. から VM を削除できます。

## <a name="configure-vmm-host-guardian-server-settings"></a>VMM ホストガーディアンサーバー設定の構成

VMM コンソールで、設定 ウィンドウを開き、**全般** の下にある **ガーディアンサービスの設定** をホストします。 このウィンドウの下部には、ヘルパー VHD の場所を構成するためのフィールドがあります。 [参照] ボタンを使用して、ライブラリ共有から VHD を選択します。 共有にディスクが表示されない場合は、VMM でライブラリを表示するために手動で更新する必要がある場合があります。

![VMM-ホストガーディアンサービスの設定](../media/Guarded-Fabric-Shielded-VM/guarded-host-vmm-hgs-settings-01.png)

## <a name="see-also"></a>関連項目

- [保護されたホストとシールドされた Vm のホスティングサービスプロバイダーの構成手順](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [保護されたファブリックとシールドされた VM](guarded-fabric-and-shielded-vms-top-node.md)
