---
title: assoc
description: '**Assoc**の Windows コマンドのトピック-ファイル名拡張子の関連付けを表示または変更します。'
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 237bedda-b24c-4fec-a39c-9b7eacf96417
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e4a6fd700cbe66897a24f01f66387e76e07b568b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71382672"
---
# <a name="assoc"></a>assoc



ファイル名拡張子の関連付けを表示または変更します。 パラメーターを指定せずに使用した場合、 **assoc**は、現在のファイル名拡張子のすべての関連付けの一覧を表示します。

> [!NOTE]
> このコマンドは、CMD 内でのみサポートされています。EXE とは、PowerShell からは使用できません。
>

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
assoc [<.ext>[=[<FileType>]]]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|< ext >|ファイル名拡張子を指定します。|
|\<の FileType >|指定したファイル名拡張子に関連付けるファイルの種類を指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   ファイル名拡張子のファイルの種類の関連付けを削除するには、SPACE キーを押して等号の後に空白を追加します。
-   開いているコマンド文字列が定義されている現在のファイルの種類を表示するには、 **ftype**コマンドを使用します。
-   **Assoc**の出力をテキストファイルにリダイレクトするには、 **>** リダイレクト演算子を使用します。

## <a name="BKMK_examples"></a>例

ファイル名拡張子 .txt の現在のファイルの種類の関連付けを表示するには、次のように入力します。
```
assoc .txt
```
ファイル名拡張子が .bak のファイルの種類の関連付けを削除するには、次のように入力します。
```
assoc .bak= 
```

> [!NOTE]
> 等号の後にスペースを追加してください。

**Assoc** 1 画面の出力を一度に表示するには、次のように入力します。
```
assoc | more
```
**Assoc**の出力をファイルに送信するには、次のように入力します。
```
assoc>assoc.txt
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)
