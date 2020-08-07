---
title: graftabl
description: Graftabl コマンドのリファレンス記事。 Windows オペレーティングシステムで、拡張文字セットをグラフィックモードで表示できるようにします。
ms.topic: article
ms.assetid: b08351d4-3d24-490c-86f6-1252da11d923
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cd20baaca94c13e725cf3121ba7a9f4f9f5524b1
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87888508"
---
# <a name="graftabl"></a>graftabl

Windows オペレーティングシステムで、拡張文字セットをグラフィックモードで表示できるようにします。 パラメーターを指定せずに**graftabl**を使用すると、前のコードページと現在のコードページが表示されます。

## <a name="syntax"></a>構文

```
graftabl <codepage>
graftabl /status
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<codepage>` | グラフィックスモードで拡張文字の外観を定義するコードページを指定します。 有効なコードページ id 番号は次のとおりです。<ul><li>**437** -米国</li><li>**850** -多言語 (ラテン I)</li><li>**852** -スラブ語 (ラテン II)</li><li>**855** -キリル語 (ロシア)</li><li>**857** -トルコ語</li><li>**860** -ポルトガル語</li><li>**861** -アイスランド語</li><li>**863** -カナダ-フランス語</li><li>**865** -北欧</li><li>**866** -ロシア語</li><li>**869** -モダンギリシャ語</li></ul> |
| /status | このコマンドによって使用されている現在のコードページを表示します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

#### <a name="remarks"></a>Remarks

- **Graftabl**コマンドは、指定したコードページの拡張文字のモニター表示にのみ影響します。 コンソールの実際の入力コードページは変更されません。 コンソールの入力コードページを変更するには、 [mode](mode.md)または[chcp](chcp.md)コマンドを使用します。

- 各終了コードとその簡単な説明を次に示します。

    | 終了コード | 説明 |
    | --------- | ----------- |
    | 0 | 文字セットが正常に読み込まれました。 前のコードページが読み込まれませんでした。 |
    | 1 | 正しくないパラメーターが指定されました。 何も処理されませんでした。 |
    | 2 | ファイルエラーが発生しました。 |

- バッチプログラムで ERRORLEVEL 環境変数を使用すると、 **graftabl**によって返される終了コードを処理できます。

### <a name="examples"></a>例

**Graftabl**によって使用される現在のコードページを表示するには、次のように入力します。

```
graftabl /status
```

コードページ 437 (米国) のグラフィックス文字セットをメモリに読み込むには、次のように入力します。

```
graftabl 437
```

コードページ 850 (多言語) のグラフィックス文字セットをメモリに読み込むには、次のように入力します。

```
graftabl 850
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

- [freedisk コマンド](freedisk.md)

- [モードコマンド](mode.md)

- [chcp コマンド](chcp.md)
