---
title: macfile
description: Macintosh サーバー、ボリューム、ディレクトリ、およびファイルのファイルサーバーを管理する、macfile コマンドのリファレンス記事です。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e2ce586c-b316-41d3-90f8-4be0d074cc0e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6937e8bbf40ec9ce908be095e5de0e04f793f40e
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85933657"
---
# <a name="macfile"></a>macfile

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Macintosh サーバー、ボリューム、ディレクトリ、およびファイルのファイル サーバーを管理します。 バッチ ファイルで、一連のコマンドをなどによって手動で開始する管理タスクを自動化できるか、事前に定義した時刻。

## <a name="modify-directories-in-macintosh-accessible-volumes"></a>Macintosh からアクセス可能なボリューム内のディレクトリを変更する

Macintosh からアクセス可能なボリュームのディレクトリ名、場所、所有者、グループ、アクセス許可を変更します。

### <a name="syntax"></a>構文

```
macfile directory[/server:\\<computername>] /path:<directory> [/owner:<ownername>] [/group:<groupname>] [/permissions:<permissions>]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| /server:`\\<computername>` | ディレクトリを変更するサーバーを指定します。 省略した場合は、操作は、ローカル コンピューターで実行されます。 |
| /path`<directory>` | 変更するディレクトリへのパスを指定します。 このパラメーターは必須です。 **注:** ディレクトリが存在している必要があります。 **macfile ディレクトリ**を使用してもディレクトリは作成されません。 |
| /owner`<ownername>` | ディレクトリの所有者を変更します。 省略した場合、所有者名は変更されません。 |
| グループ`<groupname>` | ディレクトリに関連付けられている Macintosh プライマリグループを指定または変更します。 省略した場合は、プライマリ グループは変更されません。 |
| 許可`<permissions>` | 所有者、プライマリグループ、および世界 (すべてのユーザー) のディレクトリに対するアクセス許可を設定します。 この値は11桁の数字にする必要があります。この場合、番号1はアクセス許可を付与し、0は権限を取り消します (たとえば、11111011000)。 このパラメーターを省略した場合、アクセス許可は変更されません。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

##### <a name="position-of-permissions-digit"></a>アクセス許可の数字の位置

アクセス許可の数字の位置によって、次のように設定されるアクセス許可が決まります。

| 位置 | アクセス許可の設定 |
| -------- | --------------- |
| First | OwnerSeeFiles |
| Second | OwnerSeeFolders |
| 第 3 週 | OwnerMakechanges |
| 4 番目 | GroupSeeFiles |
| 第 5 | GroupSeeFolders |
| 第 6 | GroupMakechanges |
| 第 7 | WorldSeeFiles |
| 第 8 | WorldSeeFolders |
| 9 番目 | WorldMakechanges |
| 第 10 | ディレクトリの名前変更、移動、または削除を行うことはできません。 |
| 11 番目 | 変更は、現在のディレクトリとすべてのサブディレクトリに適用されます。 |

##### <a name="remarks"></a>注釈

- 入力した情報にスペースや特殊文字が含まれている場合は、テキストを引用符で囲みます (" `<computer name>` " など)。

- **Macfile ディレクトリ**を使用して、macintosh ユーザーが macintosh アクセス可能なボリューム内の既存のディレクトリを使用できるようにします。 **Macfile ディレクトリ**コマンドでは、ディレクトリは作成されません。

- ファイル マネージャーでは、コマンド プロンプトを使用して、または **macintosh の新しいフォルダー** を使用する前に、Macintosh からアクセス可能なボリュームにディレクトリを作成するコマンド、 **macfile ディレクトリ** コマンドです。

#### <a name="examples"></a>例

[*ファイルの参照*] を割り当てるには、 *「フォルダー*」を参照し、所有者に*変更*のアクセス許可を設定して、[*フォルダー*のアクセス許可] を他のすべてのユーザーに設定し、ディレクトリの名前変更、移動、または削除を回避するには、次のように入力します。

```
macfile directory /path:e:\statistics\may sales /permissions:11111011000
```

サブディレクトリが、Macintosh からアクセス可能なボリュームの*統計情報*(E:\) にある*Sales の可能性があり*ます。ローカルサーバーのドライブ。

## <a name="join-a-macintosh-files-data-and-resource-forks"></a>Macintosh ファイルのデータとリソースフォークの結合

ファイルを作成するサーバー、ファイルを作成したユーザー、ファイルの種類、データフォークが配置されている場所、リソースフォークの場所、および出力ファイルの場所を指定します。

### <a name="syntax"></a>構文

```
macfile forkize[/server:\\<computername>] [/creator:<creatorname>] [/type:<typename>]  [/datafork:<filepath>] [/resourcefork:<filepath>] /targetfile:<filepath>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| /server:`\\<computername>` | ファイルを結合するサーバーを指定します。 省略した場合は、操作は、ローカル コンピューターで実行されます。 |
| ファ`<creatorname>` | ファイルの作成者を指定します。 Macintosh finder は、 **/creator**コマンドラインオプションを使用して、ファイルを作成したアプリケーションを特定します。 |
| /type`<typename>` | ファイルの種類を指定します。 Macintosh finder は、 **/type**コマンドラインオプションを使用して、ファイルを作成したアプリケーション内のファイルの種類を確認します。 |
| /datafork:`<filepath>` | 結合するデータ フォークの場所を指定します。 リモート パスを指定できます。 |
| /resourcefork:`<filepath>` | 参加しているリソース フォークの場所を指定します。 リモート パスを指定できます。 |
| targetfile`<filepath>` | データフォークとリソースフォークを結合することによって作成されるファイルの場所を指定します。または、変更する型またはクリエーターを含むファイルの場所を指定します。 ファイルは、指定されたサーバー上に存在する必要があります。 このパラメーターは必須です。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

##### <a name="remarks"></a>注釈

- 入力した情報にスペースや特殊文字が含まれている場合は、テキストを引用符で囲みます (" `<computer name>` " など)。

#### <a name="examples"></a>例

リソースフォーク D:\Release を使用して、Macintosh からアクセス可能なボリューム*D:\Release*に*tree_app*ファイルを*作成し、* その新しいファイルが macintosh クライアントにアプリケーションとして表示されるようにするには (macintosh アプリケーションでは*appl.exe*を使用します)、creator (署名) を*アプリ*に設定し、次のように入力します。

```
macfile forkize /resourcefork:c:\cross\mac\appcode /type:APPL /creator:MAGNOLIA /targetfile:D:\Release\tree_app
```

ファイルの作成者を*Microsoft Word 5.1*に変更するには、 *D:\Word documents\Group files*ディレクトリにあるファイル*Word.txt*のサーバー * \\ ServerA*で、次のように入力します。

```
macfile forkize /server:\\ServerA /creator:MSWD /type:TEXT /targetfile:d:\Word documents\Group files\Word.txt
```

## <a name="change-the-sign-in-message-and-limit-sessions"></a>サインインメッセージを変更し、セッションを制限する

Macintosh サーバーのファイルサーバーにユーザーがサインインしたときに表示されるサインオンメッセージを変更し、Macintosh 用のファイルサーバーとプリントサーバーを同時に使用できるユーザーの数を制限します。

### <a name="syntax"></a>構文

```
macfile server [/server:\\<computername>] [/maxsessions:{number | unlimited}] [/loginmessage:<message>]
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- |------------ |
| /server:`\\<computername>` | パラメーターを変更するサーバーを指定します。 省略した場合は、操作は、ローカル コンピューターで実行されます。 |
| maxsessions`{number | unlimited}` | Macintosh 用のファイルおよびプリントサーバーを同時に使用できるユーザーの最大数を指定します。 省略した場合は、 **maxsessions** 設定、サーバーは変更されません。 |
| /loginmessage:`<message>` | Macintosh サーバーのファイルサーバーにサインインするときに、Macintosh ユーザーに表示されるメッセージを変更します。 サインインメッセージの最大文字数は199です。 省略した場合は、 **loginmessage** メッセージは、サーバーは変更されません。 既存のサインインメッセージを削除するには、 **/loginmessage**パラメーターを含めますが、 *message*変数は空白のままにします。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

##### <a name="remarks"></a>注釈

- 入力した情報にスペースや特殊文字が含まれている場合は、テキストを引用符で囲みます (" `<computer name>` " など)。

#### <a name="examples"></a>例

ローカルサーバー上の Macintosh セッションで許可されているファイルおよびプリントサーバーの数を5つのセッションに変更し、"完了したときに Server for Macintosh からサインアウトする" というメッセージを追加するには、次のように入力します。

```
macfile server /maxsessions:5 /loginmessage:Sign off from Server for Macintosh when you are finished
```

## <a name="add-change-or-remove-macintosh-accessible-volumes"></a>Macintosh からアクセス可能なボリュームを追加、変更、または削除する

Macintosh からアクセスできるボリュームを追加、変更、または削除する。

### <a name="syntax"></a>構文

```
macfile volume {/add|/set} [/server:\\<computername>] /name:<volumename>/path:<directory>[/readonly:{true | false}] [/guestsallowed:{true | false}] [/password:<password>] [/maxusers:{<number>>|unlimited}]
macfile volume /remove[/server:\\<computername>] /name:<volumename>
```

#### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `{/add | /set}` | Macintosh からアクセス可能なボリュームを追加または変更する場合に必要です。 追加したり、指定したボリュームを変更します。 |
| /server:`\\<computername>` | 追加、変更、またはボリュームを削除するサーバーを指定します。 省略した場合は、操作は、ローカル コンピューターで実行されます。 |
| /name`<volumename>` | 必須です。 追加、変更、または削除するには、ボリューム名を指定します。 |
| /path`<directory>` | 必須およびボリュームを追加するときにだけ有効です。 追加するボリュームのルート ディレクトリへのパスを指定します。 |
| readonly`{true | false}` | ユーザーがボリューム内のファイルを変更できるかどうかを指定します。 ユーザーがボリューム内のファイルを変更できないように指定するには、 **True**を使用します。 ユーザーがボリューム内のファイルを変更できるようにするには、 **False**を使用します。 ボリュームを追加するときに省略すると、ファイルへの変更が許可されます。 ボリュームを変更する場合を省略した場合、 **読み取り専用** 設定は、ボリュームは変更されません。 |
| 許可する (& s):`{true | false}` | ゲストとしてログオンするユーザーがボリュームを使用できるかどうかを指定します。 ゲストがボリュームを使用できるように指定するには、 **True**を使用します。 ゲストがボリュームを使用できないように指定するには、 **False**を使用します。 ボリュームを追加するときに省略すると、ゲストは、ボリュームを使用できます。 ボリュームを変更する場合を省略した場合、 **guestsallowed** 設定は、ボリュームは変更されません。 |
| /password`<password>` | ボリュームへのアクセスに必要なパスワードを指定します。 ボリュームを追加するときに省略すると、パスワードは作成されません。 ボリュームを変更するときに省略すると、パスワードは変更されません。 |
| /maxusers:`{<number>> | unlimited}` | ボリューム上のファイルを同時に使用できるユーザーの最大数を指定します。 ボリュームを追加するときに省略すると、無制限の数のユーザーは、ボリュームを使用できます。 ボリュームを変更する場合を省略した場合、 **maxusers** 値は変更されません。                                                 |
| /remove | Macintosh からアクセス可能なボリュームを削除する場合に必要です。 指定されたボリュームを削除します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

##### <a name="remarks"></a>注釈

- 入力した情報にスペースや特殊文字が含まれている場合は、テキストを引用符で囲みます (" `<computer name>` " など)。

#### <a name="examples"></a>例

E ドライブの*Stats*ディレクトリを使用して、ローカルサーバーに*米国マーケティング統計*というボリュームを作成し、ゲストがそのボリュームにアクセスできないように指定するには、次のように入力します。

```
macfile volume /add /name:US Marketing Statistics /guestsallowed:false /path:e:\Stats
```

上で作成したボリュームを読み取り専用に変更し、パスワードを要求し、最大ユーザー数を5に設定するには、次のように入力します。

```
macfile volume /set /name:US Marketing Statistics /readonly:true /password:saturn /maxusers:5
```

*ランドスケープ設計*と呼ばれるボリュームをサーバー * \\ アプリ*に追加し、E ドライブの*tree*ディレクトリを使用して、ゲストがボリュームにアクセスできるように指定するには、次のように入力します。

```
macfile volume /add /server:\\Magnolia /name:Landscape Design /path:e:\trees
```

*Sales Reports*というボリュームをローカルサーバーで削除するには、次のように入力します。

```
macfile volume /remove /name:Sales Reports
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
