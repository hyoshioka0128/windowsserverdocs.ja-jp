---
ms.date: 09/27/2018
ms.topic: conceptual
keywords: OpenSSH を SSH、SSHD、インストール、セットアップ
contributor: maertendMSFT
author: maertendMSFT
title: Windows の OpenSSH サーバー構成
ms.product: w10
ms.openlocfilehash: 3e2981cbbdfe34bf28a77d5121bff0b663e0d3bf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837153"
---
# <a name="openssh-key-management"></a>OpenSSH キーの管理

Windows 環境でほとんどの認証は、ユーザー名とパスワードのペアで実行されます。
これは、一般的なドメインを共有するシステムに適しています。 複数のドメインを使用する場合など、オンプレミスとクラウド ホスト型のシステム間で、困難になります。

比較すると、Linux 環境では、一般公開キー/秘密キー ペアにドライブの認証を使用します。
OpenSSH には、具体的には、これをサポートするためにツールが含まれています。

* __ssh-keygen__セキュリティで保護されたキーを生成します。
* __ssh__と__ssh アド__秘密キーの安全な保存
* __scp__と__sftp__サーバーの初期の使用中に安全にパブリック キー ファイルをコピーするには

このドキュメントでは、Windows 上のこれらのツールを使用して、ssh キー認証の使用を開始する方法の概要を示します。 SSH キーの管理に慣れていない場合お読みください[NIST のドキュメント IR 7966](http://nvlpubs.nist.gov/nistpubs/ir/2015/NIST.IR.7966.pdf) 「対話型と自動アクセス管理、使用する Secure Shell (SSH) のセキュリティ」というタイトル。

## <a name="about-key-pairs"></a>キーのペアについて

キーのペアは、特定の認証プロトコルで使用されるパブリックおよびプライベート キー ファイルを参照してください。 

SSH 公開キー認証では、非対称暗号化アルゴリズムを使用して、– 1 つの"private"とその他の「パブリック」の 2 つのキー ファイルを生成します。 秘密キー ファイルと同等のパスワードのあらゆる状況下で保護されている必要があります。 ユーザーには、秘密キーが取得した場合、ことができますにログインするようにアクセスする任意の SSH サーバー。 公開キーは、内容は、SSH サーバーに配置され、秘密キーを損なうことがなく共有することがあります。

SSH サーバーをキー認証を使用する場合、SSH サーバーとクライアントは、秘密キーに対して指定したユーザー名の公開キーを比較します。 公開キーは、クライアント側の秘密キーに対して検証できません、認証が失敗します。 

キーのペアの生成時にパスフレーズを指定することを要求することでキーの組に多要素認証を実装することがあります (以下のキーの生成を参照してください)。 認証では、ユーザーは、パスフレーズの入力を求め、際、ユーザーの認証に SSH クライアントの秘密キーの有無と共に使用するされます。 

## <a name="host-key-generation"></a>ホスト キーの生成

公開キー要件がある特定 ACL で、Windows、時と見なされるのみ管理者とシステムへのアクセスを許可します。 簡単に、確認するには 

* OpenSSHUtils PowerShell モジュールは、キーの Acl を適切に設定するが作成され、サーバーにインストールする必要があります。
* Sshd の初回使用時のホスト キーのペアが自動的に生成されます。 Ssh エージェントが実行されている場合、キーはローカル ストアに自動的に追加します。 

キー認証を SSH サーバーを簡単にするには、管理者特権の PowerShell プロンプトから次のコマンドを実行します。

```powershell

# Install the OpenSSHUtils module to the server. This will be valuable when deploying user keys.
Install-Module -Force OpenSSHUtils -Scope AllUsers

# Start the ssh-agent service to preserve the server keys
Start-Service ssh-agent

# Now start the sshd service
Start-Service sshd
```

Sshd サービスに関連付けられているユーザーがないため、\ProgramData\ssh ホスト キーが格納されます。


## <a name="user-key-generation"></a>ユーザー キーの生成

キー ベースの認証を使用するには、は、まず、クライアントのいくつか公開/秘密キー ペアを生成する必要があります。 PowerShell または cmd からには、いくつかのキー ファイルを生成するのに、ssh-keygen を使用します。

```powershell
cd ~\.ssh\
ssh-keygen
```

これは ("username"は、ユーザー名に置換)、次のようなものを表示する必要があります

```
Generating public/private ed25519 key pair.
Enter file in which to save the key (C:\Users\username\.ssh\id_ed25519):
```

既定値を受け入れるように Enter キーを押します。 または、キーを生成するように、パスを指定できます。 この時点で求められます、秘密キー ファイルを暗号化するパスフレーズを使用します。
パスフレーズは、2 要素認証を提供するキー ファイルで動作します。 この例では、私たちは、パスフレーズを空のままです。 

```
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in C:\Users\username\.ssh\id_ed25519.
Your public key has been saved in C:\Users\username\.ssh\id_ed25519.pub.
The key fingerprint is: 
SHA256:OIzc1yE7joL2Bzy8!gS0j8eGK7bYaH1FmF3sDuMeSj8 username@server@LOCAL-HOSTNAME

The key's randomart image is:
+--[ED25519 256]--+
|        .        |
|         o       |
|    . + + .      |
|   o B * = .     |
|   o= B S .      |
|   .=B O o       |
|  + =+% o        |
| *oo.O.E         |
|+.o+=o. .        |
+----[SHA256]-----+
```

公開/秘密 ED25519 キー ペア (.pub ファイルは公開キーと、残りは秘密キー) する必要があります。

```
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        9/28/2018  11:09 AM           1679 id_ed25519
-a----        9/28/2018  11:09 AM            414 id_ed25519.pub
```

秘密キー ファイルに同様に、パスワードの保護と同等のパスワードを保護する必要がある注意してください。
支援するのにには、Windows ログインに関連付けられている、Windows のセキュリティ コンテキスト内で秘密キーを安全に保管するのに ssh を使用します。 そのためには、ssh エージェント サービスを管理者として起動し、使用 ssh-追加秘密キーを格納します。 

```powershell
# Make sure you're running as an Administrator
Start-Service ssh-agent

# This should return a status of Running
Get-Service ssh-agent

# Now load your key files into ssh-agent
ssh-add ~\.ssh\id_ed25519

```

次の手順を完了すると、秘密キーが、このクライアントからの認証に必要なときに ssh エージェントは自動的にローカルの秘密キーを取得および SSH クライアントに渡すことです。

> [!NOTE]
> 安全な場所に、秘密キーをバックアップし、ローカルのシステムから削除することを強くお勧め*後*ssh に追加します。
> エージェントからは、秘密キーを取得できません。
> アクセスを秘密キーを紛失した場合は、新しいキー ペアを作成し、対話するすべてのシステムでの公開キーを更新する必要があります。

## <a name="deploying-the-public-key"></a>公開キーを展開します。

上記で作成されたユーザー キーを使用する公開キーはというテキスト ファイルに、サーバーに配置する必要がある*authorized_keys* users\username\ssh 下。 OpenSSH ツールには、scp セキュリティで保護されたファイル転送ユーティリティには、これを支援にはが含まれます。

公開キーのコンテンツに移動する (~\.ssh\id_ed25519.pub)、テキスト ファイルと呼ばれるに authorized_keys ~\.ssh\ サーバー/ホストでします。

この例では、修復 AuthorizedKeyPermissions 関数を使用して、上記の手順で、ホストにインストールされている、OpenSSHUtils モジュールにします。

```powershell
# Make sure that the .ssh directory exists in your server's home folder
ssh user1@domain1@contoso.com mkdir C:\users\user1\.ssh\

# Use scp to opy the public key file generated previously to authorized_keys on your server
scp C:\Users\user1\.ssh\id_ed25519.pub user1@domain1@contoso.com:C:\Users\user1\.ssh\authorized_keys

# Appropriately ACL the authorized_keys file on your server  
ssh --% user1@domain1@contoso.com powershell -c $ConfirmPreference = 'None'; Repair-AuthorizedKeyPermission C:\Users\user1\.ssh\authorized_keys
```

次の手順では、Windows で ssh キー ベースの認証を使用するために必要な構成を完了します。
その後、ユーザーは、秘密キーを持つ任意のクライアントから sshd ホストに接続できます。

