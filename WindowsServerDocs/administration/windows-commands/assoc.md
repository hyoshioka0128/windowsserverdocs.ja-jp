---
title: assoc
description: Windows コマンド」のトピック**assoc** -表示またはファイル名拡張子の関連付けを変更します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: d893167081b66c81366b59613c52182a4ddba370
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816643"
---
# <a name="assoc"></a>assoc



表示またはファイル名拡張子の関連付けを変更します。 パラメーターを指定せずに使用されている場合**assoc**すべて現在ファイル名拡張子の関連付けの一覧を表示します。

> [!NOTE]
> このコマンドは cmd. 内でのみサポートされています。EXE は PowerShell から使用できません。
>

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
assoc [<.ext>[=[<FileType>]]]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|<.ext>|ファイル名拡張子を指定します。|
|\<FileType>|指定したファイル名拡張子に関連付けるファイルの種類を指定します。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

-   ファイル名拡張子のファイルの種類の関連付けを削除するには、スペースバーを押して等号の後に空白文字を追加します。
-   開いているコマンド文字列が定義されている現在のファイルの種類を表示する、 **ftype**コマンド。
-   出力をリダイレクトする**assoc** 、テキスト ファイルを使用して、 **>** リダイレクト演算子。

## <a name="BKMK_examples"></a>例

ファイル名拡張子が .txt の現在のファイル種類の関連付けを表示するには、次のように入力します。
```
assoc .txt
```
ファイル名 .bak の拡張子のファイルの種類の関連付けを削除するには、次のように入力します。
```
assoc .bak= 
```

> [!NOTE]
> 等号の後にスペースを追加してください。

出力を表示する**assoc**型、一度に 1 つの画面。
```
assoc | more
```
出力を送信する**assoc**ファイル assoc.txt を入力します。
```
assoc>assoc.txt
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)
