---
title: 個別のデバイスの割り当てを使用したデバイスの展開の計画
description: Windows Server で DDA がどのように機能するかについて説明します。
ms.prod: windows-server-threshold
ms.service: na
ms.technology: hyper-v
ms.tgt_pltfrm: na
ms.topic: article
author: chrishuybregts
ms.author: chrihu
ms.date: 02/06/2018
ms.openlocfilehash: 7df7dbd1e7252f5bab451ed9272f9cbede63d223
ms.sourcegitcommit: 216d97ad843d59f12bf0b563b4192b75f66c7742
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68476497"
---
# <a name="plan-for-deploying-devices-using-discrete-device-assignment"></a>個別のデバイスの割り当てを使用したデバイスの展開の計画
>適用先:Microsoft Hyper-v Server 2016、Windows Server 2016、Microsoft Hyper-v Server 2019、Windows Server 2019

個別のデバイス割り当てでは、物理 PCIe ハードウェアに仮想マシン内から直接アクセスできます。  このガイドでは、デバイスの個別割り当てを使用できるデバイスの種類、ホストシステム要件、仮想マシンに課せられる制限事項、および個別のデバイス割り当てのセキュリティへの影響について説明します。

個別のデバイス割り当ての最初のリリースでは、Microsoft によって正式にサポートされる2つのデバイスクラスに重点を置いています。グラフィックスアダプターと NVMe 記憶装置。  他のデバイスは動作する可能性が高く、ハードウェアベンダーはそれらのデバイスに対してサポートステートメントを提供できます。  その他のデバイスについては、これらのハードウェアベンダーに問い合わせてください。

個別のデバイスの割り当てを試す準備ができている場合は、個別のデバイス割り当てを使用して[グラフィックスデバイスをデプロイ](../deploy/Deploying-graphics-devices-using-dda.md)するか、[個別のデバイス割り当てを使用してストレージデバイスを展開](../deploy/Deploying-storage-devices-using-dda.md)して開始することができます。

## <a name="supported-virtual-machines-and-guest-operating-systems"></a>サポートされている Virtual Machines とゲストオペレーティングシステム
個別のデバイスの割り当ては、第1または第2世代の Vm でサポートされています。  また、サポートされているゲストには、Windows 10、Windows Server 2019、Windows Server 2016、 [KB 3133690](https://support.microsoft.com/kb/3133690)が適用された windows server 2012r2、および Linux OS のさまざまなディストリビューションが含まれ[ます。](../supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows.md)

## <a name="system-requirements"></a>システム要件
[Windows Server のシステム要件](../../../get-started/System-Requirements--and-Installation.md)と[Hyper-v のシステム要件](../System-requirements-for-Hyper-V-on-Windows.md)に加えて、個別のデバイスの割り当てには、PCIe の構成に対してオペレーティングシステムの制御を与えることができるサーバークラスのハードウェアが必要です。fabric (ネイティブ PCI Express コントロール)。 さらに、PCIe ルート複合は、"Access Control Services" (ACS) をサポートする必要があります。これにより、Hyper-v は i/o MMU を通過するすべての PCIe トラフィックを強制的に強制できます。

これらの機能は通常、サーバーの BIOS で直接公開されることはなく、多くの場合、他の設定の背後で隠されています。  たとえば、sr-iov のサポートには同じ機能が必要であり、BIOS では "SR-IOV を有効にする" の設定が必要になる場合があります。  BIOS で正しい設定を識別できない場合は、システムベンダーにお問い合わせください。

ハードウェアが個別のデバイス割り当てに対応できるようにするために、エンジニアは[コンピュータープロファイルスクリプト](#machine-profile-script)をまとめました。これを hyper-v 対応ホストで実行して、サーバーが正しくセットアップされているかどうか、およびデバイスに対応しているかどうかをテストできます。個別のデバイスの割り当て。

## <a name="device-requirements"></a>デバイスの要件
すべての PCIe デバイスを個別のデバイス割り当てで使用できるわけではありません。  たとえば、レガシ (INTx) PCI 割り込みを利用する古いデバイスはサポートされていません。 Jake Oshin の[ブログ投稿](https://blogs.technet.microsoft.com/virtualization/2015/11/20/discrete-device-assignment-machines-and-devices/)はより詳細に説明されています。ただし、コンシューマーの場合は、[コンピュータープロファイルスクリプト](#machine-profile-script)を実行すると、デバイスの個別割り当てに使用できるデバイスが表示されます。

詳細については、デバイスの製造元にお問い合わせください。

## <a name="device-driver"></a>デバイスドライバー
個別のデバイスの割り当てによって、PCIe デバイス全体がゲスト VM に渡されるため、VM 内にデバイスをマウントする前に、ホストドライバーをインストールする必要はありません。  ホストの唯一の要件は、デバイスの[PCIe ロケーションパス](#pcie-location-path)を決定できることです。  デバイスの識別に役立つ場合は、デバイスのドライバーをインストールすることもできます。  たとえば、ホストにデバイスドライバーがインストールされていない GPU が、Microsoft Basic レンダーデバイスとして表示される場合があります。  デバイスドライバーがインストールされている場合は、その製造元とモデルが表示される可能性があります。

デバイスがゲスト内にマウントされると、ゲスト仮想マシン内に通常のような製造元のデバイスドライバーをインストールできるようになります。  

## <a name="virtual-machine-limitations"></a>仮想マシンの制限事項
デバイスの個別割り当ての実装方法の性質により、デバイスの接続中に仮想マシンの一部の機能が制限されます。  次の機能は使用できません。
- VM の保存/復元
- VM のライブマイグレーション
- 動的メモリの使用
- 高可用性 (HA) クラスターへの VM の追加

## <a name="security"></a>セキュリティ
個別のデバイスの割り当てによって、デバイス全体が VM に渡されます。  これは、そのデバイスのすべての機能に、ゲストオペレーティングシステムからアクセスできることを意味します。 ファームウェアの更新などの一部の機能は、システムの安定性に悪影響を与える可能性があります。 そのため、ホストからデバイスをマウント解除するときに、管理者に多くの警告が表示されます。 個別のデバイスの割り当ては、Vm のテナントが信頼されている場合にのみ使用することを強くお勧めします。  

管理者が信頼されていないテナントのデバイスを使用することを希望している場合は、デバイスの製造元に、ホストにインストールできるデバイス軽減ドライバーを作成する機能が用意されています。  デバイスの対策ドライバーが提供されているかどうかの詳細については、デバイスの製造元に問い合わせてください。

デバイスの軽減ドライバーがないデバイスのセキュリティチェックをバイパスする場合は、 `-Force`パラメーターを`Dismount-VMHostAssignableDevice`コマンドレットに渡す必要があります。  そうすることで、そのシステムのセキュリティプロファイルが変更され、プロトタイプ作成または信頼された環境でのみ推奨されることがわかります。

## <a name="pcie-location-path"></a>PCIe ロケーションパス
ホストからデバイスをマウント解除してマウントするには、PCIe ロケーションパスが必要です。  ロケーションパスの例は次`"PCIROOT(20)#PCI(0300)#PCI(0000)#PCI(0800)#PCI(0000)"`のようになります。   [コンピュータープロファイルスクリプト](#machine-profile-script)は、PCIe デバイスの場所のパスも返します。

### <a name="getting-the-location-path-by-using-device-manager"></a>デバイスマネージャーを使用した場所のパスの取得
![デバイス マネージャー](../deploy/media/dda-devicemanager.png)
- デバイスマネージャーを開き、デバイスを見つけます。  
- デバイスを右クリックし、[プロパティ] を選択します。
- [詳細] タブに移動し、プロパティドロップダウンで [ロケーションパス] を選択します。  
- "PCIROOT" で始まるエントリを右クリックし、[コピー] を選択します。  これで、そのデバイスの場所のパスが作成されました。

## <a name="mmio-space"></a>MMIO Space
一部のデバイス (特に Gpu) では、そのデバイスのメモリにアクセスするために VM に割り当てられる追加の MMIO 領域が必要です。 既定では、各 VM は 128 MB の低 MMIO 領域と、512 MB の高 MMIO 領域が割り当てられています。 ただし、デバイスではより多くの MMIO 領域が必要になる場合があります。また、複数のデバイスが渡され、結合された要件がこれらの値を超えてしまう可能性があります。  MMIO Space の変更は簡単です。次のコマンドを使用して、PowerShell で実行できます。

```PowerShell
Set-VM -LowMemoryMappedIoSpace 3Gb -VMName $vm
Set-VM -HighMemoryMappedIoSpace 33280Mb -VMName $vm
```

どの程度の MMIO 領域を割り当てるかを決定する最も簡単な方法は、[マシンプロファイルスクリプト](#machine-profile-script)を使用することです。 マシンプロファイルスクリプトをダウンロードして実行するには、PowerShell コンソールで次のコマンドを実行します。

```PowerShell
curl -o SurveyDDA.ps1 https://raw.githubusercontent.com/MicrosoftDocs/Virtualization-Documentation/live/hyperv-tools/DiscreteDeviceAssignment/SurveyDDA.ps1
.\SurveyDDA.ps1
```

割り当て可能なデバイスについては、次の例のように、スクリプトによって特定のデバイスの MMIO 要件が表示されます。

```PowerShell
NVIDIA GRID K520
Express Endpoint -- more secure.
    ...
    And it requires at least: 176 MB of MMIO gap space
...
```

Low MMIO 領域は、32ビットのオペレーティングシステムと32ビットのアドレスを使用するデバイスでのみ使用されます。 ほとんどの場合、32ビット構成はあまり一般的ではないため、VM の高 MMIO 領域を設定するだけで十分です。

> [!IMPORTANT]
> MMIO space を VM に割り当てる場合、ユーザーは、必要なすべての割り当て済みデバイスについて、要求された MMIO 領域の合計と、数 MB の MMIO 領域を必要とする他の仮想デバイスがある場合に追加のバッファーを設定する必要があります。 上記で説明した既定の MMIO 値は、low および high MMIO のバッファーとして使用します (それぞれ 128 MB と 512 MB)。

ユーザーが上記の例のように1つの K520 GPU を割り当てる場合は、VM の MMIO space をコンピュータープロファイルスクリプトによって出力された値に設定し、バッファー--176 MB + 512 MB を設定する必要があります。 ユーザーが3つの K520 Gpu を割り当てる場合は、MMIO space を 176 MB に、バッファー (528 MB + 512 MB) を3倍に設定する必要があります。

MMIO 領域の詳細については、技術コミュニティブログの「[個別のデバイスの割り当て-gpu](https://techcommunity.microsoft.com/t5/Virtualization/Discrete-Device-Assignment-GPUs/ba-p/382266) 」を参照してください。

## <a name="machine-profile-script"></a>コンピュータープロファイルスクリプト
サーバーが正しく構成されているかどうか、および個別のデバイス割り当てを使用して渡すことができるデバイスを特定するために、エンジニアの1人は次の PowerShell スクリプトをまとめました。[SurveyDDA。](https://github.com/Microsoft/Virtualization-Documentation/blob/live/hyperv-tools/DiscreteDeviceAssignment/SurveyDDA.ps1)

スクリプトを使用する前に、Hyper-v の役割がインストールされていることを確認し、管理者特権を持つ PowerShell コマンドウィンドウからスクリプトを実行してください。

個別のデバイスの割り当てをサポートするようにシステムが正しく構成されていない場合、エラーメッセージが表示されます。 システムが正しく構成されていることが検出されると、このツールは、PCIe バス上で検出できるすべてのデバイスを列挙します。

検出されたデバイスごとに、個別のデバイス割り当てで使用できるかどうかがツールによって表示されます。 デバイスが個別のデバイス割り当てと互換性があると識別された場合、スクリプトによって理由が示されます。  デバイスが互換性のあるものとして正しく識別されると、デバイスの場所のパスが表示されます。  さらに、そのデバイスに[MMIO 領域](#mmio-space)が必要な場合は、表示されます。

![SurveyDDA](./images/hyper-v-surveydda-ps1.png)

## <a name="frequently-asked-questions"></a>よく寄せられる質問

### <a name="how-does-remote-desktops-remotefx-vgpu-technology-relate-to-discrete-device-assignment"></a>リモートデスクトップの RemoteFX vGPU テクノロジは、個別のデバイス割り当てとどのように関連していますか。
完全に独立したテクノロジです。 個別のデバイス割り当てを機能させるには、RemoteFX vGPU をインストールする必要はありません。 また、追加の役割をインストールする必要はありません。 Remotefx vgpu を使用するには、remotefx vGPU ドライバーが VM 内に存在するためには、RDVH ロールがインストールされている必要があります。 ハードウェアベンダーのドライバーを仮想マシンにインストールするため、デバイスの個別割り当てには、追加の役割は必要ありません。  

### <a name="ive-passed-a-gpu-into-a-vm-but-remote-desktop-or-an-application-isnt-recognizing-the-gpu"></a>GPU を VM に渡しましたが、リモートデスクトップまたはアプリケーションが GPU を認識していません
これはさまざまな原因で発生する可能性がありますが、いくつかの一般的な問題を以下に示します。
- 最新の GPU ベンダーのドライバーがインストールされており、デバイスマネージャーでデバイスの状態を確認することでエラーが報告されていないことを確認します。
- デバイスに VM 内に割り当てられている[MMIO 領域](#mmio-space)が十分にあることを確認します。
- この構成で使用されているベンダーがサポートしている GPU を使用していることを確認します。 たとえば、一部のベンダーでは、VM に渡されたときにコンシューマーカードが動作しなくなります。
- 実行中のアプリケーションが VM 内での実行をサポートしていること、および GPU とそれに関連付けられているドライバーの両方がアプリケーションでサポートされていることを確認します。 一部のアプリケーションには、Gpu と環境のホワイトリストがあります。
- ゲストでリモートデスクトップセッションホストの役割または Windows Multipoint Services を使用している場合は、特定のグループポリシーエントリが既定の GPU の使用を許可するように設定されていることを確認する必要があります。 ゲスト (またはゲストのローカルグループポリシーエディター) に適用されているグループポリシーオブジェクトを使用して、次のグループポリシーの項目に移動します。
   - コンピューターの構成
   - 管理者テンプレート
   - Windows コンポーネント
   - リモート デスクトップ サービス
   - リモート デスクトップ セッション ホスト
   - リモート セッション環境
   - すべてのリモート デスクトップ サービス セッションにハードウェアの既定のグラフィックス アダプターを使用する

    ポリシーが適用されたら、この値を [有効] に設定し、VM を再起動します。

### <a name="can-discrete-device-assignment-take-advantage-of-remote-desktops-avc444-codec"></a>個別のデバイス割り当てで、リモートデスクトップの AVC444 コーデックを利用できますか。
はい。詳細については、こちらのブログ投稿をご覧ください。[Windows 10 および Windows Server 2016 Technical Preview でのリモートデスクトッププロトコル (RDP) 10 AVC/h.264 の機能強化。](https://blogs.technet.microsoft.com/enterprisemobility/2016/01/11/remote-desktop-protocol-rdp-10-avch-264-improvements-in-windows-10-and-windows-server-2016-technical-preview/)

### <a name="can-i-use-powershell-to-get-the-location-path"></a>PowerShell を使用して場所のパスを取得できますか。
はい、これを行うにはさまざまな方法があります。 1つの例を次に示します。
```
#Enumerate all PNP Devices on the system
$pnpdevs = Get-PnpDevice -presentOnly
#Select only those devices that are Display devices manufactured by NVIDIA
$gpudevs = $pnpdevs |where-object {$_.Class -like "Display" -and $_.Manufacturer -like "NVIDIA"}
#Select the location path of the first device that's available to be dismounted by the host.
$locationPath = ($gpudevs | Get-PnpDeviceProperty DEVPKEY_Device_LocationPaths).data[0]
```

### <a name="can-discrete-device-assignment-be-used-to-pass-a-usb-device-into-a-vm"></a>個別のデバイス割り当てを使用して、USB デバイスを VM に渡すことができますか。
公式にはサポートされていませんが、お客様は USB3 コントローラー全体を VM に渡すことによって、これを行うために個別のデバイス割り当てを使用しています。  コントローラー全体が渡されると、そのコントローラーに接続されている各 USB デバイスにも VM でアクセスできるようになります。  一部の USB3 コントローラーのみが動作する場合があり、USB2 コントローラーは個別のデバイス割り当てでは使用できないことに注意してください。
