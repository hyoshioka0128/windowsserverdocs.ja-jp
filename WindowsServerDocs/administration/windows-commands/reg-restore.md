---
title: reg restore
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a51f1c0c-969b-4b76-930a-c8bb14dea26e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d6c121256cecaebc26e2c402d9b9ced8890eddc2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384671"
---
# <a name="reg-restore"></a>reg restore



書き込みが保存されたサブキーとエントリは、レジストリをバックアップします。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
Reg restore <KeyName> <FileName>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<KeyName >|復元するサブキーの完全なパスを指定します。 復元操作は、ローカル コンピューターでのみ機能します。 られているキー名では、有効なルート キーを含める必要があります。 有効なルートキーは次のとおりです。HKLM、HKCU、HKCR、HKU、および HKCC。|
|\<ファイル名 >|レジストリに書き込まれるコンテンツを含むファイルのパスと名前を指定します。 このファイルはで事前に作成する必要があります、 **reg 保存** .hiv 拡張機能を使用して操作します。|
|/?|ヘルプを表示 **reg restore** コマンド プロンプト。|

## <a name="remarks"></a>コメント

-   すべてのレジストリ エントリを編集する前に保存された親サブキー、 **reg save** 操作します。 復元と元のサブキーの編集に失敗した場合、 **reg restore** 操作します。
-   次の表に、戻り値の **reg restore** 操作します。

|値|説明|
|-----|-----------|
|0|成功|
|1|失敗|

## <a name="BKMK_examples"></a>例

キー、HKLM\Software\Microsoft\ResKit NTRKBkUp.hiv をという名前のファイルを復元し、キーの既存の内容を上書きする、次のように入力します。
```
REG RESTORE HKLM\Software\Microsoft\ResKit NTRKBkUp.hiv
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)