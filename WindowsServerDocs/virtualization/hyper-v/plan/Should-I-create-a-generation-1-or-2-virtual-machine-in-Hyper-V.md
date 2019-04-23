---
title: HYPER-V でジェネレーション 1 または 2 の仮想マシンを作成するか。
description: サポートされているなどの考慮事項のブート方法とジェネレーションがニーズを満たしているかを選択するのに役立つその他の機能の相違点を与えます。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 02e31413-6140-4723-a8d6-46c7f667792d
author: KBDAzure
ms.author: kathydav
ms.date: 12/05/2016
ms.openlocfilehash: 48319e057da9c815a77349bba34996f89973d85a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59850503"
---
# <a name="should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v"></a>HYPER-V でジェネレーション 1 または 2 の仮想マシンを作成するか。

>適用先:Windows 10、Windows Server 2016、Microsoft HYPER-V Server 2016、Windows Server 2019、Microsoft HYPER-V Server 2019

> [!WARNING]
> これまで、オンプレミスから Microsoft Azure への Windows 仮想のマシン (VM) をアップロードする予定の場合**第 1 世代の Vm のみ**VHD ファイルの形式であり、固定サイズのディスクがあるがサポートされています。 Windows VHD または VHDX をアップロードする方法の詳細については、次を参照してください。 [Azure にアップロードするには、Windows VHD または VHDX を準備する](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/prepare-for-upload-vhd-image)します。

第 1 世代または第 2 世代バーチャル マシンを作成するために選択を選んでいるゲスト オペレーティング システムのインストールと仮想マシンを展開に使用するブート方法です。 次のステートメントのいずれかが true でない限り、セキュア ブートのような機能を活用する第 2 世代バーチャル マシンを作成することをお勧めします。  

- ブートする VHD が存在しない [UEFI と互換性のある](https://technet.microsoft.com/library/hh824898.aspx)です。  
- 第 2 世代バーチャル マシンで実行するオペレーティング システムをサポートしていません。  
- 第 2 世代は、使用するブート方法をサポートしていません。  

詳細については、第 2 世代仮想マシンで使用できる機能は、次を参照してください。[生成とゲストでの Hyper-v 機能の互換性](../Hyper-V-feature-compatibility-by-generation-and-guest.md)します。

作成した後、バーチャル マシンの世代を変更することはできません。 そのため、ことを確認する際の考慮事項は、ここでは、だけでなく、オペレーティング システム、ブートの方法と、世代を選択する前に使用する機能の選択を勧めします。  

## <a name="BKMK_OS"></a>ゲスト オペレーティング システムがサポートされていますか。

第 1 世代バーチャル マシンは、ほとんどのゲスト オペレーティング システムをサポートします。 第 2 世代バーチャル マシンは、最も 64 ビット バージョンの Windows および Linux および FreeBSD オペレーティング システムの最新のバージョンをサポートします。 次のセクションを使用して、仮想マシンのサポートをインストールするゲスト オペレーティング システムを参照してください。  

- [Windows ゲスト オペレーティング システムのサポート](Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md#BKMK_Windows)  

- [CentOS と Red Hat Enterprise Linux ゲスト オペレーティング システムのサポート](Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md#BKMK_CentOS)  

- [Debian ゲスト オペレーティング システムのサポート](Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md#BKMK_Debian)  

- [FreeBSD ゲスト オペレーティング システムのサポート](Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md#BKMK_FreeBSD)  

- [Oracle Linux ゲスト オペレーティング システムのサポート](Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md#BKMK_Oracle)  

- [SUSE のゲスト オペレーティング システムのサポート](Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md#BKMK_SUSE)  

- [Ubuntu のゲスト オペレーティング システムのサポート](Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md#BKMK_Ubuntu)  

### <a name="BKMK_Windows"></a>Windows ゲスト オペレーティング システムのサポート

次の表では、Windows の 64 ビット バージョンとして使用できます、ゲスト オペレーティング システムの第 1 世代と第 2 世代バーチャル マシンを示します。  

|64 ビット バージョンの Windows|第 1 世代|第 2 世代|  
|-------------------------------|----------------|----------------|  
| Windows Server 2019 |&#10004;|&#10004;|  
| Windows Server 2016 |&#10004;|&#10004;|  
| Windows Server 2012 R2 |&#10004;|&#10004;|  
| Windows Server 2012 |&#10004;|&#10004;|  
|Windows Server 2008 R2|&#10004;| &#10006;|  
|Windows Server 2008|&#10004;| &#10006;|  
|Windows 10|&#10004;|&#10004;|  
|Windows 8.1|&#10004;|&#10004;|  
|Windows 8|&#10004;|&#10004;|  
|Windows 7|&#10004;| &#10006;|

次の表では、Windows の 32 ビット バージョンとして使用できます、ゲスト オペレーティング システムの第 1 世代と第 2 世代バーチャル マシンを示します。

|32 ビット バージョンの Windows|第 1 世代|第 2 世代|  
|-------------------------------|----------------|----------------|  
|Windows 10|&#10004;| &#10006;|  
|Windows 8.1|&#10004;| &#10006;|  
|Windows 8|&#10004;| &#10006;|  
|Windows 7|&#10004;| &#10006;|  

### <a name="BKMK_CentOS"></a>CentOS と Red Hat Enterprise Linux ゲスト オペレーティング システムのサポート

次の表に、Red Hat Enterprise Linux のバージョン\(RHEL\) CentOS として使用できます、ゲスト オペレーティング システムの第 1 世代と第 2 世代仮想マシンとします。

|オペレーティング システムのバージョン|第 1 世代|第 2 世代|  
|-----------------------------|----------------|----------------|  
|RHEL/CentOS 7.x シリーズ|&#10004;|&#10004;|  
|RHEL/CentOS 6.x シリーズ|&#10004;|&#10004;<br />**注:** Windows Server 2016 でのみサポートされます。|  
|RHEL/CentOS 5.x シリーズ|&#10004;| &#10006;|  

詳細については、次を参照してください。 [CentOS、Red Hat Enterprise Linux 仮想マシンを Hyper-v](../Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)します。  

### <a name="BKMK_Debian"></a>Debian ゲスト オペレーティング システムのサポート  

Debian のバージョンとして使用できます、ゲスト オペレーティング システムの第 1 世代と第 2 世代バーチャル マシンを次の表に示します。

|オペレーティング システムのバージョン|第 1 世代|第 2 世代|  
|-----------------------------|----------------|----------------|  
|Debian 7.x シリーズ|&#10004;| &#10006;|  
|Debian 8.x シリーズ|&#10004;|&#10004;|  

詳細については、次を参照してください。 [Debian の仮想マシンを Hyper-v](../Supported-Debian-virtual-machines-on-Hyper-V.md)します。  

### <a name="BKMK_FreeBSD"></a>FreeBSD ゲスト オペレーティング システムのサポート

次の表では、FreeBSD のバージョンとして使用できます、ゲスト オペレーティング システムの第 1 世代と第 2 世代バーチャル マシンを示します。  

|オペレーティング システムのバージョン|第 1 世代|第 2 世代|  
|-----------------------------|----------------|----------------|  
|FreeBSD 10 と 10.1|&#10004;| &#10006;|  
|FreeBSD 9.1 および 9.3|&#10004;| &#10006;|  
|FreeBSD 8.4|&#10004;| &#10006;|  

詳細については、次を参照してください。 [Hyper-v 上のバーチャル マシンを FreeBSD](../Supported-FreeBSD-virtual-machines-on-Hyper-V.md)します。  

### <a name="BKMK_Oracle"></a>Oracle Linux ゲスト オペレーティング システムのサポート  

次の表では、Red Hat 互換カーネル シリーズのバージョンとして使用できます、ゲスト オペレーティング システムの第 1 世代と第 2 世代バーチャル マシンを示します。  

|Red Hat 互換カーネル シリーズのバージョン|第 1 世代|第 2 世代|  
|---------------------------------------------|----------------|----------------|  
|Oracle Linux 7.x シリーズ|&#10004;|&#10004;|
|Oracle Linux 6.x シリーズ|&#10004;| &#10006;|  

次の表では、Unbreakable Enterprise Kernel のバージョンとして使用できます、ゲスト オペレーティング システムの第 1 世代と第 2 世代バーチャル マシンを示します。

|Unbreakable Enterprise カーネル (UEK) バージョン|第 1 世代|第 2 世代|  
|--------------------------------------------------|----------------|----------------|  
|Oracle Linux UEK R3 QU3|&#10004;| &#10006;|  
|Oracle Linux UEK R3 QU2|&#10004;| &#10006;|  
|Oracle Linux UEK R3 QU1|&#10004;| &#10006;|  

詳細については、次を参照してください。 [Hyper-v 上の Oracle Linux 仮想マシン](../Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)します。  

### <a name="BKMK_SUSE"></a>SUSE のゲスト オペレーティング システムのサポート

次の表では、SUSE のどのバージョンとして使用できます、ゲスト オペレーティング システムの第 1 世代と第 2 世代仮想マシンを示します。

|オペレーティング システムのバージョン|第 1 世代|第 2 世代|  
|-----------------------------|----------------|----------------|  
|SUSE Linux Enterprise Server 12 シリーズ|&#10004;|&#10004;|  
|SUSE Linux Enterprise Server 11 シリーズ|&#10004;| &#10006;|  
|Open SUSE 12.3|&#10004;| &#10006;|  

詳細については、次を参照してください。 [Hyper-v 上のバーチャル マシンを SUSE](../Supported-SUSE-virtual-machines-on-Hyper-V.md)します。  

### <a name="BKMK_Ubuntu"></a>Ubuntu のゲスト オペレーティング システムのサポート

次の表では、Ubuntu のバージョンとして使用できます、ゲスト オペレーティング システムの第 1 世代と第 2 世代バーチャル マシンを示します。

|オペレーティング システムのバージョン|第 1 世代|第 2 世代|  
|-----------------------------|----------------|----------------|  
|Ubuntu 14.04 およびそれ以降のバージョン|&#10004;|&#10004;|  
|Ubuntu 12.04|&#10004;| &#10006;|  

詳細については、次を参照してください。 [Ubuntu 仮想マシンを Hyper-v で](../Supported-Ubuntu-virtual-machines-on-Hyper-V.md)します。  

## <a name="BKMK_Boot"></a>仮想マシンを起動する方法は?

次の表は、メソッドは第 1 世代と第 2 世代仮想マシンでサポートされているブートを示します。  

|起動方法|第 1 世代|第 2 世代|  
|---------------|----------------|----------------|  
|標準のネットワーク アダプターを使用した PXE ブート| &#10006;|&#10004;|  
|レガシ ネットワーク アダプターを使用して PXE ブート|&#10004;| &#10006;|  
|SCSI バーチャル ハード_ディスクからブート (します。VHDX) またはバーチャル DVD (します。ISO)| &#10006;|&#10004;|  
|IDE コント ローラーのバーチャル ハード_ディスクからブート (します。VHD) またはバーチャル DVD (します。ISO)|&#10004;| &#10006;|  
|フロッピーからの起動 (します。VFD)|&#10004;| &#10006;|  

## <a name="BKMK_Advantages"></a>第 2 世代仮想マシンを使用する利点とは

第 2 世代バーチャル マシンを使用する場合のメリットの一部を次に示します。  
- **セキュア ブート**これは、ブート ローダーが承認されていないファームウェア、オペレーティング システム、または UEFI ドライバーがブート時に実行されていることを防ぐために、UEFI データベースで信頼されている機関によって署名されたことを確認する機能です。 セキュア ブートは、第 2 世代仮想マシンでは既定で有効になります。 セキュア ブートでサポートされていないゲスト オペレーティング システムを実行する必要がある場合に、バーチャル マシンの作成後に無効にできます。  詳細については、次を参照してください。 [セキュア ブート](https://technet.microsoft.com/library/dn486875.aspx)します。  

    セキュア ブートの第 2 世代の Linux 仮想マシン、仮想マシンを作成するときに、UEFI CA セキュア ブート テンプレートを選択する必要があります。  

- **ブート ボリュームの大きい**第 2 世代仮想マシンの最大のブート ボリュームは 64 TB です。 これは、最大ディスク サイズでサポートされているのです。VHDX します。 第 1 世代バーチャル マシンの最大のブート ボリュームは用に 2 TB をします。VHDX と 2040 gb 以上、します。VHD です。 詳細については、次を参照してください。 [Hyper-v 仮想ハード ディスク フォーマットに関するテクニカル プレビュー](https://technet.microsoft.com/library/hh831446.aspx)します。  

 第 2 世代仮想マシンで仮想マシンのブートとインストール時間にわずかな改善を表示することもあります。

## <a name="BKMK_DeviceCompare"></a> デバイスのサポートの違いは何ですか。

次の表では、第 1 世代と第 2 世代仮想マシン間で使用可能なデバイスを比較します。  

|第 1 世代デバイス|第 2 世代置換|第 2 世代拡張|  
|-----------------------|----------------------------|-----------------------------|  
|IDE コントローラー|仮想 SCSI コントローラー|.vhdx から起動 (最大サイズ 64 TB、オンライン サイズ変更機能)|  
|IDE CD-ROM|仮想 SCSI CD-ROM|SCSI コントローラーあたり最大 64 台の SCSI DVD デバイスをサポート|  
|従来の BIOS|UEFI ファームウェア|セキュア ブート|  
|レガシ ネットワーク アダプター|合成ネットワーク アダプター|IPv4 および IPv6 でのネットワーク ブート|  
|フロッピー コントローラーおよび DMA コントローラー|フロッピー コントローラーのサポートはなし|なし|  
|COM ポートに対する Universal Asynchronous Receiver/Transmitter (UART)|デバッグ用のオプション UART|より高速で高信頼性|  
|i8042 キーボード コントローラー|ソフトウェア ベースの入力|エミュレーションがないため、使用するリソースが減ります。 また、ゲスト オペレーティング システムから攻撃を受ける機会が減少します。|  
|PS/2 キーボード|ソフトウェア ベースのキーボード|エミュレーションがないため、使用するリソースが減ります。 また、ゲスト オペレーティング システムから攻撃を受ける機会が減少します。|  
|PS/2 マウス|ソフトウェア ベースのマウス|エミュレーションがないため、使用するリソースが減ります。 また、ゲスト オペレーティング システムから攻撃を受ける機会が減少します。|  
|S3 ビデオ|ソフトウェア ベースのビデオ|エミュレーションがないため、使用するリソースが減ります。 また、ゲスト オペレーティング システムから攻撃を受ける機会が減少します。|  
|PCI バス|必要ありません|なし|  
|Programmable Interrupt Controller (PIC)|必要ありません|なし|  
|Programmable Interval Timer (PIT)|必要ありません|なし|  
|スーパー I/O デバイス|必要ありません|なし|  

## <a name="BKMK_More"></a> 第 2 世代仮想マシンの詳細

第 2 世代仮想マシンの使用に関するいくつかその他のヒントを次に示します。

### <a name="attach-or-add-a-dvd-drive"></a>接続または DVD ドライブを追加

- 物理 CD または DVD ドライブは、第 2 世代仮想マシンに接続できません。 第 2 世代仮想マシンの仮想 DVD ドライブは、ISO イメージ ファイルだけをサポートします。 Windows 環境の ISO イメージ ファイルは、Oscdimg コマンド ライン ツールを使用して作成できます。 詳細については、「 [Oscdimg のコマンド ライン オプション](https://msdn.microsoft.com/library/hh824847.aspx)」を参照してください。
- NEW-VM Windows PowerShell コマンドレットで新しいバーチャル マシンを作成するときに、第 2 世代仮想マシンに DVD ドライブはありません。 仮想マシンの実行中には、DVD ドライブを追加できます。

### <a name="use-uefi-firmware"></a>UEFI ファームウェアを使用します。

- セキュア ブートまたは UEFI ファームウェアは、物理的な HYPER-V ホスト上必要ではありません。 HYPER-V では、HYPER-V ホスト上にあるものとは無関係の仮想マシンに仮想のファームウェアを提供します。
- 第 2 世代仮想マシンでの UEFI ファームウェアでは、セキュア ブートのセットアップ モードをサポートしていません。
- 第 2 世代仮想マシンで UEFI シェルまたは他の UEFI アプリケーションを実行しているサポートされていません。 マイクロソフト以外の UEFI シェルまたは UEFI アプリケーションの使用は、それらがソースから直接コンパイルされている場合であれば、技術的には可能です。 これらのアプリケーションが適切にデジタル署名されていない場合、仮想マシンのセキュア ブートを無効にする必要があります。

### <a name="work-with-vhdx-files"></a>VHDX ファイルを使用します。

- 仮想マシンの実行中には、第 2 世代バーチャル マシンのブート ボリュームを含む VHDX ファイルのサイズを変更することができます。
- サポートまたは推奨第 1 世代と第 2 世代バーチャル マシンの両方を起動可能な VHDX ファイルを作成することはしないでください。  
- 仮想マシンの世代は、仮想マシンのプロパティであり、仮想ハード ディスクのプロパティではありません。 したがって、第 1 世代または第 2 世代仮想マシンで VHDX ファイルが作成されていないかを判断できません。  
- IDE コント ローラーまたは第 1 世代バーチャル マシンの SCSI コント ローラーに接続できる 2 つの仮想マシンの世代で作成された VHDX ファイル。 ただし、起動可能な VHDX ファイルの場合は、第 1 世代バーチャル マシンは起動しません。

### <a name="use-ipv6-instead-of-ipv4"></a>IPv4 ではなく IPv6 を使用します。

既定では、第 2 世代仮想マシンは IPv4 を使用します。 代わりに IPv6 を使用して、実行、 [Set-vmfirmware](https://technet.microsoft.com/library/dn464287.aspx) Windows PowerShell コマンドレット。 たとえば、次のコマンドは、TestVM という名前のバーチャル マシンの IPv6 に優先プロトコルを設定します。  

```powershell
Set-VMFirmware -VMName TestVM -IPProtocolPreference IPv6  
```  

## <a name="BKMK_Debug"></a>カーネル デバッグ用に COM ポートを追加します。

COM ポートは、それらを追加するまで第 2 世代仮想マシンでは使用されません。 Windows PowerShell または Windows Management Instrumentation (WMI) で、これを行うことができます。 次の手順では、Windows PowerShell を使用する方法を示します。

COM ポートを追加します。  

1. セキュア ブートを無効にします。 セキュア ブートと互換性のないカーネルのデバッグ。 バーチャル マシンがオフの状態になっていることを確認し、使用して、 [Set-vmfirmware](https://technet.microsoft.com/library/dn464287.aspx)コマンドレット。 たとえば、次のコマンドでは、仮想マシン TestVM でセキュア ブートを無効にします。  

    ```powershell  
    Set-VMFirmware -Vmname TestVM -EnableSecureBoot Off  
    ```  

2. COM ポートを追加します。 使用して、 [Set-vmcomport](https://technet.microsoft.com/library/hh848616.aspx)これを行うコマンドレット。 たとえば、次のコマンドは、仮想マシンの名前付きパイプ TestPipe、ローカル コンピューター上に接続するための TestVM で最初の COM ポートを構成します。  

    ```powershell
    Set-VMComPort -VMName TestVM 1 \\.\pipe\TestPipe  
    ```  

> [!NOTE]  
> HYPER-V マネージャーで仮想マシンの設定で構成した COM ポートが記載されていません。

## <a name="see-also"></a>関連項目  

- [Linux および FreeBSD Virtual Machines on Hyper-v の概要](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)
- [VMConnect を使って、HYPER-V 仮想マシン上のローカル リソースの使用](../learn-more/Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)
- [Windows Server 2016 での HYPER-V のスケーラビリティの計画します。](Plan-for-Hyper-V-scalability-in-Windows-Server-2016.md)