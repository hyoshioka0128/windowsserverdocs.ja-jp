---
ms.date: 09/27/2018
ms.topic: conceptual
keywords: OpenSSH、SSH、SSHD、install、setup
contributor: maertendMSFT
ms.product: w10
author: maertendMSFT
title: Windows 用 OpenSSH サーバー構成
ms.openlocfilehash: ed424c33c4cd2c19a9b5e985ab6083bcbcb9fbdc
ms.sourcegitcommit: 0467b8e69de66e3184a42440dd55cccca584ba95
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69546260"
---
# <a name="openssh-server-configuration-for-windows-10-1809-and-server-2019"></a>Windows 10 1809 およびサーバー2019用 OpenSSH サーバー構成

このトピックでは、OpenSSH サーバー (sshd) の Windows 固有の構成について説明します。 

OpenSSH では、構成オプションに関する詳細なドキュメントを[OpenSSH.com](https://www.openssh.com/manual.html)でオンラインで管理しています。このドキュメントは、このドキュメントセットには複製されていません。 

## <a name="configuring-the-default-shell-for-openssh-in-windows"></a>Windows での OpenSSH 用の既定のシェルの構成

既定のコマンドシェルは、SSH を使用してサーバーに接続するときにユーザーに表示されるエクスペリエンスを提供します。 最初の既定のウィンドウは、Windows コマンドシェル (cmd.exe) です。 Windows には PowerShell と Bash も含まれており、サードパーティのコマンドシェルも Windows で使用でき、サーバーの既定のシェルとして構成することができます。

既定のコマンドシェルを設定するには、まず、OpenSSH インストールフォルダーがシステムパスにあることを確認します。 Windows の場合、既定のインストールフォルダーは SystemDrive: WindowsDirectory\System32\openssh. です。 次のコマンドは、現在のパス設定を示し、既定の OpenSSH インストールフォルダーを追加します。 

コマンドシェル | 使用するコマンド
------------- | -------------- 
Command | path
PowerShell | $env:p a

Windows レジストリで既定の ssh シェルを構成するには、シェルの実行可能ファイルへの完全なパスを文字列値 DefaultShell の Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OpenSSH に追加します。 

例として、次の Powershell コマンドは、既定のシェルを PowerShell .exe に設定します。

```powershell
New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -PropertyType String -Force
```

## <a name="windows-configurations-in-sshd_config"></a>Sshd_config の Windows 構成 

Windows では、sshd は既定で%programdata%\ssh\sshd_config から構成データを読み取ります。または、-f パラメーターを指定して sshd を起動することによって、別の構成ファイルを指定することもできます。
ファイルが存在しない場合、sshd はサービスの開始時に既定の構成で1つを生成します。

以下に示す要素は、sshd_config のエントリを使用して可能な Windows 固有の構成を提供します。 ここには記載されていない他の構成設定もあります。詳細については、オンラインの[Win32 OpenSSH のドキュメント](https://github.com/powershell/win32-openssh/wiki)を参照してください。 


### <a name="allowgroups-allowusers-denygroups-denyusers"></a>AllowGroups、Allowgroups、DenyGroups、Denygroups 

サーバーに接続できるユーザーとグループの制御は、AllowGroups、Allowgroups、DenyGroups、および Denygroups ディレクティブを使用して行います。 許可/拒否ディレクティブは、次の順序で処理されます。DenyUsers、AllowUsers、Denyusers、および finally Allowusers。 すべてのアカウント名は小文字で指定する必要があります。 ワイルドカードのパターンの詳細については、「ssh_config のパターン」を参照してください。

ドメインユーザーまたはグループを使用してユーザー/グループベースの規則を構成する場合``` user?domain* ```は、という形式を使用します。
Windows ではドメインプリンシパルを指定するために複数の形式を使用できますが、多くの場合、標準の Linux パターンと競合します。 そのため、* がカバー Fqdn に追加されます。 また、この方法では、@ の代わりに "?" を使用してusername@host 、形式との競合を回避します。 

ワークグループのユーザー/グループとインターネットに接続されたアカウントは、常にローカルのアカウント名に解決されます (標準の Unix 名と同様に、ドメイン部分はありません)。 ドメインユーザーとグループは、 [Namesamcompatible](https://docs.microsoft.com/windows/desktop/api/secext/ne-secext-extended_name_format)形式に厳密に解決されます-domain_short_name\user_name. すべてのユーザー/グループベースの構成規則は、この形式に従う必要があります。

ドメインユーザーとグループの例 

```
DenyUsers contoso\admin@192.168.2.23 : blocks contoso\admin from 192.168.2.23
DenyUsers contoso\* : blocks all users from contoso domain
AllowGroups contoso\sshusers : only allow users from contoso\sshusers group
```

ローカルユーザーとグループの例 

```
AllowUsers localuser@192.168.2.23
AllowGroups sshusers
```

### <a name="authenticationmethods"></a>AuthenticationMethods 

Windows OpenSSH の場合、使用できる認証方法は "パスワード" と "publickey" だけです。

### <a name="authorizedkeysfile"></a>AuthorizedKeysFile 

既定値は ". ssh/authorized_keys/authorized_keys2" です。 パスが絶対パスでない場合は、ユーザーのホームディレクトリ (またはプロファイルイメージパス) に対して相対的に取得されます。 例: c:\users\user.

### <a name="chrootdirectory-support-added-in-v7700"></a>ChrootDirectory (v 7.7.0.0 に追加されたサポート)

このディレクティブは、sftp セッションでのみサポートされています。 Cmd.exe へのリモートセッションでは、このようなことはできません。 Sftp 専用の chroot サーバーをセットアップするには、ForceCommand を内部 sftp に設定します。 Scp と sftp を許可するカスタムシェルを実装することで、scp で scp を設定することもできます。

### <a name="hostkey"></a>HostKey

既定値は、% programdata%/ssh/ssh_host_ecdsa_key、% programdata%/ssh/ssh_host_ed25519_key、% programdata%/ssh/ssh_host_rsa_key. です。 既定値が存在しない場合、sshd はサービスの開始時にこれらを自動的に生成します。

### <a name="match"></a>一致

このセクションのパターン規則に注意してください。 ユーザー名とグループ名は小文字で指定する必要があります。

### <a name="permitrootlogin"></a>PermitRootLogin

Windows には適用されません。 管理者のログインを防ぐには、管理者に DenyGroups ディレクティブを使用します。

### <a name="syslogfacility"></a>SyslogFacility

ファイルベースのログ記録が必要な場合は、LOCAL0 を使用します。 %Programdata%\ssh\logs. の下にログが生成されます。
その他の値 (既定値の AUTH を含む) は、ETW にログを記録します。 詳細については、「Windows のログ機能」を参照してください。

### <a name="not-supported"></a>サポートされていません 

次の構成オプションは、Windows Server 2019 および Windows 10 1809 に付属する OpenSSH バージョンでは使用できません。

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
* ホストベース認証
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
* PidFile
* PrintLastLog
* RDomain
* StreamLocalBindMask
* StreamLocalBindUnlink
* StrictModes
* X11DisplayOffset
* X11Forwarding
* X11UseLocalhost
* XAuthLocation

