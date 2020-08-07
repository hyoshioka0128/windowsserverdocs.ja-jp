---
title: date
description: システム日付を表示または設定する date コマンドの参照記事です。 パラメーターを指定せずに使用する場合は、
ms.topic: article
ms.assetid: ce6700fb-32f9-4350-a1af-5aee61d4448c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 8966f02a6902b6b2bccc6fdc6931485a86bd39fe
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87891515"
---
# <a name="date"></a>date

システム日付を表示または設定します。 パラメーターを指定せずに使用した場合、**日付**には現在のシステム日付の設定が表示され、新しい日付を入力するように求められます。

>[!IMPORTANT]
> このコマンドを使用するには、管理者である必要があります。

## <a name="syntax"></a>構文

```
date [/t | <month-day-year>]
```

### <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --------- | ----------- |
| `<month-day-year>` | 指定された日付を設定します。 *month*は月 (1 ~ 12 の値を含む1桁または2桁の数字)、 *day*は日 (1 ~ 31 の値を含む1桁または2桁)、*年*は年 (00 ~ 99 または 1980 ~ 2099 の値を含む2桁または4桁) です。 *月*、*日*、および*年*の値は、ピリオド (.)、ハイフン (-)、またはスラッシュ (/) で区切る必要があります。<p>**注:** 年を表すために2桁を使用する場合、値80-99 は1980から1999に対応します。 |
| /t | 新しい日付を求めるメッセージを表示せずに現在の日付を表示します。 |
| /? | コマンド プロンプトにヘルプを表示します。 |

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
Enter the new date: (mm-dd-yyyy)
```

現在の日付を保持し、コマンドプロンプトに戻るには、 **enter キーを**押します。 現在の日付を変更するには、新しい日付を入力し **、enter キーを押します。**

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)