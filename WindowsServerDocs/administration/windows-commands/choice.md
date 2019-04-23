---
title: choice
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c65a9119-410b-4dcf-9fa7-4e07d2a7238b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 78d2816bff754ef04558cf37eaada7c7fafba823
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841553"
---
# <a name="choice"></a>choice



バッチ プログラムでは、1 文字の選択肢の一覧から 1 つの項目を選択するよう求めるし、選択された項目のインデックスを返します。 パラメーターを指定せずに使用されている場合**選択肢**既定の選択肢を表示**Y**と**N**します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
choice [/c [<Choice1><Choice2><…>]] [/n] [/cs] [/t <Timeout> /d <Choice>] [/m <"Text">]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/c \<Choice1 ><Choice2><.>|作成する選択肢の一覧を指定します。 有効な選択肢には、a ~ z、A ~ Z、0 ~ 9、および拡張 ASCII 文字 (128 254) が含まれます。 既定の一覧は、"YN"として表示される`[Y,N]?`します。|
|/n|選択肢の一覧を非表示に選択肢がまだ有効になっていますとメッセージ テキスト (で指定された場合 **/m**) が引き続き表示されます。|
|/cs|選択が区別されるかを指定します。 既定では、選択肢は区別されません。|
|/t\<タイムアウト >|指定された既定のオプションを使用する前に一時停止する秒数を指定します **/d**します。 許容される値は、 **0**に**9999**します。 場合 **/t**に設定されている**0**、**選択肢**の既定の選択肢を返す前に一時停止しません。|
|/d\<選択 >|指定された秒数を待機した後に使用する既定の選択肢を指定します **/t**します。 指定された選択肢の一覧で、既定の選択肢があります。 **/c**します。|
|/m <"text">|選択肢の一覧の前に表示するメッセージを指定します。 場合 **/m**が指定されていない、選択したメッセージのみが表示されます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   ERRORLEVEL 環境変数は、ユーザーが、選択肢の一覧から選択したキーのインデックスに設定されます。 最初の選択肢の一覧では、1、2 の値を 2 つ目の値を返します。 選択が有効でないキーを押した場合**選択肢**鳴らします。 場合**選択肢**、エラー状態を検出した ERRORLEVEL 255 の値が返されます。 CTRL + BREAK または CTRL + C を押す場合**選択肢**ERRORLEVEL の値が 0 を返します。

> [!NOTE]
> バッチ プログラムで ERRORLEVEL の値を使用する場合は、降順で一覧表示します。

## <a name="BKMK_examples"></a>例

Y、N、および C の選択肢を表示するには、バッチ ファイルで、次の行を入力します。
```
choice /c ync
```
バッチ ファイルを実行すると、次のプロンプトが表示されます、**選択肢**コマンド。
```
[Y,N,C]?
```
テキストを表示し、Y、N、C、選択肢を非表示にする"はい、No、または Continue"、バッチ ファイルで次の行を入力します。
```
choice /c ync /n /m "Yes, No, or Continue?"
```
バッチ ファイルを実行すると、次のプロンプトが表示されます、**選択肢**コマンド。
```
Yes, No, or Continue?
```

> [!NOTE]
> 使用する場合、 **/n**パラメーターは使用しない **/m**、ユーザーがいない通知を受ける場合**選択肢**は入力を待機しています。

テキストと前の例で使用するオプションの両方を表示するには、バッチ ファイルで、次の行を入力します。
```
choice /c ync /m "Yes, No, or Continue"
```
バッチ ファイルを実行すると、次のプロンプトが表示されます、**選択肢**コマンド。
```
Yes, No, or Continue [Y,N,C]?
```
5 秒の制限時間を設定し、指定**N**既定値として、バッチ ファイルで次の行を入力します。
```
choice /c ync /t 5 /d n
```
バッチ ファイルを実行すると、次のプロンプトが表示されます、**選択肢**コマンド。
```
[Y,N,C]?
```

> [!NOTE]
> 、5 秒内で、ユーザーがキーを押していない場合、この例では**選択肢**選択**N**既定では 2 のエラー値を返します。 それ以外の場合、**選択肢**ユーザーの選択に対応する値を返します。

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)