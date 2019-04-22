---
title: Md
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 82162d00-cc34-4776-9e55-4b4836dbd6a9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1396038410ecc5db5a124a1768038c4f8c8bea8c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820843"
---
# <a name="md"></a>Md



ディレクトリまたはサブディレクトリを作成します。

> [!NOTE]
> このコマンドと同じ、 **mkdir** コマンドです。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
md [<Drive>:]<Path>
mkdir [<Drive>:]<Path>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ドライブ >:|新しいディレクトリを作成するドライブを指定します。|
|\<パス >|必須。 新しいディレクトリの場所と名前を指定します。 1 つのパスの最大長は、ファイル システムによって決まります。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>注釈

既定で有効になっているコマンド拡張機能では、1 つを使用できます。 **md** 指定されたパスに中間ディレクトリを作成するコマンドです。

## <a name="BKMK_examples"></a>例

現在のディレクトリ内で Directory1 という名前のディレクトリを作成するには、次のように入力します。
```
md Directory1
```
ルート ディレクトリ内のディレクトリ ツリー Taxes\Property\Current コマンド拡張機能を有効になっている使用して作成するには、次のように入力します。
```
md \Taxes\Property\Current
```
コマンド拡張機能を無効になっていますが、前の例のように、ルート ディレクトリ内のディレクトリ ツリー Taxes\Property\Current を作成するには、次の一連のコマンドを入力します。
```
md \Taxes
cd \Taxes 
md Property
cd Property
md Current
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)

[cmd](cmd.md)