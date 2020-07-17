---
title: nfsadmin
description: NFS サーバーと NFS クライアントの両方を管理する nfsadmin コマンドの参照記事。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7375b2cf-c6b8-45b5-abf6-6c10e462defd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ad88594d534c64c0651fcc4e094fef669a02f16c
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85932334"
---
# <a name="nfsadmin"></a>nfsadmin

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Nfs サーバーまたは nfs クライアントを、Microsoft Services for Network File System (NFS) を実行しているローカルコンピューターまたはリモートコンピューター上で管理するコマンドラインユーティリティ。 パラメーターを指定せずに使用します。 nfsadmin server には、NFS 構成設定の現在のサーバーが表示され、nfsadmin client には、NFS 構成設定の現在のクライアントが表示されます。

## <a name="syntax"></a>Syntax

```
nfsadmin server [computername] [-u Username [-p Password]] -l
nfsadmin server [computername] [-u Username [-p Password]] -r {client | all}
nfsadmin server [computername] [-u Username [-p Password]] {start | stop}
nfsadmin server [computername] [-u Username [-p Password]] config option[...]
nfsadmin server [computername] [-u Username [-p Password]] creategroup <name>
nfsadmin server [computername] [-u Username [-p Password]] listgroups
nfsadmin server [computername] [-u Username [-p Password]] deletegroup <name>
nfsadmin server [computername] [-u Username [-p Password]] renamegroup <oldname> <newname>
nfsadmin server [computername] [-u Username [-p Password]] addmembers <hostname>[...]
nfsadmin server [computername] [-u Username [-p Password]] listmembers
nfsadmin server [computername] [-u Username [-p Password]] deletemembers <hostname><groupname>[...]
nfsadmin client [computername] [-u Username [-p Password]] {start | stop}
nfsadmin client [computername] [-u Username [-p Password]] config option[...]
```

### <a name="general-parameters"></a>一般的なパラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| computername | 管理するリモート コンピューターを指定します。 Windows インターネットネームサービス (WINS) 名またはドメインネームシステム (DNS) 名またはインターネットプロトコル (IP) アドレスを使用して、コンピューターを指定できます。 |
| -u ユーザー名 | 使用する資格情報を持つユーザーのユーザー名を指定します。 *Domain\username*という形式のユーザー名にドメイン名を追加する必要がある場合があります。 |
| -p パスワード | **-U**オプションを使用して指定したユーザーのパスワードを指定します。 - **U**オプションを指定しても **-p**オプションを省略した場合、ユーザーのパスワードの入力を求められます。 |

### <a name="server-for-nfs-related-parameters"></a>NFS サーバーに関連するパラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| -l | クライアントによって保持されているすべてのロックを一覧表示します。 |
| -r`{client|all}` | 保持するロックの解放、 クライアント または、 すべて すべてのクライアントで指定しました。 |
| start | Nfs サーバーを起動します。 |
| stop | サーバーの NFS サービスを停止します。 |
| config | Nfs サーバーの全般設定を指定します。 少なくとも 1 つの使用は、次のオプションを指定する必要があります、 **config** コマンドの引数。<ul><li>**mapsvr = `<server>` **-NFS サーバーのユーザー名マッピングサーバーとしてサーバーを設定します。 使用する必要がありますが、このオプションは引き続き以前のバージョンと互換性のためにサポートされる、 sfuadmin ユーティリティ代わりにします。</li><li>**auditlocation = `{eventlog|file|both|none}` **-イベントを監査するかどうか、およびイベントを記録するかどうかを指定します。 次のいずれかの引数が必要です。<ul><li>**eventlog** -監査イベントがイベントビューアーアプリケーションログにのみ記録されることを指定します。</li><li>**file** -監査イベントがによって指定されたファイルにのみ記録されることを指定し `config fname` ます。</li><li>**both** -監査イベントが、によって指定されたファイルと同様にイベントビューアーアプリケーションログに記録されることを指定し `config fname` ます。</li><li>**none** -イベントが監査されないことを指定します。</li></ul><li>**fname = `<file>` **-ファイルによって指定されたファイルを監査ファイルとして設定します。 既定値は **%sfudir%\log \\ **になります。</li><li>**fsize = `<size>` **-監査ファイルの最大サイズ (mb 単位) としてサイズを設定します。 既定の最大サイズは**7 MB**です。</li><li>**`audit=[+|-]mount [+|-]read [+|-]write [+|-]create [+|-]delete [+|-]locking [+|-]all`**-ログに記録するイベントを指定します。 イベントのログ記録を開始するには、イベント名の前にプラス記号 () を入力し、イベントの **+** ログ記録を停止するには、 **-** イベント名の前にマイナス記号 () を入力します。 符号を省略した場合は、と **+** 見なされます。 他のイベント名には**すべて**使用しないでください。</li><li>**lockperiod = `<seconds>` **-Nfs サーバーが、NFS サーバーへの接続が失われ、再確立された後、または NFS サーバーサービスが再起動された後に、ロックの再利用を待機する秒数を指定します。</li><li>**portmapprotocol = `{TCP|UDP|TCP+UDP}` **-どのトランスポートプロトコルのポートマップでサポートされるかを指定します。 既定の設定は、 **TCP + UDP**です。</li><li>**mountprotocol = `{TCP|UDP|TCP+UDP}` **-マウントがサポートするトランスポートプロトコルを指定します。 既定の設定は、 **TCP + UDP**です。</li><li>**nfsprotocol = `{TCP|UDP|TCP+UDP}` **-ネットワークファイルシステム (NFS) でサポートされているトランスポートプロトコルを指定します。 既定の設定は**TCP + UDP**です。</li><li>**nlmprotocol = `{TCP|UDP|TCP+UDP}` **-ネットワークロックマネージャー (NLM) がサポートするトランスポートプロトコルを指定します。 既定の設定は、 **TCP + UDP**です。</li><li>**nsmprotocol = `{TCP|UDP|TCP+UDP}` **-ネットワークステータスマネージャー (NSM) がサポートするトランスポートプロトコルを指定します。 既定の設定は、 **TCP + UDP**です。</li><li>**enableV3 = `{yes|no}` **-NFS version 3 プロトコルをサポートするかどうかを指定します。 既定の設定は **[はい]** です。</li><li>**renewauth = `{yes|no}` **-構成の renewauthinterval によって指定された期間が経過した後に、クライアント接続を再認証する必要があるかどうかを指定します。 既定の設定は **ない**します。</li><li>**renewauthinterval = `<seconds>` **- `config renewauth` が **[はい]** に設定されている場合にクライアントが強制的に再認証されるまでの経過秒数を指定します。 既定値は**600 秒**です。</li><li>**dircache = `<size>` **-ディレクトリキャッシュのサイズを kb 単位で指定します。 として指定した数値 サイズ 4 と 128 の 4 の倍数である必要があります。 既定のディレクトリキャッシュサイズは**128 KB**です。</li><li>**translationfile = `<file>` **-Windows から UNIX ベースのファイルシステムに移動するときに、ファイル名の文字を置き換えるマッピング情報を含むファイルを指定します。 場合 ファイル が指定されていない、ファイル名の文字変換が無効にします。 場合の値 **translationfile** が変更されると、変更が有効にするためにサーバーを再起動する必要があります。</li><li>**dotfileshidden = `{yes|no}` **-ピリオド (.) で始まる名前を持つファイルを Windows ファイルシステムで非表示としてマークし、その結果、NFS クライアントから非表示にするかどうかを指定します。 既定の設定は **ない**します。</li><li>**casesensitivelookups = `{yes|no}` **-ディレクトリ参照が大文字小文字を区別するかどうかを指定します。<p>大文字と小文字を区別するファイル名をサポートするために、Windows カーネルの大文字と小文字の区別を無効にする必要もあります。 大文字と小文字の区別をサポートするには、レジストリキーの**DWord**値を `HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\kernel` **0**に変更します。</li><li>**ntfscase = `{lower|upper|preserve}` **-NTFS ファイルシステム内のファイルの名前の大文字と小文字の区別を、小文字、大文字、またはディレクトリに格納されている形式で返すかどうかを指定します。 既定の設定は **保持**します。 **Casesensitivelookups**が**yes**に設定されている場合、この設定を変更することはできません。</li></ul> |
| creategroup`<name>` | 指定したこと、新しいクライアント グループを作成 名前します。 |
| listgroups | すべてのクライアント グループの名前を表示します。 |
| deletegroup`<name>` | 指定されたクライアント グループを削除 名前します。 |
| renamegroup `<oldname>``<newname>` | *Oldname*によって指定されたクライアントグループの名前を*newname*に変更します。 |
| addmembers`<hostname>[...]` | *名前*で指定されたクライアントグループに*ホスト*を追加します。 |
| listmembers`<name>` | *名前*で指定されたクライアントグループ内のホストコンピューターの一覧を表示します。 |
| deletemembers`<hostname><groupname>[...]` | *グループ*によって指定されたクライアントグループから、*ホスト*によって指定されたクライアントを削除します。 |

### <a name="client-for-nfs-related-parameters"></a>NFS クライアントに関連するパラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| start | NFS サービスのクライアントを起動します。 |
| stop | NFS サービスのクライアントを停止します。 |
| config | NFS クライアントの全般設定を指定します。 少なくとも 1 つの使用は、次のオプションを指定する必要があります、 **config** コマンドの引数。<ul><li>**fileaccess = `<mode>` **-ネットワークファイルシステム (NFS) サーバー上に作成されるファイルの既定のアクセス許可モードを指定します。 **Mode**引数は、0 ~ 7 の3桁の数字で構成されます。これは、ユーザー、グループ、および他のユーザーに付与された既定のアクセス許可を表します。 これらの数字は、UNIX 形式の権限に変換されます。 *0 = なし*、 *1 = x (execute)*、 *2 = w (書き込み専用)*、 *3 = wx (書き込みと実行)*、 *4 = r (読み取り専用)*、 *5 = rx (読み取りおよび実行)*、 *6 = rw (読み取りと書き込み)*、 *7 = rwx (読み取り、書き込み、実行)* たとえば、は、 `fileaccess=750` 所有者に読み取り、書き込み、実行のアクセス許可を与え、そのグループに対する読み取りと実行のアクセス許可を付与し、他のユーザーに対するアクセス許可を付与しません。</li><li>**mapsvr = `<server>` **-NFS クライアントのユーザー名マッピングサーバーとしてサーバーを設定します。 使用する必要がありますが、このオプションは引き続き以前のバージョンと互換性のためにサポートされる、 sfuadmin ユーティリティ代わりにします。</li><li>**mtype = `{hard|soft}` **-既定のマウントの種類を指定します。 ハード マウントは、NFS クライアントは、成功するまで、失敗した RPC を再試行を続けます。 ソフト マウントの NFS クライアントをエラーを返した呼び出しを再試行した後は、呼び出し元のアプリケーションによって指定された時間数、 再試行 オプション。</li><li>**再試行 = `<number>` **-ソフトマウントの接続を試行する回数を指定します。 この値は、10、包括的に 1 の間でなければなりません。 既定値は **1**です。</li><li>**タイムアウト = `<seconds>` **-接続 (リモートプロシージャコール) を待機する秒数を指定します。 この値は、 *0.8*、 *0.9*、または*1 ~ 60*の整数である必要があります。 既定値は**0.8**です。</li><li>**protocol = `{TCP|UDP|TCP+UDP}` **-クライアントがサポートするトランスポートプロトコルを指定します。 既定の設定は、 **TCP + UDP**です。</li><li>全 **: `<size>` **-読み取りバッファーのサイズを kb 単位で指定します。 この値には、 *0.5、1、2、4、8、16、* または*32*を指定できます。 既定値は**32**です。</li><li>**wsize = `<size>` **-書き込みバッファーのサイズ (kb 単位) を指定します。 この値には、 *0.5、1、2、4、8、16、* または*32*を指定できます。 既定値は**32**です。</li><li>**perf = 既定**-次のパフォーマンス設定を既定値、 *mtype*、*再試行*、*タイムアウト*、元に*戻す、また*は*wsize*に復元します。 |

### <a name="examples"></a>例

NFS サーバーまたは NFS クライアントを停止するには、次のように入力します。

```
nfsadmin server stop
nfsadmin client stop
```

NFS サーバーまたは NFS クライアントを起動するには、次のように入力します。

```
nfsadmin server start
nfsadmin client start
```

NFS サーバーが大文字と小文字を区別しないように設定するには、次のように入力します。

```
nfsadmin server config casesensitive=no
```

NFS クライアントを大文字小文字を区別するように設定するには、次のように入力します。

```
nfsadmin client config casesensitive=yes
```

NFS 用の現在のサーバーまたは NFS クライアントのオプションをすべて表示するには、次のように入力します。

```
nfsadmin server config
nfsadmin client config
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [NFS コマンドレットリファレンス](https://docs.microsoft.com/powershell/module/nfs)
