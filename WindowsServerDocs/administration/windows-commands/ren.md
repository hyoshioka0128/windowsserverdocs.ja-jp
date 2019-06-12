---
title: ren
description: ファイルまたは ren コマンドで、ディレクトリの名前を変更する方法について説明します。
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 34c761cb08916d277f8f7f1c58d57a05ed2c8daf
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441814"
---
# <a name="ren"></a>ren

ファイルまたはディレクトリの名前を変更します。 このコマンドと同じ、**の名前を変更**コマンド。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
ren [<Drive>:][<Path>]<FileName1> <FileName2>
rename [<Drive>:][<Path>]<FileName1> <FileName2>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|[\<ドライブ >:] [\<パス >]\<FileName1 >|名前を変更するファイルの場所とファイルの名前を指定します。 *FileName1*ワイルドカード文字を含めることができます ( **&#42;** と **?** )。|
|\<FileName2>|ファイルの新しい名前を指定します。 複数のファイルの新しい名前を指定するのにワイルドカード文字を使用することができます。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

- ファイルの名前を変更するときに、新しいドライブまたはパスを指定できません。
- 使用することはできません、 **ren**コマンドのドライブでファイルの名前を変更する、または別のディレクトリにファイルを移動します。
- ワイルドカード文字を使用することができます ( **&#42;** と **?** ) いずれかで*FileName*パラメーター。 ワイルドカード文字で表される文字*FileName2*内の対応する文字と同じになる*FileName1*します。
- *FileName2*一意のファイル名にする必要があります。 場合*FileName2*既存のファイル名と一致する**ren**次のメッセージが表示されます。  
  ```
  Duplicate file name or file not found
  ```

## <a name="BKMK_examples"></a>例

すべてを変更するには、.doc の拡張機能に現在のディレクトリ内の .txt ファイル名拡張子を入力します。
```
ren *.txt *.doc 
```
Part10 に Chap10 からディレクトリの名前を変更するには、次のように入力します。
```
ren chap10 part10 
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)