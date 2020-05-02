---
title: reg コピー
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 3fe74213-39ec-4b2d-ba3d-086243eac997
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 91090faffbb925754a0d4ed610b37464872242db
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722581"
---
# <a name="reg-copy"></a>reg コピー



ローカルまたはリモート コンピューター上の指定の場所にレジストリ エントリをコピーします。



## <a name="syntax"></a>構文

```
reg copy <KeyName1> <KeyName2> [/s] [/f]
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<KeyName1>|コピーするサブキーの完全なパスを指定します。 リモートコンピューターを指定するには、コンピューター名 ( *KeyName*の一部\\ \\と\)して ComputerName という形式) を含めます。 ComputerName \\ \\\ を省略すると、操作は既定でローカルコンピューターに設定されます。 *KeyName* 有効なルート キーを含める必要があります。 ローカル コンピューターの有効なルート キー: HKLM、HKCU、HKCR、HKU、および HKCC します。 有効なルート キーは、リモート コンピューターが指定されている場合: HKLM および HKU します。|
|\<KeyName2>|サブキーの完全なパスを指定します。 リモートコンピューターを指定するには、コンピューター名 ( *KeyName*の一部\\ \\と\)して ComputerName という形式) を含めます。 ComputerName \\ \\\ を省略すると、操作は既定でローカルコンピューターに設定されます。 *KeyName* 有効なルート キーを含める必要があります。 ローカル コンピューターの有効なルート キー: HKLM、HKCU、HKCR、HKU、および HKCC します。 有効なルート キーは、リモート コンピューターが指定されている場合: HKLM および HKU します。|
|/s|すべてのサブキーと、指定したサブキーの下にエントリをコピーします。|
|/f|確認を求めずに、サブキーをコピーします。|
|/?|ヘルプを表示 **reg** コマンド プロンプトでコピーします。|

## <a name="remarks"></a>Remarks

-   Reg は、サブキーのコピー時に確認を求めません。
-   次の表に、戻り値の **reg コピー** 操作します。

|値|[説明]|
|-----|-----------|
|0|Success|
|1|障害|

## <a name="examples"></a>例

すべてのサブキーと MyApp のキーの下の値をキー SaveMyApp にコピーするには、次のように入力します。
```
REG COPY HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp /s
```
MyCo MyCo1、現在のコンピューター上のキーに干支をという名前のコンピューター上のキーの下にあるすべての値をコピーするには、次のように入力します。
```
REG COPY \\ZODIAC\HKLM\Software\MyCo HKLM\Software\MyCo1
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)