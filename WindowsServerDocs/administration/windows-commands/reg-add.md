---
title: reg add
description: Windows コマンドに関するトピック * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: d9ad143e-dc10-4e2e-a229-408393c40079
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: df59477c980169699dac897e36836e5226b6a0fa
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2020
ms.locfileid: "80836595"
---
# <a name="reg-add"></a>reg add


新しいサブキーまたはエントリをレジストリに追加します。

## <a name="syntax"></a>構文

```
reg add <KeyName> [{/v ValueName | /ve}] [/t DataType] [/s Separator] [/d Data] [/f]
```
このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

### <a name="parameters"></a>パラメーター

|      パラメーター      |                                                                                                                                                                                                                                                                   説明                                                                                                                                                                                                                                                                   |
|---------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| \<KeyName<em>></em> | サブキーまたは追加されるエントリの完全なパスを指定します。 リモートコンピューターを指定するには、コンピューター名 (\\\\\<ComputerName >\) を*KeyName*の一部として指定します。 \\\\ComputerName \ を省略すると、操作は既定でローカルコンピューターに設定されます。 *KeyName* 有効なルート キーを含める必要があります。 ローカル コンピューターの有効なルート キー: HKLM、HKCU、HKCR、HKU、および HKCC します。 有効なルート キーは、リモート コンピューターが指定されている場合: HKLM および HKU します。 レジストリキー名にスペースが含まれている場合は、キー名を引用符で囲みます。 |
|   /v \<ValueName >   |                                                                                                                                                                                                                                指定したサブキーの下に追加されるレジストリ エントリの名前を指定します。                                                                                                                                                                                                                                 |
|         /ve         |                                                                                                                                                                                                                                レジストリに追加されるレジストリ エントリが null 値を持つことを指定します。                                                                                                                                                                                                                                |
|     /t \<種類 >      |                                                                                                                                          レジストリ エントリの種類を指定します。 *型* 、次のいずれかを指定する必要があります。</br>REG_SZ</br>REG_MULTI_SZ</br>REG_DWORD_BIG_ENDIAN</br>REG_DWORD</br>REG_BINARY</br>REG_DWORD_LITTLE_ENDIAN</br>REG_LINK</br>REG_FULL_RESOURCE_DESCRIPTOR</br>REG_EXPAND_SZ                                                                                                                                          |
|   /s \<Separator >   |                                                                                                                                                              REG_MULTI_SZ データ型が指定されている複数のエントリがリストに表示される必要がある場合は、データの複数のインスタンスを分離するために使用する文字を指定します。 既定の区切り記号は、指定しない場合、 **\0**します。                                                                                                                                                              |
|     /d \<データ >      |                                                                                                                                                                                                                                                 新しいレジストリ エントリのデータを指定します。                                                                                                                                                                                                                                                  |
|         /f          |                                                                                                                                                                                                                                           確認を求めずに、レジストリ エントリを追加します。                                                                                                                                                                                                                                           |
|         /?          |                                                                                                                                                                                                                                              ヘルプを表示 **reg 追加** コマンド プロンプト。                                                                                                                                                                                                                                               |

## <a name="remarks"></a>コメント

-   サブツリーは、この操作を追加することはできません。 このバージョンの **reg** サブキーを追加するときに確認を要求しません。
-   次の表に、戻り値の **reg 追加** 操作します。

| 値 | 説明 |
|-------|-------------|
|   0   |   成功   |
|   1   |   失敗   |

-   REG_EXPAND_SZ キーの種類の場合は、/d パラメーター内で **%** を指定したカレット記号 ( **^** ) を使用します。

## <a name="examples"></a><a name=BKMK_examples></a>例

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

## <a name="additional-references"></a>その他の参照情報

- [コマンド ライン構文の記号](command-line-syntax-key.md)
