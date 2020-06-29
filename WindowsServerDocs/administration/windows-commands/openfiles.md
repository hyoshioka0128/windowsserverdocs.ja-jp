---
title: openfiles
description: Openfiles コマンドのリファレンストピック。管理者は、システムで開かれているファイルおよびディレクトリのクエリ、表示、または切断を行うことができます。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c3be561d-a11f-4bf1-9835-8e4e96fe98ec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e55dd88052f1bbfdebb02d1fb6d6f48261643c5c
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472598"
---
# <a name="openfiles"></a>openfiles

管理者を照会、表示、またはファイルとシステムで開かれているディレクトリの接続を切断できます。 また、このコマンドは、システム**管理オブジェクトリスト**のグローバルフラグを有効または無効にします。

## <a name="openfiles-disconnect"></a>openfiles/disconnect

管理者は、ファイルとフォルダーの共有フォルダーをリモートで開かれた接続を切断できます。

### <a name="syntax"></a>構文

```
openfiles /disconnect [/s <system> [/u [<domain>\]<username> [/p [<password>]]]] {[/id <openfileID>] | [/a <accessedby>] | [/o {read | write | read/write}]} [/op <openfile>]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| /s`<system>` | 名前または IP アドレス) に接続するリモート システムを指定します。 バックスラッシュは使用しないでください。 **/S**オプションを使用しない場合、コマンドは既定でローカルコンピューター上で実行されます。 このパラメーターは、すべてのファイルと、コマンドで指定されているフォルダーに適用されます。 |
| /u`[<domain>\]<username>` | 指定されたユーザーアカウントのアクセス許可を使用してコマンドを実行します。 **/U**オプションを使用しない場合は、既定でシステム権限が使用されます。 |
| /p`[<password>]` | 指定されているユーザー アカウントのパスワードを指定します、 **/u** オプション。 **/P**オプションを使用しない場合、コマンドの実行時にパスワードの入力を求めるメッセージが表示されます。 |
| /id`<openfileID>` | 指定したファイルの ID で開いているファイルの接続が切断します。 このパラメーターには、ワイルドカード文字 (**&#42;**) を使用できます。<p>注: を使えば、 **openfiles/query** ファイル ID を検索するコマンド |
| /a`<accessedby>` | *イテレータ*パラメーターで指定したユーザー名に関連付けられているすべての開いているファイルを切断します。 このパラメーターには、ワイルドカード文字 (**&#42;**) を使用できます。 |
| /o`{read | write | read/write}` | 指定されたオープンモード値を使用して、開いているすべてのファイルを切断します。 有効な値は、**読み取り**、**書き込み**、または**読み取り/書き込み**です。 このパラメーターには、ワイルドカード文字 (**&#42;**) を使用できます。 |
| /op`<openfile>` | 特定の開いているファイル名で作成されたすべての開いているファイル接続を切断します。 このパラメーターには、ワイルドカード文字 (**&#42;**) を使用できます。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

### <a name="examples"></a>例

*ファイル ID 26843578*の開いているファイルをすべて切断するには、次のように入力します。

```
openfiles /disconnect /id 26843578
```

ユーザー *hiropln*がアクセスするすべての開いているファイルとディレクトリを切断するには、次のように入力します。

```
openfiles /disconnect /a hiropln
```

開いているすべてのファイルとディレクトリを*読み取り/書き込みモード*で切断するには、次のように入力します。

```
openfiles /disconnect /o read/write
```

アクセスしているユーザーに関係なく、開いているファイル名 * C:\testshare のディレクトリを切断するには \* 、次のように入力します。

```
openfiles /disconnect /a * /op c:\testshare\
```

ユーザー *hiropln*によってアクセスされているリモートコンピューター *srvmain*上の開いているすべてのファイルを切断するには、次のように入力します。

```
openfiles /disconnect /s srvmain /u maindom\hiropln /id *
```

## <a name="openfiles-query"></a>openfiles/query

クエリを実行し、すべての開いているファイルを表示します。

### <a name="syntax"></a>構文

```
openfiles /query [/s <system> [/u [<domain>\]<username> [/p [<password>]]]] [/fo {TABLE | LIST | CSV}] [/nh] [/v]
```

#### <a name="parameters"></a>パラメーター


| パラメーター | 説明 |
|--|--|
| /s`<system>` | 名前または IP アドレス) に接続するリモート システムを指定します。 バックスラッシュは使用しないでください。 **/S**オプションを使用しない場合、コマンドは既定でローカルコンピューター上で実行されます。 このパラメーターは、すべてのファイルと、コマンドで指定されているフォルダーに適用されます。 |
| /u`[<domain>\]<username>` | 指定されたユーザーアカウントのアクセス許可を使用してコマンドを実行します。 **/U**オプションを使用しない場合は、既定でシステム権限が使用されます。 |
| /p`[<password>]` | 指定されているユーザー アカウントのパスワードを指定します、 **/u** オプション。 **/P**オプションを使用しない場合、コマンドの実行時にパスワードの入力を求めるメッセージが表示されます。 |
| [/fo `{TABLE | LIST | CSV}` ] | 指定した形式で出力が表示されます。 有効な値は、次のとおりです。<ul><li>**テーブル**-出力をテーブルに表示します。</li><li>**リスト**-出力を一覧に表示します。</li><li>**Csv** -コンマ区切り値 (csv) 形式で出力を表示します。</li></ul> |
| /nh | 出力に列ヘッダーを抑制します。 有効な場合にのみ、 **/fo** にパラメーターが設定されている **テーブル** または **CSV**します。 |
| /v | 詳細 (詳細) 情報を出力に表示することを指定します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

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

*Maindom*ドメインのユーザー *hiropln*の資格情報を使用して、リモートシステム*srvmain*で開いているすべてのファイルを照会して表示するには、次のように入力します。

```
openfiles /query /s srvmain /u maindom\hiropln /p p@ssW23
```

> [!NOTE]
> この例では、コマンドラインでパスワードを指定します。 パスワードを表示するには、除外、 **/p** オプション。 画面にエコーされないパスワードを入力するように求められます。

## <a name="openfiles-local"></a>openfiles/local

システム**管理オブジェクトリスト**のグローバルフラグを有効または無効にします。 パラメーターを指定せずに使用する場合**は、[** オブジェクトの**管理] リスト**のグローバルフラグの現在の状態を表示します。

> [!NOTE]
> On または**off**オプションを使用して行われた変更は、システムを再起動するまで有効**に**なりません。 [**オブジェクトの管理] リスト**のグローバルフラグを有効にすると、システムの速度が低下する可能性があります。

### <a name="syntax"></a>構文

```
openfiles /local [on | off]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| `[on | off]` | ローカルファイルハンドルを追跡する、システム**管理オブジェクトリスト**のグローバルフラグを有効または無効にします。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

### <a name="examples"></a>例

[**オブジェクトの管理] リスト**のグローバルフラグの現在の状態を確認するには、次のように入力します。

```
openfiles /local
```

既定では、[**オブジェクトの管理] リスト**のグローバルフラグは無効になっており、次のメッセージが表示されます。`INFO: The system global flag 'maintain objects list' is currently disabled.`

[オブジェクトの**管理] リスト**のグローバルフラグを有効にするには、次のように入力します。

```
openfiles /local on
```

グローバルフラグが有効になっていると、次のメッセージが表示されます。`SUCCESS: The system global flag 'maintain objects list' is enabled. This will take effect after the system is restarted.`

[オブジェクトの**管理] リスト**のグローバルフラグを無効にするには、次のように入力します。

```
openfiles /local off
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
