---
title: ren
description: Ren コマンドを使用してファイルまたはディレクトリの名前を変更する方法について説明します。
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 60398e12-a05d-4524-a73a-0a925943e21d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 2ba3f6a13dc03c0b6a5561be9f0f692546a25149
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384579"
---
# <a name="ren"></a>ren

ファイルまたはディレクトリの名前を変更します。 このコマンドは、[名前の**変更**] コマンドと同じです。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
ren [<Drive>:][<Path>]<FileName1> <FileName2>
rename [<Drive>:][<Path>]<FileName1> <FileName2>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[\<Drive >:][\<Path >] \<FileName1 >|名前を変更するファイルまたはファイルのセットの場所と名前を指定します。 *FileName1*には、ワイルドカード **&#42;** 文字 (および **?** ) を含めることができます。|
|\<FileName2 >|ファイルの新しい名前を指定します。 ワイルドカード文字を使用すると、複数のファイルに新しい名前を指定できます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント

- ファイルの名前を変更するときに、新しいドライブまたはパスを指定することはできません。
- **Ren**コマンドを使用して、ドライブ間でファイルの名前を変更したり、ファイルを別のディレクトリに移動したりすることはできません。
- どちらの FileName パラメーターでも **&#42;** 、ワイルドカード文字 (および **?** ) を使用できます。 *FileName2*のワイルドカード文字によって表される文字は、 *FileName1*内の対応する文字と同じになります。
- *FileName2*は一意のファイル名である必要があります。 *FileName2*が既存のファイル名と一致する場合は、次のメッセージ**が表示さ**れます。  
  ```
  Duplicate file name or file not found
  ```

## <a name="BKMK_examples"></a>例

現在のディレクトリにあるすべての .txt ファイル名拡張子を .doc 拡張子に変更するには、次のように入力します。
```
ren *.txt *.doc 
```
ディレクトリの名前を Chap10 から Part10 に変更するには、次のように入力します。
```
ren chap10 part10 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)