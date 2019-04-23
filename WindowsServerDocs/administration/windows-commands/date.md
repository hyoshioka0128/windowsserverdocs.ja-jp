---
title: date
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce6700fb-32f9-4350-a1af-5aee61d4448c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e774f7bfabb9b574255691dd97d2cfff36f034e7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877953"
---
# <a name="date"></a>date



表示またはシステムの日付を設定します。 パラメーターを指定せずに使用されている場合**日付**設定の現在のシステム日付を表示し、新しい日付を入力するように求められます。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
date [/t | <Month-Day-Year>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<1 か月-日-年 >|指定すると、日付を設定*月*月 (1 つまたは 2 桁) は、*日*日 (1 つまたは 2 桁) と*年*は年 (2 または 4 桁)。|
|/t|新しい日付の入力を求めることがなく、現在の日付を表示します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   現在の日付を変更するには、管理者の資格情報があります。
-   値を区切る必要があります*月*、*日*、および*年*ピリオド (.)、ハイフン (-) またはスラッシュのマーク (/)。
-   有効な*月*値は 1 ~ 12 です。
-   有効な*日*値は 1 ~ 31 です。
-   有効な*年*値は 00 ~ 99 の場合、または 1980 2099 ~ のいずれか。 2 桁の数字を使用する場合、値 99 までからの 80 は 1980 1999 から年に対応します。

## <a name="BKMK_examples"></a>例

コマンド拡張機能が有効な場合は、現在のシステム日付を表示するを入力します。
```
date /t
```
2007 年 8 月 3 日に、現在のシステム日付を変更するには、次のいずれかを入力します。
```
date 08.03.2007
date 08-03-07
date 8/3/07
```
新しい日付を入力するプロンプトが後に、現在のシステム日付を表示するには、次のように入力します。
```
The current date is: Mon 04/02/2007
Enter the new date: (mm-dd-yy)
```
現在の日付を保持し、コマンド プロンプトに戻り、ENTER キーを押します。 現在の日付を変更するには、新しい日付を入力し、し、ENTER キーを押します。

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)