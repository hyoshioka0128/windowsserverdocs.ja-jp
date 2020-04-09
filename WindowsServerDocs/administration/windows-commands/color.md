---
title: 色
description: Windows コマンドの色に関するトピック。現在のセッションのコマンドプロンプトウィンドウで、前景色と背景色を変更します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: f5b67131-d196-45ec-a3f9-b5d9f091fd86
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 0e89c20d90a3b812fa67b597c4c205d34e725785
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80847485"
---
# <a name="color"></a>色

現在のセッションのコマンドプロンプトウィンドウで、前景色と背景色を変更します。 パラメーターを指定せずに使用した場合、既定のコマンドプロンプトウィンドウの前景色と背景色が元の**色**に戻ります。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
color [[<B>]<F>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<B >|背景色を指定します。|
|\<F >|前景色を指定します。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント

-   次の表に、 *B*と*F*の値として使用できる有効な16進数の数字を示します。

|値|色|
|-----|-----|
|0|Black|
|1|青|
|2|緑|
|3|アクア|
|4|赤|
|5|紫|
|6|黄|
|7|白|
|8|灰色|
|9|薄い青|
|A|明るい緑|
|B|水色|
|C|薄い赤|
|D|淡い紫|
|E|薄い黄色|
|F|明るい白|
    
-   *B*と*F*の間には空白文字を使用しないでください。
-   16進数字を1つだけ指定した場合、対応する色が前景色として使用され、背景色が既定の色に設定されます。
-   既定のコマンドプロンプトウィンドウの色を設定するには、コマンドプロンプトウィンドウの左上隅をクリックし、 **[既定]** をクリックします。次に、 **[色]** タブをクリックし、**画面のテキスト**と画面の**背景**に使用する色をクリックします。
-   *B*と*F*が同じである場合、 **color**コマンドを実行すると ERRORLEVEL が1に設定され、前景色または背景色は変更されません。

## <a name="examples"></a><a name=BKMK_examples></a>例

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
