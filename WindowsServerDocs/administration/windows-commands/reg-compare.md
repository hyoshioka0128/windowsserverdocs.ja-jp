---
title: Reg の比較
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 9f4a8c51e7add429aab326804af698fed7007999
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887223"
---
# <a name="reg-compare"></a>Reg の比較



比較では、レジストリ サブキーまたはエントリを指定します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
reg compare <KeyName1> <KeyName2> [{/v ValueName | /ve}] [{/oa | /od | /os | on}] [/s]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<KeyName1 >|比較する最初のサブキーの完全なパスを指定します。 リモート コンピューターを指定するには、コンピューター名を含める (形式の\\ \\ComputerName\)の一部として、 *KeyName*します。 省略すると\\ \\ComputerName\ によりローカル コンピューターに既定値に操作します。 *KeyName* 有効なルート キーを含める必要があります。 ローカル コンピューターの有効なルート キーは次のとおりです。HKLM、HKCU、HKCR、HKU、および hkcc します。 リモート コンピューターが指定されている場合は、有効なルート キーは。HKLM および hku です。|
|\<KeyName2 >|比較する 2 つ目のサブキーの完全なパスを指定します。 リモート コンピューターを指定するには、コンピューター名を含める (形式の\\ \\ComputerName\)の一部として、 *KeyName*します。 省略すると\\ \\ComputerName\ によりローカル コンピューターに既定値に操作します。 内のコンピューター名のみを指定する *KeyName2* で指定したサブキーへのパスを使用する操作と、 *KeyName1*します。 *KeyName* 有効なルート キーを含める必要があります。 ローカル コンピューターの有効なルート キーは次のとおりです。HKLM、HKCU、HKCR、HKU、および hkcc します。 リモート コンピューターが指定されている場合は、有効なルート キーは。HKLM および hku です。|
|/v \<ValueName>|サブキーの下を比較する値の名前を指定します。|
|/ve|Null 値の名前を持つエントリのみを比較することを指定します。|
|[{/oa | /od | /os | on}]|比較演算の結果を表示する方法を指定します。 既定値は **/od**します。 以下の特定のオプションを参照してください。|
|/oa|すべての相違点との一致が表示されることを指定します。 既定では、差分のみが一覧表示されます。|
|/od|相違点だけが表示されることを指定します。 これは既定の動作です。|
|/os|一致だけが表示されることを指定します。 既定では、差分のみが一覧表示されます。|
|/on|何も表示されないことを指定します。 既定では、差分のみが一覧表示されます。|
|/s|すべてのサブキーとエントリを再帰的を比較します。|
|/?|ヘルプを表示 **reg 比較** コマンド プロンプト。|

## <a name="remarks"></a>注釈

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

キーの下のすべての値を比較する**MyApp**キーの下のすべての値を持つ**SaveMyApp**種類。

REG COMPARE HKLM\Software\MyCo\MyApp HKLM\Software\MyCo\SaveMyApp

キーの下のバージョンについては、値を比較する**MyCo**キーの下のバージョンの値と**MyCo1**種類。

REG COMPARE HKLM\Software\MyCo HKLM\Software\MyCo1 /v Version

すべてのサブキーと hklm \software\myco の下ですべてのサブキーと hklm \software\myco の下で、ローカル コンピューター上の値と干支をという名前のコンピューター上の値を比較するには、次のように入力します。

REG 比較\\ \\ZODIAC\HKLM\Software\MyCo \\\\します。 /s

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)