---
ms.date: 01/07/2019
ms.topic: conceptual
keywords: OpenSSH を SSH、SSHD、インストール、セットアップ
contributor: maertendMSFT
author: maertendMSFT
title: Windows の OpenSSH のインストール
ms.openlocfilehash: f617b01ee7dabd4897f99e374420f673e209e145
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859563"
---
# <a name="installation-of-openssh-for-windows-server-2019-and-windows-10"></a>Windows Server 2019 および Windows 10 の OpenSSH のインストール #

OpenSSH クライアントと OpenSSH サーバーは、Windows Server 2019 および Windows 10 1809 で個別にインストール可能なコンポーネントです。
これらの Windows バージョンを持つユーザーは、インストールして OpenSSH を構成する次の手順を使用する必要があります。 

> [!NOTE] 
> OpenSSH を PowerShell Github リポジトリから取得したユーザー (https://github.com/PowerShell/OpenSSH-Portable)そこから、手順を使用する必要がありますと__しないで__これらの手順を使用します。 


## <a name="installing-openssh-from-the-settings-ui-on-windows-server-2019-or-windows-10-1809"></a>Windows Server 2019 または Windows 10 1809 UI 設定から OpenSSH をインストールします。

OpenSSH クライアントとサーバーは、Windows 10 1809 のインストール可能な機能です。 

OpenSSH をインストールするには、設定を開始し、アプリに移動 > アプリおよび機能 > オプションの機能を管理します。 

OpenSSH クライアントが既にインストールされているかどうか、この一覧をスキャンします。 ない場合は、ページの上部にある選び「機能を追加」します。 

* OpenSSH クライアントをインストールするには、"OpenSSH Client"を検索し、[インストール] をクリックします。 
* OpenSSH server をインストールするには、"OpenSSH Server"を検索し、「インストール」 をクリックします。 

インストールが完了したら、アプリに戻ります > アプリおよび機能 > して、省略可能な機能の管理は、OpenSSH コンポーネントを一覧表示を表示する必要があります。

> [!NOTE]
> OpenSSH Server のインストール、作成し、"OpenSSH Server-で-TCP"をという名前のファイアウォール規則を有効にします。 これにより、ポート 22 で SSH トラフィックを受信できます。 

## <a name="installing-openssh-with-powershell"></a>PowerShell で OpenSSH をインストールします。 

PowerShell を使用して OpenSSH をインストールするには、最初に管理者として PowerShell を起動します。
OpenSSH 機能がインストールに使用できることを確認します。

```powershell
Get-WindowsCapability -Online | ? Name -like 'OpenSSH*'

# This should return the following output:

Name  : OpenSSH.Client~~~~0.0.1.0
State : NotPresent
Name  : OpenSSH.Server~~~~0.0.1.0
State : NotPresent
```

次に、サーバーやクライアントの機能をインストールします。

```powershell
# Install the OpenSSH Client
Add-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

# Install the OpenSSH Server
Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0

# Both of these should return the following output:

Path          :
Online        : True
RestartNeeded : False
```

## <a name="uninstalling-openssh"></a>OpenSSH をアンインストールします。

Windows 設定を使用して OpenSSH をアンインストールするには、設定を開始し、アプリに移動 > アプリおよび機能 > オプションの機能を管理します。 インストールされている機能の一覧で OpenSSH クライアントまたは OpenSSH サーバー コンポーネントを選択し、[アンインストール] を選択します。

PowerShell を使用して OpenSSH をアンインストールするには、するには、次のコマンドのいずれかを使用します。

```powershell
# Uninstall the OpenSSH Client
Remove-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

# Uninstall the OpenSSH Server
Remove-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```

OpenSSH を削除する場合に、同時に使用では、サービスがアンインストールされた後、Windows の再起動が必要にあります。


## <a name="initial-configuration-of-ssh-server"></a>SSH サーバーの初期構成

Windows の初期使用のための OpenSSH サーバーを構成するには、管理者は、PowerShell を起動し、SSHD サービスを開始するには、次のコマンドを実行します。

```powershell
Start-Service sshd
# OPTIONAL but recommended:
Set-Service -Name sshd -StartupType 'Automatic'
# Confirm the Firewall rule is configured. It should be created automatically by setup. 
Get-NetFirewallRule -Name *ssh*
# There should be a firewall rule named "OpenSSH-Server-In-TCP", which should be enabled 
```

## <a name="initial-use-of-ssh"></a>SSH の初期の使用

Windows OpenSSH Server をインストールすると、任意の Windows デバイスから PowerShell を使用して、SSH クライアントのインストールをすばやくテストできます。 PowerShell では、次のコマンドを入力します。 

```powershell
Ssh username@servername
```

任意のサーバーへの接続を最初は、次のようなメッセージになります。

```
The authenticity of host 'servername (10.00.00.001)' can't be established.
ECDSA key fingerprint is SHA256:(<a large string>).
Are you sure you want to continue connecting (yes/no)?
```

答えがある必要があります"か、yes"または"no"です。 はいすると、そのサーバーがローカルのシステムに追加する一連の既知の ssh ホスト。

求め、パスワードの時点でします。 セキュリティの予防措置として、パスワードは表示されませんを入力するとします。 

接続すると、次のようなコマンド シェル プロンプトが表示されます。

```
domain\username@SERVERNAME C:\Users\username>
```

OpenSSH を Windows server で使用される既定のシェルは、Windows コマンド シェルです。 

