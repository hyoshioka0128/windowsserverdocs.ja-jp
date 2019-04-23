---
title: 個別のデバイスの割り当てを使用してデバイスをデプロイするための計画
description: Windows Server で DDA のしくみについて説明します
ms.prod: windows-server-threshold
ms.service: na
ms.technology: hyper-v
ms.tgt_pltfrm: na
ms.topic: article
author: chrishuybregts
ms.author: chrihu
ms.date: 02/06/2018
ms.openlocfilehash: c64c2b75c00f97622278c3e590db46995e108218
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840203"
---
# <a name="plan-for-deploying-devices-using-discrete-device-assignment"></a>個別のデバイスの割り当てを使用して展開するデバイスを計画します。
>適用先:Microsoft HYPER-V Server 2016、Windows Server 2016、Microsoft HYPER-V Server 2019、Windows Server 2019

個別のデバイスの割り当ては、物理の PCIe ハードウェアを仮想マシン内から直接アクセスできます。  このガイドは、デバイス独立したデバイスの割り当て、ホスト システムの要件が使用できる仮想マシンとデバイスの割り当てが不連続のセキュリティの影響に対する制限の種類について説明します。

個別のデバイスの割り当ての初期リリースが、Microsoft で正式にサポートする 2 つのデバイス クラスに注目します。グラフィックス アダプターや NVMe ストレージ デバイス。  その他のデバイスが動作することが、ハードウェア ベンダーはそれらのデバイスのサポートのステートメントを提供すること。  その他のデバイスのハードウェア ベンダーのサポートにご連絡ください。

経由でジャンプできる場合は、個別のデバイスの割り当てを試す準備が完了したら、[展開グラフィックス デバイスを使用して個別のデバイスの割り当て](../deploy/Deploying-graphics-devices-using-dda.md)または[記憶装置を展開する個別のデバイスの割り当てを使用して](../deploy/Deploying-storage-devices-using-dda.md)開始するには

## <a name="supported-virtual-machines-and-guest-operating-systems"></a>サポートされている仮想マシンとゲスト オペレーティング システム
個別のデバイスの割り当ては第 1 世代の 2 つの Vm でサポートされています。  サポートされているゲストは、Windows 10、Windows Server 2019、Windows Server 2016、Windows Server 2012r2 でさらに、 [KB 3133690](https://support.microsoft.com/kb/3133690)適用、およびさまざまなディストリビューションの[Linux OS。](../supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows.md)

## <a name="system-requirements"></a>システム要件
加え、 [Windows Server のシステム要件の](../../../get-started/System-Requirements--and-Installation.md)と[、HYPER-V のシステム要件](../System-requirements-for-Hyper-V-on-Windows.md)、個別のデバイスの割り当て許可の対応しているサーバー クラスのハードウェアが必要です、オペレーティング システムに制御できる、PCIe ファブリック (ネイティブ PCI Express コントロール) を構成します。 また、PCIe ルート複合では「アクセス制御サービス」(ACS) は、これにより、I/O MMU を介してすべての PCIe トラフィックを強制するには、HYPER-V をサポートするためにします。

通常、これらの機能は、サーバーの BIOS で直接公開されませんし、多くの場合、その他の設定の背後にある非表示にします。  たとえば、同じ機能の SR-IOV サポートに必要なし、BIOS では、「、SR-IOV を有効にする」を設定する必要があります。  システムのベンダーに連絡してください、BIOS で正しい設定を特定できない場合。

ハードウェア、ハードウェアが個別のデバイスの割り当ての対応であることを確認するには、マイクロソフトのエンジニアが、その間、[マシン プロファイル スクリプト](#machine-profile-script)ことで、有効になっている HYPER-V ホスト サーバーが正しくセットアップされ、どのような場合は、テストを行うことができますデバイスは、個別のデバイスの割り当ての対応。

## <a name="device-requirements"></a>デバイスの要件
常にではなく PCIe デバイスは、個別のデバイスの割り当てで使用できます。  たとえば、レガシ (INTx) PCI 割り込みを利用する古いデバイスはサポートされていません。 Jake Oshin の[ブログの投稿](https://blogs.technet.microsoft.com/virtualization/2015/11/20/discrete-device-assignment-machines-and-devices/)、コンシューマーは、実行の詳細についての詳細 - ただしに移動して、[マシン プロファイル スクリプト](#machine-profile-script)いる個別のデバイスの割り当てに使用できるデバイスが表示されます。

デバイスの製造元は、詳細については、Microsoft の担当者に連絡できます。

## <a name="device-driver"></a>デバイス ドライバー
ように、ゲスト VM に個別のデバイスの割り当てが PCIe デバイス全体を渡すと、ホスト ドライバーと、VM 内でマウントされているデバイスの前にインストールする必要はありません。  ホスト上の唯一の要件は、デバイスの[PCIe ロケーション パス](#pcie-location-path)決定できます。  デバイスのドライバーは、これにより、デバイスを特定する場合に必要に応じてインストールできます。  たとえば、せず、ホストにインストールされているデバイス ドライバーの GPU 基本的なレンダリング デバイスとして表示されます。  デバイス ドライバーがインストールされている場合、製造元とモデルは表示可能性があります。

デバイスをマウントするには、ゲスト内で、デバイス ドライバーの製造元のことができます、ゲスト仮想マシン内で通常どおりインストールされました。  

## <a name="virtual-machine-limitations"></a>仮想マシンの制限事項
個別のデバイスの割り当てを実装する方法の性質上、仮想マシンの一部の機能は、デバイスを接続するときに制限されます。  次の機能は使用できません。
- VM の保存/復元
- VM のライブ マイグレーション
- 動的メモリの使用
- 高可用性 (HA) クラスターに VM の追加

## <a name="security"></a>セキュリティ
個別のデバイスの割り当ては、VM に、デバイス全体を渡します。  つまり、そのデバイスのすべての機能は、ゲスト オペレーティング システムからアクセスできます。 ファームウェアの更新など、一部の機能は、システムの安定性に悪影響を及ぼす可能性があります。 そのため、ホストからデバイスのマウントを解除するときに、管理者に多数の警告が表示されます。 個別のデバイスの割り当てが、Vm のテナントが信頼できるのみ使用を強くお勧めします。  

管理者、信頼されていないテナントでデバイスを使用する場合、ホスト上インストール可能な軽減策のデバイス ドライバーを作成する機能をデバイスの製造元を用意しました。  軽減策のデバイス ドライバーを提供するかどうかについて詳しくは、デバイスの製造元にお問い合わせください。

軽減策のデバイス ドライバがないデバイスのセキュリティ チェックを回避するには、渡す必要があります、`-Force`パラメーターを`Dismount-VMHostAssignableDevice`コマンドレット。  理解これにより、そのシステムのセキュリティ プロファイルを変更したのみプロトタイプの作成時に推奨または信頼された環境。

## <a name="pcie-location-path"></a>PCIe ロケーション パス
マウントを解除して、ホストからデバイスをマウントするには、PCIe 場所のパスが必要です。  場所のパスの例は、次のように:`"PCIROOT(20)#PCI(0300)#PCI(0000)#PCI(0800)#PCI(0000)"`します。   [マシン プロファイル スクリプト](#machine-profile-script)も PCIe デバイスの場所のパスを返します。

### <a name="getting-the-location-path-by-using-device-manager"></a>デバイス マネージャーを使用して場所のパスを取得する.
![デバイス マネージャー](../deploy/media/dda-devicemanager.png)
- デバイス マネージャーを開き、デバイスを探します。  
- デバイスを右クリックし、「プロパティです。」を選択します。
- [詳細] タブに移動し、プロパティのドロップダウンで「場所のパス」を選択します。  
- "PCIROOT"で始まるエントリを右クリックし、[コピー] を選択します。  そのデバイスの場所のパスがあるようになりました。

## <a name="mmio-space"></a>MMIO 領域
一部のデバイス、特にの Gpu では、余分な MMIO 領域にアクセスできるデバイスのメモリを VM に割り当てることが必要です。 既定では、128 MB の領域が不足して MMIO から、各 VM を開始して、512 MB の高い MMIO 容量が割り当てられます。 ただし、デバイスは MMIO スペースを増やす必要があります。 または複数のデバイスは、結合の要件は、これらの値を超えるように、を通じて渡すことができます。  MMIO 領域を変更するはとても簡単ですし、次のコマンドを使用して、PowerShell で実行できます。

```
Set-VM -LowMemoryMappedIoSpace 3Gb -VMName $vm
Set-VM -HighMemoryMappedIoSpace 33280Mb -VMName $vm
```
MMIO 領域の量を割り当てるには、使用するかを判断する最も簡単な方法、[マシン プロファイル スクリプト](#machine-profile-script)します。  デバイス マネージャーを使用してを計算することができます。 TechNet ブログの投稿を参照してください[個別のデバイスの割り当て - Gpu](https://blogs.technet.microsoft.com/virtualization/2015/11/23/discrete-device-assignment-gpus/)の詳細。

## <a name="machine-profile-script"></a>マシン プロファイル スクリプト
サーバーが正しく構成されている場合を識別してをどのようなデバイスは個別のデバイスの割り当てを使用して渡すことを簡素化するために、エンジニアの 1 つをまとめる次の PowerShell スクリプト。[SurveyDDA.ps1 します。](https://github.com/Microsoft/Virtualization-Documentation/blob/live/hyperv-tools/DiscreteDeviceAssignment/SurveyDDA.ps1)

スクリプトを使用する前にインストールされている、HYPER-V ロールがあるし、管理者特権を持つ PowerShell コマンド ウィンドウからスクリプトを実行するを確認してください。

システムが個別のデバイスの割り当てをサポートするために正しく構成されていない、ツールにより、問題については、エラー メッセージが表示されます。 ツールによって正しく構成されているシステムで見つかった場合は、PCIe バスが見つかるすべてのデバイスが列挙されます。

見つかったデバイスごとに個別のデバイスの割り当てで使用できるかどうか、ツールが表示されます。 デバイスは、個別のデバイスの割り当てと互換性のあるものとして識別されます、スクリプトは、理由を提供します。  互換性のあるものとして、デバイスが正常に識別されると、デバイスの場所のパスが表示されます。  さらに、そのデバイスが必要な場合[MMIO 領域](#mmio-space)も表示されます。

![SurveyDDA.ps1](./images/hyper-v-surveydda-ps1.png)

## <a name="frequently-asked-questions"></a>よく寄せられる質問

### <a name="how-does-remote-desktops-remotefx-vgpu-technology-relate-to-discrete-device-assignment"></a>個別のデバイスの割り当てにはリモート デスクトップの RemoteFX vGPU のテクノロジはどのように関連しますか。
これらは、完全に独立したテクノロジです。 RemoteFX vGPU を操作する個別のデバイスの割り当てをインストールする必要はありません。 さらに、追加の役割をインストールする必要はありません。 RemoteFX vGPU には、VM に存在する RemoteFX vGPU ドライバーの順序でインストールする RDVH ロールが必要です。 個別のデバイスの割り当ての仮想マシンにハードウェアの製造元のドライバーをインストールするため役割を追加する必要はありません存在します。  

### <a name="ive-passed-a-gpu-into-a-vm-but-remote-desktop-or-an-application-isnt-recognizing-the-gpu"></a>VM に、GPU を渡すはしましたが、リモート デスクトップまたはアプリケーションが GPU に認識されていません。
この状況が発生する理由がいくつかが、いくつかの一般的な問題を以下に示します。
- 最新の GPU 製造元のドライバーがインストールされているし、は、デバイス マネージャー内デバイスの状態をチェックしてエラーを報告していないことを確認します。
- そのデバイスに十分な[MMIO 領域](#mmio-space)VM 内で割り当てられました。
- 仕入先がサポートするために使用されているこの構成では GPU を使用していることを確認します。 たとえば、一部のベンダーは、作業用 VM に渡されるときに、コンシューマーのカードを防ぐ。
- サポートしていますが、VM 内で実行されていると、アプリケーションで、GPU とその関連するドライバーの両方がサポートされていることを実行中のアプリケーションを確認します。 一部のアプリケーションでは、Gpu と環境のホワイト リストがあります。
- ゲスト上、リモート デスクトップ セッション ホスト役割または Windows Multipoint Services を使用している場合は、既定の GPU の使用を許可するグループ ポリシーの特定のエントリが設定されていることを確認する必要があります。 ゲスト (またはゲスト上のローカル グループ ポリシー エディター) に適用されるグループ ポリシー オブジェクトを使用して、グループ ポリシーの次の項目に移動します。
   - コンピューターの構成
   - 管理者のテンプレート
   - Windows コンポーネント
   - リモート デスクトップ サービス
   - リモート デスクトップ セッション ホスト
   - リモート セッション環境
   - すべてのリモート デスクトップ サービス セッションにハードウェアの既定のグラフィックス アダプターを使用する

    この値が有効に設定し、ポリシーが適用されると、VM を再起動します。

### <a name="can-discrete-device-assignment-take-advantage-of-remote-desktops-avc444-codec"></a>個別のデバイスの割り当てを利用してリモート デスクトップの AVC444 コーデックのでしょうか。
はい、詳細については、このブログ投稿を参照してください。[Windows 10 および Windows Server 2016 Technical Preview でのリモート デスクトップ プロトコル (RDP) 10 AVC/H.264 強化します。](https://blogs.technet.microsoft.com/enterprisemobility/2016/01/11/remote-desktop-protocol-rdp-10-avch-264-improvements-in-windows-10-and-windows-server-2016-technical-preview/)

### <a name="can-i-use-powershell-to-get-the-location-path"></a>PowerShell を使用して、場所のパスを取得できますか。
はい、これにはこれを行うさまざまな方法があります。 1 つの例を次に示します。
```
#Enumerate all PNP Devices on the system
$pnpdevs = Get-PnpDevice -presentOnly
#Select only those devices that are Display devices manufactured by NVIDIA
$gpudevs = $pnpdevs |where-object {$_.Class -like "Display" -and $_.Manufacturer -like "NVIDIA"}
#Select the location path of the first device that's available to be dismounted by the host.
$locationPath = ($gpudevs | Get-PnpDeviceProperty DEVPKEY_Device_LocationPaths).data[0]
```

### <a name="can-discrete-device-assignment-be-used-to-pass-a-usb-device-into-a-vm"></a>USB デバイスを VM に渡す個別のデバイスの割り当てを使用できますか。
正式にはサポートされていますが、お客様が USB3 コント ローラー全体を VM に渡すことによってこれを行うに個別のデバイスの割り当てを使用します。  全体のコント ローラーがで渡されるとそのコント ローラーに接続されている各 USB デバイスは、VM にアクセスできます。  一部 USB3 コント ローラーのみが機能すると、メモと USB2 コント ローラーは、個別のデバイスの割り当てでは使用できません。
