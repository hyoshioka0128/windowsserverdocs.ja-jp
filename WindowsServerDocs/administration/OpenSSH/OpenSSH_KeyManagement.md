---
ms.date: 09/27/2018
ms.topic: conceptual
keywords: OpenSSH、SSH、SSHD、install、setup
contributor: maertendMSFT
author: maertendMSFT
title: Windows 用 OpenSSH サーバー構成
ms.product: w10
ms.openlocfilehash: ed9f3653c79f1329b1334f52fe14c1184bc99539
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866870"
---
# <a name="openssh-key-management"></a>OpenSSH キー管理

Windows 環境でのほとんどの認証は、ユーザー名とパスワードの組み合わせを使用して行われます。
これは、共通ドメインを共有するシステムに適しています。 オンプレミスとクラウドでホストされたシステムの間など、ドメイン間で作業する場合は、より困難になります。

これに対し、Linux 環境では、一般に、認証を促進するために公開キーと秘密キーのペアを使用します。
OpenSSH には、これをサポートするためのツールが含まれています。具体的には、

* secure キーを生成するための__ssh ssh-keygen__
* __ssh エージェント__と__ssh を追加__して、秘密キーを安全に格納します。
* サーバーの初回使用時に公開キーファイルを安全にコピーするための__scp__と__sftp__

このドキュメントでは、Windows でこれらのツールを使用して、SSH でキー認証の使用を開始する方法の概要を示します。 SSH キー管理に慣れていない場合は、「Secure Shell (SSH) を使用した対話型および自動化されたアクセス管理のセキュリティ」という名前の[NIST ドキュメント IR 7966](http://nvlpubs.nist.gov/nistpubs/ir/2015/NIST.IR.7966.pdf)を確認することを強くお勧めします。

## <a name="about-key-pairs"></a>キーペアについて

キーペアは、特定の認証プロトコルで使用される公開キーファイルと秘密キーファイルを指します。 

SSH 公開キー認証では、非対称暗号アルゴリズムを使用して2つのキーファイルを生成します。1つは "プライベート"、もう1つは "パブリック" です。 秘密キーファイルはパスワードと同等であり、すべての状況で保護されている必要があります。 だれかが秘密キーを取得した場合、アクセス権のある任意の SSH サーバーにログインできます。 公開キーは SSH サーバー上に配置されるものであり、秘密キーを損なうことなく共有できます。

SSH サーバーでキー認証を使用する場合、SSH サーバーとクライアントは、秘密キーに対して指定されたユーザー名の公開キーを比較します。 クライアント側の秘密キーに対して公開キーを検証できない場合、認証は失敗します。 

キーペアを生成するときにパスフレーズを指定することで、キーペアを使用して multi-factor authentication を実装できます (以下の「キー生成」を参照してください)。 認証中に、ユーザーは、ユーザーを認証するために SSH クライアントの秘密キーの存在と共に使用されるパスフレーズの入力を求められます。 

## <a name="host-key-generation"></a>ホストキーの生成

公開キーには、管理者とシステムへのアクセスのみを許可することと同等の ACL 要件があります。 これを簡単にするために、 

* キー Acl を適切に設定するために OpenSSHUtils PowerShell モジュールが作成されており、サーバーにインストールされている必要があります。
* Sshd を初めて使用するときは、ホストのキーペアが自動的に生成されます。 Ssh エージェントが実行されている場合、キーは自動的にローカルストアに追加されます。 

SSH サーバーでキー認証を簡単に行うには、管理者特権の PowerShell プロンプトから次のコマンドを実行します。

```powershell

# Install the OpenSSHUtils module to the server. This will be valuable when deploying user keys.
Install-Module -Force OpenSSHUtils -Scope AllUsers

# Start the ssh-agent service to preserve the server keys
Start-Service ssh-agent

# Now start the sshd service
Start-Service sshd
```

Sshd サービスに関連付けられているユーザーがいないため、ホストキーは \ProgramData\ssh. の下に格納されます。


## <a name="user-key-generation"></a>ユーザーキーの生成

キーベースの認証を使用するには、最初にクライアントの公開キーと秘密キーのペアを生成する必要があります。 PowerShell または cmd から ssh-keygen を使用して、いくつかのキーファイルを生成します。

```powershell
cd ~\.ssh\
ssh-keygen
```

次のような内容が表示されます ("username" はユーザー名に置き換えられます)。

```
Generating public/private ed25519 key pair.
Enter file in which to save the key (C:\Users\username\.ssh\id_ed25519):
```

Enter キーを押すと、既定値をそのまま使用することも、キーを生成するパスを指定することもできます。 この時点で、秘密キーファイルを暗号化するためにパスフレーズを使用するように求められます。
パスフレーズは、キーファイルと連携して、2要素認証を提供します。 この例では、パスフレーズを空のままにします。 

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

これで、公開/プライベート ED25519 キーペアが作成されました (pub ファイルは公開キーで、残りは秘密キーです)。

```
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        9/28/2018  11:09 AM           1679 id_ed25519
-a----        9/28/2018  11:09 AM            414 id_ed25519.pub
```

秘密キーファイルは、パスワードを保護するのと同じ方法で保護する必要があることに注意してください。
この問題を解決するには、windows ログインに関連付けられている Windows セキュリティコンテキスト内に、ssh エージェントを使用して秘密キーを安全に格納します。 これを行うには、管理者として ssh エージェントサービスを開始し、ssh 追加を使用して秘密キーを格納します。 

```powershell
# Make sure you're running as an Administrator
Start-Service ssh-agent

# This should return a status of Running
Get-Service ssh-agent

# Now load your key files into ssh-agent
ssh-add ~\.ssh\id_ed25519

```

これらの手順を完了すると、このクライアントからの認証に秘密キーが必要になるたびに、ssh エージェントは自動的にローカルの秘密キーを取得し、それを SSH クライアントに渡します。

> [!NOTE]
> 秘密キーを安全な場所にバックアップし、それをローカルシステムから削除した後で、それを ssh エージェントに追加*し*ておくことを強くお勧めします。
> エージェントから秘密キーを取得できません。
> 秘密キーにアクセスできなくなった場合は、新しいキーペアを作成し、操作するすべてのシステムで公開キーを更新する必要があります。

## <a name="deploying-the-public-key"></a>公開キーの配置

上記で作成したユーザーキーを使用するには、公開キーをサーバー上に配置して、users\username\ssh. の下に*authorized_keys*という名前のテキストファイルを作成する必要があります。 OpenSSH ツールには、これを支援するための、セキュリティで保護されたファイル転送ユーティリティである scp が含まれています。

公開キー (~\.ssh\id_ed25519.pub) の内容を、サーバー/ホスト上の authorized_keys\.内のというテキストファイルに移動する場合は。

この例では、前の手順でホストにインストールされていた OpenSSHUtils モジュールの Repair-AuthorizedKeyPermissions 関数を使用します。

```powershell
# Make sure that the .ssh directory exists in your server's home folder
ssh user1@domain1@contoso.com mkdir C:\users\user1\.ssh\

# Use scp to opy the public key file generated previously to authorized_keys on your server
scp C:\Users\user1\.ssh\id_ed25519.pub user1@domain1@contoso.com:C:\Users\user1\.ssh\authorized_keys

# Appropriately ACL the authorized_keys file on your server  
ssh --% user1@domain1@contoso.com powershell -c $ConfirmPreference = 'None'; Repair-AuthorizedKeyPermission C:\Users\user1\.ssh\authorized_keys
```

次の手順では、Windows 上の SSH でキーベースの認証を使用するために必要な構成を完了します。
その後、ユーザーは、秘密キーを持つ任意のクライアントから sshd ホストに接続できます。

