---
title: reg copy
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3fe74213-39ec-4b2d-ba3d-086243eac997
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 11cbfce39433ea18632bec16c524da191def2a07
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867563"
---
# <a name="reg-copy"></a>reg copy



ローカルまたはリモート コンピューター上の指定の場所にレジストリ エントリをコピーします。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
reg copy <KeyName1> <KeyName2> [/s] [/f]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<KeyName1 >|コピーするサブキーの完全なパスを指定します。 リモート コンピューターを指定するには、コンピューター名を含める (形式の\\ \\ComputerName\)の一部として、 *KeyName*します。 省略すると\\ \\ComputerName\ によりローカル コンピューターに既定値に操作します。 *KeyName* 有効なルート キーを含める必要があります。 ローカル コンピューターの有効なルート キーは次のとおりです。HKLM、HKCU、HKCR、HKU、および hkcc します。 リモート コンピューターが指定されている場合は、有効なルート キーは。HKLM および hku です。|
|\<KeyName2 >|サブキーの完全なパスを指定します。 リモート コンピューターを指定するには、コンピューター名を含める (形式の\\ \\ComputerName\)の一部として、 *KeyName*します。 省略すると\\ \\ComputerName\ によりローカル コンピューターに既定値に操作します。 *KeyName* 有効なルート キーを含める必要があります。 ローカル コンピューターの有効なルート キーは次のとおりです。HKLM、HKCU、HKCR、HKU、および hkcc します。 リモート コンピューターが指定されている場合は、有効なルート キーは。HKLM および hku です。|
|/s|すべてのサブキーと、指定したサブキーの下にエントリをコピーします。|
|/f|確認を求めずに、サブキーをコピーします。|
|/?|ヘルプを表示 **reg** コマンド プロンプトでコピーします。|

## <a name="remarks"></a>注釈

-   Reg は、サブキーのコピー時に確認を求めません。
-   次の表に、戻り値の **reg copy** 操作します。

|値|説明|
|-----|-----------|
|0|成功|
|1|失敗|

## <a name="BKMK_examples"></a>例

すべてのサブキーと MyApp のキーの下の値をキー SaveMyApp にコピーするには、次のように入力します。
```
REG COPY HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp /s
```
MyCo MyCo1、現在のコンピューター上のキーに干支をという名前のコンピューター上のキーの下にあるすべての値をコピーするには、次のように入力します。
```
REG COPY \\ZODIAC\HKLM\Software\MyCo HKLM\Software\MyCo1
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)
