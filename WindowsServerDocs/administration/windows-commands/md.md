---
title: Md
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 965a5c506535a2c52d6cc7b3557c6104182c12a5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373690"
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
|@no__t 0Drive >:|新しいディレクトリを作成するドライブを指定します。|
|\<Path >|必須。 新しいディレクトリの場所と名前を指定します。 1 つのパスの最大長は、ファイル システムによって決まります。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>コメント

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

[コマンド ライン構文の記号](command-line-syntax-key.md)

[Cmd](cmd.md)