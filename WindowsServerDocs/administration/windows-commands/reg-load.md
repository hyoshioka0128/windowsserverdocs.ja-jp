---
title: reg load
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3b0b2b1b-f510-4108-9e9d-7057e924aa6e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: ebc75ad78b7334f4d48a085f6870a443b31fa2a9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852193"
---
# <a name="reg-load"></a>reg load



書き込みは、サブキーと別のサブキーにエントリをレジストリに保存します。 トラブルシューティングまたはレジストリ エントリを編集するために使用される一時ファイルで使用するためのものです。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
reg load KeyName FileName
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<キー名 >|読み込むサブキーの完全なパスを指定します。 リモート コンピューターに指定する場合、コンピューター名を含める (形式の\\ \\ComputerName\)の一部として、 *KeyName*します。 省略すると\\ \\ComputerName\ によりローカル コンピューターに既定値に操作します。 *KeyName* 有効なルート キーを含める必要があります。 ローカル コンピューターの有効なルート キーは次のとおりです。HKLM、HKCU、HKCR、HKU、および hkcc します。 リモート コンピューターが指定されている場合は、有効なルート キーは。HKLM および hku です。|
|\<FileName>|読み込むファイルのパスと名前を指定します。 使用してこのファイルを事前に作成する必要があります、 **reg save** 操作と .hiv 拡張子です。|
|/?|ヘルプを表示 **reg load** コマンド プロンプト。|

## <a name="remarks"></a>注釈

次の表に、戻り値の **reg load** 操作します。

|値|説明|
|-----|-----------|
|0|成功|
|1|失敗|

## <a name="BKMK_examples"></a>例

キー HKLM\TempHive に TempHive.hiv をという名前のファイルを読み込むには、次のように入力します。
```
REG LOAD HKLM\TempHive TempHive.hiv
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)
