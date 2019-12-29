---
title: Nano Server 向けの開発
description: PowerShell のリモート処理と CIM セッション
ms.prod: windows-server
ms.service: na
manager: DonGill
ms.technology: server-nano
ms.date: 09/06/2017
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 57079470-a1c1-4fdc-af15-1950d3381860
author: jaimeo
ms.author: jaimeo
ms.localizationpriority: medium
ms.openlocfilehash: 6cf21d9db4221fd6bd76cfd5c362bb9f168d1ce9
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71360324"
---
# <a name="developing-for-nano-server"></a>Nano Server 向けの開発

>適用先:Windows Server 2016

> [!IMPORTANT]
> Windows Server バージョン 1709 以降、Nano Server は[コンテナー基本 OS イメージ](/virtualization/windowscontainers/quick-start/using-insider-container-images#install-base-container-image)としてのみ提供されます。 その意味については、「[Nano Server に加えられる変更](nano-in-semi-annual-channel.md)」をご覧ください。 

これらのトピックでは、Nano Server 上の PowerShell の重要な違いについて説明し、Nano Server で使用する独自の PowerShell コマンドレットを開発する場合のガイダンスを提供します。

- [Nano Server の PowerShell](PowerShell-on-Nano-Server.md)
- [Nano Server 用の PowerShell コマンドレットを開発する](Developing-PowerShell-Cmdlets-for-Nano-Server.md)

## <a name="using-windows-powershell-remoting"></a>Windows PowerShell リモート処理を使用する  
Windows PowerShell リモート処理を使用して Nano Server を管理するには、Nano Server の IP アドレスを管理コンピューターの信頼されたホストの一覧に追加し、使用しているアカウントを Nano Server の管理者に追加する必要があります。CredSSP を使用する場合は、その機能を有効にする必要もあります。  

> [!NOTE]
> 対象の Nano Server と管理コンピューターが同じ AD DS フォレスト (または信頼関係のあるフォレスト) に属している場合、Nano Server を信頼されたホストの一覧に追加する必要はありません。完全修飾ドメイン名を使用して、Nano Server に接続できます。次に例を示します。PS C:\>Enter-PSSession -ComputerName nanoserver.contoso.com -Credential (Get-Credential)
  
  
Nano Server を信頼されたホストの一覧に追加するには、管理者特権での Windows PowerShell プロンプトで次のコマンドを実行します。  
  
`Set-Item WSMan:\localhost\Client\TrustedHosts "<IP address of Nano Server>"`  
  
リモートの Windows PowerShell セッションを開始するには、管理者特権のローカル Windows PowerShell セッションを開始し、次のコマンドを実行します。  
  
  
```  
$ip = "\<IP address of Nano Server>"  
$user = "$ip\Administrator"  
Enter-PSSession -ComputerName $ip -Credential $user  
```  
  
  
これで、Nano Server で通常どおりに Windows PowerShell コマンドを実行できます。  
  
> [!NOTE]  
> このリリースの Nano Server では、一部の Windows PowerShell コマンドを利用できません。 どれが利用できるかを確認するには、`Get-Command -CommandType Cmdlet` を実行します  
  
リモート セッションを停止するには、コマンド `Exit-PSSession` を使用します  
  
## <a name="using-windows-powershell-cim-sessions-over-winrm"></a>WinRM を介して Windows PowerShell CIM セッションを使用する  
Windows リモート管理 (WinRM) を介して、Windows PowerShell の CIM セッションとインスタンスを使用して、WMI コマンドを実行できます。  
  
CIM セッションを開始するには、Windows PowerShell プロンプトで次のコマンドを実行します。  
  
  
```  
$ip = "<IP address of the Nano Server\>"  
$ip\Administrator  
$cim = New-CimSession -Credential $user -ComputerName $ip  
```  
  
  
セッションが確立されたら、さまざまな WMI コマンドを実行できます。以下に例を示します。  
  
  
```  
Get-CimInstance -CimSession $cim -ClassName Win32_ComputerSystem | Format-List *  
Get-CimInstance -CimSession $Cim -Query "SELECT * from Win32_Process WHERE name LIKE 'p%'"  
```  
  
  