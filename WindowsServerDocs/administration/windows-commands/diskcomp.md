---
title: diskcomp
description: 2つのフロッピーディスクの内容を比較する、コマンドの参照記事。
ms.topic: article
ms.assetid: 4f56f534-a356-4daa-8b4f-38e089341e42
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 71401942f25d3f503639b2931f2f0ee49229e15b
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890974"
---
# <a name="diskcomp"></a>diskcomp

2つのフロッピーディスクの内容を比較します。 パラメーターを指定せず**に使用**する場合は、現在のドライブを使用して両方のディスクを比較します。

## <a name="syntax"></a>構文

```
diskcomp [<drive1>: [<drive2>:]]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<drive1>` | フロッピーディスクの1つを含むドライブを指定します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>Remarks

- この**コマンドは**、フロッピーディスクでのみ機能します。 ハードディスクで**は使用でき**ません。 ドライブ1または*drive2*のハードディスクドライブを指定*すると、* **次のエラーメッセージが表示さ**れます。

  ```
  Invalid drive specification
  Specified drive does not exist
  or is nonremovable
  ```

- 比較対象の2つのディスクのすべてのトラックが同じである場合 (ディスクのボリューム番号は無視されます)、次のメッセージ**が表示さ**れます。

  ```
  Compare OK
  ```

  トラックが同じでない場合は、次のようなメッセージ**が表示さ**れます。

  ```
  Compare error on
  side 1, track 2
  ```

  この比較**が完了する**と、次のメッセージが表示されます。

  ```
  Compare another diskette (Y/N)?
  ```

  **Y**キーを押すと、次の比較のためにディスクを挿入するよう**に求めるメッセージ**が表示されます。 **N**を押した場合は、比較**が停止し**ます。

- *Drive2*パラメーターを省略した場合 **、は** *drive2*の現在のドライブを使用します。 両方のドライブパラメーターを省略した場合は、両方に現在のドライブ**が使用さ**れます。 現在のドライブがドライブ1と同じ場合は、必要に応じて**ディスクを交換**するように求める*メッセージが表示*されます。

- *Drive1*と*drive2*に同じフロッピーディスクドライブを指定すると、1つのドライブを使用してそれら**を比較し**、必要に応じてディスクを挿入するように求めます。 ディスクの容量と使用可能なメモリの量によっては、ディスクのスワップが必要になる場合があります。

- シングルサイドディスクとダブルサイドディスクを比較することはできません。また、高密度ディスクでも二重密度ディスクを使用する**ことはでき**ません。 *Drive1*のディスクが、 *drive2*のディスクと同じ種類ではない場合、次のメッセージ**が表示さ**れます。

  ```
  Drive types or diskette types not compatible
  ```

- ハードドライブまたは**subst**コマンドによって作成されたドライブでは機能**しません**。 これらの種類のいずれかのドライブで**を使用し**ようとすると、**次のエラーメッセージが表示さ**れます。

  ```
  Invalid drive specification
  ```

- **Copy**を使用して作成したディスク**を使用する**場合、次のようなメッセージが表示される**ことがあり**ます。

  ```
  Compare error on
  side 0, track 0
  ```

  この種類のエラーは、ディスク上のファイルが同じ場合でも発生する可能性があります。 重複した情報を**コピー**する場合でも、必ずしも宛先ディスク上の同じ場所に配置されるわけではありません。

- **終了コード**:

  | 終了コード | 説明 |
  | --------- | ----------- |
  | 0 | ディスクが同じです |
  | 1 | 相違点が見つかりました |
  | 3 | ハードエラーが発生しました |
  | 4 | 初期化エラーが発生しました |

  **によって**返される終了コードを処理するには、バッチプログラムの**if**コマンドラインで*ERRORLEVEL*環境変数を使用します。

## <a name="examples"></a>例

コンピューターにフロッピーディスクドライブが1つしかない場合 (ドライブ A など)、2つのディスクを比較するには、次のように入力します。

```
diskcomp a: a:
```

必要に応じて、各ディスクを挿入するように**求められ**ます。

**If**コマンドラインで*ERRORLEVEL*環境変数を使用するバッチプログラムで、次のよう**な終了コードを処理**する方法を説明します。

```
rem Checkout.bat compares the disks in drive A and B
echo off
diskcomp a: b:
if errorlevel 4 goto ini_error
if errorlevel 3 goto hard_error
if errorlevel 1 goto no_compare
if errorlevel 0 goto compare_ok
:ini_error
echo ERROR: Insufficient memory or command invalid
goto exit
:hard_error
echo ERROR: An irrecoverable error occurred
goto exit
:break
echo You just pressed CTRL+C to stop the comparison
goto exit
:no_compare
echo Disks are not the same
goto exit
:compare_ok
echo The comparison was successful; the disks are the same
goto exit
:exit
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
