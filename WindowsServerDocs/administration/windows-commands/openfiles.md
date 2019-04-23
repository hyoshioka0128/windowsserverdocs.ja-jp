---
title: openfiles
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c3be561d-a11f-4bf1-9835-8e4e96fe98ec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 83175d8529d9204c6b6d969a3db2aee2775bd0c4
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852383"
---
# <a name="openfiles"></a>openfiles



管理者を照会、表示、またはファイルとシステムで開かれているディレクトリの接続を切断できます。 有効またはシステムの管理オブジェクト リストのグローバル フラグを無効にします。

このトピックには、次のコマンドに関する情報が含まれます。
-   [openfiles/disconnect](#BKMK_disconnect)
-   [openfiles/query](#BKMK_query)
-   [openfiles/local](#BKMK_local)

## <a name="BKMK_disconnect"></a>openfiles/disconnect

管理者は、ファイルとフォルダーの共有フォルダーをリモートで開かれた接続を切断できます。

### <a name="syntax"></a>構文

```
openfiles /disconnect [/s <System> [/u [<Domain>\]<UserName> [/p [<Password>]]]] {[/id <OpenFileID>] | [/a <AccessedBy>] | [/o {read | write | read/write}]} [/op <OpenFile>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/s\<システム >|名前または IP アドレス) に接続するリモート システムを指定します。 円記号を使用しないでください。 使用しない場合、 **/s** オプション、コマンドが既定でローカル コンピューターで実行します。 このパラメーターは、すべてのファイルと、コマンドで指定されているフォルダーに適用されます。|
|/u [\<ドメイン >\]<UserName>|指定したユーザー アカウントのアクセス許可を使用してコマンドを実行します。 使用しない場合、 **/u** オプション、アクセス許可が既定で使用されるシステムです。|
|/p [\<パスワード >]|指定されているユーザー アカウントのパスワードを指定します、 **/u** オプション。 使用しない場合、 **/p** オプション、コマンドの実行時にパスワードの入力が表示されます。|
|/id \<OpenFileID>|指定したファイルの ID で開いているファイルの接続が切断します。 ワイルドカード文字 (**&#42;**) このパラメーターで使用できます。</br>注:使用することができます、 **openfiles/query**ファイル ID を検索するコマンド|
|/a\<イテレータ >|指定されているユーザー名に関連付けられた開いているすべてのファイルの接続が切断、 *イテレータ* パラメーター。 ワイルドカード文字 (**&#42;**) このパラメーターで使用できます。|
|/o {読み取り\|書き込み\|読み取り/書き込み}|Open モードを指定した値を持つすべての開いているファイルを切断します。 有効な値は、読み取り、書き込み、または読み取り/書き込みです。 ワイルドカード文字 (**&#42;**) このパラメーターで使用できます。|
|/op \<OpenFile >|特定の開いているファイル名で作成されたすべての開いているファイル接続を切断します。 ワイルドカード文字 (**&#42;**) このパラメーターで使用できます。|
|/?|コマンド プロンプトにヘルプを表示します。|

### <a name="examples"></a>例

ファイル ID 26843578 で開いているすべてのファイルを切断するには次のように入力します。
```
openfiles /disconnect /id 26843578
```
すべての開いているファイルとディレクトリを"hiropln"のユーザーがアクセスを切断するには次のように入力します。
```
openfiles /disconnect /a hiropln
```
すべての開いているファイルと読み取り/書き込みモードでのディレクトリを切断するには次のように入力します。
```
openfiles /disconnect /o read/write
```
開いているファイル名とディレクトリを切断するには"C:\TestShare\"ユーザーがアクセスしてその型に関係なく、します。
```
openfiles /disconnect /a * /op "c:\testshare\"
```
その ID に関係なく"hiropln、"ユーザーがアクセスされている"srvmain"のリモート コンピューター上のすべての開いているファイルを切断するには次のように入力します。
```
openfiles /disconnect /s srvmain /u maindom\hiropln /id *
```

## <a name="BKMK_query"></a>openfiles/query

クエリを実行し、すべての開いているファイルを表示します。

### <a name="syntax"></a>構文

```
openfiles /query [/s <System> [/u [<Domain>\]<UserName> [/p [<Password>]]]] [/fo {TABLE | LIST | CSV}] [/nh] [/v]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/s\<システム >|名前または IP アドレス) に接続するリモート システムを指定します。 円記号を使用しないでください。 使用しない場合、 **/s** オプション、コマンドが既定でローカル コンピューターで実行します。 このパラメーターは、すべてのファイルと、コマンドで指定されているフォルダーに適用されます。|
|/u [\<ドメイン >\]<UserName>|指定したユーザー アカウントのアクセス許可を使用してコマンドを実行します。 使用しない場合、 **/u** オプション、アクセス許可が既定で使用されるシステムです。|
|/p [\<パスワード >]|指定されているユーザー アカウントのパスワードを指定します、 **/u** オプション。 使用しない場合、 **/p** オプション、コマンドの実行時にパスワードの入力が表示されます。|
|[/fo {テーブル\|一覧\|CSV}]|指定した形式で出力が表示されます。 有効な値 *形式* は。</br>テーブル:出力テーブルを表示します。</br>一覧:出力一覧を表示します。</br>CSV:コンマ区切り値形式で出力を表示します。|
|/nh|出力に列ヘッダーを抑制します。 有効な場合にのみ、 **/fo** にパラメーターが設定されている **テーブル** または **CSV**します。|
|/v|詳細な情報が出力に表示されることを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

### <a name="examples"></a>例

クエリを開いているすべてのファイルの表示は、次のように入力します。
```
openfiles /query
```
ヘッダーのないテーブル形式で開いているすべてのファイルを表示し、次のように入力します。
```
openfiles /query /fo table /nh
```
照会し、詳細な情報を一覧形式で開いているすべてのファイルを表示、次のように入力します。
```
openfiles /query /fo list /v
```
"Hiropln"、"maindom"ドメイン上のユーザーの資格情報を使用して、"srvmain"のリモート システム上のすべての開いているファイルを表示し、次のように入力します。
```
openfiles /query /s srvmain /u maindom\hiropln /p p@ssW23
```

> [!NOTE]
> この例では、コマンドラインでパスワードを指定します。 パスワードを表示するには、除外、 **/p** オプション。 画面にエコーされませんが、パスワードの入力するように求められます。

## <a name="BKMK_local"></a>openfiles/local

有効またはシステムの管理オブジェクト リストのグローバル フラグを無効にします。 パラメーターを指定せずに使用する場合 **openfiles/local** 管理オブジェクトのリスト、グローバル フラグの現在の状態を表示します。

### <a name="syntax"></a>構文

```
openfiles /local [on | off]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[\|オフ]|有効またはシステムのローカルのファイル ハンドルを追跡管理オブジェクト リスト グローバル フラグを無効にします。|
|/?|コマンド プロンプトにヘルプを表示します。|

### <a name="remarks"></a>注釈

-   管理オブジェクト リストのグローバル フラグを有効にするシステムを速度の遅い可能性があります。
-   使用して行われた変更、 **に** または **オフ** システムを再起動するまでオプションは有効になりません。

### <a name="examples"></a>例

管理オブジェクトのリスト、グローバル フラグの現在の状態を確認するには、次のように入力します。
```
openfiles /local
```
既定では、管理オブジェクト リストのグローバル フラグが無効にし、次の出力が表示されます。
```
INFO: The system global flag 'maintain objects list' is currently disabled.
```
管理オブジェクト リストのグローバル フラグを有効にするには、次のように入力します。
```
openfiles /local on
```
グローバル フラグが有効にすると、次のメッセージが表示されます。
```
SUCCESS: The system global flag 'maintain objects list' is enabled.
         This will take effect after the system is restarted.
```
管理オブジェクト リストのグローバル フラグを無効にするには、次のように入力します。
```
openfiles /local off
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)