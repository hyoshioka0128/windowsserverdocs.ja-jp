---
title: reg の削除
description: '* * * * のリファレンストピック'
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: cee05071-1607-4ab1-b8ab-65caebeb85c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a4ff643970bac021a6b7dcb731e64c412deb8df3
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722574"
---
# <a name="reg-delete"></a>reg の削除



レジストリからサブキーまたはエントリを削除します。



## <a name="syntax"></a>構文

```
Reg delete <KeyName> [{/v ValueName | /ve | /va}] [/f]
```

### <a name="parameters"></a>パラメーター

|パラメーター|[説明]|
|---------|-----------|
|\<KeyName>|サブキーまたは削除するエントリの完全なパスを指定します。 リモートコンピューターを指定するには、コンピューター名 ( *KeyName*の一部\\ \\と\)して ComputerName という形式) を含めます。 ComputerName \\ \\\ を省略すると、操作は既定でローカルコンピューターに設定されます。 *KeyName* 有効なルート キーを含める必要があります。 ローカル コンピューターの有効なルート キー: HKLM、HKCU、HKCR、HKU、および HKCC します。 有効なルート キーは、リモート コンピューターが指定されている場合: HKLM および HKU します。|
|/v \<ValueName>|サブキーの特定のエントリを削除します。 エントリが指定されていない場合、すべてのエントリとサブキーの下のサブキーは削除されます。|
|/ve|値を持たないエントリのみが削除されることを指定します。|
|/va|指定したサブキーの下のすべてのエントリを削除します。 指定したサブキーの下のサブキーは削除されません。|
|/f|確認を求めずに、既存のレジストリ サブキーまたはエントリを削除します。|
|/?|ヘルプを表示 **reg 削除** コマンド プロンプト。|

## <a name="remarks"></a>Remarks

次の表に、戻り値の **reg 削除** 操作します。

|値|[説明]|
|-----|-----------|
|0|Success|
|1|障害|

## <a name="examples"></a>例

タイムアウトのレジストリ キーとそのすべてのサブキーと値を削除するには、次のように入力します。
```
REG DELETE HKLM\Software\MyCo\MyApp\Timeout
```
干支という名前のコンピューター上のレジストリ値 [HKLM\Software\MyCo MTU を削除するには、次のように入力します。
```
REG DELETE \\ZODIAC\HKLM\Software\MyCo /v MTU
```

## <a name="additional-references"></a>その他のリファレンス

- [コマンド ライン構文の記号](command-line-syntax-key.md)