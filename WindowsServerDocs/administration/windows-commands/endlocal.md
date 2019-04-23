---
title: endlocal
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 765fae3c-0c0a-4639-99a4-cf613489b949
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3e516b2bf9e8a45ada910dfbd93e3ed5e7d86c14
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862143"
---
# <a name="endlocal"></a>endlocal



バッチ ファイルでは、環境の変更のローカライズを終了し、対応する環境変数を値に戻します**setlocal**コマンドが実行されました。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
endlocal
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   **Endlocal**コマンド スクリプトまたはバッチ ファイルの外部効果がありません。
-   暗黙的な**endlocal**バッチ ファイルの末尾にあるコマンド。
-   コマンド拡張機能が有効になっている場合 (コマンド拡張機能は、既定で有効には、)、 **endlocal**コマンドでは、コマンド拡張機能 (つまり、有効または無効) の状態を復元すると、対応する前に、の**setlocal**コマンドが実行されました。

> [!NOTE]
> 有効にして、コマンド拡張機能を無効化の詳細については、次を参照してください。 [Cmd](cmd.md)します。

## <a name="BKMK_examples"></a>例

バッチ ファイルで環境変数をローカライズすることができます。 たとえば、次のプログラム superapp バッチ プログラムをネットワークで起動する、出力ファイルを転送し、メモ帳でファイルが表示されます。
```
@echo off
setlocal
path=g:\programs\superapp;%path%
call superapp>c:\superapp.out
endlocal
start notepad c:\superapp.out
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)