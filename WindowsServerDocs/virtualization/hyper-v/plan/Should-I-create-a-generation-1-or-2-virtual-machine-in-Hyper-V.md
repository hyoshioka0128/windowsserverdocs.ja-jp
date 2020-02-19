---
title: HYPER-V でジェネレーション 1 または 2 の仮想マシンを作成するか。
description: サポートされているブート方法やその他の機能の違いなど、ニーズを満たす世代を選択する際に役立つ考慮事項を示します。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 02e31413-6140-4723-a8d6-46c7f667792d
author: KBDAzure
ms.author: kathydav
ms.date: 12/05/2016
ms.openlocfilehash: fce9b45f538b0d506b621b888d413c99590b1362
ms.sourcegitcommit: 2a15de216edde8b8e240a4aa679dc6d470e4159e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/19/2020
ms.locfileid: "77465556"
---
# <a name="should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v"></a>HYPER-V でジェネレーション 1 または 2 の仮想マシンを作成するか。

>適用対象: Windows 10、Windows Server 2016、Microsoft Hyper-V Server 2016、Windows Server 2019、Microsoft Hyper-V Server 2019

> [!NOTE]
> Windows 仮想マシン (Vm) をオンプレミスから Microsoft Azure にアップロードする予定がある場合、第1世代と第2世代の Vm を VHD ファイル形式でアップロードし、容量固定のディスクを使用することがサポートされています。 Azure でサポートされている第2世代の機能の詳細については、「 [azure での第2世代の vm](https://docs.microsoft.com/azure/virtual-machines/windows/generation-2) 」を参照してください。 Windows VHD または VHDX のアップロードの詳細については、「 [Azure にアップロードする WINDOWS vhd または vhdx を準備](https://docs.microsoft.com/azure/virtual-machines/windows/prepare-for-upload-vhd-image)する」を参照してください。

第 1 世代または第 2 世代バーチャル マシンを作成するために選択を選んでいるゲスト オペレーティング システムのインストールと仮想マシンを展開に使用するブート方法です。 次のステートメントのいずれかが true でない限り、セキュア ブートのような機能を活用する第 2 世代仮想マシンを作成することをお勧めします。  

- ブートする VHD が存在しない [UEFI と互換性のある](https://technet.microsoft.com/library/hh824898.aspx)です。  
- 第 2 世代では、仮想マシンで実行するオペレーティング システムがサポートされていません。  
- 第 2 世代は、使用するブート方法をサポートしていません。  

第2世代仮想マシンで使用できる機能の詳細については、「 [hyper-v の機能と世代とゲストの互換性](../Hyper-V-feature-compatibility-by-generation-and-guest.md)」を参照してください。

作成した後、仮想マシンの世代を変更することはできません。 そのため、ここで考慮事項を確認し、世代を選択する前に使用するオペレーティングシステム、ブート方法、および機能を選択することをお勧めします。  

## <a name="which-guest-operating-systems-are-supported"></a>ゲスト オペレーティング システムがサポートされますか。

第 1 世代仮想マシンは、ほとんどのゲスト オペレーティング システムをサポートします。 第 2 世代仮想マシンは、最も 64 ビット バージョンの Windows および Linux および FreeBSD オペレーティング システムの最新のバージョンをサポートします。 次のセクションを使用して、仮想マシンのサポートをインストールするゲスト オペレーティング システムを参照してください。  

- [Windows ゲストオペレーティングシステムのサポート](#windows-guest-operating-system-support)  

- [CentOS と Red Hat Enterprise Linux ゲストオペレーティングシステムのサポート](#centos-and-red-hat-enterprise-linux-guest-operating-system-support)  

- [Debian ゲストオペレーティングシステムのサポート](#debian-guest-operating-system-support)  

- [FreeBSD ゲストオペレーティングシステムのサポート](#freebsd-guest-operating-system-support)  

- [Oracle Linux のゲストオペレーティングシステムのサポート](#oracle-linux-guest-operating-system-support)  

- [SUSE ゲストオペレーティングシステムのサポート](#suse-guest-operating-system-support)  

- [Ubuntu ゲストオペレーティングシステムのサポート](#ubuntu-guest-operating-system-support)  

### <a name="windows-guest-operating-system-support"></a>Windows ゲスト オペレーティング システムのサポート

次の表は、第 1 世代と第 2 世代の仮想マシン用にどの 64 ビット バージョンの Windows をゲスト オペレーティング システムとして使用できるかを示しています。  

|64 ビット バージョンの Windows|第 1 世代|世代 2|  
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

次の表は、第 1 世代と第 2 世代の仮想マシン用にどの 32 ビット バージョンの Windows をゲスト オペレーティング システムとして使用できるかを示しています。

|32 ビット バージョンの Windows|第 1 世代|世代 2|  
|-------------------------------|----------------|----------------|  
|Windows 10|&#10004;| &#10006;|  
|Windows 8.1|&#10004;| &#10006;|  
|Windows 8|&#10004;| &#10006;|  
|Windows 7|&#10004;| &#10006;|  

### <a name="centos-and-red-hat-enterprise-linux-guest-operating-system-support"></a>CentOS、Red Hat Enterprise Linux ゲスト オペレーティング システムのサポート

次の表に、第1世代と第2世代の仮想マシンのゲストオペレーティングシステムとして使用できる、RHEL\) および CentOS \(Red Hat Enterprise Linux のバージョンを示します。

|オペレーティング システムのバージョン|第 1 世代|世代 2|  
|-----------------------------|----------------|----------------|  
|RHEL/CentOS 7.x シリーズ|&#10004;|&#10004;|  
|RHEL/CentOS 6.x シリーズ|&#10004;|&#10004;<br />**注:** Windows Server 2016 以降でのみサポートされています。|  
|RHEL/CentOS 5.x シリーズ|&#10004;| &#10006;|  

詳細については、次を参照してください。 [CentOS、Red Hat Enterprise Linux 仮想マシンを Hyper-v](../Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md)します。  

### <a name="debian-guest-operating-system-support"></a>Debian ゲスト オペレーティング システムのサポート  

次の表は、第 1 世代と第 2 世代の仮想マシン用にどのバージョンの Debian をゲスト オペレーティング システムとして使用できるかを示しています。

|オペレーティング システムのバージョン|第 1 世代|世代 2|  
|-----------------------------|----------------|----------------|  
|Debian 7.x シリーズ|&#10004;| &#10006;|  
|Debian 8. x シリーズ|&#10004;|&#10004;|  

詳細については、次を参照してください。 [Debian の仮想マシンを Hyper-v](../Supported-Debian-virtual-machines-on-Hyper-V.md)します。  

### <a name="freebsd-guest-operating-system-support"></a>FreeBSD ゲスト オペレーティング システムのサポート

次の表は、第 1 世代と第 2 世代の仮想マシン用にどのバージョンの FreeBSD をゲスト オペレーティング システムとして使用できるかを示しています。  

|オペレーティング システムのバージョン|第 1 世代|世代 2|  
|-----------------------------|----------------|----------------|  
|FreeBSD 10 と 10.1|&#10004;| &#10006;|  
|FreeBSD 9.1 および 9.3|&#10004;| &#10006;|  
|FreeBSD 8.4|&#10004;| &#10006;|  

詳しくは、[Hyper-V での FreeBSD 仮想マシン](../Supported-FreeBSD-virtual-machines-on-Hyper-V.md)に関する記事をご覧ください。  

### <a name="oracle-linux-guest-operating-system-support"></a>Oracle Linux ゲスト オペレーティング システムのサポート  

次の表は、第 1 世代と第 2 世代の仮想マシン用にどのバージョンの Red Hat Compatible Kernel Series をゲスト オペレーティング システムとして使用できるかを示しています。  

|Red Hat 互換カーネル シリーズのバージョン|第 1 世代|世代 2|  
|---------------------------------------------|----------------|----------------|  
|Oracle Linux 7.x シリーズ|&#10004;|&#10004;|
|Oracle Linux 6.x シリーズ|&#10004;| &#10006;|  

次の表は、第 1 世代と第 2 世代の仮想マシン用にどのバージョンの Unbreakable Enterprise Kernel をゲスト オペレーティング システムとして使用できるかを示しています。

|Unbreakable Enterprise カーネル (UEK) バージョン|第 1 世代|世代 2|  
|--------------------------------------------------|----------------|----------------|  
|Oracle Linux UEK R3 QU3|&#10004;| &#10006;|  
|Oracle Linux UEK R3 QU2|&#10004;| &#10006;|  
|Oracle Linux UEK R3 QU1|&#10004;| &#10006;|  

詳細については、次を参照してください。 [Hyper-v 上の Oracle Linux 仮想マシン](../Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)します。  

### <a name="suse-guest-operating-system-support"></a>SUSE のゲスト オペレーティング システムのサポート

次の表は、第1世代および第2世代仮想マシンのゲストオペレーティングシステムとして使用できる SUSE のバージョンを示しています。

|オペレーティング システムのバージョン|第 1 世代|世代 2|  
|-----------------------------|----------------|----------------|  
|SUSE Linux Enterprise Server 12 シリーズ|&#10004;|&#10004;|  
|SUSE Linux Enterprise Server 11 シリーズ|&#10004;| &#10006;|  
|Open SUSE 12.3|&#10004;| &#10006;|  

詳細については、[Hyper-V での SUSE 仮想マシン](../Supported-SUSE-virtual-machines-on-Hyper-V.md)に関する記事をご覧ください。  

### <a name="ubuntu-guest-operating-system-support"></a>Ubuntu のゲスト オペレーティング システムのサポート

次の表は、第 1 世代と第 2 世代の仮想マシン用にどのバージョンの Ubuntu をゲスト オペレーティング システムとして使用できるかを示しています。

|オペレーティング システムのバージョン|第 1 世代|世代 2|  
|-----------------------------|----------------|----------------|  
|Ubuntu 14.04 およびそれ以降のバージョン|&#10004;|&#10004;|  
|Ubuntu 12.04|&#10004;| &#10006;|  

詳細については、次を参照してください。 [Ubuntu 仮想マシンを Hyper-v で](../Supported-Ubuntu-virtual-machines-on-Hyper-V.md)します。  

## <a name="how-can-i-boot-the-virtual-machine"></a>仮想マシンを起動する方法は?

次の表は、メソッドは第 1 世代と第 2 世代仮想マシンでサポートされているブートを示します。  

|起動方法|第 1 世代|世代 2|  
|---------------|----------------|----------------|  
|標準のネットワーク アダプターを使用した PXE ブート| &#10006;|&#10004;|  
|レガシ ネットワーク アダプターを使用して PXE ブート|&#10004;| &#10006;|  
|SCSI バーチャル ハード_ディスクからブート (します。VHDX) またはバーチャル DVD (します。ISO)| &#10006;|&#10004;|  
|IDE コント ローラーのバーチャル ハード_ディスクからブート (します。VHD) またはバーチャル DVD (します。ISO)|&#10004;| &#10006;|  
|フロッピーからの起動 (します。VFD)|&#10004;| &#10006;|  

## <a name="what-are-the-advantages-of-using-generation-2-virtual-machines"></a>第 2 世代仮想マシンを使用する利点とは

第 2 世代仮想マシンを使用する場合のメリットの一部を次に示します。  
- **セキュアブート**これは、承認されていないファームウェア、オペレーティングシステム、または UEFI ドライバーが起動時に実行されないようにするために、ブートローダーが UEFI データベース内の信頼された機関によって署名されていることを確認する機能です。 セキュア ブートは、第 2 世代仮想マシンでは既定で有効になります。 セキュア ブートでサポートされていないゲスト オペレーティング システムを実行する必要がある場合に、仮想マシンの作成後に無効にできます。  詳細については、次を参照してください。 [セキュア ブート](https://technet.microsoft.com/library/dn486875.aspx)します。  

    セキュア ブートの第 2 世代の Linux 仮想マシン、仮想マシンを作成するときに、UEFI CA セキュア ブート テンプレートを選択する必要があります。  

- **大きなブートボリューム**第2世代仮想マシンの最大ブートボリュームは、64 TB です。 これは、最大ディスク サイズでサポートされているのです。VHDX します。 第 1 世代の仮想マシンの場合、最大のブート ボリュームは .VHDX の場合 2TB、.VHD の場合 2040 GB です。 詳細については、次を参照してください。 [Hyper-v 仮想ハード ディスク フォーマットに関するテクニカル プレビュー](https://technet.microsoft.com/library/hh831446.aspx)します。  

  第 2 世代仮想マシンで仮想マシンのブートとインストール時間にわずかな改善を表示することもあります。

## <a name="whats-the-difference-in-device-support"></a>デバイスのサポートの違いは何ですか。

次の表では、第 1 世代と第 2 世代仮想マシン間で使用可能なデバイスを比較します。  

|第 1 世代デバイス|第 2 世代置換|第 2 世代拡張|  
|-----------------------|----------------------------|-----------------------------|  
|IDE コントローラー|仮想 SCSI コントローラー|.vhdx から起動 (最大サイズ 64 TB、オンライン サイズ変更機能)|  
|IDE CD-ROM|仮想 SCSI CD-ROM|SCSI コントローラーあたり最大 64 台の SCSI DVD デバイスをサポート|  
|従来の BIOS|UEFI ファームウェア|セキュア ブート|  
|レガシ ネットワーク アダプター|[統合ネットワーク アダプター]|IPv4 および IPv6 でのネットワーク ブート|  
|フロッピー コントローラーおよび DMA コントローラー|フロッピー コントローラーのサポートはなし|N/A|  
|COM ポートに対する Universal Asynchronous Receiver/Transmitter (UART)|デバッグ用のオプション UART|より高速で高信頼性|  
|i8042 キーボード コントローラー|ソフトウェア ベースの入力|エミュレーションがないため、使用するリソースが減ります。 また、ゲスト オペレーティング システムから攻撃を受ける機会が減少します。|  
|PS/2 キーボード|ソフトウェア ベースのキーボード|エミュレーションがないため、使用するリソースが減ります。 また、ゲスト オペレーティング システムから攻撃を受ける機会が減少します。|  
|PS/2 マウス|ソフトウェア ベースのマウス|エミュレーションがないため、使用するリソースが減ります。 また、ゲスト オペレーティング システムから攻撃を受ける機会が減少します。|  
|S3 ビデオ|ソフトウェア ベースのビデオ|エミュレーションがないため、使用するリソースが減ります。 また、ゲスト オペレーティング システムから攻撃を受ける機会が減少します。|  
|PCI バス|必要ありません|N/A|  
|Programmable Interrupt Controller (PIC)|必要ありません|N/A|  
|Programmable Interval Timer (PIT)|必要ありません|N/A|  
|スーパー I/O デバイス|必要ありません|N/A|  

## <a name="more-about-generation-2-virtual-machines"></a>第 2 世代仮想マシンの詳細について

第2世代仮想マシンの使用に関するその他のヒントを次に示します。

### <a name="attach-or-add-a-dvd-drive"></a>DVD ドライブの接続または追加

- 物理 CD または DVD ドライブは、第 2 世代仮想マシンに接続できません。 第 2 世代仮想マシンの仮想 DVD ドライブは、ISO イメージ ファイルだけをサポートします。 Windows 環境の ISO イメージ ファイルは、Oscdimg コマンド ライン ツールを使用して作成できます。 詳細については、「 [Oscdimg のコマンド ライン オプション](https://msdn.microsoft.com/library/hh824847.aspx)」を参照してください。
- NEW-VM Windows PowerShell コマンドレットで新しいバーチャル マシンを作成するときに、第 2 世代仮想マシンに DVD ドライブはありません。 仮想マシンの実行中には、DVD ドライブを追加できます。

### <a name="use-uefi-firmware"></a>UEFI ファームウェアを使用する

- セキュア ブートまたは UEFI ファームウェアは、物理的な HYPER-V ホスト上必要ではありません。 HYPER-V では、HYPER-V ホスト上にあるものとは無関係の仮想マシンに仮想のファームウェアを提供します。
- 第 2 世代仮想マシンでの UEFI ファームウェアでは、セキュア ブートのセットアップ モードをサポートしていません。
- 第 2 世代仮想マシンで UEFI シェルまたは他の UEFI アプリケーションを実行しているサポートされていません。 マイクロソフト以外の UEFI シェルまたは UEFI アプリケーションの使用は、それらがソースから直接コンパイルされている場合であれば、技術的には可能です。 これらのアプリケーションが適切にデジタル署名されていない場合、仮想マシンのセキュア ブートを無効にする必要があります。

### <a name="work-with-vhdx-files"></a>VHDX ファイルを操作する

- 仮想マシンの実行中には、第 2 世代バーチャル マシンのブート ボリュームを含む VHDX ファイルのサイズを変更することができます。
- サポートまたは推奨第 1 世代と第 2 世代仮想マシンの両方を起動可能な VHDX ファイルを作成することはしないでください。  
- 仮想マシンの世代は、仮想マシンのプロパティであり、仮想ハード ディスクのプロパティではありません。 したがって、第 1 世代または第 2 世代仮想マシンで VHDX ファイルが作成されていないかを判断できません。  
- IDE コント ローラーまたは第 1 世代バーチャル マシンの SCSI コント ローラーに接続できる 2 つの仮想マシンの世代で作成された VHDX ファイル。 ただし、起動可能な VHDX ファイルの場合は、第 1 世代仮想マシンは起動しません。

### <a name="use-ipv6-instead-of-ipv4"></a>IPv4 ではなく IPv6 を使用する

既定では、第 2 世代仮想マシンは IPv4 を使用します。 代わりに IPv6 を使用するには、 [Set-vmfirmware](https://technet.microsoft.com/library/dn464287.aspx) Windows PowerShell コマンドレットを実行します。 たとえば、次のコマンドは、TestVM という名前の仮想マシンの IPv6 に優先プロトコルを設定します。  

```powershell
Set-VMFirmware -VMName TestVM -IPProtocolPreference IPv6  
```  

## <a name="add-a-com-port-for-kernel-debugging"></a>カーネルデバッグ用の COM ポートを追加する

COM ポートは、追加するまで、第2世代仮想マシンでは使用できません。 これを行うには、Windows PowerShell または Windows Management Instrumentation (WMI) を使用します。 次の手順では、Windows PowerShell を使用してこれを行う方法を示します。

COM ポートを追加するには:  

1. セキュア ブートを無効にします。 カーネルデバッグはセキュアブートと互換性がありません。 バーチャルマシンがオフ状態であることを確認してから、 [set-vmfirmware](https://technet.microsoft.com/library/dn464287.aspx)コマンドレットを使用してください。 たとえば、次のコマンドでは、仮想マシン TestVM でセキュア ブートを無効にします。  

    ```powershell  
    Set-VMFirmware -Vmname TestVM -EnableSecureBoot Off  
    ```  

2. COM ポートを追加します。 これを行うには、 [Set VMComPort](https://technet.microsoft.com/library/hh848616.aspx)コマンドレットを使用します。 たとえば、次のコマンドは、仮想マシンの名前付きパイプ TestPipe、ローカル コンピューター上に接続するための TestVM で最初の COM ポートを構成します。  

    ```powershell
    Set-VMComPort -VMName TestVM 1 \\.\pipe\TestPipe  
    ```  

> [!NOTE]  
> 構成済みの COM ポートは、Hyper-v マネージャーの仮想マシンの設定に一覧表示されません。

## <a name="see-also"></a>参照  

- [Hyper-v 上の Linux および FreeBSD Virtual Machines](../Supported-Linux-and-FreeBSD-virtual-machines-for-Hyper-V-on-Windows.md)
- [VMConnect を使用して Hyper-v 仮想マシン上のローカルリソースを使用する](../learn-more/Use-local-resources-on-Hyper-V-virtual-machine-with-VMConnect.md)
- [Windows Server 2016 での Hyper-v のスケーラビリティの計画](Plan-for-Hyper-V-scalability-in-Windows-Server-2016.md)
