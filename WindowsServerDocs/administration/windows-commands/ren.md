---
title: ren
description: Ren コマンドを使用してファイルまたはディレクトリの名前を変更する方法について説明します。
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 60398e12-a05d-4524-a73a-0a925943e21d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 235497b09f44f9077b7f622f7f2b68a0bc49af86
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836045"
---
# <a name="ren"></a>ren

ファイルまたはディレクトリの名前を変更します。 このコマンドは、[名前の**変更**] コマンドと同じです。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
ren [<Drive>:][<Path>]<FileName1> <FileName2>
rename [<Drive>:][<Path>]<FileName1> <FileName2>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[\<ドライブ >:][\<パス >]\<FileName1 >|名前を変更するファイルまたはファイルのセットの場所と名前を指定します。 *FileName1*には、ワイルドカード **&#42;** 文字 (および **?** ) を含めることができます。|
|\<FileName2 >|ファイルの新しい名前を指定します。 ワイルドカード文字を使用すると、複数のファイルに新しい名前を指定できます。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント

- ファイルの名前を変更するときに、新しいドライブまたはパスを指定することはできません。
- **Ren**コマンドを使用して、ドライブ間でファイルの名前を変更したり、ファイルを別のディレクトリに移動したりすることはできません。
- どちらの FileName パラメーターでも **&#42;** 、ワイルドカード文字 ( *FileName*および **?** ) を使用できます。 *FileName2*のワイルドカード文字によって表される文字は、 *FileName1*内の対応する文字と同じになります。
- *FileName2*は一意のファイル名である必要があります。 *FileName2*が既存のファイル名と一致する場合は、次のメッセージ**が表示さ**れます。  
  ```
  Duplicate file name or file not found
  ```

## <a name="examples"></a><a name="BKMK_examples"></a>例

現在のディレクトリにあるすべての .txt ファイル名拡張子を .doc 拡張子に変更するには、次のように入力します。
```
ren *.txt *.doc 
```
ディレクトリの名前を Chap10 から Part10 に変更するには、次のように入力します。
```
ren chap10 part10 
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)