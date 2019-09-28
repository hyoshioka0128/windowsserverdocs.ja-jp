---
title: Nano Server のトラブルシューティング
description: 回復コンソール、緊急管理サービス、カーネルのデバッグ
ms.prod: windows-server
ms.service: na
manager: DonGill
ms.technology: server-nano
ms.date: 09/06/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e427c66f-9571-4b8c-b65d-e7370d91544d
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 48b63e74ab406d2e66996097d33d71f2eeaeaf20
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71391552"
---
# <a name="troubleshooting-nano-server"></a>Nano Server のトラブルシューティング

>適用先:Windows Server 2016

> [!IMPORTANT]
> Windows Server バージョン 1709 以降、Nano Server は[コンテナー基本 OS イメージ](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)としてのみ提供されます。 その意味については、「[Nano Server に加えられる変更](nano-in-semi-annual-channel.md)」をご覧ください。 

このトピックには、Nano Server のインストール環境に対する接続、診断、修復に使用できるツールについての情報が記載されています。  
  
## <a name="using-the-nano-server-recovery-console"></a>Nano Server 回復コンソールの使用 
 
Nano Server は回復コンソールを備え、ネットワーク構成エラーによって Nano Server への接続が妨げられている場合でも Nano Server にアクセスできるようになっています。 回復コンソールを使用してネットワークを修復してから、通常のリモート管理ツールを使用することができます。  
  
仮想マシンまたはモニターとキーボードが接続された物理コンピューターで Nano Server を起動すると、全画面表示でテキスト モードのログオン プロンプトが表示されます。 このプロンプトに Administrator アカウントでログインすると、Nano Server のコンピューター名と IP アドレスが確認できます。 このコンソール内を移動するには、以下のコマンドを使用します。  
  
-   方向キーを使用してスクロールします。  
  
-   Tab キーを使用して **>** で始まる任意のテキストに移動し、Enter キーを押して選択します。  
  
-   1 つ前の画面またはページに戻るには、Esc キーを押します。 ホーム ページにいる場合は、Esc キーを押すとログオフします。  
  
-   一部の画面には追加機能があり、画面の最後の行に表示されています。 たとえば、ネットワーク アダプターを表示している場合、F4 キーを押すとネットワーク アダプターが無効になります。  
  
回復コンソールでは、ネットワーク アダプターと TCP/IP の設定、ファイアウォール規則を確認して構成できます。
> [!NOTE]
> 回復コンソールでは、基本的なキーボード機能のみがサポートされます。 キーボードのライト、テンキー セクション、およびキーボード レイアウトの切り替え (CapsLock キーや NumLock キーなど) はサポートされません。 英語キーボードと英語文字セットのみがサポートされています。

## <a name="accessing-nano-server-over-a-serial-port-with-emergency-management-services"></a>緊急管理サービスを使用したシリアル ポート経由での Nano Server へのアクセス  
緊急管理サービス (EMS) では、シリアル ポート経由でターミナル エミュレーターを使用することにより、基本的なトラブルシューティングの実施、ネットワーク ステータスの取得、コンソール セッション (CMD/PowerShell を含む) の開始ができます。 このため、サーバーのトラブルシューティングを実施するうえでキーボードとモニターは不要になります。 EMS の詳細については、「[Emergency Management Services Technical Reference (緊急管理サービスのテクニカル リファレンス)](https://technet.microsoft.com/library/cc784411(v=ws.10).aspx)」を参照してください。

Nano Server イメージで EMS を有効にし、後で必要になったときにすぐ利用できるようにするには、次のコマンドレットを実行します。  
  
`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\EnablingEMS.vhdx   -EnableEMS   -EMSPort 3   -EMSBaudRate 9600`  
  
このコマンドレット例では、シリアル ポート 3、ボー レート 9600 bps での EMS を有効にします。 これらのパラメーターを含めない場合、既定値はポート 1 と 115200 bps になります。 このコマンドレットを VHDX メディア向けに使用する場合は、Hyper-V 機能と、対応する Windows PowerShell モジュールを必ず含めるようにしてください。

## <a name="kernel-debugging"></a>カーネル デバッグ  
Nano Server イメージは、さまざまな方法でカーネル デバッグをサポートするように構成できます。 VHDX イメージでカーネル デバッグを使用する場合は、Hyper-V 機能と、対応する Windows PowerShell モジュールを必ず含めるようにしてください。 リモート カーネル デバッグの詳細については、通常は「[Setting Up Kernel-Mode Debugging over a Network Cable Manually (ネットワーク ケーブル経由でのカーネル モード デバッグの手動設定)](https://msdn.microsoft.com/library/windows/hardware/hh439346%28v=vs.85%29.aspx)」と「[Remote Debugging Using WinDbg (WinDbg を使用したリモート デバッグ)](https://msdn.microsoft.com/library/windows/hardware/hh451173%28v=vs.85%29.aspx)」を参照してください。  
  
### <a name="debugging-using-a-serial-port"></a>シリアル ポートを使用したデバッグ  
シリアル ポートを使用してイメージをデバッグできるようにするには、次のコマンドレット例を使用します。  
  
`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\KernelDebuggingSerial   -DebugMethod Serial   -DebugCOMPort 1   -DebugBaudRate 9600`  
  
この例では、ポート 2 経由、ボー レート 9600 bps でのシリアル デバッグを有効にします。 これらのパラメーターを指定しない場合、既定値はポート 2 と 115200 bps になります。 EMS とカーネル デバッグを両方とも使用する場合は、2 つの異なるシリアル ポートを使用するように構成する必要があります。  
  
### <a name="debugging-over-a-tcpip-network"></a>TCP/IP ネットワーク経由でのデバッグ  
TCP/IP ネットワーク経由でイメージをデバッグできるようにするには、次のコマンドレット例を使用します。  
  
`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\KernelDebuggingNetwork   -DebugMethod Net   -DebugRemoteIP 192.168.1.100   -DebugPort 64000`  
  
このコマンドレットでは、IP アドレスが 192.168.1.100 であるコンピューターのみが接続できる状態でのカーネル デバッグを有効にし、すべての通信はポート 64000 経由で行います。 -DebugRemoteIP および -DebugPort パラメーターは必須であり、ポート番号は 49152 より大きい値にします。 このコマンドレットでは、結果として得られる VHD と共に、ファイル内にポート経由での通信に必要な暗号化キーが生成されます。 また、次の例のように、-DebugKey パラメーターで独自のキーを指定することもできます。  
  
`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\KernelDebuggingNetwork   -DebugMethod Net   -DebugRemoteIP 192.168.1.100   -DebugPort 64000   -DebugKey 1.2.3.4`  
  
### <a name="debugging-using-the-ieee1394-protocol-firewire"></a>IEEE1394 プロトコル (Firewire) を使用したデバッグ  
IEEE1394 経由でのデバッグを有効にするには、次のコマンドレット例を使用します。  
  
`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\KernelDebuggingFireWire   -DebugMethod 1394   -DebugChannel 3`  
  
-DebugChannel パラメーターは必須です。  
  
### <a name="debugging-using-usb"></a>USB を使用したデバッグ  
次のコマンドレットで USB 経由でのデバッグを有効にすることができます。  
  
`New-NanoServerImage   -MediaPath \\Path\To\Media\en_us   -BasePath .\Base   -TargetPath .\KernelDebuggingUSB   -DebugMethod USB   -DebugTargetName KernelDebuggingUSBNano`  
  
リモート デバッガーを結果として得られる Nano Server に接続する場合は、-DebugTargetName パラメーターで設定されているように、ターゲット名を指定します。    