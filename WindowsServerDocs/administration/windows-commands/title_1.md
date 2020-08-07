---
title: title
description: '[タイトル] の参照記事。コマンドプロンプトウィンドウのタイトルを作成します。'
ms.topic: article
ms.assetid: c0bbe8bd-201a-4b6c-b617-5d9809881dc8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3fede3a0f71da2913e798852817722eaea414770
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/06/2020
ms.locfileid: "87881395"
---
# <a name="title"></a>title

コマンド プロンプト ウィンドウのタイトルを作成します。



## <a name="syntax"></a>構文

```
title [<String>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<String>|コマンド プロンプト ウィンドウのタイトルを指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>Remarks

-   バッチ プログラムのウィンドウのタイトルを作成するには、 **タイトル** バッチ ファイルの先頭にあるコマンドです。
-   ウィンドウのタイトルを設定した後のみを使用してリセットできます、 **タイトル** コマンドです。

## <a name="examples"></a>例

次のサンプルスクリプトでは、バッチファイルによって**copy**コマンドが実行されている間、コマンドプロンプトウィンドウのタイトルがファイルの更新に変更されます。 コマンドが実行されると、テキスト `Files Updated` が表示され、コマンドプロンプトウィンドウのタイトルがコマンドプロンプトに戻されます。
```
@echo off
title Updating Files
copy \\server\share\*.xls c:\users\common\*.xls
echo Files Updated.
title Command Prompt
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)