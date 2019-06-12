---
title: macfile
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2ce586c-b316-41d3-90f8-4be0d074cc0e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bd7646ada96cb02ae434d4ba846da7a9c4dca51b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437473"
---
# <a name="macfile"></a>macfile

>適用先:Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Macintosh サーバー、ボリューム、ディレクトリ、およびファイルのファイル サーバーを管理します。 バッチ ファイルで、一連のコマンドをなどによって手動で開始する管理タスクを自動化できるか、事前に定義した時刻。 
-   [Macintosh からアクセス可能なボリューム内のディレクトリを変更するには](#BKMK_Moddirs)
-   [Macintosh ファイルのデータおよびリソース フォークに参加するには](#BKMK_Joinforks)
-   [ログオン メッセージを変更し、セッションの制限](#BKMK_LogonLimit)
-   [追加、変更、または Macintosh からアクセス可能なボリュームを削除するには](#BKMK_addvol)

## <a name="BKMK_Moddirs"></a>Macintosh からアクセス可能なボリューム内のディレクトリを変更するには

### <a name="syntax"></a>構文
```
macfile directory[/server:\\<computerName>] /path:<directory> [/owner:<OwnerName>] [/group:<GroupName>] [/permissions:<Permissions>]
```

### <a name="parameters"></a>パラメーター
-   /server:\\\\<computerName>ディレクトリを変更するサーバーを指定します。 省略した場合は、操作は、ローカル コンピューターで実行されます。
-   /path:<directory>必須。 変更するディレクトリへのパスを指定します。 このディレクトリが存在する必要があります。 **macfile ディレクトリ**ディレクトリは作成されません。
-   /owner:<OwnerName>ディレクトリの所有者を変更します。 省略した場合、所有者は変更されません。
-   /group:<GroupName>指定します。 または、ディレクトリに関連付けられている Macintosh のプライマリ グループを変更します。 省略した場合は、プライマリ グループは変更されません。
-   /permissions:<Permissions>所有者、プライマリ グループ、および世界 (everyone) 用のディレクトリのアクセス許可を設定します。 11 桁の数字を使用して、アクセス許可を設定します。 番号 1 は権限を付与し、0 (たとえば、11111011000) のアクセスを許可した権限を取り消します。 省略すると、アクセス許可は変更されません。
    添字の位置は、次の表に示すようにするアクセス許可を設定するが決まります。

    |位置|アクセス許可を設定します。|
    |------|------------|
    |First|OwnerSeeFiles|
    |第 2 週|OwnerSeeFolders|
    |サードパーティ|所有者の内容変更|
    |4 番目|GroupSeeFiles|
    |5 番目|GroupSeeFolders|
    |6 番目|GroupMakechanges|
    |7 番目|WorldSeeFiles|
    |8 番目|WorldSeeFolders|
    |9 番目|WorldMakechanges|
    |10 分|ディレクトリは、名前変更、移動、または削除することはできません。|
    |11 番目|変更は、現在のディレクトリとすべてのサブディレクトリに適用されます。|

-   /?
    コマンド プロンプトにヘルプを表示します。

### <a name="remarks"></a>注釈
- スペースや特殊文字が入力する情報が含まれる場合は、テキストを囲む引用符を使用して (たとえば、 **"** <em>コンピューター名</em> **"** )。
- 使用 **macfiledirectory** Macintosh からアクセス可能なボリューム内の既存のディレクトリを Macintosh ユーザーが使用できるようにします。 **Macfiledirectory** コマンドでは、ディレクトリは作成されません。 ファイル マネージャーでは、コマンド プロンプトを使用して、または **macintosh の新しいフォルダー** を使用する前に、Macintosh からアクセス可能なボリュームにディレクトリを作成するコマンド、 **macfile ディレクトリ** コマンドです。
  ### <a name="BKMK_Examples"></a>例
  次の例では、ローカル サーバーの E ドライブに Macintosh からアクセス可能なボリュームの統計で、サブディレクトリの 5 月の売上におけるのアクセス許可を変更します。 例はファイルを参照してください、「フォルダー、および作成の変更アクセス許可を、ディレクトリの変更、移動、または削除を防止所有者と他すべてユーザーに「ファイルとフォルダーのアクセスを許可を割り当てます。
  ```
  macfile directory /path:"e:\statistics\may sales" /permissions:11111011000
  ```

## <a name="BKMK_Joinforks"></a>Macintosh ファイルのデータおよびリソース フォークに参加するには

### <a name="syntax"></a>構文
```
macfile forkize[/server:\\<computerName>] [/creator:<CreatorName>] [/type:<typeName>]  [/datafork:<Filepath>] [/resourcefork:<Filepath>] /targetfile:<Filepath>
```

### <a name="parameters"></a>パラメーター

|         パラメーター          |                                                                                                           説明                                                                                                            |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /server:\\\\<computerName> |                                                            ファイルを結合するサーバーを指定します。 省略した場合は、操作は、ローカル コンピューターで実行されます。                                                            |
|   /creator:<CreatorName>   |                                      ファイルの作成者を指定します。 Macintosh のファインダーを使用して、 **/creator**コマンド ライン オプションにファイルを作成したアプリケーションを決定します。                                       |
|      /type:<typeName>      |                                 ファイルの種類を指定します。 Macintosh のファインダーを使用して、 **/type**コマンド ライン オプションをファイルを作成したアプリケーション内でファイルの種類を決定します。                                 |
|    /datafork:<Filepath>    |                                                                   結合するデータ フォークの場所を指定します。 リモート パスを指定できます。                                                                   |
|  /resourcefork:<Filepath>  |                                                                 参加しているリソース フォークの場所を指定します。 リモート パスを指定できます。                                                                 |
|   /targetfile:<Filepath>   | 必須。 データ フォークし、リソースのフォークを結合して作成されるファイルの場所を指定または、種類またはクリエーターを変更する場合は、ファイルの場所を指定します。 ファイルは、指定されたサーバー上に存在する必要があります。 |
|             /?             |                                                                                               コマンド プロンプトにヘルプを表示します。                                                                                               |

### <a name="remarks"></a>注釈
- スペースや特殊文字が入力する情報が含まれる場合は、テキストを囲む引用符を使用して (たとえば、 **"** <em>コンピューター名</em> **"** )。

### <a name="examples"></a>例
Macintosh からアクセス可能なボリューム リソース フォーク C:\Cross\Mac\Appcode を使用して、D:\Release ファイル treeapp を作成し、Macintosh クライアントにアプリケーションとして表示されるこの新しいファイルを作成する (Macintosh アプリケーションは、アプリの種類を使用) で作成者 (署名) に MAGNOLIA、型を設定します。
```
macfile forkize /resourcefork:c:\cross\mac\appcode /type:APPL /creator:MAGNOLIA /targetfile:D:\Release\treeapp
```
ファイル サーバー上のディレクトリの D:\Word documents \group ファイルで WOrd.txt の Microsoft Word 5.1 にファイルの作成者を変更する\\\SERverA、種類。
```
macfile forkize /server:\\servera /creator:MSWD /type:TEXT /targetfile:"d:\Word documents\Group files\Word.txt"
```

## <a name="BKMK_LogonLimit"></a>ログオン メッセージを変更し、セッションの制限
### <a name="syntax"></a>構文
```
macfile server [/server:\\<computerName>] [/maxsessions:{Number | unlimited}] [/loginmessage:<Message>]
```

### <a name="parameters"></a>パラメーター

|               パラメーター                |                                                                                                                                                                           説明                                                                                                                                                                            |
|----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       /server:\\\\<computerName>       |                                                                                                                        パラメーターを変更するサーバーを指定します。 省略した場合は、操作は、ローカル コンピューターで実行されます。                                                                                                                         |
| /maxsessions: {数 &#124; 無制限} |                                                                                         同時にファイルを使用し、Macintosh 用プリント サーバーはユーザーの最大数を指定します。 省略した場合は、 **maxsessions** 設定、サーバーは変更されません。                                                                                         |
|        /loginmessage:<Message>         | 変更メッセージ Macintosh ユーザーは、Macintosh サーバーのファイル サーバーにログオンするときに参照してください。 ログオン メッセージの文字の最大数は、199 です。 省略した場合は、 **loginmessage** メッセージは、サーバーは変更されません。 既存のログオン メッセージを削除するには、 **/loginmessage** 残しておくに、パラメーター、 *メッセージ* 変数が空です。 |
|                   /?                   |                                                                                                                                                               コマンド プロンプトにヘルプを表示します。                                                                                                                                                               |

### <a name="remarks"></a>注釈
- スペースや特殊文字が入力する情報が含まれる場合は、テキストを囲む引用符を使用して (たとえば、 **"** <em>コンピューター名</em> **"** )。

### <a name="examples"></a>例
ファイルの数を変更して、プリント サーバーの Macintosh セッションが許可されている、ローカル サーバーで現在の設定から 5 つのセッションとログオン メッセージを追加する"サーバーからログオフ Macintosh 用が完了したら。"を入力します。
```
macfile server /maxsessions:5 /loginmessage:"Log off from Server for Macintosh when you are finished."
```

## <a name="BKMK_addvol"></a>追加、変更、または Macintosh からアクセス可能なボリュームを削除するには
### <a name="syntax"></a>構文
```
macfile volume {/add|/set} [/server:\\<computerName>] /name:<volumeName>/path:<directory>[/readonly:{true | false}] [/guestsallowed:{true | false}] [/password:<Password>] [/maxusers:{<Number>>|unlimited}]
macfile volume /remove[/server:\\<computerName>] /name:<volumeName>
```

### <a name="parameters"></a>パラメーター

|              パラメーター               |                                                                                                                                                                       説明                                                                                                                                                                        |
|--------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|          {//追加 (& a) #124;/set}          |                                                                                                                      追加する、または Macintosh からアクセス可能なボリュームを変更するときに必要です。 追加または指定されたボリュームを変更します。                                                                                                                       |
|      /server:\\\\<computerName>      |                                                                                                             追加、変更、またはボリュームを削除するサーバーを指定します。 省略した場合は、操作は、ローカル コンピューターで実行されます。                                                                                                              |
|          /name:<volumeName>          |                                                                                                                                          必須。 追加、変更、または削除するには、ボリューム名を指定します。                                                                                                                                           |
|          /path:<directory>           |                                                                                                                必須およびボリュームを追加するときにだけ有効です。 追加するボリュームのルート ディレクトリへのパスを指定します。                                                                                                                 |
|    /readonly: {#124 (&) は true、false}     | ユーザーがボリューム内のファイルを変更できるかどうかを指定します。 ユーザーがボリューム内のファイルを変更できないことを指定する場合は true を入力します。 ユーザーがボリューム内のファイルを変更できることを指定する場合は false を入力します。 ボリュームを追加するときに省略すると、ファイルへの変更が許可されます。 ボリュームを変更する場合を省略した場合、 **読み取り専用** 設定は、ボリュームは変更されません。 |
|  /guestsallowed: {#124 (&) は true、false}  |      ゲストとしてログオンするユーザーがボリュームを使用できるかどうかを指定します。 ゲストがボリュームを使用するように指定する場合は true を入力します。 ゲストがボリュームを使用できないことを指定する場合は false を入力します。 ボリュームを追加するときに省略すると、ゲストは、ボリュームを使用できます。 ボリュームを変更する場合を省略した場合、 **guestsallowed** 設定は、ボリュームは変更されません。       |
|         /password:<Password>         |                                                                               ボリュームへのアクセスに必要なパスワードを指定します。 ボリュームを追加するときに省略すると、パスワードは作成されません。 ボリュームを変更するときに省略すると、パスワードは変更されません。                                                                               |
| /maxusers: {<Number>> &#124 無制限;} |                                                 ボリューム上のファイルを同時に使用できるユーザーの最大数を指定します。 ボリュームを追加するときに省略すると、無制限の数のユーザーは、ボリュームを使用できます。 ボリュームを変更する場合を省略した場合、 **maxusers** 値は変更されません。                                                 |
|               /remove                |                                                                                                                                Macintosh アクセス可能なボリュームを削除するときに必要です。 指定されたボリュームを削除します。                                                                                                                                |
|                  /?                  |                                                                                                                                                           コマンド プロンプトにヘルプを表示します。                                                                                                                                                           |

### <a name="remarks"></a>注釈
- スペースや特殊文字が入力する情報が含まれる場合は、テキストを囲む引用符を使用して (たとえば、 **"** <em>コンピューター名</em> **"** )。

### <a name="examples"></a>例
E ドライブに Stats ディレクトリを使用して、ローカル サーバーに米国マーケティングの統計情報と呼ばれるボリュームを作成し、ゲストでボリュームにアクセスできないことを指定するには、次のように入力します。
```
macfile volume /add /name:"US Marketing Statistics" /guestsallowed:false /path:e:\Stats
```
ボリュームを変更するには、上記で作成した読み取り専用にして、パスワードを要求して、5 つの型に最大ユーザー数を設定します。
```
macfile volume /set /name:"US Marketing Statistics" /readonly:true /password:saturn /maxusers:5
```
サーバーのランドス ケープの設計と呼ばれるボリュームを追加する\\\Magnolia、E ドライブおよびゲストの種類によって、ボリュームにアクセスできることを指定するツリー ディレクトリを使用します。
```
macfile volume /add /server:\\Magnolia /name:"Landscape Design" /path:e:\trees
```
ローカル サーバー上の営業レポートと呼ばれるボリュームを削除するには、次のように入力します。
```
macfile volume /remove /name:"Sales Reports"
```

## <a name="additional-references"></a>その他の参照
-   [コマンド ライン構文の記号](command-line-syntax-key.md)
