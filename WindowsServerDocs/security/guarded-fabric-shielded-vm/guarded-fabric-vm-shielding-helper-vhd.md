---
title: シールドされた Vm - VM シールド ヘルパー VHD を準備します。
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 0e3414cf-98ca-4e91-9e8d-0d7bce56033b
manager: dongill
author: rpsqrd
ms.technology: security-guarded-fabric
ms.date: 08/29/2018
ms.openlocfilehash: 8e14cdeed435f23f28ca514e232fbcfa6220fc74
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887723"
---
# <a name="shielded-vms---preparing-a-vm-shielding-helper-vhd"></a>シールドされた Vm - VM シールド ヘルパー VHD を準備します。

>適用対象:Windows Server 2019、Windows Server (半期チャネル)、Windows Server 2016

<!-- This comment creates a break between the Applies To above and the Important note below. -->

> [!IMPORTANT]
> これらの手順を開始する前に Windows Server 2016 用の最新の累積的な更新プログラムがインストールされているか、最新の Windows 10 を使用していることを確認します。[リモート サーバー管理ツール](https://www.microsoft.com/en-us/download/details.aspx?id=45520)します。 それ以外の場合、手順は機能しません。 

このセクションでは、既存の Vm をシールドされた Vm に変換するためのサポートを有効にするホスティング サービス プロバイダーによって実行される手順について説明します。

このトピックがシールドされた Vm の展開の全体的なプロセスがどのように適合するしくみを理解するのを参照してください。[保護されたホストとシールドされた Vm のサービス プロバイダーの構成手順をホストしている](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)します。

## <a name="which-vms-can-be-shielded"></a>Vm をシールドすることができますか。

既存の Vm のシールドのプロセスでは、次の前提条件を満たす Vm に対して使用できますのみです。

- ゲスト OS は Windows Server 2012、2012 R2、2016、または、半期チャネル リリースします。 シールドされた Vm には、既存の Linux Vm を変換することはできません。
- VM が、第 2 世代 VM (UEFI ファームウェア)
- VM の OS ボリュームの差分ディスクを使用しません。

## <a name="prepare-helper-vhd"></a>ヘルパー VHD を準備します。

1.  コンピューターで Hyper-v ホストとリモート サーバー管理ツール機能**シールドされた VM ツール**新世代 2 の作成、インストールされている VHDX が空で、Windows Server の ISO のインストールを使用して Windows Server 2016 のインストールと VMメディア。 この VM は、シールドされていない必要があり、デスクトップ エクスペリエンス搭載サーバー コアまたは Server を実行する必要があります。

    > [!IMPORTANT]
    > VM シールド ヘルパー VHD**しないで**で作成したテンプレート ディスクに関連している[ホスティング サービス プロバイダーは、シールドされた VM テンプレートを作成します。](guarded-fabric-create-a-shielded-vm-template.md)します。 テンプレート ディスクを再利用する場合があります、シールドのプロセス中に、ディスク署名競合ディスクの両方が同じ GPT ディスクの識別子を持つためです。 これは、新しい (空) の VHD を作成および ISO は、インストール メディアを使用して Windows Server 2016 のインストールを回避できます。

2.  VM を起動のセットアップ手順を完了およびデスクトップにログインします。 VM が稼働状態、VM をシャット ダウンすることを確認します。

3.  管理者特権で Windows PowerShell ウィンドウで、以前に作成する VM シールド ヘルパー ディスクに VHDX を準備するには、次のコマンドを実行します。 環境内の適切なパスのパスを更新します。

    ```powershell
    Initialize-VMShieldingHelperVHD -Path 'C:\VHD\shieldingHelper.vhdx'
    ```

4.  コマンドが正常に完了すると、VHDX を VMM ライブラリ共有にコピーします。 **しない**手順 1 の VM が再び開始します。 そうと、ヘルパー ディスクが破損します。

5.  手順 1. HYPER-V で VM を削除することができますようになりました。

## <a name="configure-vmm-host-guardian-server-settings"></a>VMM ホスト ガーディアン サーバーの設定を構成します。

VMM コンソールで 設定 ウィンドウを開きし、**ホスト ガーディアン サービスの設定****全般**。 このウィンドウの下部には、ヘルパー VHD の場所を構成するためのフィールドがあります。 [参照] ボタンを使用して、ライブラリ共有から VHD を選択します。 共有ディスクが表示されない場合は、表示することに対する VMM でライブラリを手動で更新する必要があります。

![VMM のホスト ガーディアン サービスの設定](../media/Guarded-Fabric-Shielded-VM/guarded-host-vmm-hgs-settings-01.png)

## <a name="see-also"></a>関連項目

- [保護されたホストとシールドされた Vm のサービス プロバイダーの構成手順をホストしています。](guarded-fabric-configuration-scenarios-for-shielded-vms-overview.md)
- [保護されたファブリックとシールドされた Vm](guarded-fabric-and-shielded-vms-top-node.md)
