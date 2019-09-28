---
title: HYPER-V で仮想マシンを作成します。
description: Hyper-v マネージャーまたは Windows PowerShell を使用して仮想マシンを作成する手順について説明します。
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 59297022-a898-456c-b299-d79cd5860238
author: KBDAzure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 739691650ce3cda8066e9f7ac77626f53f22affa
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364247"
---
# <a name="create-a-virtual-machine-in-hyper-v"></a>HYPER-V で仮想マシンを作成します。

>適用先:Windows 10、Windows Server 2016、Microsoft Hyper-V Server 2016、Windows Server 2019、Microsoft Hyper-V Server 2019

Hyper-v マネージャーと Windows PowerShell を使用して仮想マシンを作成する方法と、Hyper-v マネージャーで仮想マシンを作成するときのオプションについて説明します。  

## <a name="create-a-virtual-machine-by-using-hyper-v-manager"></a>Hyper-v マネージャーを使用して仮想マシンを作成する  

1.  **Hyper-v マネージャー**を開きます。  

2.  **[操作]** ウィンドウで **[新規作成]** をクリックし、 **[仮想マシン]** をクリックします。  

3.  **仮想マシンの新規作成ウィザード**で、 **[次へ]** をクリックします。  

4.  各ページで、仮想マシンに適切な選択を行います。 詳細については、このトピックで後述する「 [Hyper-v マネージャーでの新しい仮想マシンのオプションと既定値](#options-in-hyper-v-manager-new-virtual-machine-wizard)」を参照してください。  

5.  **[概要]** ページで選択内容を確認したら、 **[完了]** をクリックします。  

6.  Hyper-v マネージャーで、仮想マシンを右クリックし、 **[接続]** を選択します。  

7.  [仮想マシン接続] ウィンドウで、[**アクション** > **開始**] を選択します。  

## <a name="create-a-virtual-machine-by-using-windows-powershell"></a>Windows PowerShell を使用して仮想マシンを作成する  

1. Windows デスクトップ上で、[スタート] ボタンをクリックし、**Windows PowerShell** という名前の一部を入力します。  

2. **[Windows PowerShell]** を右クリックし、 **[管理者として実行]** を選択します。  

3. [Get VMSwitch](https://technet.microsoft.com/library/hh848499.aspx)を使用して、仮想マシンで使用する仮想スイッチの名前を取得します。  例を次に示します。  

   ```  
   Get-VMSwitch  * | Format-Table Name  
   ```  

4. 仮想マシンを作成するには、[新しい VM](https://technet.microsoft.com/library/hh848537.aspx)コマンドレットを使用します。  次の例を参照してください。  

   > [!NOTE]  
   > この仮想マシンを Windows Server 2012 R2 を実行している Hyper-v ホストに移動する場合は、-Version パラメーターを[New-VM](https://technet.microsoft.com/library/hh848537.aspx)と共に使用して、仮想マシンの構成バージョンを5に設定します。 Windows server 2016 の既定の仮想マシン構成バージョンは、Windows Server 2012 R2 以前のバージョンではサポートされていません。 仮想マシンの作成後に、仮想マシンの構成バージョンを変更することはできません。 詳細については、「[サポートされている仮想マシンの構成バージョン](../deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md#supported-virtual-machine-configuration-versions)」を参照してください。  

   - **既存の仮想ハードディスク**-既存の仮想ハードディスクを使用して仮想マシンを作成するには、次のコマンドを使用します。  
     - **-Name**は、作成する仮想マシンに対して指定する名前です。  
     - **-Memorystartupbytes**は、起動時に仮想マシンが使用できるメモリの量です。  
     - **-BootDevice**は、仮想マシンがネットワークアダプター (ネットワークアダプター) または仮想ハードディスク (VHD) のように起動したときに起動するデバイスです。  
     - **-VHDPath**は、使用する仮想マシンディスクへのパスです。  
     - **-Path**は、仮想マシンの構成ファイルを格納するパスです。  
     - **-Generation**は仮想マシンの世代です。 VHD の場合は第1世代、VHDX の場合は第2世代を使用します。 「 [Hyper-v で第1世代または第2世代の仮想マシンを作成するに](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)は」を参照してください。  
     - **-スイッチ**は、仮想マシンが他の仮想マシンまたはネットワークに接続するために使用する仮想スイッチの名前です。 「 [Hyper-v 仮想マシンの仮想スイッチを作成する」を](Create-a-virtual-switch-for-Hyper-V-virtual-machines.md)参照してください。  

       ```  
       New-VM -Name <Name> -MemoryStartupBytes <Memory> -BootDevice <BootDevice> -VHDPath <VHDPath> -Path <Path> -Generation <Generation> -Switch <SwitchName>  
       ```  

       以下に例を示します。  

       ```  
       New-VM -Name Win10VM -MemoryStartupBytes 4GB -BootDevice VHD -VHDPath .\VMs\Win10.vhdx -Path .\VMData -Generation 2 -Switch ExternalSwitch  
       ```  

       これにより、4 GB のメモリを備えた Win10VM という名前の第2世代の仮想マシンが作成されます。 現在のディレクトリの Vms-Win10.4 vhdx フォルダーから起動し、ExternalSwitch という名前の仮想スイッチを使用します。 仮想マシンの構成ファイルは、VMData フォルダーに格納されます。  

   - **新しいバーチャルハードディスク**-新しいバーチャルハードディスクを含むバーチャルマシンを作成するには、前の例の **-VHDPath**パラメーターを **-NewVHDPath**に置き換え、 **-NewVHDSizeBytes**パラメーターを追加します。 例を次に示します。  

     ```  
     New-VM -Name Win10VM -MemoryStartupBytes 4GB -BootDevice VHD -NewVHDPath .\VMs\Win10.vhdx -Path .\VMData -NewVHDSizeBytes 20GB -Generation 2 -Switch ExternalSwitch  
     ```  

   - **オペレーティングシステムイメージを起動する新しい仮想ハードディスク**-オペレーティングシステムイメージを起動する新しい仮想ディスクを使用して仮想マシンを作成するには、「 [Windows 10 での hyper-v の仮想マシンの作成チュートリアル](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_create_vm)」の PowerShell の例を参照してください。  

5. [VM の起動](https://technet.microsoft.com/library/hh848589.aspx)コマンドレットを使用して、仮想マシンを起動します。 次のコマンドレットを実行します。ここで、Name は、作成した仮想マシンの名前です。  

   ```  
   Start-VM -Name <Name>  
   ```  

   以下に例を示します。  

   ```  
   Start-VM -Name Win10VM  
   ```  

6. 仮想マシン接続 (VMConnect) を使用して仮想マシンに接続します。  

   ```  
   VMConnect.exe  
   ```  

## <a name="options-in-hyper-v-manager-new-virtual-machine-wizard"></a>Hyper-v マネージャーの仮想マシンの新規作成ウィザードのオプション  
次の表に、Hyper-v マネージャーで仮想マシンを作成するときに選択できるオプションと、それぞれの既定値を示します。  

|ページ|Windows Server 2016 および Windows 10 の既定値|その他のオプション|  
|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|  
|**名前と場所の指定**|名前:新しい仮想マシン。<br /><br />所在地:**C:\ProgramData\Microsoft\Windows\Hyper-V @ no__t-1**.|また、独自の名前を入力し、仮想マシンの別の場所を選択することもできます。<br /><br />ここで、仮想マシンの構成ファイルが格納されます。|  
|**世代の指定**|第 1 世代|第2世代仮想マシンの作成を選択することもできます。 詳細については、「 [hyper-v で第1世代または第2世代の仮想マシンを作成する必要がありますか?](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md) 」を参照してください。|  
|**メモリの割り当て**|起動メモリ:1024 MB<br /><br />動的メモリ:**選択されていません**|起動メモリを32MB から5902MB に設定できます。<br /><br />動的メモリを使用するように選択することもできます。 詳細については、「 [hyper-v 動的メモリの概要](https://technet.microsoft.com/library/hh831766.aspx)」を参照してください。|  
|**ネットワークの構成**|接続されていません|既存の仮想スイッチの一覧から、使用する仮想マシンのネットワーク接続を選択できます。 「 [Hyper-v 仮想マシンの仮想スイッチを作成する」を](Create-a-virtual-switch-for-Hyper-V-virtual-machines.md)参照してください。|  
|**仮想ハード ディスクの接続**|仮想ハード_ディスクを作成します。<br /><br />名前: <*vmname*> .vhdx<br /><br />**場所**:**C:\Users\Public\Documents\Hyper-V\Virtual ハードディスク @ no__t-1**<br /><br />**［サイズ］** :127 GB|また、既存のバーチャルハードディスクを使用するか、後でバーチャルハードディスクを待機して接続するかを選択することもできます。|  
|**インストール オプション**|後でオペレーティングシステムをインストールする|これらのオプションを使用すると、バーチャルマシンのブート順序が変更され、.iso ファイル、起動可能なフロッピーディスク、または Windows 展開サービス (WDS) などのネットワークインストールサービスからインストールできるようになります。|  
|**概要**|選択したオプションが表示され、それらが正しいことを確認できます。<br /><br />-Name<br />-生成<br />-メモリ<br />-ネットワーク<br />-ハードディスク<br />-オペレーティングシステム|**クォータを調整する**ページから概要をコピーし、電子メールまたはその他の場所に貼り付けて、仮想マシンを追跡しやすくすることができます。|  

## <a name="see-also"></a>関連項目  

- [新規-VM](https://technet.microsoft.com/library/hh848537.aspx)  

- [サポートされている仮想マシンの構成バージョン](../deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md#supported-virtual-machine-configuration-versions)  

-   [Hyper-v に第1世代または第2世代の仮想マシンを作成する必要がありますか。](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)  

-   [Hyper-V 仮想マシン用の仮想スイッチを作成する](Create-a-virtual-switch-for-Hyper-V-virtual-machines.md)  
