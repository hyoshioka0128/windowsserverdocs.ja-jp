---
title: 編集
description: '[編集] コマンドのリファレンストピックでは、MS-DOS エディターを起動して、ASCII テキストファイルを作成および変更できます。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 4e0ff2e8-3518-47c1-8c69-5e93f895fa0e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a9f6c78889f466015d60149c27a87dcefe840133
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436917"
---
# <a name="edit"></a>編集

ASCII テキストファイルを作成および変更する MS-DOS エディターを起動します。

## <a name="syntax"></a>構文

```
edit [/b] [/h] [/r] [/s] [/<nnn>] [[<drive>:][<path>]<filename> [<filename2> [...]]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `[<drive>:][<path>]<filename> [<filename2> [...]]` | 1つ以上の ASCII テキストファイルの場所と名前を指定します。 ファイルが存在しない場合は、MS-DOS エディターによって作成されます。 ファイルが存在する場合は、MS-DOS エディターが開き、その内容が画面に表示されます。 *Filename*オプションには、ワイルドカード文字 (**&#42;** と **?**) を含めることができます。 複数のファイル名をスペースで区切ります。 |
| /b | 白黒モードで、MS-DOS エディターが白黒で表示されるようにします。 |
| /h | 現在のモニターで使用できる最大行数を表示します。 |
| /r | 読み取り専用モードでファイルを読み込みます。 |
| /s | 短いファイル名の使用を強制します。 |
| `<nnn>` | バイナリファイルを読み込み、行を*nnn*文字幅に折り返します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>解説

- 追加のヘルプを表示するには、MS-DOS エディターを開き、F1 キーを押します。

- 一部のモニターでは、ショートカットキーの表示が既定でサポートされていません。 モニターにショートカットキーが表示されない場合は、 **/b**を使用します。

### <a name="examples"></a>例

MS-DOS エディターを開くには、次のように入力します。

```
edit
```

現在のディレクトリに*newtextfile*という名前のファイルを作成して編集するには、次のように入力します。

```
edit newtextfile.txt
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)
