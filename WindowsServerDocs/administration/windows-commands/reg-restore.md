---
title: Reg 復元
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 0025a37ed8ca50b47e7750501a7362659b500537
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858773"
---
# <a name="reg-restore"></a>Reg 復元



書き込みが保存されたサブキーとエントリは、レジストリをバックアップします。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
Reg restore <KeyName> <FileName>
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<キー名 >|復元するサブキーの完全なパスを指定します。 復元操作は、ローカル コンピューターでのみ機能します。 られているキー名では、有効なルート キーを含める必要があります。 有効なルート キーは次のとおりです。HKLM、HKCU、HKCR、HKU、および hkcc します。|
|\<FileName>|レジストリに書き込まれるコンテンツを含むファイルのパスと名前を指定します。 このファイルはで事前に作成する必要があります、 **reg 保存** .hiv 拡張機能を使用して操作します。|
|/?|ヘルプを表示 **reg 復元** コマンド プロンプト。|

## <a name="remarks"></a>注釈

-   すべてのレジストリ エントリを編集する前に保存された親サブキー、 **reg 保存** 操作します。 復元と元のサブキーの編集に失敗した場合、 **reg 復元** 操作します。
-   次の表に、戻り値の **reg 復元** 操作します。

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

[コマンドライン構文キー](command-line-syntax-key.md)