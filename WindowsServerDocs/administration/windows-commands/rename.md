---
title: rename
description: '[名前の変更] コマンドの参照記事。ファイルまたはディレクトリの名前を変更します。'
ms.topic: article
ms.assetid: 7f2ea658-0fa9-4015-8031-22c2b0089231
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a2ab634be010f470314658b25daac92c00d4706c
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883794"
---
# <a name="rename"></a>rename

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ファイルまたはディレクトリの名前を変更します。

> [!NOTE]
> このコマンドは、 [ren コマンド](ren.md)と同じです。

## <a name="syntax"></a>構文

```
rename [<drive>:][<path>]<filename1> <filename2>
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
|--|--|
| `[<drive>:][<path>]<filename1>` | 名前を変更するファイルまたはファイルのセットの場所と名前を指定します。 *Filename1*には、ワイルドカード文字 (**&#42;** と **?**) を含めることができます。 |
| `<filename2>` | ファイルの新しい名前を指定します。 ワイルドカード文字を使用すると、複数のファイルに新しい名前を指定できます。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>Remarks

- ファイルの名前を変更するときに、新しいドライブまたはパスを指定することはできません。 また、このコマンドを使用して、ドライブ間でファイルの名前を変更したり、ファイルを別のディレクトリに移動したりすることはできません。

- *Filename2*のワイルドカード文字によって表される文字は、 *filename1*内の対応する文字と同じになります。

- *Filename2*は一意のファイル名である必要があります。 *Filename2*が既存のファイル名と一致する場合、次のメッセージが表示され `Duplicate file name or file not found` ます。

### <a name="examples"></a>例

現在のディレクトリにあるすべての .txt ファイル名拡張子を .doc 拡張子に変更するには、次のように入力します。

```
rename *.txt *.doc
```

ディレクトリの名前を*Chap10*から*Part10*に変更するには、次のように入力します。

```
rename chap10 part10
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [ren コマンド](ren.md)
