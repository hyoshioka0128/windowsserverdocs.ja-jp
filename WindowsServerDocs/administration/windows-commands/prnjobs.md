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
ms.openlocfilehash: 231b8a7a9f4f8623b3d84cc789064d256883a733
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837295"
---
# <a name="prnjobs"></a>prnjobs

>適用対象: Windows Server (半期チャネル)、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

一時停止、再開、キャンセルすると、および印刷ジョブを一覧表示します。

## <a name="syntax"></a>構文
```
cscript Prnjobs {-z | -m | -x | -l | -?} [-s <ServerName>] 
[-p <printerName>] [-j <JobID>] [-u <UserName>] [-w <Password>]
```

### <a name="parameters"></a>パラメーター

|          パラメーター           |                                                                                                                                                                                        説明                                                                                                                                                                                        |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              ~ z              |                                                                                                                                                                 **-j**パラメーターで指定された印刷ジョブを一時停止します。                                                                                                                                                                 |
|              -m              |                                                                                                                                                                指定した印刷ジョブを再開、 **-j** パラメーター。                                                                                                                                                                 |
|              -x              |                                                                                                                                                                指定した印刷ジョブを取り消し、 **-j** パラメーター。                                                                                                                                                                 |
|              -l              |                                                                                                                                                                        印刷キュー内のすべての印刷ジョブを一覧表示します。                                                                                                                                                                         |
|       -s \<ServerName >       |                                                                                                                  管理するプリンターをホストするリモート コンピューターの名前を指定します。 コンピューターを指定しないと、ローカル コンピューターが使用されます。                                                                                                                  |
|      -p \<printerName >       |                                                                                                                                                           管理するプリンターの名前を指定します。 必須。                                                                                                                                                            |
|         -j \<JobID >          |                                                                                                                                                                印刷ジョブをキャンセルする (ID 番号) を指定します。                                                                                                                                                                 |
| -u \<UserName >-w <Password> | 管理するプリンターをホストするコンピューターに接続するアクセス許可を持つアカウントを指定します。 ターゲット コンピューターのローカル Administrators グループのすべてのメンバーにこれらのアクセス許可があるが、アクセス許可は、他のユーザーに与えることもできます。 アカウントを指定しない場合は、コマンドを実行するこれらのアクセス許可を持つアカウントでログオンする必要があります。 |
|              /?              |                                                                                                                                                                           コマンド プロンプトでヘルプを表示します。                                                                                                                                                                            |

## <a name="remarks"></a>コメント
-   **Prnjobs.vbs**コマンドは、%windir%\system32\ printing_Admin_Scripts\\<language> ディレクトリにある Visual Basic スクリプトです。 このコマンドを使用するには、コマンドプロンプトで「 **cscript** 」と入力し、prnjobs.vbs ファイルへの完全なパスを入力するか、ディレクトリを適切なフォルダーに変更します。 例 :
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

## <a name="additional-references"></a>その他の参照情報

-   - [コマンド ライン構文の記号](command-line-syntax-key.md)
-   [印刷コマンドのリファレンス](print-command-reference.md)
