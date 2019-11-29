---
ms.date: 09/27/2018
ms.topic: conceptual
keywords: OpenSSH, SSH, SSHD, インストール, 設定
contributor: maertendMSFT
ms.product: w10
author: maertendMSFT
title: Windows 用 OpenSSH サーバー構成
ms.openlocfilehash: ed424c33c4cd2c19a9b5e985ab6083bcbcb9fbdc
ms.sourcegitcommit: 0467b8e69de66e3184a42440dd55cccca584ba95
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/16/2019
ms.locfileid: "69546260"
---
# <a name="openssh-server-configuration-for-windows-10-1809-and-server-2019"></a>Windows 10 1809 および Server 2019 用 OpenSSH Server 構成

このトピックでは、OpenSSH サーバー (sshd) の Windows 固有の構成について説明します。 

OpenSSH では、構成オプションに関する詳細なドキュメントが [OpenSSH.com](https://www.openssh.com/manual.html) でオンラインで管理されています。それらについては、このドキュメント セットでは繰り返しません。 

## <a name="configuring-the-default-shell-for-openssh-in-windows"></a>Windows での OpenSSH 用の既定のシェルの構成

既定のコマンド シェルでは、ユーザーが SSH を使用してサーバーに接続するときに表示されるエクスペリエンスが提供されます。 最初の既定の Windows は、Windows コマンド シェル (cmd.exe) です。 Windows には PowerShell と Bash も含まれています。サードパーティのコマンド シェルも Windows で使用でき、サーバーの既定のシェルとして構成できます。

既定のコマンド シェルを設定するには、まず、OpenSSH インストール フォルダーがシステム パスにあることを確認します。 Windows では、既定のインストール フォルダーは SystemDrive:WindowsDirectory\System32\openssh です。 次のコマンドによって現在のパス設定が表示され、それに既定の OpenSSH インストール フォルダーが追加されます。 

コマンド シェル | 使用するコマンド
------------- | -------------- 
コマンド | パス
PowerShell | $env:path

既定の ssh シェルの構成は、シェルの実行可能ファイルへの完全なパス Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OpenSSH を、Windows レジストリの文字列値 DefaultShell に追加することで行われます。 

例として、次の Powershell コマンドによって、既定のシェルが PowerShell.exe に設定されます。

```powershell
New-ItemProperty -Path "HKLM:\SOFTWARE\OpenSSH" -Name DefaultShell -Value "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe" -PropertyType String -Force
```

## <a name="windows-configurations-in-sshd_config"></a>sshd_config 内の Windows 構成 

Windows の sshd では、既定で %programdata%\ssh\sshd_config から構成データが読み取られます。または、-f パラメーターを指定して sshd.exe を起動することで、別の構成ファイルを指定できます。
ファイルが存在しない場合は、サービスの開始時に sshd によって既定の構成で生成されます。

以下に示す要素では、sshd_config のエントリを使用して可能な Windows 固有の構成が提供されます。 ここには記載されていないその他の構成設定もあります。詳細については、オンラインの [Win32 OpenSSH ドキュメント](https://github.com/powershell/win32-openssh/wiki)を参照してください。 


### <a name="allowgroups-allowusers-denygroups-denyusers"></a>AllowGroups、AllowUsers、DenyGroups、DenyUsers 

サーバーに接続できるユーザーとグループの制御は、AllowGroups、AllowUsers、DenyGroups、および DenyUsers の各ディレクティブを使用して行います。 allow/deny ディレクティブは、次の順序で処理されます。DenyUsers、AllowUsers、DenyGroups、最後に AllowGroups。 すべてのアカウント名は、小文字で指定する必要があります。 ワイルドカードのパターンの詳細については、ssh_config の PATTERNS を参照してください。

ドメイン ユーザーまたはグループを使用してユーザー/グループ ベースの規則を構成する場合は、``` user?domain* ``` の形式を使用します。
Windows では、ドメイン プリンシパルを指定するために複数の形式を使用できますが、標準の Linux パターンと競合するものが多数あります。 そのため、FQDN をカバーするために * が追加されています。 また、この方法では、@ の代わりに "?" を使用して、username@host 形式との競合を回避しています。 

ワーク グループ users/groups とインターネットに接続されたアカウントは、常にローカルのアカウント名に解決されます (標準の Unix 名と同様に、ドメイン部分がありません)。 ドメイン ユーザーとグループは、[NameSamCompatible](https://docs.microsoft.com/windows/desktop/api/secext/ne-secext-extended_name_format) 形式 (domain_short_name\user_name) に厳密に解決されます。 すべてのユーザー/グループ ベースの構成規則は、この形式に従う必要があります。

ドメイン ユーザーとグループの例 

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

Windows OpenSSH の場合、使用できる認証方法は "password" と "publickey" だけです。

### <a name="authorizedkeysfile"></a>AuthorizedKeysFile 

既定値は ".ssh/authorized_keys .ssh/authorized_keys2" です。 パスが絶対パスでない場合は、ユーザーのホーム ディレクトリ (またはプロファイル イメージ パス) に対して相対的に取得されます。 例: c:\users\user

### <a name="chrootdirectory-support-added-in-v7700"></a>ChrootDirectory (v7.7.0.0 に追加されたサポート)

このディレクティブは、sftp セッションでのみサポートされます。 cmd.exe へのリモート セッションでは、このようなことはできません。 sftp 専用の chroot サーバーをセットアップするには、ForceCommand を internal-sftp に設定します。 scp と sftp だけを許可するカスタム シェルを実装することで、chroot を使用する scp をセットアップすることもできます。

### <a name="hostkey"></a>HostKey

既定値は、%programdata%/ssh/ssh_host_ecdsa_key、%programdata%/ssh/ssh_host_ed25519_key、および %programdata%/ssh/ssh_host_rsa_key です。 既定値が存在しない場合は、サービスの開始時に sshd によってこれらが自動的に生成されます。

### <a name="match"></a>一致

このセクションのパターン規則に注意してください。 ユーザー名とグループ名は小文字にする必要があります。

### <a name="permitrootlogin"></a>PermitRootLogin

Windows では適用されません。 管理者のログインを防ぐには、DenyGroups ディレクティブで Administrators を使用します。

### <a name="syslogfacility"></a>SyslogFacility

ファイルベースのログ記録が必要な場合は、LOCAL0 を使用します。 ログは、%programdata%\ssh\logs に生成されます。
既定値の AUTH を含むその他の値では、ETW にログが記録されます。 詳細については、Windows のログ機能を参照してください。

### <a name="not-supported"></a>サポートされない 

Windows Server 2019 および Windows 10 1809 に付属する OpenSSH バージョンでは、次の構成オプションは使用できません。

* AcceptEnv
* AllowStreamLocalForwarding
* AuthorizedKeysCommand
* AuthorizedKeysCommandUser
* AuthorizedPrincipalsCommand
* AuthorizedPrincipalsCommandUser
* Compression
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

