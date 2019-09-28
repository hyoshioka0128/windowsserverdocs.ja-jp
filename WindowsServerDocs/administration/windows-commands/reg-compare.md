---
title: reg 比較
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 177dc6a3-034e-4846-a394-330d03c14e0b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bfccc1f64b0113967a52e3ac0516d800cfea3532
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384716"
---
# <a name="reg-compare"></a>reg 比較



比較では、レジストリ サブキーまたはエントリを指定します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
reg compare <KeyName1> <KeyName2> [{/v ValueName | /ve}] [{/oa | /od | /os | on}] [/s]
```

## <a name="parameters"></a>パラメーター

|    パラメーター    |                                                                                                                                                                                                                                                                                          説明                                                                                                                                                                                                                                                                                           |
|-----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   \<KeyName1 >   |                                                               比較する最初のサブキーの完全なパスを指定します。 リモートコンピューターを指定するには、コンピューター名を、 *KeyName*の一部として \\ @ No__t-1 computername @ no__t の形式で指定します。 @No__t-0 @ no__t-1 Computername \ を省略すると、操作は既定でローカルコンピューターに設定されます。 *KeyName* 有効なルート キーを含める必要があります。 ローカルコンピューターの有効なルートキーは次のとおりです。HKLM、HKCU、HKCR、HKU、および HKCC。 リモートコンピューターが指定されている場合、有効なルートキーは次のとおりです。HKLM と HKU。                                                                |
|   \<KeyName2 >   | 比較する 2 つ目のサブキーの完全なパスを指定します。 リモートコンピューターを指定するには、コンピューター名を、 *KeyName*の一部として \\ @ No__t-1 computername @ no__t の形式で指定します。 @No__t-0 @ no__t-1 Computername \ を省略すると、操作は既定でローカルコンピューターに設定されます。 内のコンピューター名のみを指定する *KeyName2* で指定したサブキーへのパスを使用する操作と、 *KeyName1*します。 *KeyName* 有効なルート キーを含める必要があります。 ローカルコンピューターの有効なルートキーは次のとおりです。HKLM、HKCU、HKCR、HKU、および HKCC。 リモートコンピューターが指定されている場合、有効なルートキーは次のとおりです。HKLM と HKU。 |
| /v \<ValueName > |                                                                                                                                                                                                                                                                     サブキーの下を比較する値の名前を指定します。                                                                                                                                                                                                                                                                      |
|       /ve       |                                                                                                                                                                                                                                                         Null 値の名前を持つエントリのみを比較することを指定します。                                                                                                                                                                                                                                                         |
|      [{/oa      |                                                                                                                                                                                                                                                                                              /od                                                                                                                                                                                                                                                                                               |
|       /oa       |                                                                                                                                                                                                                                             すべての相違点との一致が表示されることを指定します。 既定では、相違点だけが表示されます。                                                                                                                                                                                                                                             |
|       /od       |                                                                                                                                                                                                                                                          相違点だけが表示されることを指定します。 これは既定の動作です。                                                                                                                                                                                                                                                          |
|       /os       |                                                                                                                                                                                                                                                    一致だけが表示されることを指定します。 既定では、相違点だけが表示されます。                                                                                                                                                                                                                                                     |
|       /on       |                                                                                                                                                                                                                                                       何も表示されないことを指定します。 既定では、相違点だけが表示されます。                                                                                                                                                                                                                                                        |
|       /s        |                                                                                                                                                                                                                                                                         すべてのサブキーとエントリを再帰的を比較します。                                                                                                                                                                                                                                                                          |
|       /?        |                                                                                                                                                                                                                                                                    ヘルプを表示 **reg 比較** コマンド プロンプト。                                                                                                                                                                                                                                                                    |

## <a name="remarks"></a>コメント

次の表に、戻り値の **reg 比較**します。

|値|説明|
|-----|-----------|
|0|比較の結果が成功して、結果は変わりません。|
|1|比較が失敗しました。|
|2|比較が成功し、相違が検出されました。|

次の表は、結果に表示されるシンボルを一覧表示します。

|シンボル|説明|
|------|-----------|
|=|*KeyName1* データに等しい *KeyName2* データ。|
|<|*KeyName1* データより小さい *KeyName2* データ。|
|>|*KeyName1* データがより大きい *KeyName2* データ。|

## <a name="BKMK_examples"></a>例

キー **MyApp**の下にあるすべての値を、キー **Savemyapp**の下のすべての値と比較するには、次のように入力します。

REG COMPARE HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp

キー **MyCo**の下のバージョンの値と、 **MyCo1**キーの下のバージョンの値を比較するには、次のように入力します。

REG COMPARE HKLM\Software\MyCo HKLM\Software\MyCo1/v バージョン

HKLM\Software\MyCo の下にあるすべてのサブキーと値を、ローカルコンピューター上の HKLM\Software\MyCo の下のすべてのサブキーと値を使用して比較するには、次のように入力します。

REG COMPARE \\ @ no__t-1ZODIAC\HKLM\Software\MyCo \\ @ no__t。 /s

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)