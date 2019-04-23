---
title: rem
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1a45b585-a83c-4ff6-badd-ff40f34cec23
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 85c8a69bf21a386cd36e45bbca6dacd35aef2509
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847003"
---
# <a name="rem"></a>rem



バッチ ファイルまたは構成でレコードのコメント (注釈)。SYS です。 コメントが指定されていない場合 **rem** の上下の間隔を追加します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
rem [<Comment>]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<コメント >|コメントとして追加する文字の文字列を指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   **Rem** コマンドは、画面にコメントを表示できません。 使用する必要があります、 **にエコー** コマンド、バッチ ファイルまたは構成を実行します。画面にコメントを表示する SYS ファイルです。
-   リダイレクト文字を使用することはできません (**<** または **>**) またはパイプ (**|**) バッチ ファイルのコメントにします。
-   使用できますが **rem** 、コメントの上下の間隔をバッチ ファイルに追加することがなく、空白行を使用することもできます。 バッチ ファイルが処理されるときに、空白行は無視されます。

## <a name="BKMK_examples"></a>例

次の例は、コメント、および上下の間隔は、「解説」を使用するバッチ ファイルを示しています。
```
@echo off
rem  This batch program formats and checks new disks.
rem  It is named Checknew.bat.
rem
rem echo Insert new disk in Drive B.
pause 
format b: /v chkdsk b: 
```
前に説明のコメントを含めることを **プロンプト** 、config コマンドです。SYS ファイル、構成に次の行を追加します。システム ドライブ:
```
rem Set prompt to indicate current directory
prompt $p$g
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)