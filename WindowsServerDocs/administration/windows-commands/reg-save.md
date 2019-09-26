---
title: reg save
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b326482b-c8af-467d-a20c-0481eeda3d5c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2a46dfe081421ed727bd7ffeeab364e6c23dd801
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841083"
---
# <a name="reg-save"></a>reg save



指定したファイルで指定されたサブキー、エントリ、およびレジストリの値のコピーを保存します。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
reg save <KeyName> <FileName> [/y]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<キー名 >|サブキーの完全なパスを指定します。 リモート コンピューターに指定する場合、コンピューター名を含める (形式の\\ \\ComputerName\)の一部として、 *KeyName*します。 省略すると\\ \\ComputerName\ によりローカル コンピューターに既定値に操作します。 *KeyName* 有効なルート キーを含める必要があります。 ローカル コンピューターの有効なルート キーは次のとおりです。HKLM、HKCU、HKCR、HKU、および hkcc します。 リモート コンピューターが指定されている場合は、有効なルート キーは。HKLM および hku です。|
|\<FileName>|作成されるファイルのパスと名前を指定します。 パスが指定されていない場合は、現在のパスが使用されます。|
|/y|名前の既存のファイルを上書き *FileName* 確認を求めずにします。|
|/?|ヘルプを表示 **reg save** コマンド プロンプト。|

## <a name="remarks-optional-section"></a>「解説」\<省略可能なセクション >

-   次の表に、戻り値の **reg save** 操作します。

|Value|説明|
|-----|-----------|
|0|成功|
|1|失敗|
-   すべてのレジストリ エントリを編集する前に保存された親サブキー、 **reg save** 操作します。 復元と元のサブキーの編集に失敗した場合、 **reg restore** 操作します。

## <a name="BKMK_examples"></a>例

現在のフォルダーに hive MyApp AppBkUp.hiv という名前のファイルを保存するには、次のように入力します。
```
REG SAVE HKLM\Software\MyCo\MyApp AppBkUp.hiv
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)
