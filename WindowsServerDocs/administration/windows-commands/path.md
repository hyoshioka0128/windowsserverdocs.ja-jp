---
title: path
description: PATH 環境変数でコマンドパスを設定するための参照記事。実行可能ファイル (.exe) を検索するために使用されるディレクトリのセットを指定します。
ms.topic: article
ms.assetid: 1bfa1349-e79a-472b-a9e6-d7a91149ae8f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4c81dfef09b4c9a411db9469ec851d4f92180f1d
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87885108"
---
# <a name="path"></a>path

PATH 環境変数でコマンドパスを設定し、実行可能 (.exe) ファイルの検索に使用するディレクトリのセットを指定します。 パラメーターを指定せずに使用した場合、このコマンドは現在のコマンドパスを表示します。

## <a name="syntax"></a>構文

```
path [[<drive>:]<path>[;...][;%PATH%]]
path ;
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| `[<drive>:]<path>` | ドライブとコマンドのパスを設定するディレクトリを指定します。 現在のディレクトリはコマンドのパスで指定したディレクトリの前に常に検索します。 |
| ; | コマンド パス内のディレクトリを分割します。 その他のパラメーターを指定せずに使用する場合 **;** PATH 環境変数からの既存のコマンド パスをクリアし、Cmd.exe、現在のディレクトリのみで検索するように指示します。 |
| `%PATH%` | コマンド パスを PATH 環境変数で指定されているディレクトリの既存のセットに追加します。 このパラメーターを指定すると、Cmd.exe によって PATH 環境変数内のコマンドパス値に置き換えられ、コマンドプロンプトでこれらの値を手動で入力する必要がなくなります。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="remarks"></a>Remarks


- Windows オペレーティングシステムでは、既定のファイル名拡張子を使用して、.exe、.com、.bat、.cmd の順に検索します。 つまり、acct.bat という名前のバッチファイルを探していても、同じディレクトリ内に acct.exe という名前のアプリがある場合は、コマンドプロンプトで .bat 拡張子を含める必要があります。

- コマンドパス内の2つ以上のファイルのファイル名と拡張子が同じである場合、このコマンドは最初に現在のディレクトリ内の指定されたファイル名を検索します。 次に、PATH 環境変数に示されている順序で、コマンドパス内のディレクトリを検索します。

- 配置した場合、 **パス** コマンド、項目ファイルを Windows オペレーティング システムは、お使いのコンピューターにログオンするたびに自動的に指定した MS-DOS サブシステムの検索パスを追加します。 Cmd.exe では、項目のファイルは使用しません。 ショートカットから起動すると、Cmd.exe は、[マイ コンピューター/プロパティ/[詳細設定/環境を設定する環境変数を継承します。

## <a name="examples"></a>例

外部コマンドに対して*c:\user\taxes*、 *b:\user\invest*、および*b:\bin*のパスを検索するには、次のように入力します。

```
path c:\user\taxes;b:\user\invest;b:\bin
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
