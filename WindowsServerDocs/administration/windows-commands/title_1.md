---
title: title
description: '[タイトル] の参照記事。コマンドプロンプトウィンドウのタイトルを作成します。'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: c0bbe8bd-201a-4b6c-b617-5d9809881dc8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 732a0de30b9495e6281248120d2a90f85734ad8b
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/02/2020
ms.locfileid: "85930057"
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

## <a name="remarks"></a>注釈

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