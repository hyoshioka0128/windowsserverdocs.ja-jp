---
title: Md (英語の可能性あり)
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 82162d00-cc34-4776-9e55-4b4836dbd6a9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e2fad89fe4b7e8425064301f6020fefaa5705b25
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839585"
---
# <a name="md"></a>Md (英語の可能性あり)



ディレクトリまたはサブディレクトリを作成します。

> [!NOTE]
> このコマンドと同じ、 **mkdir** コマンドです。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
md [<Drive>:]<Path>
mkdir [<Drive>:]<Path>
```

### <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<ドライブ >:|新しいディレクトリを作成するドライブを指定します。|
|\<パス >|必須。 新しいディレクトリの場所と名前を指定します。 1 つのパスの最大長は、ファイル システムによって決まります。|
|/?|コマンド プロンプトでヘルプを表示します。|

## <a name="remarks"></a>コメント

既定で有効になっているコマンド拡張機能では、1 つを使用できます。 **md** 指定されたパスに中間ディレクトリを作成するコマンドです。

## <a name="examples"></a><a name=BKMK_examples></a>例

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
md \Taxes\Property
md \Taxes\Property\Current
```

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)

[Cmd](cmd.md)