---
title: Reg のエクスポート
description: 'Windows コマンド」のトピック * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0ad9526f-1e29-4fa5-9d2d-feaa92f12d7c
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d7aeddb4b069b1baf5b8f7aaea2730a2b25bdad7
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889653"
---
# <a name="reg-export"></a>Reg のエクスポート



他のサーバーに転送するためのファイルに指定されたサブキー、エントリ、およびローカル コンピューターの値をコピーします。

このコマンドを使用する方法の例については、[例](#BKMK_examples)を参照してください。

## <a name="syntax"></a>構文

```
Reg export KeyName FileName [/y]
```

## <a name="parameters"></a>パラメーター

|パラメーター|説明|
|---------|-----------|
|\<キー名 >|サブキーの完全なパスを指定します。 エクスポート操作は、ローカル コンピューターでのみ機能します。 られているキー名では、有効なルート キーを含める必要があります。 有効なルート キーは次のとおりです。HKLM、HKCU、HKCR、HKU、および hkcc します。|
|\<FileName>|操作中に作成されるファイルのパスと名前を指定します。 拡張子が .reg のファイルが必要です。|
|/y|名前の既存のファイルを上書き *FileName* 確認を求めずにします。|
|/?|ヘルプを表示 **reg エクスポート** コマンド プロンプト。|

## <a name="remarks"></a>注釈

次の表に、戻り値の **reg エクスポート** 操作します。

|値|説明|
|-----|-----------|
|0|成功|
|1|失敗|

## <a name="BKMK_examples"></a>例

すべてのサブキーの内容は、MyApp キーの値を AppBkUp.reg ファイルをエクスポートするには、次のように入力します。
```
reg export HKLM\Software\MyCo\MyApp AppBkUp.reg
```

#### <a name="additional-references"></a>その他の参照情報

[コマンドライン構文キー](command-line-syntax-key.md)