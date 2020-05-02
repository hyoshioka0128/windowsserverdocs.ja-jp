---
title: Md
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 82162d00-cc34-4776-9e55-4b4836dbd6a9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a605571fb74af99d0f365a100dd33fd4db0d3f22
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82724006"
---
# <a name="md"></a>Md



ディレクトリまたはサブディレクトリを作成します。

> [!NOTE]
> このコマンドと同じ、 **mkdir** コマンドです。



## <a name="syntax"></a>構文

```
md [<Drive>:]<Path>
mkdir [<Drive>:]<Path>
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<ドライブ>:|新しいディレクトリを作成するドライブを指定します。|
|\<パス>|必須。 新しいディレクトリの場所と名前を指定します。 1 つのパスの最大長は、ファイル システムによって決まります。|
|/?|コマンド プロンプトにヘルプを表示します。|

## <a name="remarks"></a>Remarks

既定で有効になっているコマンド拡張機能では、1 つを使用できます。 **md** 指定されたパスに中間ディレクトリを作成するコマンドです。

## <a name="examples"></a>例

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

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)

[Cmd](cmd.md)