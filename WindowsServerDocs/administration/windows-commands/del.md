---
title: del
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 6e569443a56646862c7a2c9fbd2c599cede941a1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378703"
---
# <a name="del"></a>del



1つ以上のファイルを削除します。 このコマンドは、 **erase**コマンドと同じです。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
del [/p] [/f] [/s] [/q] [/a[:]<Attributes>] <Names>
erase [/p] [/f] [/s] [/q] [/a[:]<Attributes>] <Names>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<Names >|1つ以上のファイルまたはディレクトリのリストを指定します。 複数のファイルを削除するには、ワイルドカードを使用できます。 ディレクトリを指定すると、ディレクトリ内のすべてのファイルが削除されます。|
|/p|指定されたファイルを削除する前に確認メッセージを表示します。|
|/f|読み取り専用ファイルを強制的に削除します。|
|/s|現在のディレクトリとすべてのサブディレクトリから、指定されたファイルを削除します。 削除中のファイルの名前が表示されます。|
|/q|クワイエット モードを指定します。 削除の確認を求めるメッセージは表示されません。|
|/a [:] \<Attributes >|次のファイル属性に基づいてファイルを削除します。</br>**r** 読み取り専用ファイル</br>**h** ファイルを非表示</br>**i** コンテンツ インデックス付きのファイルがありません</br>**s** システム ファイル</br>**a** アーカイブ ファイル</br>**l** 再解析ポイント</br>-Prefix は ' not ' を意味します|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント

> [!CAUTION]
> **Del**を使用してディスクからファイルを削除した場合、そのファイルを取得することはできません。
> -   **/P**を使用する場合、 **del**はファイルの名前を表示し、次のメッセージを送信します。

    `FileName, Delete (Y/N)?`

    To confirm the deletion, press Y. To cancel the deletion and display the next file name (that is, if you specified a group of files), press N. To stop the **del** command, press CTRL+C.
- コマンド拡張機能を無効にすると、削除されているファイルの名前を表示する代わりに、見つからなかったファイルの名前が **/s**によって表示されます (つまり、動作が逆になります)。
- *名前*にフォルダーを指定すると、そのフォルダー内のすべてのファイルが削除されます。 たとえば、次のコマンドは、\ Work フォルダー内のすべてのファイルを削除します。  
  ```
  del \work
  ```  
- ワイルドカード ( **&#42;** と **?** ) を使用して、一度に複数のファイルを削除することができます。 ただし、誤ってファイルが削除されないようにするには、 **del**コマンドでワイルドカードを使用することをお勧めします。 たとえば、次のコマンドを入力したとします。  
  ```
  del *.*
  ```  
  **Del**コマンドを実行すると、次のプロンプトが表示されます。

  `Are you sure (Y/N)?`

  現在のディレクトリにあるすべてのファイルを削除するには、Y キーを押してから enter キーを押します。 削除を取り消すには、N キーを押してから enter キーを押します。

> [!NOTE]
> **Del**コマンドでワイルドカード文字を使用する前に、同じワイルドカード文字を**dir**コマンドと共に使用して、削除されるすべてのファイルを一覧表示します。
> -   異なるパラメーターを持つ**del**コマンドは、回復コンソールから使用できます。

## <a name="BKMK_examples"></a>例

C ドライブの Test という名前のフォルダー内のすべてのファイルを削除するには、次のいずれかを入力します。
```
del c:\test
del c:\test\*.*
```
現在のディレクトリから .bat ファイル名拡張子を持つすべてのファイルを削除するには、次のように入力します。
```
del *.bat
```
現在のディレクトリにあるすべての読み取り専用ファイルを削除するには、次のように入力します。
```
del /a:r *.*
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)
