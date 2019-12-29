---
title: color
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5b67131-d196-45ec-a3f9-b5d9f091fd86
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ed792e4626897945e688f1c54767d7680ade6d99
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379241"
---
# <a name="color"></a>color



現在のセッションのコマンドプロンプトウィンドウで、前景色と背景色を変更します。 パラメーターを指定せずに使用した場合、既定のコマンドプロンプトウィンドウの前景色と背景色が元の**色**に戻ります。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
color [[<B>]<F>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<B >|背景色を指定します。|
|\<F >|前景色を指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント

-   次の表に、有効な 16 進数の値として使用できる*B*と*F*します。

|値|色|
|-----|-----|
|0|黒|
|1|青|
|2|[緑]|
|3|アクア|
|4|[赤]|
|5|ひし|
|6|黄|
|7|White|
|8|灰色|
|9|薄い青|
|A|明るい緑|
|B|水色|
|c|薄い赤|
|D|淡い紫|
|E|薄い黄色|
|F|明るい白|
    
-   *B*と*F*の間には空白文字を使用しないでください。
-   16進数字を1つだけ指定した場合、対応する色が前景色として使用され、背景色が既定の色に設定されます。
-   コマンドプロンプトウィンドウの既定の色を設定するには、コマンドプロンプトウィンドウの左上隅をクリックし、 **[既定]** をクリックします。次に、 **[色]** タブをクリックし、**画面のテキスト**と画面の背景に使用する色をクリックします。.
-   *B*と*F*が同じである場合、 **color**コマンドを実行すると ERRORLEVEL が1に設定され、前景色または背景色は変更されません。

## <a name="BKMK_examples"></a>例

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

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)
