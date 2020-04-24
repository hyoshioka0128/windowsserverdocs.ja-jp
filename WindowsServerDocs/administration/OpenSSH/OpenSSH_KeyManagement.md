---
ms.date: 09/27/2018
ms.topic: conceptual
contributor: maertendMSFT
author: maertendmsft
title: Windows 用 OpenSSH サーバー構成
ms.product: windows-server
ms.openlocfilehash: defb8875ca73c0d08fb0fa0764ed3ddf9003e09c
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2020
ms.locfileid: "80852045"
---
# <a name="openssh-key-management"></a>OpenSSH キーの管理

Windows 環境でのほとんどの認証は、ユーザー名とパスワードの組み合わせを使用して行われます。
これは、共通ドメインを共有するシステムでは正常に機能します。 オンプレミスのシステムとクラウドでホストされたシステムの間など、ドメインをまたがって作業する場合は、より困難になります。

これに対し、Linux 環境では一般に、認証を促進するために公開キー/秘密キーのペアが使用されます。
OpenSSH には、これをサポートするためのツールが含まれています。具体的には次のとおりです。

* セキュリティ キーを生成するための __ssh-keygen__
* 秘密キーを安全に格納するための __ssh-agent__ と __ssh-add__
* サーバーの初回使用時に公開キー ファイルを安全にコピーするための __scp__ と __sftp__

このドキュメントでは、Windows 上でこれらのツールを使用して、SSH によるキー認証の使用を開始する方法の概要を示します。 SSH キーの管理に慣れていない場合は、「Secure Shell (SSH) を使用した対話型および自動化されたアクセス管理のセキュリティ」というタイトルの [NIST ドキュメント IR 7966](http://nvlpubs.nist.gov/nistpubs/ir/2015/NIST.IR.7966.pdf) を確認することを強くお勧めします。

## <a name="about-key-pairs"></a>キー ペアについて

キー ペアは、特定の認証プロトコルで使用される公開および秘密キー ファイルを意味します。 

SSH 公開キー認証では、非対称暗号アルゴリズムを使用して 2 つのキー ファイルが生成されます。1 つは "秘密"、もう 1 つは "公開" です。 秘密キー ファイルはパスワードと同等であり、すべての状況下で保護される必要があります。 ユーザーの秘密キーを入手した人は、ユーザーがアクセス権を持つ SSH サーバーにそのユーザーとしてログインできます。 公開キーは SSH サーバー上に配置されるものであり、秘密キーを侵害することなく共有できます。

SSH サーバーでキー認証を使用する場合、SSH サーバーとクライアントにより、指定されたユーザー名の公開キーが秘密キーと比較されます。 クライアント側の秘密キーに対して公開キーを検証できない場合、認証は失敗します。 

キー ペアを生成するときにパスフレーズの指定を要求することで、キー ペアを使用した多要素認証を実装できます (以下のキー生成に関する説明を参照してください)。 認証中に、ユーザーは、ユーザーを認証するために SSH クライアント上の秘密キーの存在と共に使用されるパスフレーズの入力を求められます。 

## <a name="host-key-generation"></a>ホスト キーの生成

公開キーには、Windows 上で管理者とシステムへのアクセスのみを許可することと同等の特定の ACL 要件があります。 これを簡単にするために、 

* キー ACL を適切に設定するために OpenSSHUtils PowerShell モジュールが作成されており、サーバーにインストールされている必要があります
* sshd を初めて使用するときに、ホストのキー ペアが自動的に生成されます。 ssh-agent が実行されている場合、キーはローカル ストアに自動的に追加されます。 

SSH サーバーでのキー認証を簡単に行うには、管理者特権の PowerShell プロンプトから次のコマンドを実行します。

```powershell

# Install the OpenSSHUtils module to the server. This will be valuable when deploying user keys.
Install-Module -Force OpenSSHUtils -Scope AllUsers

# Start the ssh-agent service to preserve the server keys
Start-Service ssh-agent

# Now start the sshd service
Start-Service sshd
```

sshd サービスに関連付けられているユーザーがいないため、ホストキーは \ProgramData\ssh の下に格納されます。


## <a name="user-key-generation"></a>ユーザー キーの生成

キーベースの認証を使用するには、最初にクライアント用の公開/秘密キーのペアをいくつか生成する必要があります。 PowerShell または cmd から ssh-keygen を使用して、いくつかのキー ファイルを生成します。

```powershell
cd ~\.ssh\
ssh-keygen
```

これにより、次のような内容が表示されます ("username" はご自身のユーザー名に置き換えられます)

```
Generating public/private ed25519 key pair.
Enter file in which to save the key (C:\Users\username\.ssh\id_ed25519):
```

Enter キーを押して既定値をそのまま使用することも、キーを生成するパスを指定することもできます。 この時点で、秘密キー ファイルを暗号化するためにパスフレーズを使用するように求められます。
パスフレーズがキー ファイルと連携して、2 要素認証が提供されます。 この例では、パスフレーズを空のままにしています。 

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

これで、公開/プライベート ED25519 キー ペアが作成されました (.pub ファイルが公開キーで、残りは秘密キーです)。

```
Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        9/28/2018  11:09 AM           1679 id_ed25519
-a----        9/28/2018  11:09 AM            414 id_ed25519.pub
```

秘密キー ファイルはパスワードと同等のもので、パスワードを保護するのと同じ方法で保護する必要があることに注意してください。
そのために、ssh-agent を使用して、Windows ログインに関連付けられている Windows セキュリティ コンテキスト内に秘密キーを安全に格納します。 これを行うには、管理者として ssh-agent サービスを開始し、ssh-add を使用して秘密キーを格納します。 

```powershell
# Make sure you're running as an Administrator
Start-Service ssh-agent

# This should return a status of Running
Get-Service ssh-agent

# Now load your key files into ssh-agent
ssh-add ~\.ssh\id_ed25519

```

これらの手順を完了すると、このクライアントからの認証に秘密キーが必要になるたびに、ssh-agent によってローカルの秘密キーが自動的に取得されて、SSH クライアントに渡されます。

> [!NOTE]
> 秘密キーを ssh-agent に追加した "*後*"、セキュリティで保護された場所にバックアップしてから、ローカル システムから削除することを強くお勧めします。
> 秘密キーをエージェントから取得することはできません。
> 秘密キーにアクセスできなくなった場合は、新しいキー ペアを作成し、操作するすべてのシステム上で公開キーを更新する必要があります。

## <a name="deploying-the-public-key"></a>公開キーのデプロイ

上で作成したユーザー キーを使用するには、サーバー上の users\username\.ssh\. の下にある *authorized_keys* という名前のテキスト ファイルに公開キーを配置する必要があります。 OpenSSH ツールには、これを支援するための、セキュリティで保護されたファイル転送ユーティリティである scp が含まれています。

公開キー (~\.ssh\id_ed25519.pub) の内容を、サーバー/ホスト上の ~\.ssh\ 内の authorized_keys という名前のテキスト ファイルに移動します。

この例では、前の手順でホストにインストールされていた OpenSSHUtils モジュール内の Repair-AuthorizedKeyPermissions 関数を使用します。

```powershell
# Make sure that the .ssh directory exists in your server's home folder
ssh user1@domain1@contoso.com mkdir C:\users\user1\.ssh\

# Use scp to copy the public key file generated previously to authorized_keys on your server
scp C:\Users\user1\.ssh\id_ed25519.pub user1@domain1@contoso.com:C:\Users\user1\.ssh\authorized_keys

# Appropriately ACL the authorized_keys file on your server  
ssh --% user1@domain1@contoso.com powershell -c $ConfirmPreference = 'None'; Repair-AuthorizedKeyPermission C:\Users\user1\.ssh\authorized_keys
```

これらの手順で、Windows 上の SSH でキーベース認証を使用するために必要な構成を完了します。
その後、ユーザーは、秘密キーを持つ任意のクライアントから sshd ホストに接続できます。

