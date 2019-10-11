---
title: reg save
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 6ae07cd3c90c51e7bd494bc6c35919680cde912a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371696"
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
|\<KeyName >|サブキーの完全なパスを指定します。 リモートコンピューターを指定する場合は、コンピューター名を、 *KeyName*の一部として \\ @ No__t-1 computername @ no__t の形式で指定します。 @No__t-0 @ no__t-1 Computername \ を省略すると、操作は既定でローカルコンピューターに設定されます。 *KeyName* 有効なルート キーを含める必要があります。 ローカルコンピューターの有効なルートキーは次のとおりです。HKLM、HKCU、HKCR、HKU、および HKCC。 リモートコンピューターが指定されている場合、有効なルートキーは次のとおりです。HKLM と HKU。|
|\<ファイル名 >|作成されるファイルのパスと名前を指定します。 パスが指定されていない場合は、現在のパスが使用されます。|
|/y|名前の既存のファイルを上書き *FileName* 確認を求めずにします。|
|/?|ヘルプを表示 **reg save** コマンド プロンプト。|

## <a name="remarks-optional-section"></a>解説 \<optional section >

-   次の表に、戻り値の **reg save** 操作します。

|値|説明|
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

[コマンド ライン構文の記号](command-line-syntax-key.md)