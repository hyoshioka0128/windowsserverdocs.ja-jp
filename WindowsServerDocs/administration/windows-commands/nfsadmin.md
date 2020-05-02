---
title: nfsadmin
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 7375b2cf-c6b8-45b5-abf6-6c10e462defd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c8020b028a046ead36b5f95604cd81d679861746
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723773"
---
# <a name="nfsadmin"></a>nfsadmin

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

使用する **nfsadmin** NFS および NFS クライアントのサーバーを管理します。  
  
## <a name="syntax"></a>構文  
**nfsadmin server** `[` *computerName*`] [``[``]]` *UserName* \-u UserName\-p*パスワード*l\-  
  
**nfsadmin server** `[` *computerName*`] [` \- `{` *client* *Password* `|` *UserName* `]]` u UserName `[`p パスワード\-r クライアントすべて\-`}`  
  
**nfsadmin server** `[` *computerName*`] [` \- `|` *UserName* `]] {`u UserName `[`p*パスワード*の開始\-の停止`}`  
  
**nfsadmin server** `[` *computerName*`] [` `[``]]` *Option* *Password* *UserName* u UserName \-p パスワード構成オプション\-`[...]`  
  
**nfsadmin server** `[` *computerName*`] [` `[``]]` *Name* *Password* *UserName* u UserName \-p パスワード creategroup 名\-  
  
**nfsadmin server** `[` *computerName*`] [` `[``]]` *UserName* u UserName \-p*パスワード*listgroups パラメータ\-  
  
**nfsadmin server** `[` *computerName*`] [` `[``]]` *Name* *Password* *UserName* u UserName \-p パスワード deletegroup 名\-  
  
**nfsadmin server** `[` *computerName*`] [` `[` *Password* *UserName* `]]` *OldName NewName* u UserName \-p パスワード renamegroup OldName NewName\-  
  
**nfsadmin server** `[` *computerName*`] [` `[` *Password* *UserName* `]]` *Name Host* u UserName \-p パスワード addmembers 名前ホスト\-`[...]`  
  
**nfsadmin server** `[` *computerName*`] [` `[``]]` *UserName* u UserName \-p*パスワード*listmembers\-  
  
**nfsadmin server** `[` *computerName*`] [` `[` *Password* *UserName* `]]` *Group Host* u UserName \-p パスワード deletemembers Group Host\-`[...]`  
  
**nfsadmin client** `[` *computerName*`] [` \- `|` *UserName* `]] {`u UserName `[`p*パスワード*の開始\-の停止`}`  
  
**nfsadmin client** `[` *computerName*`] [` `[``]]` *Option* *Password* *UserName* u UserName \-p パスワード config オプション\-`[...]`  
  
## <a name="description"></a>[説明]  
**Nfsadmin** コマンド\-ライン ユーティリティは、Microsoft Services for Network File System を実行しているローカルまたはリモート コンピューターに NFS クライアントや NFS サーバーを管理 \(NFS\)します。 必要な権限がないアカウントでログオンしている場合は、ユーザー名とは、アカウントのパスワードを指定できます。 によって実行されるアクション **nfsadmin** を指定するコマンド引数に依存します。  
  
サービスに加えて\-固有のコマンド引数とオプション、 **nfsadmin** 次を受け入れます。  
  
*コンピューター名*  
管理するリモート コンピューターを指定します。 Windows インターネット ネーム サービスを使用しているコンピューターを指定することができます \(WINS\) 名またはドメイン ネーム システム \(DNS\) 名、またはインターネット プロトコルによって \(IP\) アドレス。  
  
u ユーザー*名* ** \-**  
使用する資格情報を持つユーザーのユーザー名を指定します。 ドメイン**\\**<em>ユーザー</em>名<em>の形式で</em>ユーザー名にドメイン名を追加する必要がある場合があります。  
  
*Password* ** \-p**パスワード  
U オプションを使用して指定したユーザーのパスワードを指定します。 ** \-** U オプションを指定しても** \-p**オプションを省略した場合は、ユーザーのパスワードの入力を求められます。 ** \-**  
  
#### <a name="administering-server-for-nfs"></a>Nfs サーバーを管理します。  
使用して、 **nfsadmin server** nfs サーバーを管理するコマンドです。 特定のアクションを **nfsadmin server** はコマンドのオプションは、指定した引数に依存します。  
  
**\-l**  
クライアントによって保持されているすべてのロックを一覧表示します。  
  
r {*クライアント* | **すべて**} ** \-**  
保持するロックの解放、 *クライアント* または、 **すべて** すべてのクライアントで指定しました。  
  
**start**  
NFS サーバーサービスを開始します。  
  
**stop**  
サーバーの NFS サービスを停止します。  
  
**.config**  
Nfs サーバーの全般設定を指定します。 少なくとも 1 つの使用は、次のオプションを指定する必要があります、 **config** コマンドの引数。  
  
**mapsvr\=**<em>サーバー</em>  
セット *server* nfs サーバーのユーザー名マッピング サーバーとします。 使用する必要がありますが、このオプションは引き続き以前のバージョンと互換性のためにサポートされる、 **sfuadmin** ユーティリティ代わりにします。  
  
**auditlocation\=**{**eventlog** | **ファイル** | **両方** | **none**}  
イベントを監査するかどうかと、イベントの記録場所を指定します。 次の引数のいずれかが必要です。  
  
**ログ**  
だけで、イベント ビューアーのアプリケーション ログに監査イベントが記録されることを指定します。  
  
**拡張子**  
指定されたファイルだけに監査イベントが記録されることを示す **config fname**します。  
  
**両方とも**  
監査対象のイベントで指定されたファイルと同様に、イベント ビューアーのアプリケーション ログで記録されることを示す **config fname**します。  
  
"**なし**"  
イベントは監査されませんを指定します。  
  
**fname\=**<em>ファイル</em>  
指定されたファイルの設定 *ファイル* 監査ファイルとして。 既定値は %sfudir\\ログ\\nfssvr.log  
  
**fsize\=**\=*サイズ*  
セット *サイズ* メガバイト単位監査ファイルの最大サイズとして。 既定の最大サイズは、7 MB です。  
  
**監査\=** \] **create** **delete** **mount** **\-** **read** **all** **write** **locking**マウント読み取り書き込みの作成削除\[ロックをすべて**\+** 作成| \[ \] **\+** **\+** | **\-** \[ \] | **\-** \] \[ \] | **\-** \[ **\+** **\+** | **\+** **\-**\[**\+**|**\-** \[\] \] | **\-**  
ログに記録するイベントを指定します。 イベントのログ記録を開始するには、 \( **\+** \)イベント名の前にプラス記号を入力します。イベントのログ記録を停止するには、 \( **\-** \)イベント名の前にマイナス記号 (-) を入力します。 符号を省略すると、プラス記号が使われます。 使用しないで **すべて** に他の任意のイベントの名前。  
  
**lockperiod\=**<em>(秒)</em>  
NFS サーバーが nfs サーバーへの接続が失われたれて再確立された後、または、NFS サーバー サービスが再起動された後にロックを再要求を待機する秒数を指定します。  
  
Portmapprotocol\={TCP |UDP |TCP\+UDP  
Portmap をサポートするトランスポート プロトコルを指定します。 既定の設定は **TCP\+UDP**します。  
  
mountprotocol\={TCP |UDP |TCP\+UDP}  
トランスポートを指定のプロトコルがサポートをマウントします。 既定の設定は **TCP\+UDP**します。  
  
nfsprotocol\={TCP |UDP |TCP\+UDP}  
指定するトランスポート プロトコルの Network File System \(NFS\) をサポートしています。 既定の設定は**TCP\+UDP**です。  
  
nlmprotocol\={TCP |UDP |TCP\+UDP}  
指定するトランスポート プロトコルのネットワーク ロック マネージャー \(NLM\) をサポートしています。 既定の設定は **TCP\+UDP**します。  
  
nsmprotocol\={TCP |UDP |TCP\+UDP}  
指定するトランスポート プロトコルのネットワーク ステータス マネージャー \(NSM\) をサポートしています。 既定の設定は **TCP\+UDP**します。  
  
**enableV3\=**{**はい** | **ない**}  
NFS version 3 プロトコルをサポートするかどうかを指定します。 既定の設定は **[はい]** です。  
  
**renewauth\=**{**はい** | **ない**}  
クライアント接続がで指定された時間が経過したら再認証される必要があるかどうかを指定 **config renewauthinterval**します。 既定の設定は **ない**します。  
  
**renewauthinterval\=**<em>(秒)</em>  
場合に再認証されるクライアントが強制されるまでの経過秒数を指定 **config renewauth** に設定されている **はい**します。 既定値は 600 秒です。  
  
**dircache\=**<em>サイズ</em>  
ディレクトリ キャッシュのキロバイト単位のサイズを指定します。 として指定した数値 *サイズ* 4 と 128 の 4 の倍数である必要があります。 既定のディレクトリ\-キャッシュ サイズは 128 KB です。  
  
**translationfile**\=translationfile\[ファイル\]  
移動するときに Windows からのファイル名の文字を置換するためのマッピング情報を含むファイルを指定\-を UNIX ベース\-ベースのファイル システムです。 場合 *ファイル* が指定されていない、ファイル名の文字変換が無効にします。 場合の値 **translationfile** が変更されると、変更が有効にするためにサーバーを再起動する必要があります。  
  
**dotfileshidden**\={**yes** | **no**}  
名前をピリオド\(で始まるファイルを作成するかどうかを指定します。\) Windows ファイルシステムでは非表示としてマークされ、その結果、NFS クライアントでは非表示になります。 既定の設定は **ない**します。  
  
**casesensitivelookups\=**{**はい** | **ない**}  
ディレクトリ検索が大文字小文字を区別するかどうかを示す \(文字ケースの正確な一致を必要とする\)です。  
  
Windows カーネルのケースを無効にすることも必要\-ケースをサポートするために nfs サーバーの順序で小文字を区別しない\-機密性の高いファイルの名前。 Windows カーネルのケースを無効にすることができます\-を 0 には、次のレジストリ キーをオフにすると小文字を区別しません。  
  
HKLM\\システム\\CurrentControlSet\\コントロール\\セッション マネージャー\\カーネル  
  
DWOrd obcaseinsensitive   
  
> [!IMPORTANT]  
> このセクションでは、Windows Server 2008 R2、Windows Server 2008 および Windows Server 2003 にのみ適用されます。 このセクションでは、Windows Server 2012 R2 または Windows Server 2012 には適用されません。  
  
**ntfscase\=**{**低い** | **上** | **保持**}  
NTFS ファイル システム内のファイル名の文字の大文字と小文字が小文字、大文字、またはディレクトリに格納されている形式で返されるかどうかを指定します。 既定の設定は **保持**します。 場合、この設定は変更できません **casesensitivelookups** に設定されている **はい**します。  
  
**creategroup** *名*  
新しいクライアントグループを作成し、指定した*名前を付け*ます。  
  
**listgroups パラメータ**  
すべてのクライアント グループの名前を表示します。  
  
**deletegroup** *名*  
*名前*で指定したクライアントグループを削除します。  
  
**renamegroup** *OldName NewName*  
*OldName*によって指定されたクライアントグループの名前を*NewName*に変更します。  
  
**addmembers** *名前のホスト*\[...\]  
*名前*で指定されたクライアントグループに*ホスト*を追加します。  
  
**listmembers** *名*  
*名前*で指定されたクライアントグループ内のホストコンピューターの一覧を表示します。  
  
**deletemembers** *グループホスト*\[...\]  
*グループ*によって指定されたクライアントグループから、*ホスト*によって指定されたクライアントを削除します。  
  
コマンドオプションまたは引数を指定しない場合、 **nfsadmin server**では、NFS 構成設定の現在のサーバーが表示されます。  
  
#### <a name="administering-client-for-nfs"></a>NFS クライアントを管理します。  
使用して、 **nfsadmin client** NFS クライアントを管理するコマンドです。 特定のアクションを **nfsadmin client** は指定するコマンド引数によって異なります。  
  
**start**  
NFS クライアントサービスを開始します。  
  
**stop**  
NFS サービスのクライアントを停止します。  
  
**.config**  
NFS クライアントの全般設定を指定します。 少なくとも 1 つの使用は、次のオプションを指定する必要があります、 **config** コマンドの引数。  
  
**fileaccess\=**<em>モード</em>  
-   ネットワーク ファイル システムに作成されるファイルの既定のアクセス許可モードを指定 \(NFS\) サーバーです。 *モード* 引数は、0 から 7 への 3 桁で構成されます \(包括的な\) ユーザー、グループ、およびその他のユーザーに与える既定のアクセス許可を表す \(それぞれ\)します。 UNIX を数字に変換\-アクセス許可を次のようにスタイル: 0\=なし、1\=2 x\=w 3\=wx 4\=r、5\=rx、6\=rw、7 と\=rwx します。 たとえば、 **fileaccess\=750** 利用 rwx のアクセス許可の所有者に、rx アクセス許可、グループ、および他のユーザーへのアクセス権限がありません。  
  
**mapsvr\=**<em>サーバー</em>  
セット *server* NFS 用のクライアントのユーザー名マッピング サーバーとします。 使用する必要がありますが、このオプションは引き続き以前のバージョンと互換性のためにサポートされる、 **sfuadmin** ユーティリティ代わりにします。  
  
**mtype\=**{**ハード** | **ソフト**}  
既定のマウントの種類を指定します。 ハード マウントは、NFS クライアントは、成功するまで、失敗した RPC を再試行を続けます。 ソフト マウントの NFS クライアントをエラーを返した呼び出しを再試行した後は、呼び出し元のアプリケーションによって指定された時間数、 **再試行** オプション。  
  
**再試行\=**<em>数</em>  
ソフト マウントの接続を確立しようとする回数を指定します。 この値は、10、包括的に 1 の間でなければなりません。 既定値は 1 です。  
  
**タイムアウト\=**<em>(秒)</em>  
接続を待機する秒数を指定 \(リモート プロシージャ コール\)します。 この値は、0.8、0.9、または 60、包括的には、1 から整数にする必要があります。 既定値は 0.8 です。  
  
**プロトコル\={TCP |UDP |TCP\+UDP}**  
トランスポート プロトコルのサポートを指定します。 既定の設定は**TCP\+UDP**です。  
  
**rsize\=**<em>サイズ</em>  
読み取りバッファーのサイズを指定します。 この値は、0.5、1、2、4、8、16、または 32 を指定できます。 既定値は 32 です。  
  
**wsize\=**<em>サイズ</em>  
書き込みバッファーのサイズを指定します。 この値は、0.5、1、2、4、8、16、または 32 を指定できます。 既定値は 32 です。  
  
**perf\=の既定値**  
既定値に、次のパフォーマンス設定が復元されます。  
  
-   **mtype**  
  
-   **再試行**  
  
-   **timeout**  
  
-   **rsize**  
  
-   **wsize**  
  
**fileaccess\=**<em>モード</em>  
ネットワーク ファイル システムに作成されるファイルの既定のアクセス許可モードを指定 \(NFS\) サーバーです。 *モード* 引数は、0 から 7 への 3 桁で構成されます \(包括的な\) ユーザー、グループ、およびその他のユーザーに与える既定のアクセス許可を表す \(それぞれ\)します。 UNIX を数字に変換\-アクセス許可を次のようにスタイル: 0\=なし、1\=2 x\=w 3\=wx 4\=r、5\=rx、6\=rw、7 と\=rwx します。 たとえば、 **fileaccess\=750** 利用 rwx のアクセス許可の所有者に、rx アクセス許可、グループ、および他のユーザーへのアクセス権限がありません。  
  
コマンドオプションまたは引数を指定しない場合、 **nfsadmin client**では、NFS 構成設定の現在のクライアントが表示されます。  
  

