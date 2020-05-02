---
title: rem
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 1a45b585-a83c-4ff6-badd-ff40f34cec23
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d115548f15ff45087a771458062da8a3ef919eb3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722463"
---
# <a name="rem"></a>rem



バッチ ファイルまたは構成でレコードのコメント (注釈)。SYS です。 コメントが指定されていない場合 **rem** の上下の間隔を追加します。



## <a name="syntax"></a>構文

```
rem [<Comment>]
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<コメント>|コメントとして追加する文字の文字列を指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>Remarks

-   **Rem** コマンドは、画面にコメントを表示できません。 使用する必要があります、 **にエコー** コマンド、バッチ ファイルまたは構成を実行します。画面にコメントを表示する SYS ファイルです。
-   バッチファイルコメントにリダイレクト文字 (**<** また**>** は) または**|** パイプ () を使用することはできません。
-   使用できますが **rem** 、コメントの上下の間隔をバッチ ファイルに追加することがなく、空白行を使用することもできます。 バッチ ファイルが処理されるときに、空白行は無視されます。

## <a name="examples"></a>例

コメントと垂直方向の間隔に対して解説を使用するバッチファイルを表示するには、次のようにします。
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

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)