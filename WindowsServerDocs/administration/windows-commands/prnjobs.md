---
title: prnjobs
description: コマンドラインから印刷ジョブを管理する方法について説明します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 5ad34199-7a5a-40c1-8053-bccd5929df43
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 002098ba64e97c243d1cb53813b9fa858d32c752
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2020
ms.locfileid: "83821242"
---
# <a name="prnjobs"></a>prnjobs

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

一時停止、再開、キャンセルすると、および印刷ジョブを一覧表示します。

## <a name="syntax"></a>構文
```
cscript Prnjobs {-z | -m | -x | -l | -?} [-s <ServerName>]
[-p <printerName>] [-j <JobID>] [-u <UserName>] [-w <Password>]
```

### <a name="parameters"></a>パラメーター

|          パラメーター           |                                                                                                                                                                                        説明                                                                                                                                                                                        |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              -Z              |                                                                                                                                                                 **-j**パラメーターで指定された印刷ジョブを一時停止します。                                                                                                                                                                 |
|              -M              |                                                                                                                                                                指定した印刷ジョブを再開、 **-j** パラメーター。                                                                                                                                                                 |
|              -X              |                                                                                                                                                                指定した印刷ジョブを取り消し、 **-j** パラメーター。                                                                                                                                                                 |
|              -l              |                                                                                                                                                                        印刷キュー内のすべての印刷ジョブを一覧表示します。                                                                                                                                                                         |
|       -s \< ServerName>       |                                                                                                                  管理するプリンターをホストするリモート コンピューターの名前を指定します。 コンピューターを指定しないと、ローカル コンピューターが使用されます。                                                                                                                  |
|      -p \< printerName>       |                                                                                                                                                           管理するプリンターの名前を指定します。 必須。                                                                                                                                                            |
|         -j \< JobID>          |                                                                                                                                                                印刷ジョブをキャンセルする (ID 番号) を指定します。                                                                                                                                                                 |
| -u \< ユーザー名>-w<Password> | 管理するプリンターをホストするコンピューターに接続するアクセス許可を持つアカウントを指定します。 ターゲット コンピューターのローカル Administrators グループのすべてのメンバーはこれらのアクセス許可を持っていますが、アクセス許可を他のユーザーに与えることもできます。 アカウントを指定しない場合は、コマンドを実行するこれらのアクセス許可を持つアカウントでログオンする必要があります。 |
|              /?              |                                                                                                                                                                           コマンド プロンプトにヘルプを表示します。                                                                                                                                                                            |

## <a name="remarks"></a>注釈
-   **Prnjobs.vbs**コマンドは、%windir%\system32\ printing_Admin_Scripts ディレクトリにある Visual Basic スクリプトです \\ <language> 。 このコマンドを使用するには、コマンドプロンプトで「 **cscript** 」と入力し、prnjobs.vbs ファイルへの完全なパスを入力するか、ディレクトリを適切なフォルダーに変更します。 次に例を示します。
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnjobs.vbs
    ```
-   入力する情報にスペースが含まれる場合は、テキストを囲む引用符を使用して (たとえば、 `"computer Name"`)。

## <a name="examples"></a><a name="BKMK_examples"></a>例
印刷用に HRServer という名前のリモートコンピューターに送信されたジョブ ID が27の印刷ジョブを一時停止するには、次のように入力します。
```
cscript prnjobs.vbs -z -s HRServer -p colorprinter -j 27
```
Colorprinter_2 という名前のローカルプリンターのキューにある現在のすべての印刷ジョブを一覧表示するには、次のように入力します。
```
cscript prnjobs.vbs -l -p colorprinter_2
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [印刷コマンドのリファレンス](print-command-reference.md)
