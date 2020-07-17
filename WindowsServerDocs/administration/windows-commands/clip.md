---
title: clip
description: コマンドの出力をコマンドラインから Windows クリップボードにリダイレクトする、clip コマンドの参照記事。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 85322d85-3376-4806-845b-93ac77fe27bf
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3c0e23c18d356740a639af760fc7433db59d012a
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929890"
---
# <a name="clip"></a>clip

コマンドの出力をコマンドラインから Windows クリップボードにリダイレクトします。 このコマンドを使用すると、クリップボードからテキストを受信できる任意のアプリケーションにデータを直接コピーできます。 また、このテキスト出力を他のプログラムに貼り付けることもできます。

## <a name="syntax"></a>構文

```
<command> | clip
clip < <filename>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<command>` | 出力を Windows クリップボードに送信するコマンドを指定します。 |
| `<filename>` | Windows クリップボードに送信する内容を含むファイルを指定します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

## <a name="examples"></a>例

現在のディレクトリの一覧を Windows クリップボードにコピーするには、次のように入力します。

```
dir | clip
```

*汎用*のプログラムの出力を Windows クリップボードにコピーするには、次のように入力します。

```
awk -f generic.awk input.txt | clip
```

*readme.txt*という名前のファイルの内容を Windows クリップボードにコピーするには、次のように入力します。

```
clip < readme.txt
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)