---
title: reg load
description: 'Windows コマンドに関するトピック * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: db661e311e3fe8c393750716de5dab375e7817f4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384699"
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
|\<KeyName >|読み込むサブキーの完全なパスを指定します。 リモートコンピューターを指定する場合は、コンピューター名 (\\\\ComputerName\) を*KeyName*の一部として指定します。 \\\\ComputerName \ を省略すると、操作は既定でローカルコンピューターに設定されます。 *KeyName* 有効なルート キーを含める必要があります。 ローカル コンピューターの有効なルート キー: HKLM、HKCU、HKCR、HKU、および HKCC します。 有効なルート キーは、リモート コンピューターが指定されている場合: HKLM および HKU します。|
|\<ファイル名 >|読み込むファイルのパスと名前を指定します。 使用してこのファイルを事前に作成する必要があります、 **reg 保存** 操作と .hiv 拡張子です。|
|/?|ヘルプを表示 **reg ロード** コマンド プロンプト。|

## <a name="remarks"></a>注釈

次の表に、戻り値の **reg ロード** 操作します。

|Value|説明|
|-----|-----------|
|0|成功|
|1|失敗|

## <a name="BKMK_examples"></a>例

キー HKLM\TempHive に TempHive.hiv をという名前のファイルを読み込むには、次のように入力します。
```
REG LOAD HKLM\TempHive TempHive.hiv
```

#### <a name="additional-references"></a>その他の参照情報

[コマンド ライン構文の記号](command-line-syntax-key.md)