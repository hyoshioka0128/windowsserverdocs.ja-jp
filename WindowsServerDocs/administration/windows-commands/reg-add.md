---
title: reg add
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d9ad143e-dc10-4e2e-a229-408393c40079
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d46fc2df23391a1dbb782014addc68d9522d603a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441913"
---
# <a name="reg-add"></a>reg add


新しいサブキーまたはエントリをレジストリに追加します。

## <a name="syntax"></a>構文

```
reg add <KeyName> [{/v ValueName | /ve}] [/t DataType] [/s Separator] [/d Data] [/f]
```
このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="parameters"></a>パラメーター

|      パラメーター      |                                                                                                                                                                                                                                                                   説明                                                                                                                                                                                                                                                                   |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| \<キー名<em>></em> | サブキーまたは追加されるエントリの完全なパスを指定します。 リモート コンピューターを指定するには、コンピューター名を含める (形式の\\ \\ \<ComputerName >\)の一部として、 *KeyName*します。 省略すると\\ \\ComputerName\ によりローカル コンピューターに既定値に操作します。 *KeyName* 有効なルート キーを含める必要があります。 ローカル コンピューターの有効なルート キーは次のとおりです。HKLM、HKCU、HKCR、HKU、および hkcc します。 リモート コンピューターが指定されている場合は、有効なルート キーは。HKLM および hku です。 レジストリ キーの名前にスペースが含まれている場合は、キー名を引用符で囲みます。 |
|   /v \<ValueName>   |                                                                                                                                                                                                                                指定したサブキーの下に追加されるレジストリ エントリの名前を指定します。                                                                                                                                                                                                                                 |
|         /ve         |                                                                                                                                                                                                                                レジストリに追加されるレジストリ エントリが null 値を持つことを指定します。                                                                                                                                                                                                                                |
|     /t\<型 >      |                                                                                                                                          レジストリ エントリの種類を指定します。 *型* 、次のいずれかを指定する必要があります。</br>REG_SZ</br>REG_MULTI_SZ</br>REG_DWORD_BIG_ENDIAN</br>REG_DWORD</br>REG_BINARY</br>REG_DWORD_LITTLE_ENDIAN</br>REG_LINK</br>REG_FULL_RESOURCE_DESCRIPTOR</br>REG_EXPAND_SZ                                                                                                                                          |
|   /s\<区切り記号 >   |                                                                                                                                                              REG_MULTI_SZ データ型が指定されている複数のエントリがリストに表示される必要がある場合は、データの複数のインスタンスを分離するために使用する文字を指定します。 既定の区切り記号は、指定しない場合、 **\0**します。                                                                                                                                                              |
|     /d\<データ >      |                                                                                                                                                                                                                                                 新しいレジストリ エントリのデータを指定します。                                                                                                                                                                                                                                                  |
|         /f          |                                                                                                                                                                                                                                           確認を求めずに、レジストリ エントリを追加します。                                                                                                                                                                                                                                           |
|         /?          |                                                                                                                                                                                                                                              ヘルプを表示 **reg add** コマンド プロンプト。                                                                                                                                                                                                                                               |

## <a name="remarks"></a>注釈

-   サブツリーは、この操作を追加することはできません。 このバージョンの **reg** サブキーを追加するときに確認を要求しません。
-   次の表に、戻り値の **reg 追加** 操作します。

| Value | 説明 |
|-------|-------------|
|   0   |   成功   |
|   1   |   失敗   |

-   REG_EXPAND_SZ キーの種類のキャレット記号を使用して ( **^** ) と **%** "/d パラメーターの中

## <a name="BKMK_examples"></a>例

リモート コンピューター ABC に HKLM\Software\MyCo キーを追加して、次のように入力します。
```
REG ADD \\ABC\HKLM\Software\MyCo
```
という名前の値を持つ HKLM\Software\MyCo にレジストリ エントリを追加する **データ** の REG_BINARY とのデータ入力 **fe340ead**, 、種類。
```
REG ADD HKLM\Software\MyCo /v Data /t REG_BINARY /d fe340ead
```
値の名前と共に HKLM\Software\MyCo に複数の値のレジストリ エントリを追加する **MRU** の REG_MULTI_SZ とのデータ入力 **fax\0mail\0\0**, 、種類。
```
REG ADD HKLM\Software\MyCo /v MRU /t REG_MULTI_SZ /d fax\0mail\0\0
```
値の名前と共に HKLM\Software\MyCo に展開されたレジストリ エントリを追加する **パス** の REG_EXPAND_SZ とのデータ入力 **%systemroot%** , 、種類。
```
REG ADD HKLM\Software\MyCo /v Path /t REG_EXPAND_SZ /d ^%systemroot^%
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)
