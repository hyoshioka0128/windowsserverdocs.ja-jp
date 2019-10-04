---
ms.date: 09/27/2019
ms.topic: conceptual
keywords: OpenSSH、SSH、SSHD、install、setup
contributor: maertendMSFT
author: maertendMSFT
title: Windows 用 OpenSSH のインストール
ms.openlocfilehash: 3c742e20432d20ea3c402af66f19a803ea1f3a56
ms.sourcegitcommit: 73898afec450fb3c2f429ca373f6b48a74b19390
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/03/2019
ms.locfileid: "71934935"
---
# <a name="installation-of-openssh-for-windows-server-2019-and-windows-10"></a>Windows Server 2019 および Windows 10 用 OpenSSH のインストール #

OpenSSH クライアントおよび OpenSSH サーバーは、Windows Server 2019 および Windows 10 1809 の個別にインストール可能なコンポーネントです。
これらの Windows バージョンを使用するユーザーは、次の手順に従って、OpenSSH のインストールと構成を行う必要があります。 

> [!NOTE] 
> PowerShell Github リポジトリから OpenSSH を取得したユーザー https://github.com/PowerShell/OpenSSH-Portable) (そこからの手順を使用する必要があり、これらの手順__は使用しないでください)__ 。 


## <a name="installing-openssh-from-the-settings-ui-on-windows-server-2019-or-windows-10-1809"></a>Windows Server 2019 または Windows 10 1809 の設定 UI からの OpenSSH のインストール

OpenSSH クライアントとサーバーは、Windows 10 1809 のインストール可能な機能です。 

OpenSSH をインストールするには、[設定] を開始し、[アプリ > アプリと機能] > [オプション機能の管理] の順に選択します。 

この一覧をスキャンして、OpenSSH クライアントが既にインストールされているかどうかを確認します。 それ以外の場合は、ページの上部にある [機能の追加] を選択し、次のように入力します。 

* OpenSSH クライアントをインストールするには、"OpenSSH クライアント" に移動し、[インストール] をクリックします。 
* OpenSSH サーバーをインストールするには、"OpenSSH サーバー" に移動し、[インストール] をクリックします。 

インストールが完了したら、[アプリ > アプリと機能] に戻り > オプション機能を管理します。 OpenSSH コンポーネントが一覧表示されます。

> [!NOTE]
> OpenSSH サーバーをインストールすると、"OpenSSH-Server-TCP" という名前のファイアウォール規則が作成され、有効になります。 これにより、ポート22での SSH 受信トラフィックが許可されます。 

## <a name="installing-openssh-with-powershell"></a>PowerShell を使用した OpenSSH のインストール 

PowerShell を使用して OpenSSH をインストールするには、最初に管理者として PowerShell を起動します。
OpenSSH 機能をインストールに使用できるようにするには、次のようにします。

```powershell
Get-WindowsCapability -Online | ? Name -like 'OpenSSH*'

# This should return the following output:

Name  : OpenSSH.Client~~~~0.0.1.0
State : NotPresent
Name  : OpenSSH.Server~~~~0.0.1.0
State : NotPresent
```

次に、サーバーまたはクライアント機能をインストールします。

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

## <a name="uninstalling-openssh"></a>OpenSSH のアンインストール

Windows の設定を使用して OpenSSH をアンインストールするには、設定 を開始し、アプリ > アプリと機能 > オプション機能の管理 をクリックします。 インストールされている機能の一覧で、OpenSSH クライアントまたは OpenSSH サーバーコンポーネントを選択し、[アンインストール] を選択します。

PowerShell を使用して OpenSSH をアンインストールするには、次のコマンドのいずれかを使用します。

```powershell
# Uninstall the OpenSSH Client
Remove-WindowsCapability -Online -Name OpenSSH.Client~~~~0.0.1.0

# Uninstall the OpenSSH Server
Remove-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
```

サービスがアンインストール時に使用されている場合は、OpenSSH を削除した後に Windows の再起動が必要になることがあります。


## <a name="initial-configuration-of-ssh-server"></a>SSH サーバーの初期構成

Windows で初めて使用するために OpenSSH サーバーを構成するには、管理者として PowerShell を起動し、次のコマンドを実行して SSHD サービスを開始します。

```powershell
Start-Service sshd
# OPTIONAL but recommended:
Set-Service -Name sshd -StartupType 'Automatic'
# Confirm the Firewall rule is configured. It should be created automatically by setup. 
Get-NetFirewallRule -Name *ssh*
# There should be a firewall rule named "OpenSSH-Server-In-TCP", which should be enabled
# If the firewall does not exist, create one
New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22
```

## <a name="initial-use-of-ssh"></a>SSH の初回使用

Windows に OpenSSH サーバーをインストールすると、SSH クライアントがインストールされている任意の Windows デバイスから PowerShell を使用して簡単にテストできます。 PowerShell で、次のコマンドを入力します。 

```powershell
Ssh username@servername
```

サーバーへの最初の接続では、次のようなメッセージが表示されます。

```
The authenticity of host 'servername (10.00.00.001)' can't be established.
ECDSA key fingerprint is SHA256:(<a large string>).
Are you sure you want to continue connecting (yes/no)?
```

回答は、"yes" または "no" のいずれかにする必要があります。 [はい] をオンにすると、そのサーバーが既知の ssh ホストのローカルシステムの一覧に追加されます。

この時点で、パスワードの入力を求められます。 セキュリティ上の理由から、入力したとおりにパスワードは表示されません。 

接続すると、次のようなコマンドシェルプロンプトが表示されます。

```
domain\username@SERVERNAME C:\Users\username>
```

Windows OpenSSH サーバーで使用される既定のシェルは、Windows コマンドシェルです。 

