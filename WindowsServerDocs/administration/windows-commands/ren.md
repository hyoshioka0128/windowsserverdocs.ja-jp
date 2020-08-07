---
title: ren
description: ファイルまたはディレクトリの名前を変更する ren コマンドのリファレンス記事です。
ms.topic: article
ms.assetid: 60398e12-a05d-4524-a73a-0a925943e21d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: e21b521947ed02307c470932fffcf466016bae8b
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883805"
---
# <a name="ren"></a>ren

> 適用対象: Windows Server (半期チャネル)、Windows Server 2019、Windows Server 2016、Windows Server 2012 R2、Windows Server 2012

ファイルまたはディレクトリの名前を変更します。

> [!NOTE]
> このコマンドは、[名前の[変更] コマンド](rename.md)と同じです。

## <a name="syntax"></a>構文

```
ren [<drive>:][<path>]<filename1> <filename2>
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
ren *.txt *.doc
```

ディレクトリの名前を*Chap10*から*Part10*に変更するには、次のように入力します。

```
ren chap10 part10
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [rename コマンド](rename.md)
