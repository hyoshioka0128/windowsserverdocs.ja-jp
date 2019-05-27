---
title: color
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: f8d23cc1bb5739b47c755d90c927cbcf82b8da7f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59825023"
---
# <a name="color"></a>color



前景色と背景の変更は、コマンド プロンプト ウィンドウで、現在のセッションの色します。 パラメーターを指定せずに使用されている場合**色**既定のコマンド プロンプト ウィンドウ前景色と背景色を復元します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
color [[<B>]<F>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<B &GT;|背景色を指定します。|
|\<F &GT;|前景色を指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   次の表に、有効な 16 進数の値として使用できる*B*と*F*します。  
    |Value|色|
    |-----|-----|
    |0|黒|
    |1|青|
    |2|[緑]|
    |3|Aqua|
    |4|[赤]|
    |5|紫色|
    |6|黄|
    |7|White|
    |8|灰色|
    |9|薄い青|
    |A|明るい緑|
    |B|明るい水色|
    |C|淡い赤|
    |D|ライトの紫|
    |E|淡い黄色|
    |F|明るいホワイト|
-   間のスペース文字は使用しないでください*B*と*F*します。
-   16 進数字の 1 つだけを指定すると、対応する色は、前景色として使用し、背景色が既定の色に設定。
-   コマンド プロンプト ウィンドウの既定の色を設定するには、コマンド プロンプト ウィンドウの左上隅をクリックし**の既定値**、 をクリックして、**色**タブをクリックし、を使用する色をクリックします。**テキストを画面**と**画面の背景**します。
-   場合*B*と*F*は同じで、**色**コマンド ERRORLEVEL を 1 に設定して、前景色または背景色のいずれかに変更は行われません。

## <a name="BKMK_examples"></a>例

灰色と前景の色を赤にするには、コマンド プロンプト ウィンドウの背景色を変更するに次のように入力します。
```
color 84
```
コマンド プロンプト ウィンドウの前景色の色を淡い黄色に変更するに次のように入力します。
```
color e
```

> [!NOTE]
> この例で 16 進数字の 1 つだけが指定されているために、バック グラウンドが既定の色に設定します。

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)