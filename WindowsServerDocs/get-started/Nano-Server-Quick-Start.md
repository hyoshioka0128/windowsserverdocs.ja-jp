---
title: Nano Server のクイック スタート
description: 物理マシンまたは仮想マシンに基本的な Nano Server を迅速に展開する手順
ms.prod: windows-server-threshold
ms.service: na
manager: DonGill
ms.technology: server-nano
ms.date: 09/05/2017
ms.tgt_pltfrm: na
ms.topic: get-started-article
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 488d0bed661cf2078d20e491a8c68b2a29a42b73
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/22/2018
ms.locfileid: "2082374"
---
# <a name="nano-server-quick-start"></a>Nano Server のクイック スタート

>適用対象: Windows Server 2016

> [!IMPORTANT]
> Windows Server バージョン 1709 以降、Nano Server は[コンテナー基本 OS イメージ](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)としてのみ提供されます。 その意味については、「[Nano Server に加えられる変更](nano-in-semi-annual-channel.md)」をご覧ください。 

DHCP を使用して IP アドレスを取得する Nano Server の基本的な展開をすばやく開始するには、このセクションの手順に従います。 Nano Server VHD は、仮想マシンで実行するか、物理コンピューター上で起動することができます。それぞれで手順は若干異なります。

これらのクイック スタート手順で基本的な展開を試した後は、独自のカスタム イメージの作成、さまざまな方法によるパッケージ管理、ドメイン操作などの詳細については、「[Nano Server の展開](Deploy-Nano-Server.md)」を参照してください。
  
**仮想マシンでの Nano Server**  
  
仮想マシンで実行される Nano Server VHD を作成するには、次の手順に従います。  
  
## <a name="to-quickly-deploy-nano-server-in-a-virtual-machine"></a>仮想マシンに Nano Server をすばやく展開するには  
  
1.  Windows Server 2016 ISO の \NanoServer フォルダーにある *NanoServerImageGenerator* フォルダーを、お使いのハード ディスクのフォルダーにコピーします。  
  
2.  管理者として Windows PowerShell を起動します。NanoServerImageGenerator フォルダーを配置したフォルダーに移動し、次を使ってモジュールをインポートします。 `Import-Module .\NanoServerImageGenerator -Verbose`  
>[!NOTE]  
>場合によっては Windows PowerShell 実行ポリシーを調整する必要があります。その場合は、 `Set-ExecutionPolicy RemoteSigned` を使います。  
  
3.  次のコマンドを実行して、コンピューター名を設定し、Hyper-V **ゲスト ドライバー**を含む Standard Edition の VHD を作成します。コマンドを実行すると、新しい VHD の管理者パスワードの入力を求められます。  
  
    `New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath <path to root of media> -BasePath .\Base -TargetPath .\NanoServerVM\NanoServerVM.vhd -ComputerName <computer name>` 説明:  
  
    -   **-MediaPath <path to root of media\>** には、Windows Server 2016 ISO の内容のルートへのパスを指定します。 たとえば、ISO の内容を d:\TP5ISO にコピーした場合は、そのパスを使用します。  
  
    -   **-BasePath** (省略可能) には、Nano Server WIM とパッケージのコピー先として作成するフォルダーを指定します。  
  
    -   **-TargetPath** には、VHD または VHDX を作成する場所のパスを指定します。ファイル名と拡張子を含めます。  
  
    -   **Computer_name** には、作成する Nano Server 仮想マシンのコンピューター名を指定します。  
  
    **例:** `New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath f:\ -BasePath .\Base -TargetPath .\Nano1\Nano.vhd -ComputerName Nano1`  
  
    この例では、f:\\ としてマウントされている ISO から VHD を作成します。 VHD を作成する際に、New-NanoServerImage を実行したのと同じディレクトリ内の Base というフォルダーを使用します。また、コマンドを実行したフォルダー内の Nano1 というフォルダーに VHD (Nano.vhd) を配置します。 コンピューター名は Nano1 になります。 作成された VHD には Windows Server 2016 Standard Edition が含まれており、Hyper-V 仮想マシンの展開に適しています。 第 1 世代仮想マシンが必要な場合は、-TargetPath に **.vhd** 拡張子を指定して、VHD イメージを作成します。 第 2 世代仮想マシンの場合は、-TargetPath に **.vhdx** 拡張子を指定して、VHDX イメージを作成します。 -TargetPath に **.wim** 拡張子を指定して、WIM ファイルを直接生成することもできます。  
  
    > [!NOTE]  
    > New-NanoServerImage は、Windows 8.1、Windows 10、Windows Server 2012 R2、および Windows Server 2016 でサポートされます。  
  
4.  Hyper-V マネージャーで、新しい仮想マシンを作成し、手順 3. で作成した VHD を使用します。  
  
5.  仮想マシンを起動し、Hyper-V マネージャーで仮想マシンに接続します。  
  
6.  手順 3. のスクリプトを実行したときに指定した管理者とパスワードを使用して、回復コンソールにログオンします (このガイドの「Nano Server 回復コンソール」を参照してください)。  
 > [!NOTE]  
    > 回復コンソールでは、基本的なキーボード機能のみがサポートされます。 キーボードのライト、テンキー セクション、およびキーボード レイアウトの切り替え (CapsLock キーや NumLock キーなど) はサポートされません。
  
7.  Nano Server 仮想マシンの IP アドレスを取得し、Windows PowerShell リモート処理などのリモート管理ツールを使用して、仮想マシンに接続し、リモートで管理します。  
  
**物理コンピューターでの Nano Server**  
  
プレインストールされているデバイス ドライバーを使用して、物理コンピューターで Nano Server を実行する VHD を作成することもできます。 起動したり、ネットワークに接続したりするためにハードウェアに必要なドライバーが提供されていない場合は、このガイドの「ドライバーの追加」セクションの手順に従ってください。  
  
## <a name="to-quickly-deploy-nano-server-on-a-physical-computer"></a>物理コンピューターに Nano Server をすばやく展開するには  
  
1.  Windows Server 2016 ISO の \NanoServer フォルダーにある *NanoServerImageGenerator* フォルダーを、お使いのハード ディスクのフォルダーにコピーします。  
  
2.  管理者として Windows PowerShell を起動します。NanoServerImageGenerator フォルダーを配置したフォルダーに移動し、次を使ってモジュールをインポートします。 `Import-Module .\NanoServerImageGenerator -Verbose`  
  
>[!NOTE]  
>場合によっては Windows PowerShell 実行ポリシーを調整する必要があります。その場合は、 `Set-ExecutionPolicy RemoteSigned` を使います。  
  
3.  次のコマンドを実行して、コンピューター名を設定し、OEM ドライバーと Hyper-V を含む VHD を作成します。コマンドを実行すると、新しい VHD の管理者パスワードの入力を求められます。  
  
    `New-NanoServerImage -Edition Standard -DeploymentType Host -MediaPath <path to root of media> -BasePath .\Base -TargetPath .\NanoServerPhysical\NanoServer.vhd -ComputerName <computer name> -OEMDrivers -Compute -Clustering` 説明:  
  
    -   **-MediaPath <path to root of media\>** には、Windows Server 2016 ISO の内容のルートへのパスを指定します。 たとえば、ISO の内容を d:\TP5ISO にコピーした場合は、そのパスを使用します。  
  
    -   **BasePath** には、Nano Server WIM とパッケージのコピー先として作成するフォルダーを指定します。 このパラメーターは省略可能です。  
  
    -   **TargetPath** には、VHD または VHDX を作成する場所のパスを指定します。ファイル名と拡張子を含めます。  
  
    -   **Computer_name** は、作成する Nano Server のコンピューター名です。  
  
    **例:**`New-NanoServerImage -Edition Standard -DeploymentType Host -MediaPath F:\ -BasePath .\Base -TargetPath .\Nano1\NanoServer.vhd -ComputerName Nano-srv1 -OEMDrivers -Compute -Clustering`  
  
    この例では、F:\\ としてマウントされている ISO から VHD を作成します。 VHD を作成する際に、New-NanoServerImage を実行したのと同じディレクトリ内の Base というフォルダーを使用します。また、コマンドを実行したフォルダー内の Nano1 というフォルダーに VHD を配置します。 コンピューター名は Nano-srv1 になり、最も一般的なハードウェアの OEM ドライバーがインストールされ、Hyper-V の役割とクラスタリング機能が有効になります。 Nano Standard Edition が使用されます。  
  
4.  Nano Server VHD を実行する物理サーバーに管理者としてログインします。  
  
5.  このスクリプトで作成された VHD を物理コンピューターにコピーし、この新しい VHD から起動するように構成します。 これを行うには、次の手順に従います。  
  
    1.  生成された VHD をマウントします。 この例では、D:\\ にマウントされます。  
  
    2.  **bcdboot d:\windows** を実行します。  
  
    3.  VHD のマウントを解除します。  
  
6.  Nano Server VHD から物理コンピューターを起動します。  
  
7.  手順 3. のスクリプトを実行したときに指定した管理者とパスワードを使用して、回復コンソールにログオンします (このガイドの「Nano Server 回復コンソール」を参照してください)。
> [!NOTE]  
    > 回復コンソールでは、基本的なキーボード機能のみがサポートされます。 キーボードのライト、テンキー セクション、およびキーボード レイアウトの切り替え (CapsLock キーや NumLock キーなど) はサポートされません。 
  
8.  Nano Server コンピューターの IP アドレスを取得し、Windows PowerShell リモート処理などのリモート管理ツールを使用して、仮想マシンに接続し、リモートで管理します。  
