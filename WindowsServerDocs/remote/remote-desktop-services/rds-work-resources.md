---
title: Windows Server の PowerShell を使用して RDS タイトル "Work Resources" をカスタマイズする
description: Windows Server の既定のワークスペース名を変更する方法を説明します。
ms.prod: windows-server-threshold
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 10/26/2017
ms.topic: article
author: Heidilohr
ms.openlocfilehash: 43837826a6cddc2c3c4c7c1af874334718a3a067
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826713"
---
# <a name="customize-the-rds-title-work-resources-using-powershell-on-windows-server"></a>Windows Server の PowerShell を使用して RDS タイトル "Work Resources" をカスタマイズする

Windows Server を使用して、RD web アクセスまたはリモート デスクトップの新しいアプリを介して Remoteapp またはデスクトップにアクセスする、気付き、ワークスペースが既定で「職場のリソース」をタイトルです。  PowerShell コマンドレットを使用して、タイトルを簡単に変更することができます。

タイトルを変更するには、接続ブローカー サーバーの新しい PowerShell ウィンドウを開きし、次のコマンドで RemoteDesktop モジュールをインポートします。

```powershell
    Import-Module RemoteDesktop
```

次に、セット RDWorkspace コマンドを使用して、ワークスペース名を変更します。

```powershell
    Set-RDWorkspace [-Name] <string> [-ConnectionBroker <string>]  [<CommonParameters>]
```   

たとえば、"Contoso Remoteapp"にワークスペース名を変更するのに、次のコマンドを使用できます。

```powershell
    Set-RDWorkspace -Name "Contoso RemoteApps" -ConnectionBroker broker01.contoso.com
```

複数の接続ブローカーの高可用性モードでを実行している場合は、アクティブな broker に対してこれを実行する必要があります。 このコマンドを使用することができます。

```powershell
    Set-RDWorkspace -Name "Contoso RemoteApps" -ConnectionBroker (Get-RDConnectionBrokerHighAvailability).ActiveManagementServer
```

セット RDWorkspace コマンドレットの詳細については、次を参照してください。、[セット RDSWorkspace](https://docs.microsoft.com/powershell/module/remotedesktop/set-rdworkspace?view=win10-ps)参照。