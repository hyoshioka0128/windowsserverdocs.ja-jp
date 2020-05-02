---
title: date
description: システム日付を表示または設定する日付の参照トピックです。 パラメーターを指定せずに使用する場合は、
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ce6700fb-32f9-4350-a1af-5aee61d4448c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d7bcdb35579ac86b4ec7f9c7c639cf905f6a05fa
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82716805"
---
# <a name="date"></a>date

システム日付を表示または設定します。 パラメーターを指定せずに使用した場合、**日付**には現在のシステム日付の設定が表示され、新しい日付を入力するように求められます。



## <a name="syntax"></a>構文

```
date [/t | <Month-Day-Year>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<月-日の>|指定された日付を設定します。 *month*は月 (1 桁または2桁)、 *day*は日 (1 桁または2桁)、*年*は年 (2 桁または4桁) です。|
|/t|新しい日付を求めるメッセージを表示せずに現在の日付を表示します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>Remarks

-   現在の日付を変更するには、管理者の資格情報が必要です。
-   *月*、*日*、および*年*の値は、ピリオド (.)、ハイフン (-)、またはスラッシュ (/) で区切る必要があります。
-   有効な*月*の値は 1 ~ 12 です。
-   有効な*日付*の値は 1 ~ 31 です。
-   有効な*年*の値は、00 ~ 99、1980 ~ 2099 のいずれかです。 2桁の数字を使用する場合、80 ~ 99 の値は、1980から1999までの年数に対応します。

## <a name="examples"></a>例

コマンド拡張機能が有効になっている場合、現在のシステム日付を表示するには、次のように入力します。
```
date /t
```
現在のシステム日付を2007年8月3日に変更するには、次のいずれかを入力します。
```
date 08.03.2007
date 08-03-07
date 8/3/07
```
現在のシステム日付を表示し、その後に新しい日付を入力するプロンプトを表示するには、次のように入力します。
```
The current date is: Mon 04/02/2007
Enter the new date: (mm-dd-yy)
```
現在の日付を保持し、コマンドプロンプトに戻るには、enter キーを押します。 現在の日付を変更するには、新しい日付を入力し、enter キーを押します。

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)