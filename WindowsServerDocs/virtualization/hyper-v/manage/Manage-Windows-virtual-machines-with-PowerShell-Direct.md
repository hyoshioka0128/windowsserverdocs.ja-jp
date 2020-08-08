---
title: PowerShell Direct を使用して Windows 仮想マシンを管理する
description: PowerShell Direct を使用して仮想マシンを管理する手順について説明します。
manager: dongill
ms.topic: article
ms.assetid: b5715c02-a90f-4de9-a71e-0fc09093ba2d
author: kbdazure
ms.author: kathydav
ms.date: 10/04/2016
ms.openlocfilehash: 97f8c2a0bcfec3699593e5162ede8cff3e411b0d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2020
ms.locfileid: "87941977"
---
# <a name="manage-windows-virtual-machines-with-powershell-direct"></a>PowerShell Direct を使用して Windows 仮想マシンを管理する

>適用対象: Windows 10、Windows Server 2016、Windows Server 2019

PowerShell Direct を使用すると、windows 10、windows Server 2016、または Windows Server 2019 Hyper-v ホストから、windows 10、Windows Server 2016、または Windows Server 2019 の仮想マシンをリモートで管理できます。 PowerShell Direct を使用すると、Hyper-v ホストまたは仮想マシンのいずれかのネットワーク構成またはリモート管理設定に関係なく、仮想マシン内で Windows PowerShell を管理できます。 これにより、HYPER-V の管理者を自動化し、仮想マシン管理と構成スクリプトを作成しやすくなります。

PowerShell ダイレクトを実行するには、次の 2 つの方法があります。

- 作成し、PSSession コマンドレットを使用して、直接の PowerShell セッションを終了します。

- Invoke-command コマンドレットにスクリプトまたはコマンドを実行します。

以前の仮想マシンを管理している場合は、仮想マシン接続 (VMConnect) を使用するか、[仮想マシン用の仮想ネットワークを構成します](https://technet.microsoft.com/library/cc816585.aspx)。

## <a name="create-and-exit-a-powershell-direct-session-using-pssession-cmdlets"></a>作成し、PSSession コマンドレットを使用して、直接の PowerShell セッションを終了します。

1. Hyper-V ホストで、管理者として Windows PowerShell を開きます。

2. 仮想マシンに接続するには、 [PSSession](https://technet.microsoft.com/library/hh849707.aspx)コマンドレットを使用します。 次のコマンドのいずれかを実行して、仮想マシン名または GUID を使用してセッションを作成します。

    ```
    Enter-PSSession -VMName <VMName>
    ```

    ```
    Enter-PSSession -VMGUID <VMGUID>
    ```

3. 仮想マシンの資格情報を入力します。
4. 必要がある任意のコマンドを実行します。 これらのコマンドは、使用してセッションを作成した仮想マシンで実行します。

5.  完了したら、[出口](https://technet.microsoft.com/library/hh849743.aspx)を使用してセッションを終了します。

    ```
    Exit-PSSession
    ```

## <a name="run-script-or-command-with-invoke-command-cmdlet"></a>Invoke-command コマンドレットにスクリプトまたはコマンドを実行します。
[Invoke-Command](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Invoke-Command) コマンドレットを使用して、あらかじめ設定された一連のコマンドを仮想マシン上で実行できます。 仮想マシン名が PSTest であり、実行するスクリプト (foo.ps1) が C:/ ドライブ上のスクリプト フォルダー内にある場合に、Invoke-Command コマンドレットを使用する方法の例を以下に示します。

```
Invoke-Command -VMName PSTest  -FilePath C:\script\foo.ps1
```

単一のコマンドを実行するには、**-ScriptBlock** パラメーターを使用します。

```
Invoke-Command -VMName PSTest  -ScriptBlock { cmdlet }
```

## <a name="whats-required-to-use-powershell-direct"></a>PowerShell を使用して何が必要なでしょうか。
仮想マシンで PowerShell ダイレクト セッションを作成するには

-   仮想マシンでは、ホスト上でローカルに実行する必要があり、起動します。

-   HYPER-V の管理者として、ホスト コンピューターには、ログインする必要があります。

-   仮想マシンの有効なユーザー資格情報を指定する必要があります。

-   ホストオペレーティングシステムは、少なくとも Windows 10 または Windows Server 2016 を実行している必要があります。

-   仮想マシンは Windows 10 または Windows Server 2016 以降を実行している必要があります。

[GET VM](https://docs.microsoft.com/powershell/module/hyper-v/get-vm)コマンドレットを使用して、使用している資格情報が hyper-v の管理者ロールを持っていることを確認し、ホスト上でローカルに実行されている仮想マシンの一覧を取得して、起動します。

## <a name="see-also"></a>参照
「 [-PSSession](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Enter-PSSession) 
 」と入力します。[終了-PSSession](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Exit-PSSession) 
[Invoke コマンド](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Core/Invoke-Command)



