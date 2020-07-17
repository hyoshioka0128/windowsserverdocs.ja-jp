---
title: color
description: 現在のセッションのコマンドプロンプトウィンドウで、前景色と背景色を変更する color コマンドの参照記事。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f5b67131-d196-45ec-a3f9-b5d9f091fd86
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 93c51fdbf1909adfda06730c3a517f602f8024b8
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85929805"
---
# <a name="color"></a>color

現在のセッションのコマンドプロンプトウィンドウで、前景色と背景色を変更します。 パラメーターを指定せずに使用した場合、既定のコマンドプロンプトウィンドウの前景色と背景色が元の**色**に戻ります。

## <a name="syntax"></a>構文

```
color [[<b>]<f>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<b>` | 背景色を指定します。 |
| `<f>` | 前景色を指定します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

各値の説明:

次の表に、およびの値として使用できる有効な16進数の数字を示し `<b>` `<f>` ます。

| 値 | 色 |
| ----- | ----- |
| 0 | Black |
| 1 | 青 |
| 2 | [緑] |
| 3 | Aqua |
| 4 | 赤 |
| 5 | パープル |
| 6 | 黄 |
| 7 | White |
| 8 | グレー |
| 9 | 薄い青 |
| a | 明るい緑 |
| b | 水色 |
| c | 薄い赤 |
| d | 淡い紫 |
| e | 薄い黄色 |
| f | 明るい白 |

#### <a name="remarks"></a>注釈

- との間には空白文字を使用しないで `<b>` `<f>` ください。

- 16進数字を1つだけ指定した場合、対応する色が前景色として使用され、背景色が既定の色に設定されます。

- 既定のコマンドプロンプトウィンドウの色を設定するには、**コマンドプロンプト**ウィンドウの左上隅を選択し、[**既定**] を選択し、[**色**] タブを選択して、画面の**テキスト**と**画面の背景**に使用する色を選択します。

- `<b>`と `<f>` が同じ色の値の場合、ERRORLEVEL はに設定され、 `1` 前景色または背景色は変更されません。

## <a name="examples"></a>例

コマンドプロンプトウィンドウの背景色をグレーに、前景色を赤に変更するには、次のように入力します。

```
color 84
```

コマンドプロンプトウィンドウの前景色を明るい黄色に変更するには、次のように入力します。

```
color e
```

> [!NOTE]
> この例では、1つの16進数のみが指定されているため、背景が既定の色に設定されています。

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
