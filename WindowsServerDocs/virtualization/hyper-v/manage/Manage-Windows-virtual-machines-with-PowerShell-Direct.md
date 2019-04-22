---
title: PowerShell ダイレクトでの Windows 仮想マシンを管理します。
description: PowerShell Direct を使用して、ネットワーク接続またはリモートの接続に依存することがなく仮想マシンを管理する方法を説明します。
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b5715c02-a90f-4de9-a71e-0fc09093ba2d
author: KBDAzure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 4081a9737825d2f50f0d3b19b3bada3b9bbc76f1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814703"
---
# <a name="manage-windows-virtual-machines-with-powershell-direct"></a>PowerShell ダイレクトでの Windows 仮想マシンを管理します。

>適用先:Windows 10、Windows Server 2016、Windows Server 2019
  
PowerShell Direct を使用すると、Windows 10、Windows Server 2016 または Windows Server 2019 の HYPER-V ホストから Windows 10、Windows Server 2016 または Windows Server 2019 仮想マシンをリモートで管理します。 PowerShell ダイレクトでネットワーク構成またはいずれかの HYPER-V ホスト上のリモート管理設定に関係なくまたは仮想マシン内の Windows PowerShell の管理ができます。 これを使うと、Hyper-V 管理者が仮想マシンの管理や設定を容易に自動化したり、スクリプトを作成したりすることができます。  
  
PowerShell ダイレクトを実行するには、次の 2 つの方法があります。  
  
- 作成し、PSSession コマンドレットを使用して、直接の PowerShell セッションを終了します。
  
- Invoke-command コマンドレットにスクリプトまたはコマンドを実行します。
  
以前の仮想マシンを管理している場合は、仮想マシン接続 (VMConnect) を使用するか、[仮想マシン用の仮想ネットワークを構成します](https://technet.microsoft.com/library/cc816585.aspx)。  
  
## <a name="create-and-exit-a-powershell-direct-session-using-pssession-cmdlets"></a>作成し、PSSession コマンドレットを使用して、直接の PowerShell セッションを終了します。  
  
1. Hyper-V ホストで、管理者として Windows PowerShell を開きます。  
  
2. 使用して、 [Enter-pssession](https://technet.microsoft.com/library/hh849707.aspx)コマンドレットを仮想マシンに接続します。 仮想マシンの名前または GUID を使用してセッションを作成するには、次のコマンドのいずれかを実行します。  
  
    ```  
    Enter-PSSession -VMName <VMName>  
    ```  
  
    ```  
    Enter-PSSession -VMGUID <VMGUID>  
    ```  
  
3. 仮想マシン用の資格情報を入力します。   
4. 必要なコマンドを実行します。 これらのコマンドは、セッションを作成した仮想マシン上で実行されます。  
  
5.  完了したらを使用して、 [Exit-pssession](https://technet.microsoft.com/library/hh849743.aspx)セッションを閉じます。   
  
    ```  
    Exit-PSSession  
    ```  
  
## <a name="run-script-or-command-with-invoke-command-cmdlet"></a>Invoke-command コマンドレットにスクリプトまたはコマンドを実行します。  
[Invoke-Command](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Invoke-Command) コマンドレットを使用して、あらかじめ設定された一連のコマンドを仮想マシン上で実行できます。 仮想マシン名が PSTest であり、実行するスクリプト (foo.ps1) が C:/ ドライブ上のスクリプト フォルダー内にある場合に、Invoke-Command コマンドレットを使用する方法の例を以下に示します。  
  
```  
Invoke-Command -VMName PSTest  -FilePath C:\script\foo.ps1  
```  
  
1 つのコマンドを使用するには、**-ScriptBlock** パラメーターを使用します。  
  
```  
Invoke-Command -VMName PSTest  -ScriptBlock { cmdlet }  
```  
  
## <a name="whats-required-to-use-powershell-direct"></a>PowerShell を使用して何が必要なでしょうか。  
仮想マシンで PowerShell ダイレクト セッションを作成するには  
  
-   仮想マシンはホストのローカルで実行されており、起動する必要があります。  
  
-   HYPER-V の管理者として、ホスト コンピューターには、ログインする必要があります。  
  
-   仮想マシンの有効なユーザー資格情報を指定する必要があります。  
  
-   少なくとも、ホスト オペレーティング システムを実行する必要があります Windows 10 または Windows Server 2016。
  
-   仮想マシンを実行する必要があります、少なくとも Windows 10 または Windows Server 2016。  
  
使用することができます、 [GET-VM](https://docs.microsoft.com/powershell/module/hyper-v/get-vm)コマンドレットを使用する資格情報に HYPER-V 管理者の役割があることを確認し、ホスト上でローカルで実行し、起動した仮想マシンの一覧を取得します。  
  
## <a name="see-also"></a>関連項目  
[Enter-PSSession](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Enter-PSSession)  
[Exit-pssession](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Exit-PSSession)  
[Invoke-Command](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Invoke-Command)  
  


