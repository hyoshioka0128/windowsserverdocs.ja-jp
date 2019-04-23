---
title: Reg delete
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cee05071-1607-4ab1-b8ab-65caebeb85c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 369ef3bda37ab8e143a14f0f9707b9bbf14bd5f8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877083"
---
# <a name="reg-delete"></a>Reg delete



レジストリからサブキーまたはエントリを削除します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
Reg delete <KeyName> [{/v ValueName | /ve | /va}] [/f]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<キー名 >|サブキーまたは削除するエントリの完全なパスを指定します。 リモート コンピューターを指定するには、コンピューター名を含める (形式の\\ \\ComputerName\)の一部として、 *KeyName*します。 省略すると\\ \\ComputerName\ によりローカル コンピューターに既定値に操作します。 *KeyName* 有効なルート キーを含める必要があります。 ローカル コンピューターの有効なルート キーは次のとおりです。HKLM、HKCU、HKCR、HKU、および hkcc します。 リモート コンピューターが指定されている場合は、有効なルート キーは。HKLM および hku です。|
|/v \<ValueName>|サブキーの特定のエントリを削除します。 エントリが指定されていない場合、すべてのエントリとサブキーの下のサブキーは削除されます。|
|/ve|値を持たないエントリのみが削除されることを指定します。|
|/va|指定したサブキーの下のすべてのエントリを削除します。 指定したサブキーの下のサブキーは削除されません。|
|/f|確認を求めずに、既存のレジストリ サブキーまたはエントリを削除します。|
|/?|ヘルプを表示 **reg 削除** コマンド プロンプト。|

## <a name="remarks"></a>注釈

次の表に、戻り値の **reg 削除** 操作します。

|値|説明|
|-----|-----------|
|0|成功|
|1|失敗|

## <a name="BKMK_examples"></a>例

タイムアウトのレジストリ キーとそのすべてのサブキーと値を削除するには、次のように入力します。
```
REG DELETE HKLM\Software\MyCo\MyApp\Timeout
```
干支という名前のコンピューター上のレジストリ値 HKLM\Software\MyCo MTU を削除するには、次のように入力します。
```
REG DELETE \\ZODIAC\HKLM\Software\MyCo /v MTU
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)