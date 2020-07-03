---
title: その他
description: '[その他] コマンドのリファレンス記事。一度に1つの出力画面が表示されます。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ded14f6a-d82f-4aeb-a2d8-7ec1c94dfb8f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/26/2019
ms.openlocfilehash: fec0ffbd7f2ce5d1efe1953cb4ab283d33f06ec8
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935730"
---
# <a name="more"></a>その他

一度に1つの出力画面を表示します。

> [!NOTE]
> パラメーターの**数**が異なるコマンドは、回復コンソールからも使用できます。

## <a name="syntax"></a>構文

```
<command> | more [/c] [/p] [/s] [/t<n>] [+<n>]
more [[/c] [/p] [/s] [/t<n>] [+<n>]] < [<drive>:][<path>]<filename>
more [/c] [/p] [/s] [/t<n>] [+<n>] [<files>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<command>` | 出力を表示するコマンドを指定します。 |
| /c | ページを表示する前に画面をクリアします。 |
| /p | フォームフィード文字を展開します。 |
| /s | 複数の空白行を1つの空白行として表示します。 |
| /t`<n>` | *N*で指定したスペースの数としてタブを表示します。 |
| +`<n>` | *N*で指定した行から始まる最初のファイルを表示します。 |
| `[<drive>:][<path>]<filename>` | 表示するファイルの場所と名前を指定します。 |
| `<files>` | 表示するファイルの一覧を指定します。 ファイルは、スペースを使用して区切る必要があります。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>注釈

- 次のサブコマンドは、**より多く**のプロンプト () で受け入れられ `-- More --` ます。

    | Key | アクション |
    | --- | ------ |
    | Space キー | **Space**キーを押すと、次の画面が表示されます。 |
    | Enter | **Enter**キーを押して、一度に1行ずつファイルを表示します。 |
    | f | **F**キーを押して、コマンドラインに表示されている次のファイルを表示します。 |
    | q | **Q**キーを押して、 **more**コマンドを終了します。 |
    | = | 行番号を表示します。 |
    | irtran-p`<n>` | **P**キーを押して次の*n*行を表示します。 |
    | 2$s`<n>` | 次の*n*行をスキップするには、 **S**キーを押します。 |
    | ? | 押し**ますか?** を選択すると、**より多く**のプロンプトで使用できるコマンドが表示されます。|

- リダイレクト文字 () を使用する場合は、 `<` ファイル名もソースとして指定する必要があります。

- パイプ () を使用する場合は、 `|` **dir**、 **sort**、 **type**などのコマンドを使用できます。

### <a name="examples"></a>例

Clients という名前のファイルの情報の最初の画面を表示するには、次のいずれかのコマンドを入力します *。*

```
more < clients.new
type clients.new | more
```

**More**コマンドを実行すると、クライアントからの情報の最初の画面が表示されます。 space キーを押すと、次の画面に情報が表示されます。

ファイルクライアントを表示する前に画面をクリアし、余分な空白行をすべて削除するには、次のいずれかのコマンドを入力します *。*

```
more /c /s < clients.new
type clients.new | more /c /s
```

現在の行番号を表示するには、**次のように入力します**。

```
more =
```

現在の行番号が、**より多く**のプロンプトに追加されます。`-- More [Line: 24] --`

**より多く**のプロンプトで特定の行数を表示するには、次のように入力します。

```
more p
```

次のよう**に、表示**する行数を求めるプロンプトが表示され `-- More -- Lines:` ます。 表示する行数を入力し、enter キーを押します。 画面が変更され、その行数のみが表示されます。

**詳細**なプロンプトで特定の行数をスキップするには、次のように入力します。

```
more s
```

次のよう**に、スキップ**する行の数を求めるプロンプトが表示され `-- More -- Lines:` ます。 スキップする行数を入力し、enter キーを押します。 これらの行がスキップされたことを示すように画面が変更されます。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [Windows 回復環境 (WinRE)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference)
