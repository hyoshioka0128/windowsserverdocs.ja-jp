---
title: macfile
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: e2ce586c-b316-41d3-90f8-4be0d074cc0e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0156be5a3209bf8cedf13b35ceab61ef38a0f49a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80840315"
---
# <a name="macfile"></a>macfile

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

Macintosh サーバー、ボリューム、ディレクトリ、およびファイルのファイル サーバーを管理します。 バッチ ファイルで、一連のコマンドをなどによって手動で開始する管理タスクを自動化できるか、事前に定義した時刻。 
-   [Macintosh からアクセス可能なボリューム内のディレクトリを変更するには](#BKMK_Moddirs)
-   [Macintosh ファイルのデータとリソースフォークを結合するには](#BKMK_Joinforks)
-   [ログオンメッセージを変更し、セッションを制限するには](#BKMK_LogonLimit)
-   [Macintosh からアクセス可能なボリュームを追加、変更、または削除するには](#BKMK_addvol)

## <a name="to-modify-directories-in-macintosh-accessible-volumes"></a><a name=BKMK_Moddirs></a>Macintosh からアクセス可能なボリューム内のディレクトリを変更するには

### <a name="syntax"></a>構文
```
macfile directory[/server:\\<computerName>] /path:<directory> [/owner:<OwnerName>] [/group:<GroupName>] [/permissions:<Permissions>]
```

#### <a name="parameters"></a>パラメーター
-   /server:\\\\<computerName> は、ディレクトリを変更するサーバーを指定します。 省略した場合は、操作は、ローカル コンピューターで実行されます。
-   /path:<directory> が必要です。 変更するディレクトリへのパスを指定します。 このディレクトリが存在する必要があります。 **macfile ディレクトリ**では、ディレクトリは作成されません。
-   /owner:<OwnerName> によって、ディレクトリの所有者が変更されます。 省略した場合、所有者は変更されません。
-   グループ化/:<GroupName> ディレクトリに関連付けられているプライマリ Macintosh であるグループの変更または指定します。 省略した場合は、プライマリ グループは変更されません。
-   /permissions:<Permissions> 所有者、プライマリ グループは、および世界 (everyone) 用のディレクトリに対する権限を設定します。 11 桁の数字を使用して、アクセス許可を設定します。 番号 1 は権限を付与し、0 (たとえば、11111011000) のアクセスを許可した権限を取り消します。 省略すると、アクセス許可は変更されません。
    添字の位置は、次の表に示すようにするアクセス許可を設定するが決まります。

    |[位置]|アクセス許可を設定します。|
    |------|------------|
    |First|OwnerSeeFiles|
    |Second|OwnerSeeFolders|
    |3 番目|OwnerMakechanges|
    |4 番目|GroupSeeFiles|
    |第 5|GroupSeeFolders|
    |第 6|GroupMakechanges|
    |第 7|WorldSeeFiles|
    |第 8|WorldSeeFolders|
    |9 番目|WorldMakechanges|
    |第 10|ディレクトリは、名前変更、移動、または削除することはできません。|
    |11 番目|変更は、現在のディレクトリとすべてのサブディレクトリに適用されます。|

-   /?
    コマンド プロンプトでヘルプを表示します。

### <a name="remarks"></a>コメント
- 入力した情報にスペースや特殊文字が含まれている場合は、テキストを引用符で囲みます (たとえば、* * * *<em>コンピューター名</em>* * * *)。
- 使用 **macfiledirectory** Macintosh からアクセス可能なボリューム内の既存のディレクトリを Macintosh ユーザーが使用できるようにします。 **Macfiledirectory** コマンドでは、ディレクトリは作成されません。 ファイル マネージャーでは、コマンド プロンプトを使用して、または **macintosh の新しいフォルダー** を使用する前に、Macintosh からアクセス可能なボリュームにディレクトリを作成するコマンド、 **macfile ディレクトリ** コマンドです。
  ### <a name="examples"></a><a name=BKMK_Examples></a>例
  次の例では、ローカル サーバーの E ドライブに Macintosh からアクセス可能なボリュームの統計で、サブディレクトリの 5 月の売上におけるのアクセス許可を変更します。 この例では、[ファイルの参照]、[フォルダーの参照]、所有者に対する [変更] アクセス許可を割り当て、他のすべてのユーザーに対して [ファイル] および [フォルダーのアクセス許可] を参照して、ディレクトリの名前変更、移動、または削除を禁止します。
  ```
  macfile directory /path:e:\statistics\may sales /permissions:11111011000
  ```

## <a name="to-join-a-macintosh-files-data-and-resource-forks"></a><a name=BKMK_Joinforks></a>Macintosh ファイルのデータとリソースフォークを結合するには

### <a name="syntax"></a>構文
```
macfile forkize[/server:\\<computerName>] [/creator:<CreatorName>] [/type:<typeName>]  [/datafork:<Filepath>] [/resourcefork:<Filepath>] /targetfile:<Filepath>
```

#### <a name="parameters"></a>パラメーター

|         パラメーター          |                                                                                                           説明                                                                                                            |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| /server:\\\\<computerName> |                                                            ファイルを結合するサーバーを指定します。 省略した場合は、操作は、ローカル コンピューターで実行されます。                                                            |
|   /creator:<CreatorName>   |                                      ファイルの作成者を指定します。 Macintosh finder は、 **/creator**コマンドラインオプションを使用して、ファイルを作成したアプリケーションを特定します。                                       |
|      /type:<typeName>      |                                 ファイルの種類を指定します。 Macintosh finder は、 **/type**コマンドラインオプションを使用して、ファイルを作成したアプリケーション内のファイルの種類を確認します。                                 |
|    /dataフォーク:<Filepath>    |                                                                   結合するデータ フォークの場所を指定します。 リモート パスを指定できます。                                                                   |
|  /resourceフォーク:<Filepath>  |                                                                 参加しているリソース フォークの場所を指定します。 リモート パスを指定できます。                                                                 |
|   /targetfile:<Filepath>   | 必須。 データ フォークし、リソースのフォークを結合して作成されるファイルの場所を指定または、種類またはクリエーターを変更する場合は、ファイルの場所を指定します。 ファイルは、指定されたサーバー上に存在する必要があります。 |
|             /?             |                                                                                               コマンド プロンプトでヘルプを表示します。                                                                                               |

### <a name="remarks"></a>コメント
- 入力した情報にスペースや特殊文字が含まれている場合は、テキストを引用符で囲みます (たとえば、* * * *<em>コンピューター名</em>* * * *)。

### <a name="examples"></a>例
リソースフォーク D:\Release を使用して macintosh からアクセス可能なボリュームにファイル treeapp を作成し、この新しいファイルをアプリケーションとして Macintosh クライアントに表示するには (Macintosh アプリケーションでは APPL.EXE を使用します)、creator (署名) をアプリに設定し、次のように入力します。
```
macfile forkize /resourcefork:c:\cross\mac\appcode /type:APPL /creator:MAGNOLIA /targetfile:D:\Release\treeapp
```
ファイルの作成者を Microsoft Word 5.1 に変更するには、D:\Word documents\Group \\files ディレクトリの file.txt ファイルで、次のように入力します。
```
macfile forkize /server:\\servera /creator:MSWD /type:TEXT /targetfile:d:\Word documents\Group files\Word.txt
```

## <a name="to-change-the-logon-message-and-limit-sessions"></a><a name=BKMK_LogonLimit></a>ログオンメッセージを変更し、セッションを制限するには
### <a name="syntax"></a>構文
```
macfile server [/server:\\<computerName>] [/maxsessions:{Number | unlimited}] [/loginmessage:<Message>]
```

#### <a name="parameters"></a>パラメーター

|               パラメーター                |                                                                                                                                                                           説明                                                                                                                                                                            |
|----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       /server:\\\\<computerName>       |                                                                                                                        パラメーターを変更するサーバーを指定します。 省略した場合は、操作は、ローカル コンピューターで実行されます。                                                                                                                         |
| /maxsessions: {数 & #124; 無制限} |                                                                                         Macintosh 用のファイルおよびプリントサーバーを同時に使用できるユーザーの最大数を指定します。 省略した場合は、 **maxsessions** 設定、サーバーは変更されません。                                                                                         |
|        /loginmessage:<Message>         | macintosh サーバーのファイルサーバーにログオンするときに、Macintosh ユーザーに表示されるメッセージを変更します。 ログオン メッセージの文字の最大数は、199 です。 省略した場合は、 **loginmessage** メッセージは、サーバーは変更されません。 既存のログオン メッセージを削除するには、 **/loginmessage** 残しておくに、パラメーター、 *メッセージ* 変数が空です。 |
|                   /?                   |                                                                                                                                                               コマンド プロンプトでヘルプを表示します。                                                                                                                                                               |

### <a name="remarks"></a>コメント
- 入力した情報にスペースや特殊文字が含まれている場合は、テキストを引用符で囲みます (たとえば、* * * *<em>コンピューター名</em>* * * *)。

### <a name="examples"></a>例
ローカルサーバーで許可されている Macintosh セッションのファイルおよびプリントサーバーの数を現在の設定から5つのセッションに変更し、完了時に Macintosh 用のログオンメッセージをサーバーから追加するには、次のように入力します。
```
macfile server /maxsessions:5 /loginmessage:Log off from Server for Macintosh when you are finished.
```

## <a name="to-add-change-or-remove-macintosh-accessible-volumes"></a><a name=BKMK_addvol></a>Macintosh からアクセス可能なボリュームを追加、変更、または削除するには
### <a name="syntax"></a>構文
```
macfile volume {/add|/set} [/server:\\<computerName>] /name:<volumeName>/path:<directory>[/readonly:{true | false}] [/guestsallowed:{true | false}] [/password:<Password>] [/maxusers:{<Number>>|unlimited}]
macfile volume /remove[/server:\\<computerName>] /name:<volumeName>
```

#### <a name="parameters"></a>パラメーター

|              パラメーター               |                                                                                                                                                                       説明                                                                                                                                                                        |
|--------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|          {//追加 (& a) #124;/set}          |                                                                                                                      追加する、または Macintosh からアクセス可能なボリュームを変更するときに必要です。 指定されたボリュームを追加または変更します。                                                                                                                       |
|      /server:\\\\<computerName>      |                                                                                                             追加、変更、またはボリュームを削除するサーバーを指定します。 省略した場合は、操作は、ローカル コンピューターで実行されます。                                                                                                              |
|          /name:<volumeName>          |                                                                                                                                          必須。 追加、変更、または削除するには、ボリューム名を指定します。                                                                                                                                           |
|          /path:<directory>           |                                                                                                                必須およびボリュームを追加するときにだけ有効です。 追加するボリュームのルート ディレクトリへのパスを指定します。                                                                                                                 |
|    /readonly: {#124 (&) は true、false}     | ユーザーがボリューム内のファイルを変更できるかどうかを指定します。 ユーザーがボリューム内のファイルを変更できないように指定するには、「true」と入力します。 ユーザーがボリューム内のファイルを変更できるように指定するには、「false」と入力します。 ボリュームを追加するときに省略すると、ファイルへの変更が許可されます。 ボリュームを変更する場合を省略した場合、 **読み取り専用** 設定は、ボリュームは変更されません。 |
|  /guestsallowed: {#124 (&) は true、false}  |      ゲストとしてログオンするユーザーがボリュームを使用できるかどうかを指定します。 ゲストがボリュームを使用できるように指定するには、「true」と入力します。 ゲストがボリュームを使用できないように指定するには、「false」と入力します。 ボリュームを追加するときに省略すると、ゲストは、ボリュームを使用できます。 ボリュームを変更する場合を省略した場合、 **guestsallowed** 設定は、ボリュームは変更されません。       |
|         /password:<Password>         |                                                                               ボリュームへのアクセスに必要なパスワードを指定します。 ボリュームを追加するときに省略すると、パスワードは作成されません。 ボリュームを変更するときに省略すると、パスワードは変更されません。                                                                               |
| /maxusers: {<Number>> & #124 無制限;} |                                                 ボリューム上のファイルを同時に使用できるユーザーの最大数を指定します。 ボリュームを追加するときに省略すると、無制限の数のユーザーは、ボリュームを使用できます。 ボリュームを変更する場合を省略した場合、 **maxusers** 値は変更されません。                                                 |
|               /remove                |                                                                                                                                Macintosh アクセス可能なボリュームを削除するときに必要です。 指定されたボリュームを削除します。                                                                                                                                |
|                  /?                  |                                                                                                                                                           コマンド プロンプトでヘルプを表示します。                                                                                                                                                           |

### <a name="remarks"></a>コメント
- 入力した情報にスペースや特殊文字が含まれている場合は、テキストを引用符で囲みます (たとえば、* * * *<em>コンピューター名</em>* * * *)。

### <a name="examples"></a>例
E ドライブに Stats ディレクトリを使用して、ローカル サーバーに米国マーケティングの統計情報と呼ばれるボリュームを作成し、ゲストでボリュームにアクセスできないことを指定するには、次のように入力します。
```
macfile volume /add /name:US Marketing Statistics /guestsallowed:false /path:e:\Stats
```
ボリュームを変更するには、上記で作成した読み取り専用にして、パスワードを要求して、5 つの型に最大ユーザー数を設定します。
```
macfile volume /set /name:US Marketing Statistics /readonly:true /password:saturn /maxusers:5
```
ランドスケープ設計と呼ばれるボリュームを追加するには、サーバー \\\Magnolia に E ドライブの tree ディレクトリを使用し、ゲストがボリュームにアクセスできるように指定するには、次のように入力します。
```
macfile volume /add /server:\\Magnolia /name:Landscape Design /path:e:\trees
```
ローカル サーバー上の営業レポートと呼ばれるボリュームを削除するには、次のように入力します。
```
macfile volume /remove /name:Sales Reports
```

## <a name="additional-references"></a>その他の参照情報
-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
