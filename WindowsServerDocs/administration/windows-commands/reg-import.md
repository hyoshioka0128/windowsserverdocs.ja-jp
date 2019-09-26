---
title: reg import
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0be103de-08fc-4f02-b590-361782680b3e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7d1dd1b61848671b528c62fd22fe656e14fda7b1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861843"
---
# <a name="reg-import"></a>reg import



コピーを含むファイルの内容は、ローカル コンピューターのレジストリにレジストリ キー、エントリ、および値をエクスポートします。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
Reg import FileName
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<FileName>|ローカル コンピューターのレジストリにコピーされるコンテンツを含むファイルのパスと名前を指定します。 使用してこのファイルを事前に作成する必要があります **reg export**します。|
|/?|ヘルプを表示 **reg import** コマンド プロンプト。|

## <a name="remarks"></a>注釈

次の表に、戻り値の **reg インポート** 操作します。

|値|説明|
|-----|-----------|
|0|成功|
|1|失敗|

## <a name="BKMK_examples"></a>例

レジストリ エントリ AppBkUp.reg という名前のファイルからをインポートするには、次のように入力します。
```
reg import AppBkUp.reg
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)
