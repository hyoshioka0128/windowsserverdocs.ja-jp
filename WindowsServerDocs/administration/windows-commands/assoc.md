---
title: assoc
description: ファイル名拡張子の関連付けを表示または変更する assoc コマンドのリファレンストピックです。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 237bedda-b24c-4fec-a39c-9b7eacf96417
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f637e1f744ec412899320cfbb368633b222da8d3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718960"
---
# <a name="assoc"></a>assoc

ファイル名拡張子の関連付けを表示または変更します。 パラメーターを指定せずに使用した場合、 **assoc**は、現在のファイル名拡張子のすべての関連付けの一覧を表示します。

> [!NOTE]
> このコマンドは、CMD 内でのみサポートされています。EXE とは、PowerShell からは使用できません。

## <a name="syntax"></a>構文

```
assoc [<.ext>[=[<filetype>]]]
```

### <a name="parameters"></a>パラメーター

| パラメーター | [説明] |
| --------- | ----------- |
| `<.ext>` | ファイル名拡張子を指定します。 |
| `<filetype>` | 指定したファイル名拡張子に関連付けるファイルの種類を指定します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

### <a name="remarks"></a>Remarks

- ファイル名拡張子のファイルの種類の関連付けを削除するには、SPACE キーを押して等号の後に空白を追加します。

- 開いているコマンド文字列が定義されている現在のファイルの種類を表示するには、 **ftype**コマンドを使用します。

- **Assoc**の出力をテキストファイルにリダイレクトするには、 `>`リダイレクト演算子を使用します。

## <a name="examples"></a>例

ファイル名拡張子 .txt の現在のファイルの種類の関連付けを表示するには、次のように入力します。

```
assoc .txt
```

ファイル名拡張子が .bak のファイルの種類の関連付けを削除するには、次のように入力します。

```
assoc .bak= 
```

> [!NOTE]
> 等号の後にスペースを追加してください。

**Assoc** 1 画面の出力を一度に表示するには、次のように入力します。

```
assoc | more
```

**Assoc**の出力をファイルに送信するには、次のように入力します。

```
assoc>assoc.txt
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ftype コマンド](ftype.md)
