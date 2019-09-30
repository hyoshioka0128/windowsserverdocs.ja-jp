---
title: reg の削除
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 7156bf58b27da1602931f0dc1903de71d86764e7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384764"
---
# <a name="reg-delete"></a>reg の削除



レジストリからサブキーまたはエントリを削除します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
Reg delete <KeyName> [{/v ValueName | /ve | /va}] [/f]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<KeyName >|サブキーまたは削除するエントリの完全なパスを指定します。 リモートコンピューターを指定するには、コンピューター名を、 *KeyName*の一部として \\ @ No__t-1 computername @ no__t の形式で指定します。 @No__t-0 @ no__t-1 Computername \ を省略すると、操作は既定でローカルコンピューターに設定されます。 *KeyName* 有効なルート キーを含める必要があります。 ローカルコンピューターの有効なルートキーは次のとおりです。HKLM、HKCU、HKCR、HKU、および HKCC。 リモートコンピューターが指定されている場合、有効なルートキーは次のとおりです。HKLM と HKU。|
|/v \<ValueName >|サブキーの特定のエントリを削除します。 エントリが指定されていない場合、すべてのエントリとサブキーの下のサブキーは削除されます。|
|/ve|値を持たないエントリのみが削除されることを指定します。|
|/va|指定したサブキーの下のすべてのエントリを削除します。 指定したサブキーの下のサブキーは削除されません。|
|/f|確認を求めずに、既存のレジストリ サブキーまたはエントリを削除します。|
|/?|ヘルプを表示 **reg delete** コマンド プロンプト。|

## <a name="remarks"></a>コメント

次の表に、戻り値の **reg delete** 操作します。

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

[コマンド ライン構文の記号](command-line-syntax-key.md)