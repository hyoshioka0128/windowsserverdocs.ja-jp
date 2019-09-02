---
title: del
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 346eede2-2085-44f5-9936-6877b5d5a833
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b10da1a6035155d525a516f35f83a25209e90075
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433891"
---
# <a name="del"></a>del



1 つまたは複数のファイルを削除します。 このコマンドと同じ、**消去**コマンド。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
del [/p] [/f] [/s] [/q] [/a[:]<Attributes>] <Names>
erase [/p] [/f] [/s] [/q] [/a[:]<Attributes>] <Names>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<名 >|1 つまたは複数のファイルまたはディレクトリの一覧を指定します。 ワイルドカードを使用して、複数のファイルを削除することがあります。 ディレクトリが指定されている場合は、ディレクトリ内のすべてのファイルが削除されます。|
|/p|指定したファイルを削除する前に確認が求められます。|
|/f|読み取り専用ファイルを削除します。|
|/s|指定された現在のディレクトリとすべてのサブディレクトリからファイルを削除します。 削除されているファイルの名前が表示されます。|
|/q|クワイエット モードを指定します。 削除の確認は求められません。|
|/a[:]\<Attributes>|次のファイル属性に基づいてファイルを削除します。</br>**r** 読み取り専用ファイル</br>**h** ファイルを非表示</br>**i** コンテンツ インデックス付きのファイルがありません</br>**s** システム ファイル</br>**a** アーカイブ ファイル</br>**l** 再解析ポイント</br>-"Not"を意味をプレフィックスします。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

> [!CAUTION]
> 使用する場合**del**をディスクからファイルを削除する、それを取得できません。
> -   使用する場合 **/p**、 **del**ファイルの名前を表示し、次のメッセージを送信します。

    `FileName, Delete (Y/N)?`

    To confirm the deletion, press Y. To cancel the deletion and display the next file name (that is, if you specified a group of files), press N. To stop the **del** command, press CTRL+C.
- コマンド拡張機能を無効にした場合 **/s**が削除されているファイルの名前を表示する代わりに見つからなかったファイルの名前が表示されます (つまり、動作が取り消されます)。
- 内のフォルダーを指定する場合*名*フォルダー内のファイルがすべて削除されます。 たとえば、次のコマンドでは、すべて \Work フォルダー内のファイルの削除されます。  
  ```
  del \work
  ```  
- ワイルドカードを使用することができます ( **&#42;** と **?** )、一度に 1 つ以上のファイルを削除します。 ただし、ファイルが誤って削除されないようにには使用注意が必要では、ワイルドカード、 **del**コマンド。 たとえば、次のコマンドを入力するとします。  
  ```
  del *.*
  ```  
  **Del**コマンドには、次のプロンプトが表示されます。

  `Are you sure (Y/N)?`

  すべての現在のディレクトリにファイルを削除するには、Y キーを押し、し、ENTER キーを押します。 削除を取り消す場合に、N キーを押すと、キーを押しますを入力します。

> [!NOTE]
> ワイルドカード文字を使用する前に、 **del**コマンドを使用して同じワイルドカード文字を使用して、 **dir**コマンドが削除されるすべてのファイルを一覧表示します。
> -   **Del**コマンドで他のパラメーターは、回復コンソールから利用できます。

## <a name="BKMK_examples"></a>例

ドライブ C 上のテストをという名前のフォルダー内のすべてのファイルを削除するには、次のいずれかを入力します。
```
del c:\test
del c:\test\*.*
```
.Bat ファイル名拡張子を持つすべてのファイルを現在のディレクトリから削除するには、次のように入力します。
```
del *.bat
```
現在のディレクトリ内のすべての読み取り専用ファイルを削除するには、次のように入力します。
```
del /a:r *.*
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)
