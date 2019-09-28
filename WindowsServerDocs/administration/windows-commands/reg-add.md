---
title: reg add
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 5b478ce0c98ec77f1387d8f894364f53cf8d2142
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371767"
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
| \<KeyName<em>></em> | サブキーまたは追加されるエントリの完全なパスを指定します。 リモートコンピューターを指定するには、コンピューター名 (\\ @ no__t-1 @ no__t-2ComputerName Computername の形式で、 *KeyName*の一部として \) を含めます。 @No__t-0 @ no__t-1 Computername \ を省略すると、操作は既定でローカルコンピューターに設定されます。 *KeyName* 有効なルート キーを含める必要があります。 ローカルコンピューターの有効なルートキーは次のとおりです。HKLM、HKCU、HKCR、HKU、および HKCC。 リモートコンピューターが指定されている場合、有効なルートキーは次のとおりです。HKLM と HKU。 レジストリキー名にスペースが含まれている場合は、キー名を引用符で囲みます。 |
|   /v \<ValueName >   |                                                                                                                                                                                                                                指定したサブキーの下に追加されるレジストリ エントリの名前を指定します。                                                                                                                                                                                                                                 |
|         /ve         |                                                                                                                                                                                                                                レジストリに追加されるレジストリ エントリが null 値を持つことを指定します。                                                                                                                                                                                                                                |
|     /t \<Type >      |                                                                                                                                          レジストリ エントリの種類を指定します。 *型* 、次のいずれかを指定する必要があります。</br>REG_SZ</br>REG_MULTI_SZ</br>REG_DWORD_BIG_ENDIAN</br>REG_DWORD</br>REG_BINARY</br>REG_DWORD_LITTLE_ENDIAN</br>REG_LINK</br>REG_FULL_RESOURCE_DESCRIPTOR</br>REG_EXPAND_SZ                                                                                                                                          |
|   /s \<Separator >   |                                                                                                                                                              REG_MULTI_SZ データ型が指定されている複数のエントリがリストに表示される必要がある場合は、データの複数のインスタンスを分離するために使用する文字を指定します。 既定の区切り記号は、指定しない場合、 **\0**します。                                                                                                                                                              |
|     /d @no__t 0Data >      |                                                                                                                                                                                                                                                 新しいレジストリ エントリのデータを指定します。                                                                                                                                                                                                                                                  |
|         /f          |                                                                                                                                                                                                                                           確認を求めずに、レジストリ エントリを追加します。                                                                                                                                                                                                                                           |
|         /?          |                                                                                                                                                                                                                                              ヘルプを表示 **reg 追加** コマンド プロンプト。                                                                                                                                                                                                                                               |

## <a name="remarks"></a>コメント

-   サブツリーは、この操作を追加することはできません。 このバージョンの **reg** サブキーを追加するときに確認を要求しません。
-   次の表に、戻り値の **reg 追加** 操作します。

| 値 | 説明 |
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
