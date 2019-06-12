---
title: HYPER-V で仮想マシンを作成します。
description: HYPER-V マネージャーまたは Windows PowerShell を使用して仮想マシンを作成する手順します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 59297022-a898-456c-b299-d79cd5860238
author: KBDAzure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 3b850d19663115b72d809af1ae92a444f5491496
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66810429"
---
# <a name="create-a-virtual-machine-in-hyper-v"></a>HYPER-V で仮想マシンを作成します。

>適用先:Windows 10、Windows Server 2016、Microsoft HYPER-V Server 2016、Windows Server 2019、Microsoft HYPER-V Server 2019

Windows PowerShell とオプションが、HYPER-V マネージャーで仮想マシンを作成するときと、HYPER-V マネージャーを使用して仮想マシンを作成する方法を説明します。  

## <a name="create-a-virtual-machine-by-using-hyper-v-manager"></a>HYPER-V マネージャーを使用して仮想マシンを作成します。  

1.  開いている**Hyper V マネージャー**します。  

2.  **アクション**ウィンドウで、をクリックして**新規**、 をクリックし、**仮想マシン**。  

3.  **仮想マシンの新規作成ウィザード**、 をクリックして**次**します。  

4.  各ページでは、仮想マシンの適切な選択を行います。 詳細については、次を参照してください。[新しい仮想マシンのオプションと既定値は、Hyper-v マネージャーで](#options-in-hyper-v-manager-new-virtual-machine-wizard)このトピックで後述します。  

5.  選択したことを確認したら、**概要**] ページで [**完了**します。  

6.  HYPER-V マネージャーでは、仮想マシンを右クリックし、選択**接続**します。  

7.  仮想マシン接続 ウィンドウで、次のように選択します。**アクション** > **開始**します。  

## <a name="create-a-virtual-machine-by-using-windows-powershell"></a>Windows PowerShell を使用して仮想マシンを作成します。  

1. Windows デスクトップ上で、[スタート] ボタンをクリックし、**Windows PowerShell** という名前の一部を入力します。  

2. 右クリックして**Windows PowerShell**選択**管理者として実行**します。  

3. 使用して使用する仮想マシンを仮想スイッチの名前を取得[Get-vmswitch](https://technet.microsoft.com/library/hh848499.aspx)します。  以下に例を示します。  

   ```  
   Get-VMSwitch  * | Format-Table Name  
   ```  

4. 使用して、 [NEW-VM](https://technet.microsoft.com/library/hh848537.aspx)コマンドレットで仮想マシンを作成します。  次の例を参照してください。  

   > [!NOTE]  
   > この仮想マシンを Windows Server 2012 R2 を実行する HYPER-V ホストに移動することがありますと、を使用して、バージョン パラメーターを指定すると[NEW-VM](https://technet.microsoft.com/library/hh848537.aspx) 5 に仮想マシンの構成バージョンを設定します。 Windows Server 2016 の仮想マシン構成バージョンを既定値は、Windows Server 2012 R2 またはそれ以前のバージョンによってサポートされていません。 仮想マシンを作成した後、仮想マシンの構成バージョンを変更できません。 詳細については、次を参照してください。[サポートされている仮想マシン構成バージョン](../deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md#supported-virtual-machine-configuration-versions)します。  

   - **既存のバーチャル ハード ディスク**- で既存の仮想ハード ディスク、仮想マシンを作成するために、次のコマンドを使用することができます、  
     - **-Name**作成している仮想マシンに指定される名前を指定します。  
     - **-MemoryStartupBytes**の起動時に仮想マシンに使用可能なメモリの量です。  
     - **-一**はネットワーク アダプター (ネットワーク アダプター) または仮想ハード_ディスク (VHD) のような開始時に、仮想マシンを起動するデバイスです。  
     - **-VHDPath**を使用する仮想マシンのディスクへのパスです。  
     - **-Path**は仮想マシンの構成ファイルを格納するパスです。  
     - **世代**は仮想マシンの世代。 VHD および VHDX の第 2 世代の第 1 世代を使用します。 参照してください[HYPER-V でジェネレーション 1 または 2 仮想マシンを作成する必要があります。](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)  
     - **-スイッチ**他の仮想マシンまたはネットワークへの接続に使用する仮想マシンを仮想スイッチの名前を指定します。 参照してください[、HYPER-V 仮想マシン用の仮想スイッチの作成](Create-a-virtual-switch-for-Hyper-V-virtual-machines.md)です。  

       ```  
       New-VM -Name <Name> -MemoryStartupBytes <Memory> -BootDevice <BootDevice> -VHDPath <VHDPath> -Path <Path> -Generation <Generation> -Switch <SwitchName>  
       ```  

       例:  

       ```  
       New-VM -Name Win10VM -MemoryStartupBytes 4GB -BootDevice VHD -VHDPath .\VMs\Win10.vhdx -Path .\VMData -Generation 2 -Switch ExternalSwitch  
       ```  

       これは、4 GB のメモリで Win10VM という名前の第 2 世代仮想マシンを作成します。 VMs\Win10.vhdx、現在のディレクトリ内のフォルダーから起動し、ExternalSwitch をという名前の仮想スイッチを使用します。 仮想マシンの構成ファイルは、おり、フォルダーに格納されます。  

   - **新しいバーチャル ハード ディスク**- を新しい仮想ハード_ディスクと仮想マシンを作成、置換、 **- VHDPath**パラメーターでは、上記の例から **- NewVHDPath**を追加し、 **-NewVHDSizeBytes**パラメーター。 以下に例を示します。  

     ```  
     New-VM -Name Win10VM -MemoryStartupBytes 4GB -BootDevice VHD -NewVHDPath .\VMs\Win10.vhdx -Path .\VMData -NewVHDSizeBytes 20GB -Generation 2 -Switch ExternalSwitch  
     ```  

   - **オペレーティング システム イメージに起動する仮想ハード ディスクが新しい**でオペレーティング システム イメージをブートは、PowerShell の例を参照してください新しい仮想ディスクを仮想マシンを作成する -[で Hyper-v の仮想マシンのチュートリアルを作成。Windows 10](https://msdn.microsoft.com/virtualization/hyperv_on_windows/quick_start/walkthrough_create_vm)します。  

5. 使用して仮想マシンの起動、 [START-VM](https://technet.microsoft.com/library/hh848589.aspx)コマンドレット。 名前が作成した仮想マシンの名前を次のコマンドレットを実行します。  

   ```  
   Start-VM -Name <Name>  
   ```  

   次に、例を示します。  

   ```  
   Start-VM -Name Win10VM  
   ```  

6. 仮想マシン接続 (VMConnect) を使用して、仮想マシンに接続します。  

   ```  
   VMConnect.exe  
   ```  

## <a name="options-in-hyper-v-manager-new-virtual-machine-wizard"></a>Hyper V マネージャー仮想マシンの新規作成ウィザードのオプション  
次の表は、オプションごとに、HYPER-V マネージャーと、既定の仮想マシンを作成するときに選択することができます。  

|ページ|Windows Server 2016 および Windows 10 の既定値|その他のオプション|  
|--------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|  
|**名前と場所の指定**|名前:新しい仮想マシン。<br /><br />所在地:**C:\ProgramData\Microsoft\Windows\Hyper-V\\** .|独自の名前を入力し、仮想マシンを別の場所を選択できます。<br /><br />これは、仮想マシンの構成ファイルを格納します。|  
|**世代の指定**|第 1 世代|第 2 世代仮想マシンを作成することもできます。 詳細については、次を参照してください。 [、Hyper-v でジェネレーション 1 または 2 仮想マシンを作成する必要があります。](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)|  
|**メモリの割り当て**|起動メモリ:1024 MB<br /><br />動的メモリ:**選択されていません**|5902 MB に、32 MB から起動メモリを設定できます。<br /><br />動的メモリを使用することもできます。 詳細については、次を参照してください。 [Hyper-v 動的メモリの概要](https://technet.microsoft.com/library/hh831766.aspx)します。|  
|**ネットワークの構成**|接続されていません|既存の仮想スイッチの一覧から使用する仮想マシンのネットワーク接続を選択することができます。 参照してください[、HYPER-V 仮想マシン用の仮想スイッチの作成](Create-a-virtual-switch-for-Hyper-V-virtual-machines.md)です。|  
|**仮想ハード ディスクの接続**|仮想ハード_ディスクを作成します。<br /><br />名: <*vmname*> .vhdx<br /><br />**場所**:**C:\Users\Public\Documents\Hyper-V\Virtual Hard Disks\\**<br /><br />**［サイズ］** :127 GB|既存の仮想ハード_ディスクを使用して、待機または後で仮想ハード ディスクをアタッチすることもできます。|  
|**インストール オプション**|後で、オペレーティング システムをインストールします。|これらのオプションは、.iso ファイル、起動可能なフロッピー ディスク、または Windows 展開サービス (WDS) などのネットワーク インストール サービスからインストールできるように、仮想マシンの起動順序を変更します。|  
|**概要**|正しいことを検証できるように、選択したオプションが表示されます。<br /><br />-名前<br />世代<br />メモリ<br />-ネットワーク<br />ハード ディスク<br />オペレーティング システム|**クォータを調整する**ページから、概要をコピーして、電子メールや、仮想マシンを追跡するための別の場所に貼り付けます。|  

## <a name="see-also"></a>関連項目  

- [New-VM](https://technet.microsoft.com/library/hh848537.aspx)  

- [サポートされている仮想マシンの構成のバージョン](../deploy/Upgrade-virtual-machine-version-in-Hyper-V-on-Windows-or-Windows-Server.md#supported-virtual-machine-configuration-versions)  

-   [HYPER-V にジェネレーション 1 または 2 仮想マシンを作成する必要があります。](../plan/Should-I-create-a-generation-1-or-2-virtual-machine-in-Hyper-V.md)  

-   [Hyper-V 仮想マシン用の仮想スイッチを作成する](Create-a-virtual-switch-for-Hyper-V-virtual-machines.md)  
