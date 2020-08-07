---
title: prnjobs
description: 印刷ジョブを一時停止、再開、キャンセル、および一覧表示する prnjobs.vbs コマンドの参照記事。
ms.topic: article
ms.assetid: 5ad34199-7a5a-40c1-8053-bccd5929df43
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: d955f50761e1229e0a1acf21a9f2179525bd7ee4
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87884744"
---
# <a name="prnjobs"></a>prnjobs

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

一時停止、再開、キャンセルすると、および印刷ジョブを一覧表示します。 このコマンドは、ディレクトリにある Visual Basic スクリプトです `%WINdir%\System32\printing_Admin_Scripts\<language>` 。 コマンドプロンプトでこのコマンドを使用するには、「 **cscript** 」に続けて prnjobs.vbs ファイルの完全なパスを入力するか、ディレクトリを適切なフォルダーに変更します。 (例: `cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnjobs.vbs`)。

## <a name="syntax"></a>構文

```
cscript prnjobs {-z | -m | -x | -l | -?} [-s <Servername>] [-p <Printername>] [-j <JobID>] [-u <Username>] [-w <password>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| -Z | **-J**パラメーターによって指定された印刷ジョブを一時停止します。 |
| -M | **-J**パラメーターによって指定された印刷ジョブを再開します。 |
| -X | **-J**パラメーターによって指定された印刷ジョブをキャンセルします。 |
| -l | 印刷キュー内のすべての印刷ジョブを一覧表示します。 |
| -s `<Servername>` | 管理するプリンターをホストするリモート コンピューターの名前を指定します。 コンピューターを指定しない場合は、ローカルコンピューターが使用されます。 |
| -p`<Printername>` | 必須。 管理するプリンターの名前を指定します。 |
| -j`<JobID>` | 印刷ジョブをキャンセルする (ID 番号) を指定します。 |
| -u `<Username>` -w`<password>` | 管理するプリンターをホストするコンピューターに接続するアクセス許可を持つアカウントを指定します。 ターゲット コンピューターのローカル Administrators グループのすべてのメンバーはこれらのアクセス許可を持っていますが、アクセス許可を他のユーザーに与えることもできます。 アカウントを指定しない場合は、コマンドが機能するように、これらのアクセス許可を持つアカウントでログオンする必要があります。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>Remarks

- 入力した情報にスペースが含まれている場合は、テキストを引用符で囲みます (例、"コンピューター名")。

### <a name="examples"></a>例

印刷用に HRServer という名前のリモートコンピューターに送信されたジョブ ID が27の印刷ジョブを一時停止するには、次のように入力します。

```
cscript prnjobs.vbs -z -s HRServer -p colorprinter -j 27
```

Colorprinter_2 という名前のローカルプリンターのキューにある現在のすべての印刷ジョブを一覧表示するには、次のように入力します。

```
cscript prnjobs.vbs -l -p colorprinter_2
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [印刷コマンドのリファレンス](print-command-reference.md)
