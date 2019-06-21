---
ms.date: 09/27/2018
ms.topic: conceptual
keywords: OpenSSH を SSH、SSHD、インストール、セットアップ
contributor: maertendMSFT
ms.product: w10
author: maertendMSFT
title: Windows の OpenSSH サーバー構成
ms.openlocfilehash: 7eff3d3e1af67c9daf7a68c67c3609c0ee89fc93
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280036"
---
# <a name="openssh-server-configuration-for-windows-10-1809-and-server-2019"></a>Windows 10 1809 および Server 2019 # の OpenSSH サーバー構成

このトピックでは、OpenSSH サーバー (sshd) の Windows 固有の構成について説明します。 

OpenSSH でオンラインの構成オプションの詳細なドキュメントを保持する[OpenSSH.com](https://www.openssh.com/manual.html)、このドキュメント セットでは重複できません。 

## <a name="configuring-the-default-shell-for-openssh-in-windows"></a>OpenSSH を Windows での既定のシェルの構成

既定のコマンド シェルでは、SSH を使用してサーバーに接続するときに表示エクスペリエンスを提供します。 既定の初期の Windows は、Windows コマンド シェル (cmd.exe) です。 Windows PowerShell と Bash にも含まれます、サード パーティ製のコマンド シェルが Windows に使用できるも、サーバーの既定のシェルとして構成することがあります。

コマンド シェルを既定値を設定するには、OpenSSH のインストール フォルダーがシステム パスにあるをまず確認します。 Windows では、既定のインストール フォルダーは SystemDrive:WindowsDirectory\System32\openssh します。 次のコマンドは、現在のパス設定を表示し、OpenSSH の既定のインストール フォルダーを追加しています。 

コマンド シェル | コマンドを使用するには
------------- | -------------- 
コマンド | path
PowerShell | $env:path: パス

構成、既定 ssh シェルは、Windows レジストリにして行います DefaultShell 文字列値で実行可能ファイルを Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OpenSSH シェルへの完全なパスを追加します。 

例としては、次の Powershell コマンドは、PowerShell.exe を使用する既定のシェルを設定します。

```powershell
New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -PropertyType String -Force
```

## <a name="windows-configurations-in-sshdconfig"></a>Sshd_config で Windows の構成 

Windows、sshd が %programdata%\ssh\sshd_config から既定では、構成データを読み取るまたは sshd.exe-f パラメーターを使用してを起動することで、異なる構成ファイルを指定することがあります。
ファイルが存在しない場合は、sshd を生成します、既定の構成、サービスを開始します。

以下に示す要素は、Windows 固有の sshd_config のエントリから構成可能な限りを提供します。 その他の構成設定はではここでは、一覧にないように、オンラインの詳細については、 [Win32 OpenSSH ドキュメント](https://github.com/powershell/win32-openssh/wiki)します。 


### <a name="allowgroups-allowusers-denygroups-denyusers"></a>AllowGroups、マッチ、DenyGroups、DenyUsers 

ユーザーとグループは、サーバーに接続できるを制御するときは AllowGroups、マッチ、DenyGroups および DenyUsers ディレクティブを使用します。 許可または拒否のディレクティブは、次の順序で処理されます。DenyUsers、マッチ、DenyGroups、および最後に AllowGroups します。 すべてのアカウント名は小文字で指定する必要があります。 ワイルドカードのパターンの詳細については ssh_config パターンを参照してください。

ベースのドメイン ユーザーまたはグループと規則をユーザー/グループを構成するときに、次の形式を使用:``` user?domain* ```します。
Windows ドメインのプリンシパルを指定するための形式の複数の許可が、Linux の標準のパターンと競合する多くします。 そのため、* Fqdn についての説明に追加されます。 また、このアプローチを使用して"?"の代わりに @ との競合を回避するために、username@host形式。 

グループのユーザー/グループの作業とインターネットに接続されたアカウントは、常に、ローカルのアカウント名 (ないドメイン部分、Unix の標準的な名前に似ています) に解決されます。 ドメイン ユーザーとグループに厳密に解決[NameSamCompatible](https://docs.microsoft.com/windows/desktop/api/secext/ne-secext-extended_name_format) domain_short_name\user_name 形式。 すべてのユーザー/グループ ベースの構成ルールは、この形式に従う必要があります。

ドメイン ユーザーおよびグループの例 

```
DenyUsers contoso\admin@192.168.2.23 : blocks contoso\admin from 192.168.2.23
DenyUsers contoso\* : blocks all users from contoso domain
AllowGroups contoso\sshusers : only allow users from contoso\sshusers group
```

ローカル ユーザーとグループの例 

```
AllowUsers localuser@192.168.2.23
AllowGroups sshusers
```

### <a name="authenticationmethods"></a>AuthenticationMethods 

Windows の OpenSSH、のみ使用可能な認証方法は、"password"と"publickey"です。

### <a name="authorizedkeysfile"></a>AuthorizedKeysFile 

既定では".ssh/authorized_keys .ssh/authorized_keys2"です。 パスが絶対でない場合は、ユーザーのホーム ディレクトリ (またはプロファイル イメージのパス) 取得されます。 例: c:\users\user します。

### <a name="chrootdirectory-support-added-in-v7700"></a>ChrootDirectory (v7.7.0.0 で追加されたサポート)

このディレクティブは、sftp セッションでのみサポートされます。 Cmd.exe をリモート セッションには、これを優先しません。 Sftp 専用 chroot サーバーをセットアップするには、内部 sftp に ForceCommand を設定します。 設定することも scp を chroot で scp と sftp はのみを許可するカスタム シェルを実装することで。

### <a name="hostkey"></a>ホット キー

既定では、%programdata%/ssh/ssh_host_ecdsa_key、%programdata%/ssh/ssh_host_ed25519_key、%programdata%/ssh/ssh_host_rsa_key します。 既定値が存在しない場合は、sshd 自動的にこれらのサービスの開始を生成します。

### <a name="match"></a>一致

このセクションの規則をパターンに注意してください。 ユーザーとグループ名は小文字でなければなりません。

### <a name="permitrootlogin"></a>PermitRootLogin

Windows では適用されません。 管理者のログインを防ぐためには、管理者を使用して、DenyGroups ディレクティブを使用します。

### <a name="syslogfacility"></a>SyslogFacility

ファイル ベースのログ記録が必要な場合は、LOCAL0 を使用します。 %Programdata%\ssh\logs では、ログが生成されます。
その他の値には、ETW へのログ記録認証の既定値を含むよう指示します。 詳細については、Windows でのログ記録の機能を参照してください。

### <a name="not-supported"></a>サポートされていません 

次の構成オプションでは、Windows Server 2019 および Windows 10 1809 に付属する OpenSSH バージョンで使用できません。

* AcceptEnv
* AllowStreamLocalForwarding
* AuthorizedKeysCommand
* AuthorizedKeysCommandUser
* AuthorizedPrincipalsCommand
* AuthorizedPrincipalsCommandUser
* 圧縮
* ExposeAuthInfo
* GSSAPIAuthentication
* GSSAPICleanupCredentials
* GSSAPIStrictAcceptorCheck
* HostbasedAcceptedKeyTypes
* HostbasedAuthentication
* HostbasedUsesNameFromPacketOnly
* IgnoreRhosts
* IgnoreUserKnownHosts
* KbdInteractiveAuthentication
* KerberosAuthentication
* KerberosGetAFSToken
* KerberosOrLocalPasswd
* KerberosTicketCleanup
* PermitTunnel
* PermitUserEnvironment
* PermitUserRC
* すれば
* PrintLastLog
* RDomain
* StreamLocalBindMask
* StreamLocalBindUnlink
* StrictModes
* X11DisplayOffset
* X11 フォワーディング
* X11UseLocalhost
* XAuthLocation

